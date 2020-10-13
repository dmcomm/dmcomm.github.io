---
layout: page
title: Electrical
permalink: /electrical/
---

## Misc

These ACom variants are mostly made with E3 series resistors, with the bottom end equal to the top end plus the one 2 ranks below. For example: 4K7 with 4K7+1K; 10K with 10K+2K2. 3K6 with 4K7 is also present, to be closer to the ACom recommended values.

## Original V-Pet

Testing an Old Japanese V1. ACom supply voltage at 4.8V.

Not connected: [zoomed out](/images/scope/vpet_open_20ms.png), [left](/images/scope/vpet_open1.png), [right](/images/scope/vpet_open2.png). Peaks 2.9V. Listening 2.6V to 2.8V with significant ripple. Initial pull-down 64ms. Start bit 2.0ms high, 0.9ms low. Bit one 2.7ms high, 1.6ms low. Bit zero 1ms high, 3.3ms low. Bit length 4.3ms for both one and zero. After final bit, drives high, then releases after ~0.2ms.

[100K across](/images/scope/vpet_100k.png). Listening drops to 1.4V, so the weak pull-up is ~100K. Peaks drop to 2.8V, so the strong pull-up is ~~3K. 

[47K across](/images/scope/vpet_47k_pulled.png). Listening drops to 1.0V and the V-Pet detects it (will not transmit). Threshold is between 1.0V and 1.4V.

[With 22K ACom](/images/scope/vpet_ar22k.png). Valleys rise to 0.6V.

[With 3K6 ACom](/images/scope/vpet_ar3k6.png). Valleys rise to 1.7V, so the pull-down is ~2K. Peaks drop to 2.8V.

[22K ACom transmits](/images/scope/vpet_as22k.png). Valleys rise to 0.3V. This is OK.

[4K7 ACom transmits and V-Pet replies](/images/scope/vpet_asr4k7.png). Transmission is good. V-Pet replies after 18.6ms.

