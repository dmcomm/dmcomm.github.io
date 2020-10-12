---
layout: page
title: Original V-Pet
permalink: /vpet/
---

## Protein

These are called "Vitamins" in English.

Each protein restores 1 Strength heart and adds 2 to Weight. Every 4 protein adds 1 to each of 3 different counters: Energy, Pre-Enhancement and Vulnerability. (For all of the preceding, this only happens if the number in question is currently allowed to increase.) The count from 0-3 protein is saved across evolution, though Pre-Enhancement and Vulnerability are not. For example, if a Digimon eats a total of 22 protein during the Baby 1 and Baby 2 stages, the Child stage starts with a protein count of 2, and eating another 2 protein will increase the affected counters.

## Energy

Each species has a default/"full" number of energy, which it resets to upon sleeping for 8 hours continuously. The energy meter looks full at this number.

**No overfill**: Confirmed on English V2 and V3; Japanese V4 and V5. The energy cannot be increased above the default value. To identify this, after a night's sleep, count the number of battles to lose the rightmost energy bar. After another night's sleep, give 4 protein then again count the number of battles to lose the rightmost energy bar. For the same species, the two counts should be the same. On V-Pets where overfill is possible, this test results in the second count being 1 higher.

**Wrapping**: Confirmed on both variants of Japanese V1; Strong English V1; Japanese V2. Overfilling the energy by 10 resets it to the default value. To identify this: 

* Start with any Digimon who normally loses the rightmost energy bar after one battle.
* Let it sleep overnight (energy resets to default).
* Give 40 protein (energy would be default+10, but returns to +0).
* Battle once, and it will lose an energy bar (default-1).
* Give another 40 protein (default+9).
* Battle once, and it won't lose an energy bar (default+8).
* Give another 8 protein (default+10 -> +0 again).
* Battle once, and it will lose an energy bar (default-1).

**Visible overfill**: Only on the Weak English V1. The energy can be filled to 99 without any wrapping; the meter visibly overflows to the right for all Digimon; and at high numbers of energy, Digimon with 10 or 20 default energy will overflow the meter into the top-right followed by the bottom-left corner (the famous "!!!!" glitch).

There are 6 extra energy bars which appear outside the meter. The bottom-right extra bar appears with only a few extra energy, then there is a big gap, then the four bars in the top-right appear one at a time, shortly followed by the one in the bottom-left. Numemon has 10 default energy, gains the first bar in the top-right at 42 energy (128 protein from default) and the bottom-left at 45. Digimon with 20 default energy gain the first bar in the top-right at 84 energy (256 protein from default) and the bottom-left at 90. 

The cap of 99 energy can be checked for 20-energy Digimon by counting relative to the bottom-left extra bar: after giving some number of protein which would mean energy above 99 if there was no cap, they always lose that bar after 10 battles. It can also be checked for Mamemon and Monzaemon due to their immunity to injury at high numbers of protein (see "Vulnerability" below). Other Digimon will die too quickly to check it.

![Energy glitch](/images/vpet_energy_glitch.png)

## Enhancement

First is the Pre-Enhancement counter. Arbitrarily this description supposes that it starts at 0. It resets to 0 when the Digimon evolves. Wrapping the 4-protein counter makes it go up by 1. A care mistake makes it go down by 1. (Contrary to popular belief, training does nothing here.) The full possible range is -4 to +4. But during a single evolution stage, it can only go up 4 times and down 4 times. For example, if you put it up to 3, then it can only go down to -1, and then it can go up to 0 after that. Once it has moved up 4 times and down 4 times, it's stuck at 0 until the Digimon evolves again. Most likely, there are two counters for protein power-up and care mistakes, each ranging from 0-4, with `PreEnhancement = ProteinPowerUp - CareMistakes`.

Then the Pre-Enhancement is combined with the Digimon's current strength hearts to get the final Enhancement value which can be seen in the battle signals. The result is the average of the two, rounded down, with a minimum of 0. However, the Weak English V1 fails to take account of the strength hearts for this calculation, and behaves as if they are always at 0!

![Enhancement result table](/images/vpet_enhancement_table.png)

## Vulnerability

Combined with species, this determines the probability of being injured after battle. It ranges from 0-15 (additional protein after this appear to have no effect).

This was most likely intended to increase the probability of injury when more protein are eaten, but is very buggy. For example, all second and third Perfects become immune to injury at Vulnerability 15. Devimon also does, but only on the Old Japanese V1. On V5, some Digimon also change the number of medical treatments needed when injured. For example, Gazimon changes from 1 to 2 treatments at 4 Vulnerability, Gizamon does so at 6, and Devidramon changes from 5 to 1 treatments at a Vulnerability of 8.

## List of oddities

* Old Japanese V1
  * Maybe the brown and slate coloured ones (with Japan chain/packaging) - more confirmation needed. "Old"/"New" is still a bit of a guess too.
  * Refusing battle or medicine often shows the first walking frame before starting the refusal animation. [The brown one in this video](https://drive.google.com/file/d/0B-WY-Md6XwaxTDYzaU5SbmFwLTQ/view?usp=sharing). To test this, let the Digimon walk for a few frames before interrupting it, or the difference might not appear.
  * Devimon becomes immune to injury at 15 Vulnerability (see above).
* Old/New Japanese V1; Strong English V1; Japanese V2; maybe Japanese V3
  * Energy wrapping at +10 (see above).
* Weak English V1
  * Fails to add the strength hearts when calculating Enhancement (see above).
  * Visible energy overfill (see above).
  * The walk animation differs by one frame. Shortly before snapping at the right-hand side, it faces left for one frame where all the other versions face right. [The brown one in this video](https://drive.google.com/file/d/1rQY_LnlEg9O5bYbjvVNfN84Nm95OK-CS/view?usp=sharing). (Thanks to BetamonZ at WtW for spotting this, and for the video.) This is only visible on non-symmetrical Digimon. It is difficult to see, so I recommend syncing your own Digimon's walk with the video and holding it up alongside.
  * The clock gains 2-3 seconds on hatching, evolution, and possibly some other events. Note this is not a gradual clock drift. (Thanks to BetamonZ at WtW for spotting this.)
* V5 (only checked Japanese) and Weak English V1 (why these two?!)
  * Going into the lights menu and selecting "On", the Digimon resumes walking from the position it was in before, while all the other versions go back to the start of the walking animation.
  * Possibly some sound and visual timing changes in training, battle and the clock screen.
* V5 (only checked Japanese)
  * The number of bars in the energy meter is calculated differently from the others, requiring far more battles to lose the rightmost bar, and then the other bars go more quickly. Details to follow.
  * As Vulnerability increases, some Digimon change the number of medical treatments needed when injured (see above).

