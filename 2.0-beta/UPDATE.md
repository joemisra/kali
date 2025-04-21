## Firmware!

### Update 

You will need Chrome and a good micro-usb cable.

**keep eurorack power off while using usb** 

[Download most recent Kali beta firmware from this repository](https://github.com/joemisra/kali/beta-2.0)
* Unzip the firmware if it isn't already, you will see Kali.bin
* In a Chrome browser window, navigate to the [Electrosmith Web Programmer](https://electro-smith.github.io/Programmer/). This will not work in Safari.
* Once there, while holding down the BOOT button (circled below) connect the Daisy Patch Submodule on the back of Kali to your computer using a micro USB cable.
![IMG_7858](https://user-images.githubusercontent.com/326734/189494464-a1afc99d-b773-4440-bfa1-7d2296a3fbbe.png)
* If you have successfully entered the bootloader, the right/left sync LED will be on.
![IMG_7862](https://user-images.githubusercontent.com/326734/189494472-ecba0036-2e82-45a8-8dbf-5607bd30f60e.png)
* Connect Daisy as a DFU device by **clicking the "Connect" button** at the top of the Electrosmith Web Programmer page
* In the dialog box that opens, select **"DFU in FS Mode"** and then click "Connect"
* If this is successful, scroll down to the last section on the page
* Click the button where it says **Choose File** and select the unzipped Kali.bin file.
* Now you can click the **Program** button. (uploader_section.png)

#### Troubleshooting

### If the daisy patch submodule does not show up when using the web programmer:   
* Some micro usb cables only supply power and there is generally no way to distinguish them, avoid the ones that come with chargers.
* If the screen is on and/or you can see flashing LEDs on the front side, unplug it, hold down the 'boot' button on the daisy patch submodule, and plug it back in.

