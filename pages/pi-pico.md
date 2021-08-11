---
layout: page
title: Pi Pico
permalink: /guide/pi-pico/
---

## Introduction

Experimental build using Raspberry Pi Pico to communicate with pronged and infrared Digimon toys. There is a choice between Arduino and CircuitPython firmware, providing different functionality. This is a brief guide for people already familiar with the project.

The Alpha apps on Android do not currently work with the Pi Pico, but an update is expected soon.

This document is part of the DMComm Software under the [MIT License](https://github.com/dmcomm/dmcomm-python/blob/main/LICENSE.txt). 

## Circuit

* [Schematic](/images/pi_pico_schematic.pdf)
* [Example breadboard diagram](/images/pi_pico_breadboard.png)
* [Example breadboard photo](/images/pi_pico_breadboard.jpg) - note the breadboard in the photo is a rare one with 6 rows on each side, but the same layout should fit on a normal 5-row breadboard.

The schematic shows the different sections of the circuit for each type of device. You can leave out any sections you're not using. The Xros Loader section is not entirely working, and may change to something completely different or be abandoned, so I'd only suggest building that if you're really keen to help!

The new prong circuit is a 3-state level shifter like a D-Com, but with far fewer components. (It can't be used on 8-bit AVR because of a difference in how the pins are controlled.)

## Arduino

In the Arduino IDE, install "Arduino Mbed OS RP2040 Boards" using the Boards Manager. To flash the Pi Pico using Arduino for the first time, you need to hold the BOOTSEL button while connecting to the computer. Flash the sketch from the [pi-pico branch](https://github.com/dmcomm/dmcomm-project/blob/pi-pico/dmcomm/dmcomm.ino). You can right-click the "Raw" button and choose "Save as" to download the single file.

Only pronged devices are currently supported. Usage is the same as for the original version (except currently missing the "T" command).

## CircuitPython

### Setup

* Download latest CircuitPython from [the S3 storage](https://adafruit-circuit-python.s3.amazonaws.com/index.html?prefix=bin/raspberry_pi_pico/) (even 7.0 alpha 5 is missing something essential).
* Connect the Pi Pico to the computer while holding the BOOTSEL button. The RPI-RP2 drive should appear.
* Copy the CircuitPython image to the RPI-RP2 drive. The CIRCUITPY drive should appear.
* Get the [dmcomm-python](https://github.com/dmcomm/dmcomm-python) repo. If you don't have Git, you can use the "Download ZIP" option.
* Copy `code.py` and the `lib` folder to the CIRCUITPY drive (there might already be a `lib` folder there, so really you are copying the `lib/dmcomm` folder into it).
* Now you can send commands using the desktop version of Alpha Serial as usual. Alpha Terminal does not appear to be working.

### Usage

* Pronged protocols are the same as for the Arduino version.
* Experimental protocols start with "!". These may change at any time.
* "!IC" for the iC uses the same 16-bit system as prongs, including the "@" and "^" calculation options. This protocol seems to be done, and will probably exit the "!" land as soon as I make a decision about how to label the protocols.
* "!DL" and "!FL" for the Data Link and Fusion Loader have a variable number of bytes in each packet, and currently no calculation options. These protocols will probably change.
* Turn "0" is not fully supported on infrared (will only capture one packet).
* For iC, Data Link and Fusion Loader, don't hold it too close to the circuit. Using the layout above, about 5cm from the LED seems good.
* Xros Loader is not supported in this version. Please get in touch if you want to help gather data.

### iC

* `!IC1-C067-4257-0197-0007-81C7` - example battle ("gao-chu-3" from the spreadsheet)

### Data Link

* `!DL1-3600B1000800002416300111-E7B1B1000800002416300111` - example battle
* `!DL1-D500B11000000113-86B1B11000000113` - give 10 points (going first)
* `!DL2-86B1B11000000113-86B1B11000000113` - give 10 points (going second)
* `!DL1-D500B10000100113-86B1B10000100113` - take points (going first)
* `!DL2-96B1B11000100113-96B1B11000100113` - take points (going second)

### Fusion Loader

This device seems to retry individual packets. The software doesn't do this, which basically means the device gets stuck for an annoyingly long time after a communication error, but it does work most of the time.

For trading, only the sending side can initiate. Data from the receiving side seems to differ, but the sending side doesn't seem to care which variant of the receiving data it gets.

* `!FL1-770000000000C04040000000808020880B-FB000000000060900B-C7F0200B` - example battle
* `!FL1-2B00200B-9B4040A00B-C7F0200B` - send Agumon
* `!FL1-2B00200B-C73040A00B-C7F0200B` - send Aquilamon
* `!FL1-2B00200B-67F040A00B-C7F0200B` - send Ballistamon
* `!FL1-2B00200B-20B440A00B-C7F0200B` - send Devimon
* `!FL1-2B00200B-049240A00B-C7F0200B` - send Guardromon
* `!FL2-AB80200B-5B40C0A00B-7B50200B` - receive Agumon (or anyone really)
* `!FL2-AB80200B-2730C0A00B-7B50200B` - receive Aquilamon (or anyone really)
* `!FL2-AB80200B-5B40C0A00B` - receive dummy code (so you don't lose your Digimon)

### Further research

Let's chat before duplicating effort! There is a big spreadsheet for the iC already.

For the iC, the redundant bits have already been found and processed. For the other two devices, there is probably something like that too which we don't know about yet.
