---
layout: post
title: Uninstalling Applications
author: jesse.wolcott
---

There are a great many reasons why "Multiple plans for attack" is the right way to think in almost all arenas of life, and Powershell and workstation management with MS Intune consistently reward those who are... More able to handle adversity. Yeah, we will describe it like that. In many cases, a tradition .NET call to the ```.Uninstall()``` class is the fast, easy way to uninstall things with Powershell. If you're like me, and live in a "constrained-mode" world, sometimes you can't use classes like that. 

I made a gist that uses the registry, Uninstall strings from installers, and ```Start-Process``` to uninstall applications. It is a lot more manual than the ole ```.Uninstall()``` plan, but it is what it is.

[Check it out here on GitHub Gists](https://gist.github.com/jessewolcott/258e90ac3a83d10698b7442b9ce13ae1)