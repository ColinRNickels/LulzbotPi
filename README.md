# Lulzbot Pi Project
![LulzbotPi Project](https://i.imgur.com/x3jztbd.jpg)

## Overview

The NCSU Libraries' [D. H. Hill Library Makerspace](https://www.lib.ncsu.edu/do/make-at-hill) is a hands on DIY style makerspace. We have 12 [Lulzbot Mini](https://www.lulzbot.com/store/printers/lulzbot-mini) 3D Printers that we allow students to use themselves. While we do provide training and one on one assistance, our users experienced failure frequently due to software issues on our MacBook Air computers running [Cura Lulzbot Edition](https://www.lulzbot.com/cura). Additionally, the need to constantly tether these 3D printers to full size laptops limited the amount of space available for other projects. We decided we needed a new method of running these printers that was smaller, more reliable, and easy to use. This is the result of that project.

## Features

- Small footprint
- Easy to use
- Open Source Software
- Inexpensive per Unit
- No custom development
- Highly Reliable

## Hardware

*This section will contain a full BOM*

## Software

- [Octopi](https://octopi.octoprint.org/)
- [Octoprint-TouchUI](https://github.com/BillyBlaze/OctoPrint-TouchUI)
- [Scrollbar Anywhere](https://chrome.google.com/webstore/detail/scrollbar-anywhere/namcaplenodjnggbfkbopdbfngponici?hl=en)
- [Etcher](etcher.io)

## Implementation Notes

### Installing Octopi and Octoprint-TouchUI
1. Download the latest version of Octopi at http://octoprint.org/download/
2. Download and install etcher (or similar imaging tool) https://etcher.io/
3. Connect MicroSD card to computer
4. Use Etcher to install the octopi image onto the MicroSD card. (Etcher should select the right drive automatically, if you only have one connected)
5. Insert imaged MicroSD card into Raspberry Pi and boot Pi.
6. Log in on the command line (default user is pi, default password is raspberry).
7. Type the following command - sudo nano /etc/network/interfaces
8. Delete everything in this document (control + k will delete an entire line)
9. Add the following lines:
```
auto wlan0
iface wlan0 inet dhcp
	wireless-essid [your ssid]
	wireless-mode managed
```
 *use managed if you are authenticated via mac address, if you have some other network configuration see [this tutorial](http://weworkweplay.com/play/automatically-connect-a-raspberry-pi-to-a-wifi-network/)
 
10. Press control + x to exit. Press y to save changes
11. Type sudo reboot - and then wait for it to restart
12. Wait for device to boot, it should give you a set of ip addresses (ex. 10.139.180.100) to go to on your computer on the NCSU network. Go to one of them
13. Go to the settings in octoprint, then plugins. Then install the touchUI plugin.
14. Then back on the rapsberry pi type sudo apt-get update (this might take a few minutes)
15. Then follow the directions here: https://github.com/BillyBlaze/OctoPrint-TouchUI/wiki/Setup:-Boot-to-Browser-(OctoPi-or-Jessie-Light)
16. Reboot device - it should boot directly to touchui now.

### Setting up scrolling
1. Ensure you're connected to the internet
2. Press Ctrl + alt + f3 to get to a terminal window
3. Enter the command ```sudo nano _____________ chromium.xinit``` 
4. Comment out kiosk mode in the start up options for chromium
5. Reboot
6. In Chromium, go to extensions
7. Install scroll anywhere extension
8. Repeat steps 2 - 4 this time restoring kiosk mode.
9. Reboot

### Setting up the screen
Follow the directions [here](https://learn.adafruit.com/adafruit-5-800x480-tft-hdmi-monitor-touchscreen-backpack/raspberry-pi-config) to force the correct resolution

### Setting up the keyboard
1. press ctrl + alt + F3 to get a terminal window.
2. run ```sudo raspi-config```
3. Select 4. Internationalisation options
4. Select Change Keyboard Layout
5. Select the appropriate layout (we chose US)

### Setting up USB automount
*This section in progress*
1. press ctrl + alt + F3 to get a terminal window.
2. Enter ```sudo apt-get install usbmount ```
3. Enter ```sudo nano /etc/usbmount/usbmount.conf```
4. Change the first mountpoint from ```/media/usb0``` to the default directory that octoprint looks for gcodes ```_____```

### Saving an image
*This section yet to come*
