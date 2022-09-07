# dsp.coffee KALI

![kbaliwakeup-7](https://user-images.githubusercontent.com/326734/182261061-2471d0ba-7678-4e46-93a4-f95b2bcd2673.png)

For detailed information please check the KALI Wiki:

https://github.com/joemisra/kali/wiki

## Firmware!

### Update 

**keep eurorack power off while using usb** 

* Download most recent Kali firmware from this repository.

* In a Chrome browser window, navigate to the [Electrosmith Web Programmer](https://electro-smith.github.io/Programmer/)

* Once there, connect the Daisy Patch Submodule on the back of Kali to your computer using a micro USB cable. 

* Put the Daisy into flashable mode by holding down the BOOT button, and pressing the RESET button. Once you release the RESET button you can let go of the BOOT button (You'll know you performed the button combo correctly if the USER LED on your Daisy stops flashing)

* Connect Daisy as a DFU device by clicking the "Connect" button at the top of the Web Programmer page

* In the dialog box that opens, select "DFU in FS Mode" and then click "Connect"

* Unzip the kali________.zip you downloaded, near the bottom of the programmer page will be an option to select a file from your computer, choose Kali.bin from the unzipped archive.

### Troubleshooting

* If the daisy patch submodule does not show up when using the web programmer:   
If the screen is on and/or you can see flashing LEDs on the front side, unplug it, hold down the 'boot' button on the daisy patch submodule, and plug it back in.

If the LED on the board is on, this indicates it is in firmware updating mode. If it isn't showing up in this state try another micro-usb cable as some are only for power, and are missing the wires for data. There is usually no way to visually distinguish this.

* If the screen does not turn on:
This was a problem in early versions of the firmware, so first make sure your firmware is the latest. If that does not fix it:   

* Plug the daisy patch submodule in via USB (no Eurorack power).
* If you've got some flashing sync lights on the front panel, this means that the firmware is running, but the screen was not successfully initialized (likely), not firmly plugged in (not as likely), or is dead (rare).
* To confirm that the screen is not loose or dead: Press the 'reset' button on the daisy patch submodule and it will re-initialize everything. The screen show now work.
* If the screen is still not working, check to see if the screen is loose. There's only ~1mm of space between the front panel and the connector side of the screen, so it would be unusual for it to be unseated, but it's possible.
* Unplug the submodule and with some sort of non-conductive blunt but thin object (like the eraser end of a pencil) press gently but firmly down on the left side of the screen, as close as you can possibly get to the edge. It won't take much pressure. [Note that the right side of the screen is not reinforced, and can be pushed in, so avoid that side!]
* Now repeat the first three steps.
* If you are still having problems, the screen may indeed be dead, luckily these are inexpensive and fairly easy to swap. Please get in touch and we can arrange a replacement. If you are comfortable taking the panel off we can send just a new screen, if not we will sort it out!
