---
layout: post
title: "Capemgr for Beaglebone with linux 4.4"
date:   2017-3-15 18:34:26
tags: beaglebone capemger
categories: "Beaglebone"
---
# Capemgr

Capemgr was created out of a need for boards like the BeagleBone to be able to detect installed expansion boards at boot time and allocate appropriate resources (load drivers, allocate GPIO, reserve bus addresses, etc) on kernels which use Device Tree. Traditionally, a Device Tree was a static file (or set of files) which described a machine (often an Embedded SoC and the board it's installed on). 

# Beaglebone-universal-io
Device tree overlay and support scripts for using most available hardware I/O on the BeagleBone without editing dts files or rebuilding the kernel.

## Capes

* cape-universal Exports all pins not used by HDMIN and eMMC (including audio)
* cape-universaln Exports all pins not used by HDMI and eMMC (no audio pins are exported)
* cape-unversalh Exports all pins not used by eMMC
* cape-unversala Exports all pins
* cape-univ-emmc Exports pins used by eMMC, load if eMMC is disabled
* cape-univ-hdmi Exports pins used by HDMI video, load if HDMI is disabled
* cape-univ-audio Exports pins used by HDMI audio

# Enable/disable capes with uEnv.txt (on boot):

Modify `/boot/uEnv.txt`:

## Manually

```
bone_capemgr.enable_partno=[part],[part]...
bone_capemgr.disable_partno=[part],[part]...
```

## Use Beaglebone-universal-io

```
cmdline: cape_universal=enable
```

# Enable/disable capes with slots (after boot):
Show slots:
```
debian@beaglebone:~$ cat /sys/devices/platform/bone_capemgr/slots
 0: PF----  -1
 1: PF----  -1
 2: PF----  -1
 3: PF----  -1
```

## Manually
Add devices:
```
sudo sh -c "echo 'BB-UART1' > /sys/devices/platform/bone_capemgr/slots"

[  255.828371] bone_capemgr bone_capemgr: part_number 'BB-UART1', version 'N/A'
[  255.828436] bone_capemgr bone_capemgr: slot #4: override
[  255.828468] bone_capemgr bone_capemgr: Using override eeprom data at slot 4
[  255.828501] bone_capemgr bone_capemgr: slot #4: 'Override Board Name,00A0,Override Manuf,BB-UART1'
[  255.855687] 48022000.serial: ttyS1 at MMIO 0x48022000 (irq = 181, base_baud = 3000000) is a 8250
[  255.856691] bone_capemgr bone_capemgr: slot #4: dtbo 'BB-UART1-00A0.dtbo' loaded; overlay id #0

debian@beaglebone:~$ cat /sys/devices/platform/bone_capemgr/slots
 0: PF----  -1
 1: PF----  -1
 2: PF----  -1
 3: PF----  -1
 4: P-O-L-   0 Override Board Name,00A0,Override Manuf,BB-UART1
```

Remove Device:
```
sudo sh -c "echo '-4' > /sys/devices/platform/bone_capemgr/slots"

[  787.808035] bone_capemgr bone_capemgr: Removed slot #4

debian@beaglebone:~$ cat /sys/devices/platform/bone_capemgr/slots
 0: PF----  -1
 1: PF----  -1
 2: PF----  -1
 3: PF----  -1
```

## Use Beaglebone-universal-io

```
echo [cape-name] > /sys/devices/platform/bone_capemgr/slots
```


# Reference

1. [http://elinux.org/Capemgr](http://elinux.org/Capemgr)
2. [https://github.com/beagleboard/bb.org-overlays/blob/master/readme.md](https://github.com/beagleboard/bb.org-overlays/blob/master/readme.md)
3. [https://github.com/cdsteinkuehler/beaglebone-universal-io](https://github.com/cdsteinkuehler/beaglebone-universal-io)