---
layout: page
title: Pi Pico
permalink: /guide/pi-pico/
---

## Introduction

Experimental build using Raspberry Pi Pico to communicate with pronged and infrared Digimon toys. There is a choice between Arduino and CircuitPython firmware, providing different functionality. This is a brief guide for people already familiar with the project.

This document is part of the DMComm Software under the [MIT License](https://github.com/dmcomm/dmcomm-python/blob/main/LICENSE.txt). 

## App status

* Alpha on Windows: OK.
* Alpha on Android: not currently working, but an update is expected soon.
* W0rld on Windows: not working for unknown reasons.
* W0rld on Android: not currently working, but an update is quite likely after Alpha.
* ACom Wiki on Android: OK.

## Circuit

* [Schematic](/images/pi_pico_schematic.pdf)
* [Example breadboard diagram](/images/pi_pico_breadboard.png)
* [Example breadboard photo](/images/pi_pico_breadboard.jpg) - note the breadboard in the photo is a rare one with 6 rows on each side, but the same layout should fit on a normal 5-row breadboard.

The schematic shows the different sections of the circuit for each type of device. You can leave out any sections you're not using. The IR LED circuit can be used by itself for D-Scanner barcodes, and in that case a red LED also works. The Xros Loader section is not entirely working, and may change to something completely different or be abandoned, so I'd only suggest building that if you're really keen to help!

The new prong circuit is a 3-state level shifter like a D-Com, but with far fewer components. (It can't be used on 8-bit AVR because of a difference in how the pins are controlled.)

## Arduino

Only pronged devices are currently supported. Usage is the same as for the original version, except currently missing the "T" command. Almost all the code is the same as the original version, so this is probably more reliable than the CircuitPython firmware option.

In the Arduino IDE, install "Arduino Mbed OS RP2040 Boards" using the Boards Manager. (This project uses the official Arduino support and not the older unofficial one from Earle Philhower.) To flash the Pi Pico using Arduino for the first time, you need to hold the BOOTSEL button while connecting to the computer. Flash the sketch from the [pi-pico branch](https://github.com/dmcomm/dmcomm-project/blob/pi-pico/dmcomm/dmcomm.ino). You can right-click the "Raw" button and choose "Save as" to download the single file.

## CircuitPython

### Setup

* Download CircuitPython 7 from the [website](https://circuitpython.org/board/raspberry_pi_pico/). Tested with `7.0.0`. More recent versions will probably work.
* Connect the Pi Pico to the computer while holding the BOOTSEL button. The RPI-RP2 drive should appear.
* Copy the CircuitPython image to the RPI-RP2 drive. The CIRCUITPY drive should appear.
* Get the [dmcomm-python](https://github.com/dmcomm/dmcomm-python) repo. If you don't have Git, you can use the "Download ZIP" option.
* Copy `code.py` and the `lib` folder to the CIRCUITPY drive (there might already be a `lib` folder there, so really you are copying the `lib/dmcomm` folder into it).
* Now you can use the desktop versions of the Alpha apps as usual. Alpha Serial shows some odd output at startup, but this is not a problem.
* To update CircuitPython, repeat the first three steps. To update DMComm, replace the specified files on the CIRCUITPY drive with new ones from the git repo.

### Usage

* Pronged protocols are the same as for the Arduino version.
* Experimental protocols start with "!". These may change at any time.
* "!IC" for the iC uses the same 16-bit system as prongs, including the "@" and "^" calculation options. This protocol seems to be done, and will probably exit the "!" land as soon as I make a decision about how to label the protocols.
* "!DL" and "!FL" for the Data Link and Fusion Loader have a variable number of bytes in each packet, and currently no calculation options. These protocols will probably change.
* "!BC" for D-Scanner barcodes takes 13 decimal digits, and is used only with turn "1" because it is transmit-only. This protocol also seems to be done.
* Turn "0" is not fully supported on infrared (will only capture one packet).
* For iC, Data Link and Fusion Loader, don't hold it too close to the circuit. Using the layout above, about 5cm from the LED seems good.
* For D-Scanner barcodes, hold the barcode scanner closer to the LED.
* Xros Loader is not supported in this version. Please get in touch if you want to help gather data.

### iC

* `!IC1-C067-4257-0197-0007-81C7` - example battle ("gao-chu-3" from the spreadsheet)

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

### D-Scanner

* `!BC1-0000000000111` - scan Gabumon on D-Scanner v1
* `!BC1-0000000020211` - scan Renamon on D-Scanner v2
* `!BC1-0000000750311` - scan Bearmon on D-Scanner v3

### Further research

Let's chat before duplicating effort! There is a big spreadsheet for the iC already. Barcode data is complete and should be added soon.

For the iC, the redundant bits have already been found and processed. For the Data Link and Fusion Loader, there could be something like that too which we don't know about yet.

Codes for the Data Link appear to change according to some sort of player ID value.
