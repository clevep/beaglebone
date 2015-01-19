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
	1. sudo adduser (username)
	2. sudo visudo
		* add: (username)    ALL=(ALL:ALL) ALL
	3. su (username)
	4. __From here on out, everything can be done headless.__
4. Create ssh keys
	* ssh-keygen -t rsa -C "your_email@example.com"
5. Download this repo
	1. Add public ssh key to github: https://github.com/settings/ssh
	2. git clone git@github.com:clevep/beaglebone


## Get USB sound working

Install packages:

	sudo apt-get install libasound2 libasound2-doc alsa-base alsa-utils alsa-oss alsamixergui mpd mpc


List sound cards:

	aplay -l

You should see both the on-board HDMI sound card (boo) and your USB sound card (yay).


Test your sound card:

	aplay -D hw:1,0 test.wav


The device format is: 

	hw:(soundcard),(device)


If that works, configure it to be the default:

	sudo vim /etc/asound.conf

Enter:

        pcm.!default {
		type hw
		card 1
	}

	ctl.!default {
		type hw
		card 1
	}

Restart alsa and test:

	sudo /etc/init.d/alsa-utils restart
	aplay test.wav

Control volume using alsamixer.

Test recording:

	arecord -f S16_LE -Dplug:default /tmp/test-recording.wav

Ctrl+C to stop recording.

	aplay -f S16_LE -Dplug:default /tmp/test-recording.wav


### Links

* https://groups.google.com/forum/#!topic/beagleboard/8uRhKoaXlvA
* http://www.debianhelp.co.uk/sound.htm
* http://www.alsa-project.org/main/index.php/Asoundrc
* http://www.mythtv.org/wiki/Digital_Audio_Tutorial
