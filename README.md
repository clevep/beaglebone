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

###  Image your SD card

	diskutil list

Identify your SD card. Mine was /dev/disk3.

Make sure the infile and outfile are set properly in the next code or you can do serious damage. this process will be time consuming.

	diskutil unmount disk3
	sudo dd if=images/BBB-eMMC-flasher-debian-7.5-2014-05-14-2gb.img of=/dev/disk3

