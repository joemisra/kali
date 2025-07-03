## Kali Firmware Update Instructions

### Important Safety Warning
**ALWAYS KEEP EURORACK POWER OFF WHILE USING USB CONNECTION**

### What You'll Need
- Google Chrome browser (Safari will not work)
- A quality micro-USB data cable (not just a charging cable)
- Kali module with Daisy Patch Submodule

### Update Process

1. **Download the firmware**
   - [Download the latest Kali 2.0 beta firmware](https://github.com/joemisra/kali/releases/tag/v2.005)
   - Unzip the file if needed - you should see a Kali.bin file

2. **Prepare for update**
   - Open Google Chrome and navigate to the [Electrosmith Web Programmer](https://electro-smith.github.io/Programmer/)
   - Locate the BOOT button on the Daisy Patch Submodule (see image below)
   
   ![BOOT button location](https://user-images.githubusercontent.com/326734/189494464-a1afc99d-b773-4440-bfa1-7d2296a3fbbe.png)

3. **Enter bootloader mode**
   - While holding down the BOOT button, connect the micro-USB cable to your computer
   - Release the BOOT button after connecting
   - Successful bootloader entry is indicated by the right/left sync LED staying on. Color of LED may vary.
    
   ![Sync LED indicator](https://user-images.githubusercontent.com/326734/189494472-ecba0036-2e82-45a8-8dbf-5607bd30f60e.png)

4. **Connect to the programmer**
   - Click the "Connect" button at the top of the Electrosmith Web Programmer
   - In the dialog box, select "DFU in FS Mode" and click "Connect"

5. **Upload the firmware**
   - Scroll down to the bottom section of the page
   - Click "Choose File" and select the Kali.bin file you downloaded
   - Click the "Program" button and wait for the process to complete
   
   <img width="536" alt="image" src="https://github.com/user-attachments/assets/d8002869-3017-41ba-969f-044a1d226faf" />

### Troubleshooting


**If the Daisy Patch Submodule doesn't appear in the web programmer:**
- Try a different micro-USB cable. Many cables (especially those included with chargers) only provide power and not data.
- If the module's screen is on or you see flashing LEDs:
  1. Unplug the USB cable
  2. Hold down the BOOT button on the Daisy Patch Submodule
  3. While still holding the button, plug in the USB cable
  4. Release the button after 2 seconds
  5. Try connecting again in the web programmer

**After successful update:**
- Disconnect the USB cable
- Reconnect your eurorack power
- Your Kali will start with the new firmware
