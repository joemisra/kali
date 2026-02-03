MIDI In: User Guide

- Purpose: How to plug in, select channels, and control Kali via MIDI CC, notes, and clock. Detailed developer notes follow below.

Quick Start

- Connect: Plug your MIDI source into the module’s MIDI input.
- Set Channels: Use MIDI Channels 1–8 as described below.
- Try A CC: On Channel 7, send CC 2 to move DSP Parameter 1 (P1).
- Sync To MIDI: Set Global Sync Mode to “MIDI Clock” and send MIDI clock/start/stop.

MIDI Channels

- LFO 1–6: Use Channels 1–6 (one per LFO, same CC map for each).
- DSP Engine: Use Channel 7 (mode and P1–P4, plus distortion/filter/delay range).
- Global Options: Use Channel 8 (clocking, reverb sends, I/O, debug).

LFO CC Map (Channels 1–6)

- CC 1 (Waveform): Selects LFO shape.
- CC 2 (Mode): Selects LFO operating mode.
- CC 3 (Oneshot): 0=loop, 1=single cycle/env.
- CC 4 (Meta): Multiplies left time; musical meta control.
- CC 5 (MetaDivider): Divides numerator; rhythmic division.
- CC 6 (Polarity): 0..3 per STPolarityNames.
- CC 7 (Adjust): Contextual LFO adjust (0–100%).
- CC 8 (Offset): Output DC offset (± range).
- CC 9 (Attenuate): Output attenuation (1–100%).
- CC 10 (PhaseOffset): 0–360° phase shift.
- CC 11 (GateIn): Trigger/reset source per STGateSources.
- CC 12 (OffsetCal): Calibrated offset trim.
- CC 13 (AttenuateCal): Calibrated attenuation trim.
- CC 14 (Attack): ADSR attack time.
- CC 15 (Decay): ADSR decay time.
- CC 16 (Sustain): ADSR sustain level (0–1).
- CC 17 (Release): ADSR release time.
- CC 18 (Eschaton): End‑of‑cycle action.
- CC 19 (Incandenza): EOC target (which LFO/target).
- CC 20 (FMSource): FM source target.
- CC 21 (FMSourceAmount): FM modulation amount (±%).
- CC 22 (AMSource): AM source target.
- CC 23 (AMAmount): AM modulation amount (±%).

DSP CC Map (Channel 7)

- CC 1 (Mode): Selects DSP algorithm.
- CC 2–5 (P1–P4): Primary DSP parameters.
- CC 6 (Distortion): Distortion algorithm.
- CC 7 (DistortionAmount): Amount (0–99).
- CC 8 (DistortionTarget): Off/Dry/Wet/Both.
- CC 9 (DistortionTrim): Output trim (0–100%).
- CC 10 (FilterType): FIR/IIR/Off.
- CC 11 (DelayRangePreset): Precision/Studio/Ambient/Looper/Experimental.

Global CC Map (Channel 8)

- CC 1 (LfoRateMultiplier): Global LFO rate multiplier.
- CC 2 (LeftClockRateMultiplier): Clock out PPQN.
- CC 3 (RightClockRateMultiplier): R clock divider.
- CC 4 (ExternalCvClockPPQN): Expected PPQN for CV clock.
- CC 5 (SyncEngine): Internal/External CV/MIDI Clock.
- CC 6 (SyncButtonMode): 0=Trigger, 1=Reset.
- CC 7 (FreezeButtonMode): 0=Freeze, 1=Reset.
- CC 8 (UseAllpass): Toggle allpass.
- CC 9 (ReverbWetSend): 0–50.
- CC 10 (ReverbDrySend): 0–50.
- CC 11 (ReverbFeedback): 50–99.
- CC 12 (ReverbDamp): 1–19 kHz.
- CC 13 (AdcAttenuation): Input gain 0–255.
- CC 14 (DacAttenuation): Output gain 0–255.
- CC 15 (InputWidth): 0–1 (mono→stereo width).
- CC 16 (InvertEncoders): 0/1.
- CC 17 (EnableDebugInfo): 0/1.

Notes and Clock

- Notes: Note On/Off are received and tracked; velocity>0 = active. Useful for future mapping and diagnostics.
- MIDI Clock: Responds to Timing Clock, Start, Stop, Continue. Set Sync Mode to “MIDI Clock” to follow external tempo.

Scaling and Behavior

- Value Range: CC values 0–127 scale to each parameter’s min..max and step.
- Enums: Discrete options pick nearest valid index (see on‑screen names).
- Rate Limit: CC updates are rate‑limited to keep the UI/audio smooth (P1–P4 are extra protected).
- Coalescing: If you send rapid CCs, only the last value each cycle is applied.

Troubleshooting

- No Response: Confirm you’re on the right channel (1–8) and CC number.
- Clock Not Following: Set Global Sync Mode to “MIDI Clock” and send clock.
- Jumpy UI Under Heavy CC: Slow the controller’s CC rate or reduce message fan‑out.
- Levels Too Hot: Lower Global Adc/Dac attenuation via CC 13/14 on Channel 8.

Advanced Tips

- Same LFO Map: The LFO CC map above applies identically to Channels 1–6 (targets LFO 1–6 respectively).
- Safe Flooding: Per‑CC throttling protects audio/UI; you can still modulate quickly within reason.
- Presets: MIDI CC for preset load/save is not mapped; use the front panel for now.

Developer Notes

MIDI Implementation Overview

- Purpose: Explain how MIDI is handled, mapped, and throttled in this firmware, including threading, performance safeguards, and how to extend mappings.

Event Flow

- Input: `libDaisy` MIDI queue via `patch.midi`.
- Polling: `Kali::HandleMIDI()` drains the queue from the main loop (not in ISR/audio).
  - Location: `Kali.cpp:209`.
- Coalescing: Within each call, Control Change (CC) events are coalesced so only the last value per `(channel, cc)` is applied that cycle.
- Application: Coalesced CCs are handed to `KaliMIDI::receiveControlChange(...)` which rate‑limits per CC and applies mapped changes when updated.
- Real‑time: System RealTime messages (Clock/Start/Stop/Continue) are handled immediately when draining.

Threading Model

- ISR (TIM2): No MIDI, no I2C. Only maintains a simple countdown flag.
  - Location: `Kali.cpp` (function `handlar`).
- Audio callback: No MIDI or OLED I2C.
  - Location: `Kali.cpp` (function `AudioCallback`).
- Main loop: Handles MIDI polling, coalescing, mapped updates, deferred settings saves, codec attenuation updates, and OLED refresh (~30 fps).

Control Change (CC) Handling

- Rate limiting: Per‑CC minimum time between updates.
  - Default: 10 ms per CC.
  - Legacy safeguard: Extra 25 ms min for CC 21–24 (historically P1–P4 on older layouts).
  - Location: `KaliMIDI.cpp:31` (`receiveControlChange`).
- Coalescing: Only the latest value per `(channel, cc)` in a drain cycle gets applied.
  - Location: `Kali.cpp:209` (`HandleMIDI`).
- Mapping: O(1) lookup from `(channel, cc)` to a mapping index using a precomputed table.
  - Lookup table: `KaliMIDI::cc_lookup[16][128]`.
  - Location: `KaliMIDI.h:48`, `KaliMIDI.cpp:121`, `KaliMIDI.cpp:202`.
- Processing: If a custom callback is present, it is invoked; otherwise `defaultCCHandler` scales and writes into Options.
  - Locations: `KaliMIDI.cpp:202` (`processMappedCC`), `KaliMIDI.cpp` (`defaultCCHandler`).

Channel Layout (current)

- Channels 0–5: LFO banks (six LFOs; one channel each)
  - CC 1..23: Waveform, Mode, Oneshot, Meta, MetaDivider, Polarity, Adjust, Offset, Attenuate, PhaseOffset, GateIn, OffsetCal, AttenuateCal, ADSR (Attack/Decay/Sustain/Release), Eschaton, Incandenza, FMSource, FMSourceAmount, AMSource, AMAmount.
- Channel 6: DSP options
  - CC 1..11: Mode, P1, P2, P3, P4, Distortion, DistortionAmount, DistortionTarget, DistortionTrim, FilterType, DelayRangePreset.
- Channel 7: Global options
  - CC 1..17: LfoRateMultiplier, LeftClockRateMultiplier, RightClockRateMultiplier, ExternalCvClockPPQN, SyncEngine, SyncButtonMode, FreezeButtonMode, UseAllpass, ReverbWetSend, ReverbDrySend, ReverbFeedback, ReverbDamp, AdcAttenuation, DacAttenuation, InputWidth, InvertEncoders, EnableDebugInfo.
- Mappings initialization: `KaliMIDI.cpp:121` (`initializeCCMappings`).

Notes and Clock

- Notes: 128‑entry note buffer tracks note on/off with bounds checks; `LastNote` retained.
  - Locations: `KaliMIDI.h` (`NoteOnBuffer`), `KaliMIDI.cpp` (`receiveNoteOn`, `receiveNoteOff`).
- MIDI Clock: Real‑time messages update `midi_clock_flag`, trigger sends, and reset counters.
  - Location: `Kali.cpp:209` in `HandleMIDI()`.

OLED/UI

- All OLED I2C operations occur in the main loop at ~30 fps to avoid blocking ISR/audio.
- Contrast management is also handled outside of ISR.
- Location: `Kali.cpp` (main loop and `updateoled`).

Performance Safeguards

- No I2C or heavy work in ISR.
- No MIDI in ISR/audio threads.
- CC coalescing per cycle + per‑CC rate limiting.
- Bounded MIDI drain per call (`maxDrain` in `HandleMIDI`) to cap per‑loop work.
- O(1) CC mapping lookup via `cc_lookup`.
- Increased mapping capacity: `MAX_CC_MAPPINGS = 192` (headroom above current 166 mappings).

Extending/Modifying Mappings

- Add or edit mappings in `initializeCCMappings`.
  - Use `addCCMapping(channel, cc, bank, option_index, lfo_index = -1, callback = nullptr)`.
  - The lookup table is auto‑updated when adding mappings.
- For custom behavior, pass a `CCCallback` to transform a CC before applying.
- To change throttling for a specific CC, adjust logic in `receiveControlChange`.

Troubleshooting

- Screen freezes under heavy CC:
  - Ensure no I2C in ISR/audio (already addressed).
  - Adjust per‑CC rate limits or reduce `maxDrain` in `HandleMIDI`.
  - Consider coalescing window tuning if needed for extremely fast controllers.
- Unexpected CC numbers from controllers:
  - Verify channel/CC against the layout above.
  - Use the debug screen or log last MIDI event (`Kali::GetLastMIDIEvent`).
