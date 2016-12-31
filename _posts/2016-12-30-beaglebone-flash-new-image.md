---
layout: post
title: "Beaglebone Black Flash New Image"
date:   2016-12-30 23:17:43
categories: "Beaglebone"
---

References:  
[http://beagleboard.org/getting-started](http://beagleboard.org/getting-started)  
[https://gist.github.com/interwebjill/5ee49aa0e199c8515f9be16a4672d730](https://gist.github.com/interwebjill/5ee49aa0e199c8515f9be16a4672d730)  

# 0. What you need

1. microSD card >= 4G
2. Internet
3. Host computer, in my case is a macbook
4. Beaglebone Black

# 1. Download latest image

Download the image from [http://beagleboard.org/latest-images](http://beagleboard.org/latest-images)  
Extract it using Unarchiver for macOS and 7zip for PC

# 2. Write image to mircoSD

List existing storage device 

```
df -h
```

Insert mircoSD card and run list device again to know the name of your microSD card it should be like /dev/disk**N**s1 where **N** is a variant. 

Unmount the microSD card

```
sudo diskutil unmount /dev/diskNs1
```

Then, execute the following command with caution:

```
sudo dd if=/path/to/downloaded.img of=/dev/rdiskN bs=1m
```

replace `/path/to/downloaded.img` with the path where the image file is located, detail can be find [here](https://help.ubuntu.com/community/Installation/FromImgFiles)

Wait... until it finished. You may encounter with an error like "The disk you inserted was not readable by this computer", just ignore it.

# 3. Flash the image to eMMC

1. Unplug all the wires to your Beaglebone Black (powered off)
2. Insert the microSD card into your board
3. Press S2 button while plugging the power (either the 5V or usb)
4. Lift off until you see all four LEDs flashed

Now the Beaglebone Black is booted from your microSD. Then we need to flash the image into the eMMC on board. ssh to board with usb:

```
ssh debian@192.168.7.2
$sudo vim /boot/uEnv.txt
```

uncommment the following line:

```
cmdline=init=/opt/scripts/tools/eMMC/init-eMMC-flasher-v3.sh
```

and shutdown the board:

```
$sudo shutdown now
```

Redo the boot process:

1. Press S2 button while plugging the power (either the 5V or usb)
2. Lift off until you see all four LEDs flashed

Wait for a few second for the system to boot and you will see **Knight Rider** led sequence which indicate the it is flashing to eMMC

This will take up for a long time and the system will shutdown once the process is finished

# 4. Done

Remove microSD card. ssh to your board and run apt upgrade after finished flashing. 

```
sudo apt-get update
sudo apt-get upgrade
```