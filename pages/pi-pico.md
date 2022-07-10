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
* Alpha Terminal on Android: OK; make sure you have the new version from Google Play.
* Alpha Serial on Android: not working; we are looking into it.
* W0rld on Windows: OK when using the `data` serial port (see below).
* W0rld on Android: not working; we are looking into it.
* ACom Wiki on Android: OK.

## Circuit

* [Schematic](/images/pi_pico_schematic.pdf) (updated 2022-07-10)
* [Example breadboard diagram](/images/pi_pico_breadboard.png) - with prongs and all IR including Xros Loader, but not the button.
* [Example breadboard photo](/images/pi_pico_breadboard.jpg) - as in the diagram above. Note the breadboard in the photo is a rare one with 6 rows on each side, but the same layout should fit on a normal 5-row breadboard.
* [Photo with just the IR components, from the side](/images/pi_pico_ir_components.jpg) - TSMP58000 at the back, TSOP4838 directly in front of it - if using both, cut the TSOP4838 shorter so the TSMP58000 can see over it.

The schematic shows the different sections of the circuit for each type of device. You can leave out any sections you're not using. The IR LED circuit can be used by itself for D-Scanner barcodes, and in that case a red LED also works. The Xros Loader section is not entirely working, and may change to something completely different or be abandoned, so I'd only suggest building that if you're really keen to help!

The new prong circuit is a 3-state level shifter like a D-Com, but with far fewer components. (It can't be used on 8-bit AVR because of a difference in how the pins are controlled.)

### Parts list

Insulated breadboard wires are good for connecting far-apart holes, and can be used for connectors to pronged toys. For short breadboard connections of 2-5 holes with no other components in between, you can get a neater result by using legs cut from extra resistors.

Base ([breadboard](/images/pi_pico_button.jpg)):
* Pi Pico with headers
* 400 tie point breadboard
* small pushbutton (tactile switch) recommended if using CircuitPython
    * typically 3×3 on breadboard, but can insert 2 pins and flatten the others
    * a wire can be used instead: add for updates; remove for normal use

Prong circuit ([breadboard](/images/pi_pico_prongs.jpg)):
* Resistors, 1 each of 470K, 100K, 4K7, 1K
* 1nF ceramic capacitor
* 3 short wires
* Connector to toy e.g. 2 breadboard wires

IR LED circuit ([breadboard](/images/pi_pico_ir_led.jpg)), shared between all IR devices and D-Scanner barcodes:
* 950nm IR LED
* 220R resistor
* 1 short wire
    * can be shared with prong circuit
    * or can connect resistor to nearby ground pin instead, but it's a bit tight

Data Link and Fusion Loader ([front-right in this photo](/images/pi_pico_ir_components.jpg)):
* TSOP4838 IR sensor

iC/Twin/DigiWindow ([breadboard](/images/pi_pico_ic.jpg)):
* TSMP58000 IR sensor
* 22K resistor
* 1nF ceramic capacitor
* 2 short wires

Xros Loader (highly experimental):
* QSE159 IR sensor
* 220R resistor
* 2 × 100nF ceramic capacitor
* 2 short wires
* 2 breadboard wires

Talispod/dam (experimental):
* 1K2 resistor
* 4K7 resistor
* 1nF ceramic capacitor
* 3 short wires
* 1 breadboard wire
* Connector to the toy
    * Note: we can't just stick wires into the prongs as with Digimon
    * Craft a connector?
    * Desolder a Talisdam cord, replace with something else, and use the cord with other toys?
    * Custom connectors are in development

## Arduino

Only pronged devices are currently supported. Usage is the same as for the original version, except currently missing the "T" command. Almost all the code is the same as the original version, so this is probably more reliable than the CircuitPython firmware option.

In the Arduino IDE, install "Arduino Mbed OS RP2040 Boards" using the Boards Manager. (This project uses the official Arduino support and not the older unofficial one from Earle Philhower.) To flash the Pi Pico using Arduino for the first time, you need to hold the BOOTSEL button while connecting to the computer. Flash the sketch from the [pi-pico branch](https://github.com/dmcomm/dmcomm-project/blob/pi-pico/dmcomm/dmcomm.ino). You can right-click the "Raw" button and choose "Save as" to download the single file.

## CircuitPython

### Setup

* Download CircuitPython 7 from the [website](https://circuitpython.org/board/raspberry_pi_pico/). Tested with `7.3.1`. More recent `7.x.x` will probably work.
* Connect the Pi Pico to the computer while holding the BOOTSEL button. The RPI-RP2 drive should appear.
* Copy the CircuitPython image to the RPI-RP2 drive. The CIRCUITPY drive should appear.
* Get the [dmcomm-python](https://github.com/dmcomm/dmcomm-python) repo. If you don't have Git, you can use the "Download ZIP" option.
* Copy `code.py` and the `lib` folder to the CIRCUITPY drive (there might already be a `lib` folder there, so really you are copying the `lib/dmcomm` folder into it).
* Copy `boot.py` too if you want to switch to the `data` serial port and disable the CIRCUITPY drive (unless the custom button is held at startup). The `data` serial port is required for w0rld, but may not show all error messages. The CIRCUITPY drive is required for updating DMComm, but can make the program restart unexpectedly.
* Now you can use the Alpha apps or ACom Wiki as usual. Alpha Serial shows some odd output at startup, but this is not a problem.
* To update CircuitPython, repeat the first three steps.
* To update DMComm, replace the specified files on the CIRCUITPY drive with new ones from the git repo. If you copied `boot.py` earlier, connect the Pi Pico to the computer while holding the custom button (wait until CIRCUITPY appears before releasing the button). If you copied `boot.py` and don't have a button, connect GP3 to GND with a wire, then connect the Pi Pico to the computer.

### Usage

* Pronged protocols are the same as for the Arduino version.
* "IC" for the iC uses the same 16-bit system as prongs, including the "@" and "^" calculation options. (Nothing changed from the experimental "!IC", so if you have a "!IC" code, you can just remove the "!".)
* "BC" for D-Scanner barcodes takes 13 decimal digits, and is used only with turn "1" because it is transmit-only. (Nothing changed from the experimental "!BC", so if you have a "!BC" code, you can just remove the "!".)
* Experimental protocols start with "!". These may change at any time.
* "!DL" and "!!FL" for the Data Link and Fusion Loader have a variable number of bytes in each packet, and currently no calculation options. These protocols will probably change. "!FL" codes had the bits in reverse order: to use them with the latest version, they will need to be converted using `utils/bit_reverse.py`.
* Turn "0" is not fully supported on infrared (will only capture one packet).
* For iC, Twin, Data Link and Fusion Loader, don't hold it too close to the circuit. Using the layout above, about 5cm from the LED seems good. For the Twin, hold it at an angle so the IR window is facing the LED (even connecting two Twins, holding them with the corners facing gives a much longer range than the way you're apparently supposed to hold them).
* For D-Scanner barcodes, hold the barcode scanner close to the LED, maybe almost touching.
* Xros Loader is not supported in this version. Please get in touch if you want to help gather data.

### iC

* `IC1-C067-4257-0197-0007-@F007` - Battle with iC 10x for Digi Shop 1
* `IC1-D067-4257-0197-0007-@F007` - Battle with iC 20x for Digi Shop 2
* `IC1-E067-4257-0197-0007-@F007` - Battle with Burst for Digi Shop 3
* `IC1-D577-4927-0B47-0007-@F007` - Battle with DigiWindow for Digi Shop 4

### Twin

jyoshiikuta shared a [spreadsheet](https://docs.google.com/spreadsheets/d/1-puBPGGxOGDkeOiYYP0wp9RQacDEvTBs/edit).

### Fusion Loader

This device seems to retry individual packets. The software doesn't do this, which basically means the toy gets stuck for an annoyingly long time after a communication error, but it does work most of the time.

For trading, only the sending side can initiate. The receiving side varies with the Digimon sent. If it does not match, the communication completes and the toy says "OK", but the Digimon has not actually gone.

* `!!FL1-D0110401010000000202030000000000EE-D009060000000000DF-D0040FE3` - example battle
* `!!FL1-D00400D4-D0050202D9-D0040FE3` - send Agumon
* `!!FL1-D00400D4-D005020CE3-D0040FE3` - send Aquilamon
* `!!FL1-D00400D4-D005020FE6-D0040FE3` - send Ballistamon
* `!!FL1-D00400D4-D005022D04-D0040FE3` - send Devimon
* `!!FL1-D00400D4-D005024920-D0040FE3` - send Guardromon
* `!!FL2-D00401D5-D0050302DA-D0040ADE` - receive Agumon
* `!!FL2-D00401D5-D005030CE4-D0040ADE` - receive Aquilamon

### D-Scanner

* `BC1-0000000000111` - scan Gabumon on D-Scanner v1
* `BC1-0000000020211` - scan Renamon on D-Scanner v2
* `BC1-0000000750311` - scan Bearmon on D-Scanner v3

The complete list is in a [spreadsheet](https://docs.google.com/spreadsheets/d/1wiIKQ0mRrzf5UuVdZyyg1QeLWvLohZ7D/edit).

### Further research

Let's chat before duplicating effort! A lot of data has been gathered already.

For the iC, the redundant bits have already been found and processed. For the Data Link and Fusion Loader, there could be something like that too which we don't know about yet.

Codes for the Data Link appear to change according to some sort of player ID value.
