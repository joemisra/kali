# Kali firmware update methods (Daisy Patch SM)

This document expands on the earlier brainstorming and gives **actionable, testable steps** to try three updater paths on Kali (Daisy Patch SM hardware):

1. **Protected GPIO/ADC loader (audio or square-wave encoded data; no USB host required at runtime)**
2. **System-Memory ROM bootloader over UART (using ST-LINK MiniE v3 only for recovery)**
3. **USB Mass-Storage-Class (MSC) drag-and-drop loader (allows firmware and preset writes over USB)**

The guidance assumes you currently flash Kali with an ST-LINK MiniE v3 and `dfu-util` command-line switches from the Daisy examples. Memory sector numbers below match the STM32H7 used on Daisy Patch SM.

## 0) Common preparation
- **Reserve flash layout**
  - Sector 0 (128 KB) : Permanent boot stub + loader (marked write-protected in Option Bytes).
  - Sector 1–(N-1) : Application slots (either single-slot or dual A/B if you want atomic rollbacks).
- **Vector hand-off**
  - Boot stub jumps by relocating MSP and PC from the chosen app image vector table; ensure the app is linked with an offset (e.g., `0x0802_0000` if loader uses the first 128 KB).
- **CRC guard**
  - Place a 32-bit CRC and image length in a small header before the app vector; stub validates before jumping and falls back to loader on failure.

## 1) GPIO/ADC loader (audio or square-wave, no USB host)
Goal: allow in-rack updates by playing an encoded bitstream into accessible GPIOs.

### Hardware hookup
- Pick two exposed pins on the Patch SM ribbon/header:
  - **RX pin**: digital GPIO or ADC channel (for Manchester/ASK decoding). Use a series resistor (~1–10 kΩ) to protect against overdrive.
  - **Optional ACK pin**: open-drain output back to the host tool (can be skipped if you encode ACK/NACK as timing gaps).
- Provide a simple 3.5mm or 2-pin header adapter so a phone/laptop can play the signal.

### Firmware steps
1. **Boot stub entry test**: On reset, read a dedicated GPIO strap (e.g., a button combo or config jumper). If asserted, enter loader; otherwise validate the app CRC and jump.
2. **Clock recovery**: Configure a timer input capture on the RX pin; use **Manchester encoding** (self-clocking) with a symbol period you can reliably sample (start with 2–4 kHz).
3. **Framing**: Define a packet header `{sync word, payload length, block index, CRC32}`. Payload size 256–512 bytes keeps flash erase cadence reasonable.
4. **Decoding loop**: In an ISR, convert edges to bits, assemble packets, verify CRC32. NACK on CRC failure (toggle ACK pin or insert a long idle gap that the host interprets as retry request).
5. **Flash writes**: Inside loader (not the app), call `HAL_FLASH_Unlock`, erase the target sectors (`HAL_FLASHEx_Erase`), program with 64-bit writes (`HAL_FLASH_Program` with `FLASH_TYPEPROGRAM_FLASHWORD` on H7), then `HAL_FLASH_Lock`. Keep the loader in sector 0, marked read-only via Option Bytes to avoid self-erasure.
6. **Post-write verify**: Re-read programmed flash and CRC it. If good, set an "app valid" flag in a small config page (e.g., last 8 KB of sector 0) and reboot.
7. **Presets/samples**: Add a secondary packet type that writes to a reserved data sector (e.g., last 1–2 sectors). The same host tool can send presets without replacing firmware.

### Host-side test plan
- Write a Python tool that takes `kali.bin`, Manchester-encodes it, and plays via audio (PyAudio) or a GPIO dongle. Include retransmit on NACK.
- Bench test with ST-LINK attached to recover if decoding fails. Intentionally corrupt a packet to confirm CRC/NACK path and that the loader stays resident.

## 2) ROM System-Memory bootloader over UART (no new loader firmware required)
Goal: leverage the STM32H7 factory bootloader to avoid USB while keeping a low-friction wired path.

### Hardware hookup
- Expose **USART1** (or another ROM-supported UART per AN2606 for the Patch SM MCU) on a small header. A TRS-to-UART cable or USB-UART dongle works.
- Add a **BOOT0 strap** (jumper/button) that you can pull high during reset, or configure Option Bytes to boot from System Memory and then reset via software.

### Steps to try
1. With ST-LINK, program your current Kali image normally so you have a known-good firmware.
2. Assert BOOT0 (jumper) and reset; the MCU enters the ROM loader.
3. On a host PC, use `stm32flash -b 115200 -w kali.bin /dev/ttyUSB0` (or ST’s `stm32cubeprogrammer` UART mode) to flash over UART.
4. Clear BOOT0, reset; confirm Kali runs. Repeat to validate the path.
5. For field use without jumpers: add a small **ROM-boot helper** in your sector-0 stub that sets the Option Bytes to boot System Memory once, triggers a system reset, and blinks an LED while waiting. After UART flashing, the helper restores normal boot options.

## 3) USB MSC drag-and-drop loader (firmware + presets over USB)
Goal: allow copying firmware or preset files to a small virtual disk. USB is allowed for data; ST-LINK/DFU remain as recovery.

### Firmware structure
- Loader enumerates as **USB MSC** exposing a tiny FAT volume (e.g., 64–128 KB). Include a README and placeholder files.
- Detect new files via FAT callbacks (e.g., Chan FatFs `disk_ioctl` events or a polling loop). Accept `KALI_FIRM.BIN` and `KALI_PRESET.BIN` (or similar).
- After a successful copy and close, validate CRC/length, program flash (same HAL flow as above), update the “app valid” flag, then **reboot** into the app. Optionally re-enumerate to show success.

### Steps to try
1. Link the loader to sector 0 (128 KB) and the app to start at `0x0802_0000` (or after your chosen loader size). Protect sector 0 in Option Bytes.
2. Use CubeMX or the Daisy USB stack to enable **USB device MSC** with a RAM-backed block device sized to the small FAT volume.
3. Implement file handling:
   - Mount the RAM disk with FatFs; initialize it with a minimal FAT image in flash or format on first boot.
   - Poll for file arrival; when `KALI_FIRM.BIN` appears, close handles, unmount, CRC-check, and flash.
   - For presets, write the payload into a reserved data sector and update an index table.
4. Testing:
   - From a host PC, copy a known-good `kali.bin` onto the volume; watch LED/serial logs for status; verify reboot into new firmware.
   - Corrupt the file to confirm CRC rejection and that the loader stays active.
   - Copy a preset file and confirm it appears in your preset storage.

## Recovery and validation
- Keep **ST-LINK + dfu-util** workflow as a safety net. If any loader path misbehaves, fully erase flash (`st-flash erase` or CubeProgrammer mass-erase) and re-flash the known-good Kali image plus the protected loader.
- Add a **watchdog** in the loader to recover from stalled transfers; kick it during packet/USB activity.
- Log status over UART/USB CDC during development for visibility.

## Verification matrix
Use this checklist while prototyping:

| Path | Can enter loader without rack removal? | Tested CRC failure? | Tested power loss mid-flash? | Preset write tested? |
|------|----------------------------------------|---------------------|------------------------------|----------------------|
| GPIO/ADC | ☐ | ☐ | ☐ | ☐ |
| ROM UART | ☐ | n/a (ROM) | ☐ | n/a |
| USB MSC | ☐ | ☐ | ☐ | ☐ |

Fill the table as you validate each scenario on hardware.