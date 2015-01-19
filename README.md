# beaglebone
Notes and useful files I've collected while playing with my Beaglebone Black.

## Upgrade your image using a SD card on OSX

### Links

1. [Instructions](http://beagleboard.org/getting-started)
2. [Images](http://beagleboard.org/latest-images)
3. Might need XZ Utils to decompress the image
	* [Project page](http://tukaani.org/xz/)
	* [OSX package](http://sourceforge.net/projects/macpkg/files/XZ/5.0.7/XZ.pkg/download)
	* To decompress an xz file: xz -d foo.xz
4. [Ubuntu info](http://elinux.org/BeagleBoardUbuntu)

###  Image your SD card

	diskutil list

Identify your SD card. Mine was /dev/disk3.

Make sure the infile and outfile are set properly in the next code or you can do serious damage. this process will be time consuming.

	diskutil unmount disk3
	sudo dd if=images/BBB-eMMC-flasher-debian-7.5-2014-05-14-2gb.img of=/dev/disk3

This took me roughly 30 minutes.

Power down the BBB, insert the SD card, and power up the board while holding down the boot button (next to the Micro HDMI port).

The image will now install. When the LEDs stop blinking, the image is installed (this can take ~45 mins). Reboot the board.


## First boot for your BBB

1. Connect network, monitor, keyboard, and mouse.
2. If on wireless:
	1. Open the Wicd Network Manager
	2. Open preferences, add wlan0 as the wireless interface, click ok
	3. Click refresh, connect to wifi
3. Add user
	* sudo adduser (username)
	* sudo visudo
		* add: (username)    ALL=(ALL:ALL) ALL
	* su (username)
	* __From here on out, everything can be done headless.__
4. Create ssh keys
	* ssh-keygen -t rsa -C "your_email@example.com"
5. Download this repo
	* Add public ssh key to github: https://github.com/settings/ssh
	* git clone git@github.com:clevep/beaglebone


## Get sound working

### Links

* http://www.debianhelp.co.uk/sound.htm
