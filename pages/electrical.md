---
layout: page
title: Electrical
permalink: /electrical/
---

## Misc

All these items take turns to transmit packets of 16 data bits, with LSB first.

[AlphaCom background info](https://www.alphahub.site/guide). The ACom variants used for testing here are mostly made with E3 series resistors, named after R1, with R2 equal to R1 plus the resistor 2 ranks below it. For example: R1=4K7 with R2=4K7+1K; R1=10K with R2=10K+2K2. R1=3K6 with R2=4K7 is also present, to be closer to the ACom recommended values.

For the Digimon's pull-down resistance (call it Rd): note that the test point connects to the ACom's supply voltage through R1, and to ground though R2 and Rd in parallel.

## Original V-Pet

Testing an Old Japanese V1. ACom supply voltage at 4.8V.

Not connected: [zoomed out](/images/scope/vpet_open_20ms.png), [left](/images/scope/vpet_open1.png), [right](/images/scope/vpet_open2.png). Peaks 2.9V. Listening 2.6V to 2.8V with significant ripple. ([This](/images/scope/vpet_open_ripple_later.png) taken later, showing a slightly lower voltage. 50Hz ripple could be mains interference. Turning off the sound makes no difference.) Initial pull-down 64ms. Start bit 2.0ms high, 0.9ms low. Bit one 2.7ms high, 1.6ms low. Bit zero 1ms high, 3.3ms low. Bit length 4.3ms for both one and zero. After final bit, drives high, then releases after ~0.2ms.

[100K across](/images/scope/vpet_100k.png). Listening drops to 1.4V, so the weak pull-up is ~100K. Peaks drop to 2.8V, so the strong pull-up is ~~3K.

[47K across](/images/scope/vpet_47k_pulled.png). Listening drops to 1.0V and the V-Pet detects it (will not transmit). Threshold is between 1.0V and 1.4V.

[With 22K ACom](/images/scope/vpet_ar22k.png). Valleys rise to 0.6V.

[With 3K6 ACom](/images/scope/vpet_ar3k6.png). Valleys rise to 1.7V, so the pull-down is ~3K. Peaks drop to 2.8V.

[22K ACom transmits](/images/scope/vpet_as22k.png). Valleys rise to 0.3V. This is OK.

[4K7 ACom transmits and V-Pet replies](/images/scope/vpet_asr4k7.png). Transmission is good. V-Pet replies after 18.6ms.

## Original Pendulum

Testing an Asia release Pendulum 4.5. ACom supply voltage at 4.8V.

Not connected: [zoomed out before](/images/scope/pen_open_20ms_before.png), [zoomed out](/images/scope/pen_open_20ms.png), [left](/images/scope/pen_open1.png), [right](/images/scope/pen_open2.png). Peaks 2.2V-2.4V. Valleys 0.1V. Listening 1.8V (with a slight 50Hz ripple; the higher-frequency ripple in these screenshots was not there later and is probably also interference). Initial pull-down 60ms. Start bit 2.0ms high, 0.9ms low. Bit one 2.6ms high, 1.5ms low. Bit zero 0.9ms high, 3.2ms low. Bit length 4.1ms for both one and zero. After final bit, drives high, then releases pretty much immediately, with some capacitive decay back to the listening level.

[220K across](/images/scope/pen_220k.png). Listening drops to 1.3V, so the weak pull-up is ~360K. Peaks drop to 2.2V-2.3V, say an 0.05V drop, so the strong pull-up is ~~5K.

[100K across](/images/scope/pen_100k_pulled.png). Listening drops to 1.0V-1.1V and the Pendulum detects it (will not transmit). Threshold is between 1.0V and 1.3V.

[With 22K ACom](/images/scope/pen_ar22k.png). Valleys rise to 0.3V.

[With 3K6 ACom](/images/scope/pen_ar3k6.png). Valleys rise to 1.0V, so the pull-down is ~1K2. Peaks rise to 2.5V.

[4K7 ACom transmits and Pendulum replies](/images/scope/pen_asr4k7.png). Transmission is good. Pendulum replies after 8.2ms.

[22K ACom transmits and Pendulum replies](/images/scope/pen_asr22k.png). ACom's valleys rise to 0.2V. Note the capacitive loading. Pendulum replies after 4.1ms this time. Other reply times were observed which fell between the two (seems unrelated to the resistance).

[22K ACom transmits (zoomed in)](/images/scope/pen_as22k_1ms.png). [1K ACom for comparison](/images/scope/pen_as1k_1ms.png) suggesting that the input resistance is negligible and we can treat this as a pure capacitive input. With the 22K, rise and fall times 20%-80% are ~160us, suggesting a capacitance of ~5nF.

