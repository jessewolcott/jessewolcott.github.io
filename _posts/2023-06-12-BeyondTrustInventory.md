---
layout: post
title: BeyondTrust Inventory and Cleanup
author: jesse.wolcott
---

I will go on record as saying that there is no finer remote access support tool than BeyondTrust Remote Support (née Bomgar). It does everything that you're supposed to be able to do in a remote support client, and does it with reasonable security. I have used SmartCards, done remote registry work, copied files, all of it, and BT is amazing. Its expensive, but its "the right tool for the job". 

Tasked with deploying the jump client and maintaining that jump client list, well... Thats where things start to come off the rails a little bit. The Intune and MSI documentation is incomplete (generous description). I will post, at some point, about deploying the jump client with InTune, but to be perfectly honest, *I haven't figured out how to do it in a way that isn't miserable*. Thats how the subject of today's script came about... My package deployed continually for a week before someone told me that every machine in the jump client list was there 3-4 times. Yikes. 

Thankfully, BeyondTrust supports API and my aforementioned REST gist is applicable here. The following script does a few things:

1. Removes entries marked "uninstall". This happens if you uninstall the jump client from the local machine.
1. Removes entries marked as "lost". This happens when a machine doesn't check in for 60 days (I think).
1. Removes duplicates, leaving only the most recent connection.

Here's the link for the script on Github. Run it as a scheduled task or whatever is best for you:

[Jump Client Cleanup](https://github.com/jessewolcott/InfrastructureScripts/blob/main/JumpClientCleanup.ps1)