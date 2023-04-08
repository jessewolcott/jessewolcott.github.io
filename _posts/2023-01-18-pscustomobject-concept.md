---
id: 844
title: 'PSCustomObject &#8211; Concept'
date: '2023-01-18T23:27:16-05:00'
author: jesse.wolcott
layout: post
guid: 'https://www.jessewolcott.com/pscustomobject-concept/'
permalink: /pscustomobject-concept/
categories:
    - Uncategorized
---

I have struggled with basic programming concepts in my journey towards understanding Powershell, and the term “Object Oriented Programming” has only recently begun to coalesce a reasonable definition in my head. I’ve largely used PoSH for reporting and functionality in my life, and being able to use PSCustomObject has been a roadblock that I have only begun to overcome.

There is an idea that defining an array and then adding things to it with `+=` is computationally expensive, since, after the addition of the item, the object (array) has to be recreated completely to emcompass the new addition. If an object is never an array, but remains solely an object, no such “waste” exists. The issue with PSCustomObject is that OFTEN, `+=` is used to add a line to a report, or hash table, or array, or whatever it is. I use it as little as possible, but I need serious re-structuring of the process in my head to make it go.

I have an uptime report that I was fairly proud of… Until recently. I begun to send myself 2-3 reports a day (as scheduled tasks) and it got to be cumbersome, especially when I realized that its the same servers and I could definitely streamline the whole process. Now its a mess of `+=` and PSCustomObject is defined about 6 different places. It works, and is fast enough, and does what I want, but I can’t shake the feeling that I could accomplish the same task in about half as many lines!