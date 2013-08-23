---
layout: post
title: "DFU-Programmer Linux Tips Aery32 Rev0"
description: "Some DFU Programmer issues Encountered by a First time User"
author: "SETKEH"
author-email: "setkeh@gmail.com"

tags:
- "git"

categories:
- article

level: beginner

tweet-text: "DFU-Programmer Tips Aery32 Rev0 #aery32devzone"

summary: "First time Users Observations and Encountered Issues With DFU-Programmer using aery32 Rev0"
---

<div style="margin: 15px 0; font-size: 10px;">
<img style="margin-bottom: 5px;" itemprop="image" src="http://th04.deviantart.net/fs70/PRE/f/2013/100/6/f/simple_gnu_linux_wallpaper_by_dablim-d5kdma2.jpg" alt="Linux logo" />Linux Logo by Dablim is licensed under the Creative Commons Attribution 3.0 Unported License.
</div>

I am a First time Aery32 user and fairly new to Micro Controllers all together and i Recently had an Aery32 Donated to me and i have just had a chance to look at seting it up ill go through how i did it.
Im Running Archlinux 64Bit on Kernel 3.10.7-1-ARCH as of this writing though it should work on all Linux Distro's.

The Setup.
----------
So the initial setup is farily easy, Most of these Steps can be found in the [Quick Start Guide.](http://www.aery32.com/quick-start/)

First things First install DFU-Programmer

Ubuntu:
	
	sudo apt-get install dfu-programmer

Archlinux: 
You Can use Yaourt or your Favorite AUR Helper
	
	yaourt dfu-programmer

or you can [Download the AUR Tarball](https://aur.archlinux.org/packages/df/dfu-programmer/dfu-programmer.tar.gz) and user makepkg to build a DFU-Programmer Archlinux Package and install it Using.

	sudo pacman -U *.pkg.tar.xz

Then Follow [AVR 32-bit Toolchain on Linux](http://devzone.aery32.com/2012/07/06/how-to-install-avr-32-bit-toolchain-on-linux/) by Kim Blomqvist Who Kindly Posted that to Devzone.

Then you can Clone the [Aery32 Github Repo](https://github.com/aery32/aery32).

	git clone https://github.com/aery32/aery32

Then

	cd aery32

The Last Thing to do is add a Udev Rule so that your linux Machine can see and give you access to your aery32 following [W|zzys Guide for Udev](http://blog.padman.id.au/?p=61) You will also need to Add your user to the plugdev group.

	sudo gpasswd -a YouUserName plugdev

Awesome were all done :D

Testing.
--------
Now you can Either modify main.cpp as it states in the [Quick Start Guide](http://www.aery32.com/quick-start/) Yourself or you can use [My Pre Modified one](https://gist.github.com/setkeh/6315692).
Then we can compile and uplaod the code to the Aery.

	make programs

This is where i had another issue and the point of writing this article.

	setkeh@Workstation-Arch ~/github/aery32 (git)-[master] % make programs
	dfu-programmer at32uc3a1256 erase
	make: *** [dfu-program] Error 1

NOTE: This is Simaler to the udev error outlined in W|zzy's blog post but its not the same issue and from what i understand and chatting with W|zzy this issue seems to be only an issue on the REV 0 Aery.

The fix for this is pretty simple open up the Aery32 Makefile in your favorite editor.

Change Line41 from:

	MPART=uc3a1256

To:

	MPART=uc3a1128

Now when you run make programs you should see something like this:

	setkeh@Workstation-Arch ~/github/aery32 (git)-[master] % make programs
	dfu-programmer at32uc3a1128 erase
	dfu-programmer at32uc3a1128 flash aery32.hex
	Validating...
	5080 bytes used (4.13%)
	dfu-programmer at32uc3a1128 start
	dfu-programmer: failed to release interface 0.
	make: *** [dfu-start] Error 1

Now im not 100% sure what the failed to release error is all about though it can be safely ignored and you program should start running after the make is completed it does not seem to have any bearing on the operation of the toolchain and Aery at all dispite this error my programs compile and upload fine of course if you know how to fix it please hit me up in #aery32 on freenode.

I hope this helps any newbies like myself get there aery32 boards setup ready for development in there linux enviroments, I have Enjoyed writing this article and hope to write more :D
Good luck on your Aery Projects.
