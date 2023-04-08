---
id: 819
title: 'Powershell&ndash; If/else for checking if a user is logged in'
date: '2020-12-23T16:45:12-05:00'
author: jesse.wolcott
layout: post
guid: 'https://www.jessewolcott.com/?p=819'
permalink: /powershell-if-else-for-checking-if-a-user-is-logged-in/
categories:
    - Uncategorized
---

Sometimes, you’d like to check if a particular user (like a local admin) is logged in, before you run your script. Here is that code:

> $CurrentlyLoggedInUserName = \[Environment\]::UserName
> 
> if( $CurrentlyLoggedInUserName -eq “jwolcott”) {
> 
> write-host “true”
> 
>  }else {
> 
> write-host “false”
> 
>  }