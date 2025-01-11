---
layout: post
title: Red Light Therapy (is it baloney?)
author: jesse.wolcott
---

I'm of the staunch and unwavering opinion that if something you see on social media actually worked, it would be marketed on major media channels and/or illegal. That said, there are some marginally helpful things that have benefits that are indisputable that skirt the line of "worth it". That is to say, "does this take more time or money than the benefit it brings". A lot of these edge / fine line cases are up to personal opinion. If I'm already engaging in an activity that is adjacent to the Marginally Beneficial Idea (MBI), maybe I can derive the benefit with little additional extra output. Red light therapy may be one of those things, so I decided to check it out, and build something of my own.

## Whats the poing?

Why? Who cares? What benefit are you going to derive from this baloney? Excellent question! 

[The Cleveland Clinic](https://my.clevelandclinic.org/health/articles/22114-red-light-therapy) says that red light therapy can help with wrinkles, acne, scars. It is said that red light activates the mitochondria (which everyone knows is the powerhouse of the cell). 

[NIH](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3926176/) seems to think that 650nm light has demonstrated efficacy and safety for skin rejuvenation and intradermal collagen increase. I like the sound of that.

There are some other folks that tout (potential baloney) benefits of "reduced systemic inflammation", reduction of dementia, osteoarthritis, and tendinitis  In addition, there is a decent body of work that says it stimulated hair growth, which, honestly, sounds good on my face and head, not so great on my back. C'est la vie. 

As per usual, my expectations are "this is all baloney". I'm willing to stand in front of this thing for 10 minutes, 3 times a week, just to see. Whats the worst that could happen? Maybe it will not cure my dementia.

## The build

Commercial Red Light therapy is very expensive. I don't think that some LEDs should be that expensive, and thankfully, we have Chinese-origin junk shops blasting us with products in every app from Temu to Tiktok. I found some red light panels on Temu for $17 a piece, and since I want to try this for my entire body, I grabbed 6 of them. 

![Temu Junk 1](/assets/img/2024/04/temu-red-light.png)

Obviously, we will need to mount these in some way. The big fancy panels have touch screens and all kinds of crazy stuff, but at the end of the day, the functionally only needs a few things. I had not considered that there are two sets of LEDs on these panels, one set of visible red light and the other of near-infrared, which is not visible. Inside the panel, we can see that there are two separate power supplies, which is pretty cool if you consider the implication for controlling it. So, what are our goals?

* Add a timer with 5, 10, and 15 minute settings
* Add the ability to "communicate" that something has happened by flashing individual panels.

The obvious choice for this is some basic commodity hardware like AC relays and something like an ESP32. I was sure that I was not the first person to tread this path, so I googled and found this:

https://randomnerdtutorials.com/esp32-relay-module-ac-web-server/

Being totally certain and full of myself, I started searching for a board that was already integrated. I found [this thing](https://www.aliexpress.us/item/3256804095629006.html?gatewayAdapt=glo2usa4itemAdapt#nav-specification) on Aliexpress, which is a bit more than I wanted to spend but hey, I'm worth it. And after all, why spend money on a refined product when you can be frustrated building it yourself? 


| Item                 | Quantity | Source     | Cost (EA) | Cost (Total) | 
|----------------------|----------|------------|-----------|--------------|
| Red Light Panels     | 6        | Temu       | $17.16    | $102.96      |
| Wood (1x2)           | 6        | Home Depot | $XX.XX    | $XX.XX       |
| ESP32 16 Relay Board | 1        | AliExpress | $60       | $60.00       |

A grand total of 300 bucks. 