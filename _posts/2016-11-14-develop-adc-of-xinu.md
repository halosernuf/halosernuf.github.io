---
layout: post
title: "ADC of Beaglebone under Xinu(A Unix like OS)"
date: 2016-11-14 21:12:50
categories: Xinu
tags: ADC Xinu Beaglebone
---

# 1. ADC of AM335x

The internal ADC of AM335x is called TSC\_ADC\_SS (Touchscreen\_ADC\_subsystem), which is an 8 channel general purpose ADC, with optional support for interleaving Touch Screen conversions. The TSC_ADC_SS can be used and configured in one of the following application options:  

8 general purpose ADC channels  
4 wire TS, with 4 general purpose ADC channels  
5 wire TS, with 3 general purpose ADC channels  
8 wire TS  

[<img src="/images/xinu/beaglebone/ADC.png">]()

## 1.1 TSC_ADC properties

There are 7 analog inputs on the BeagleBone.

* ADC properties:  
    * 12 bits (Output values in the range 0-4095)
    * 125ns sample time
    * 0-1.8V range **(do not exceed!)**
    * 2 uA current flows into the ADC pin in this range
    * If using a voltage divider, the lower leg (the one connected to ground) should be <= 1k Ohm
    * Since we are measuring millivolts, resistors with 0.1% error tolerance should be used in a voltage divider.
    * There is a 1.8V reference voltage VDD_ADC at Port 9 Pin 32.
    * There is a GNDA_ADC that should be grounded on Port9 Pin 34.

# 2 Connectivity 

[<img src="/images/xinu/beaglebone/ADC_connectivity.png">]()

## 2.1 CM\_WKUP\_ADC\_TSC\_CLKCTRL

This register inside Control Module wakeup manages the clocks of ADC. As described in the definiation of CM\_WKUP\_ADC\_TSC\_CLKCTRL register default the CTRL is set to 0x0 which means Module is disable by SW. Any OCP access to
module results in an **error**, except if resulting from a module wakeup
(asynchronous wakeup). **No clock no function**

[<img src="/images/xinu/beaglebone/ADC_CLKCTRL.png">]()
