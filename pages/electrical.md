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

## Pendulum X

Testing a Pendulum X 1.0. ACom supply voltage at 4.7V.

Not connected: [zoomed out](/images/scope/penx_open_20ms.png), [left](/images/scope/penx_open1.png), [right](/images/scope/penx_open2.png). Peaks 3V. Valleys 0V. Listening 2.9V. Initial pull-down 59ms. Start bit 2.1ms high, 1.7ms low. Bit one 3.1-3.2ms high, 1.7ms low (length 4.8-4.9ms). Bit zero 1.1ms high, 3.9ms low (length 5.0ms). After final bit, drives high, starts driving low again after 1.1ms as if we were going to have another zero bit, then releases after ~0.2ms at ~2V.

[22K across](/images/scope/penx_22k.png). Listening drops to 1.1V, so the weak pull-up is ~36K. Peaks drop to ~2.9V, so the strong pull-up is ~~1K.

[10K across](/images/scope/penx_10k_pulled.png). Listening drops to 0.55V and the PenX detects it (will not transmit). Threshold is between 0.55V and 1.1V.

[With 3K6 ACom](/images/scope/penx_ar3k6.png). Valleys rise to 0.3V.

[With 1K ACom](/images/scope/penx_ar1k.png). Valleys rise to 0.9V, so the pull-down is ~300R. Peaks drop to 2.9V.

[4K7 ACom transmits and PenX replies](/images/scope/penx_asr4k7.png). Transmission is good. PenX replies after 6.3ms (and this seems reasonably consistent).

[22K ACom transmits and PenX replies](/images/scope/penx_asr22k_ok.png). Valleys rise to 1.0-1.1V and the PenX still accepts it, so the threshold is between 1.0V and 1.1V. Note this is not the same as "22K across", since both of the ACom resistors are pulling down in parallel, giving 12K. Note the capacitive loading. PenX replies after 6.2ms.

[22K ACom transmits (zoomed in)](/images/scope/penx_as22k_1ms.png). [1K ACom for comparison](/images/scope/penx_as1k_1ms.png), showing negligible input resistance like the Pendulum. With the 22K, rise and fall times 20%-80% are ~120us, suggesting a capacitance of ~4nF.

## Digital Monster 20th

Testing a first-wave brown version. ACom supply voltage at 4.7V. The battery voltage dropped during this session beyond what would normally be expected. The V-Pet is attempting to send a copy except where otherwise specified.

Not connected: [zoomed out](/images/scope/dm20_open_50ms.png), [left](/images/scope/dm20_open1.png), [right](/images/scope/dm20_open2.png). Peaks 3.0V. Valleys 0.0V. Listening 2.0V with a large 50Hz ripple. Initial pull-down 60ms. Start bit 2.0ms high, 1.0ms low. Bit one 2.5-2.6ms high, 1.5-1.6ms low, length 4.1ms. Bit zero 0.8-0.9ms high, 3.3ms low, length 4.1-4.2ms. After final bit, drives high, then releases immediately, with a large capacitive decay back to the listening level. Fall time 20%-80% is ~28ms.

[1M across](/images/scope/dm20_1M_other_50ms.png) ("other" battle here, but sending a copy looks the same shape). Listening drops to 1.5V, so the weak pull-up is ~330K. Supposing an RC circuit with 330K and the 28ms above, the capacitance is ~60nF.

[470K across](/images/scope/dm20_470k_other_50ms.png) ("other" battle). Listening drops to 0.7V, the V-Pet detects it and replies with an [error packet](/images/scope/dm20_470k_other_20ms_pkt2.png). It doesn't reply when trying to send a copy, but will still send the initial packet even though the line is pulled low. Threshold is between 0.7V and 1.5V.

1K across: [zoomed out](/images/scope/dm20_1k_20ms.png), [zoomed in](/images/scope/dm20_1k.png). The V-Pet still transmits even though the line is definitely pulled low. Peaks drop to 2.2V, so the strong pull-up is ~400R.

[With 1K ACom](/images/scope/dm20_ar1k.png). Valleys rise to 0.6V, so the pull-down is ~200R. Peaks drop to 2.7V.

[1K ACom transmits and V-Pet replies](/images/scope/dm20_asr1k.png). Transmission is good. V-Pet replies after 15ms.

[3K6 ACom transmits and V-Pet replies](/images/scope/dm20_asr3k6.png). Transmission is OK. Note the capacitive loading. V-Pet replies after 15ms.

[4K7 ACom transmits and V-Pet replies](/images/scope/dm20_asr4k7.png). The distortion is growing. V-Pet replies after 15ms.

[10K ACom transmits and V-Pet replies](/images/scope/dm20_asr10k_20ms_2.png). Transmission looks dodgy but seems to have been accepted. V-Pet replies after 19ms this time.

22K ACom transmits and V-Pet replies with an error packet: [sending](/images/scope/dm20_asr22k_20ms_1.png), [reply](/images/scope/dm20_asr22k_20ms_2.png). V-Pet replies after 28ms this time.

[22K ACom transmits (zoomed in)](/images/scope/dm20_as22k_2ms.png). [1K ACom for comparison](/images/scope/dm20_as1k_2ms.png), still showing slight capacitive loading but not enough to be concerned about here. With the 22K, rise time 20%-80% is ~560us, fall time 1.0ms. As discussed above, the ACom's pull-down resistance is the lower one, and the V-Pet's 330K weak pull-up should not make that much difference, so this is the opposite of expected. Supposing 22K with 560us, capacitance would be ~18nF.

## Xros Wars Mini

Testing Shoutmon version. ACom supply voltage at 4.8V.

Not connected: [zoomed out](/images/scope/xrosmini_open_20ms.png), [left](/images/scope/xrosmini_open1.png), [right](/images/scope/xrosmini_open2.png). Note that an inactive line is low for these! Peaks 2.8 V. Valleys 0V. Listening 0V. Initial pull-up 42ms. Start bit 11.2ms low, 5.6ms high. Bit one 1.3-1.4ms low, 4.1-4.2ms high (length 5.4-5.6ms). Bit zero 4.1-4.2ms low, 1.2-1.4ms high (length 5.3-5.6ms). After final bit, releases with a small capacitive decay.

[1K across](/images/scope/xrosmini_1k.png). Peaks drop to 1.2V, so the pull-up is ~1K3.

[With 22K ACom set to pull up](/images/scope/xrosmini_aur22k.png). (When the Mini is pulling down, the test point connects to 4.8V through 22K, and to ground through the Mini in parallel with 26K7.) Listening rises to 1.4V, so the weak pull-down is ~14K. Valleys rise to 0.3V, so the strong pull-down is ~~1K5.

[With 10K ACom set to pull up](/images/scope/xrosmini_au10k_error.png). Listening rises to 2.0V and the Mini detects it (will not transmit). Threshold is between 1.4V and 2.0V.

The following AComs are set to pull down when listening.

3K6 ACom [transmits](/images/scope/xrosmini_asr3k6_1.png) and Mini [replies](/images/scope/xrosmini_asr3k6_2.png). This looks OK. Mini replies after 17ms.

10K ACom [transmits](/images/scope/xrosmini_asr10k_1.png) and Mini [replies](/images/scope/xrosmini_asr10k_2.png). This looks OK. Mini replies after 18ms.

22K ACom [transmits](/images/scope/xrosmini_as22k_noreply.png) and Mini ignores it. The peaks are probably below the voltage threshold.

[22K ACom transmits (zoomed in)](/images/scope/xrosmini_as22k_1ms.png). [1K ACom for comparison](/images/scope/xrosmini_as1k_1ms.png), which is pretty much straight. With the 22K, rise time 20%-80% is ~120us, fall time ~100us, suggesting a capacitance of ~3nF.

