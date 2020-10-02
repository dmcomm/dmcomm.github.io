---
layout: page
title: Xros Wars Mini
permalink: /xros_mini/
---

## Electrical

The voltage levels are inverted compared with the other devices, i.e. the line is at 0V when nothing is happening. The packet patterns have the same stages (with inverted voltage). Bit 1 is short low, long high. Bit 0 is long low, short high. So if considering this as a case of inverted voltage, the bit patterns are inverted compared with the other devices too.

## Field mapping

* Packet 1
  * 4 bits?: Version? If so, ShoutmonRed = 1
  * 8 bits?: Slot? Is there any sort of attribute here?
  * 4 bits: always 7
* Packet 2
  * 12 bits?: Power. Each Digimon has a minimum and a maximum. Each protein makes it go up by 1. Training makes it go up. Leaving the lights on makes it go down. It also seems to go down slowly by itself, so maybe like Strength but with more than 4 of them. The variable bonus seems to be carried across evolution, so a max power Digimon remains at max power after evolving.
  * 4 bits: always 7
* Packet 3
  * 2 bits?: always 0?
  * 10 bits: Shot sizes. Break into pairs and read the pairs from the right. 0b00=1, 0b01=2, 0b10=3, 0b11=big. E.g. `0x15D = 0b01,01,01,11,01 = shots 2,big,2,2,2`.
  * 4 bits: always 7
* Packet 4
  * 4 bits: CheckDigit @C
  * 3 bits?: always 0?
  * 5 bits: HitMe. Read bits from the right. 1 = I was hit. 0 = I dodged. The device who goes second inverts these bits; but if the device who goes first receives incorrect hit bits in the response, it ignores them when calculating the result.
  * 4 bits: always 7

## Digimon

* Shoutmon: Slot 1, Power 0x05-0x14
* Guilmon: Slot 0x0B, Power 0x15-0x24
* Agumon: Slot 0x0C, Power ?-0x34
* V-Mon: Slot 0x0D, Power ?-0x44
* Shoutmon X4: Slot 0x10, Power ?-0x74

## Codes

* `Y1-1017-0097-2E47-@C1F7` Shoutmon with 9 power shoots 1,2,3,big,3 and loses every round.
* `Y2-1017-0057-0007-@C^1^F7` Shoutmon with 5 power shoots only singles and lets the opponent decide.


