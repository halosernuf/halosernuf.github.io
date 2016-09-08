---
layout: post
title: beaglebone macos 10.11
date:   2016-09-06 14:25:21 
categories: "Beaglebone"
---
You may found the HoRNDIS rel7 [not function](http://joshuawise.com/horndis) on El Capitan(10.11). The discussion can be found [here](https://github.com/jwise/HoRNDIS/issues/42). The solution is as follows.

### For first time installation:

1. Install [HoRNDIS rel8pre2](http://nyus.joshuawise.com/HoRNDIS-rel8pre2-dbg.pkg)
2. Install [PL2303 driver](/files/beaglebone/PL2303_MacOSX_1_6_0_20151022.zip)
3. Reboot

### If you have tried HoRNDIS rel7

1. Remove previous installation  
   ```sudo rm -rf /System/Library/Extensions/HoRNDIS.kext```  
   ```sudo rm -rf /Library/Extensions/HoRNDIS.kext```  
2. Install [HoRNDIS rel8pre2](http://nyus.joshuawise.com/HoRNDIS-rel8pre2-dbg.pkg)
3. Install [PL2303 driver](/files/beaglebone/PL2303_MacOSX_1_6_0_20151022.zip)
4. Reboot


Connect your board with usb. You may find beaglebone black added to your network
[<img class="center" src="/images/beaglebone/1.png"/>](/images/beaglebone/1.png)