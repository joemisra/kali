# dsp.coffee KALI

![kbaliwakeup-7](https://user-images.githubusercontent.com/326734/182261061-2471d0ba-7678-4e46-93a4-f95b2bcd2673.png)

For detailed information please check the KALI Wiki:

https://github.com/joemisra/kali/wiki

Or join the dsp.coffee dev Discord server:

https://discord.gg/KxttAMc9tw

## Firmware!

### Update 

**keep eurorack power off while using usb** 

* [Download most recent Kali firmware from this repository](https://github.com/joemisra/kali/tree/main/firmware).

* In a Chrome browser window, navigate to the [Electrosmith Web Programmer](https://electro-smith.github.io/Programmer/)

* Once there, while holding down the BOOT button (circled below) connect the Daisy Patch Submodule on the back of Kali to your computer using a micro USB cable.

![IMG_7858](https://user-images.githubusercontent.com/326734/189494464-a1afc99d-b773-4440-bfa1-7d2296a3fbbe.png)

* If you have successfully entered the bootloader, the right sync LED will be on.

![IMG_7862](https://user-images.githubusercontent.com/326734/189494472-ecba0036-2e82-45a8-8dbf-5607bd30f60e.png)

* Connect Daisy as a DFU device by clicking the "Connect" button at the top of the Web Programmer page

* In the dialog box that opens, select "DFU in FS Mode" and then click "Connect"

* Unzip the kali________.zip you downloaded, near the bottom of the programmer page will be an option to select a file from your computer, choose Kali.bin from the unzipped archive.

#### Troubleshooting

### If the daisy patch submodule does not show up when using the web programmer:   
* Some micro usb cables only supply power and there is generally no way to distinguish them, avoid the ones that come with chargers.
* If the screen is on and/or you can see flashing LEDs on the front side, unplug it, hold down the 'boot' button on the daisy patch submodule, and plug it back in.

