---
id: 737
title: 'Sun JVS Power Supply Rebuild'
date: '2018-02-08T03:18:28-05:00'
author: jesse.wolcott
layout: post
guid: 'https://www.jessewolcott.com/?p=737'
permalink: /sun-jvs-power-supply-rebuild/
categories:
    - Arcade
---

So we use these Sun power supplies to power our naomis and whatnot, because they’re nice, usually pinned correctly, and have an adjustable 3.3v rail. Thats all well and good, and if you want them to last forever, you can recap them, just like you would anything else. I looked around at the internet, and found lots of different mentions of this power supply, but the cap lists didn’t match my findings, and the board didn’t even look the same. As it goes, check your work, don’t trust me blindly, and make sure that you verify what you’re changing out. The C5 on twistedsymphony’s rebuilt ([here](http://solid-orange.com/1465)) is the AC filter cap, and on my board, C5 is some little baby cap. That could end in tears. Anyhow, on with it.

First, get your power supply, your screwdriver set, your flush cutters, magnet parts cup, all the normal things. Take everything apart, so we can get a good look.

You can grab your calipers to check my work (or take my word for it) that the fan is a 12v 8cm brushless fan. Additionally, it is 2.5cm thick… You might see these fans listed as 3”x3”x1”, but mm is usually a bit closer so I go with that. I’m going with a nice silent case fan from Microcenter ([This one, actually](http://www.microcenter.com/product/341408/UCTB8_TB_Silence_80mm_Twister_Bearing_Case_Fan)). You can probably get one way cheaper on ebay or aliexpress, but this is one of my bench power supplies, so we’re going for gold.

Next up, the cap list.

| Sun 400-5397 PSU Cap list |  |
|---|---|
| location | V | Uf |  |
| C5 | 35v | 22uf |  |
| C11 | 200v | 820uf(m) |  |
| C13 | 35v | 22uf |  |
| C16 | 35v | 22uf |  |
| C22 | 16v | 1000uf |  |
| C23 | 25v | 470uf |  |
| C24 | 25v | 47uf |  |
| C28 | 10v | 2200uf |  |
| C29 | 10v | 2200uf |  |
| C33 | 10V | 2200uf |  |
| C34 | 10v | 2200uf |  |
| C37 | 50v | 2.2uf |  |
| C41 | 50v | 2.2uf |  |
| C43 | 35v | 22uf |  |
| C44 | 25v | 47uf |  |

Use flux, clean up after yourself, make nice field windings and heatshrink the cable if you need to re-use the fan connector. We want this to last a while!