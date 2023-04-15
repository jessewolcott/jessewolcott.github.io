---
id: 125
title: 'Building a Simple LAMP Web App'
date: '2013-06-01T18:12:52-04:00'
author: jesse.wolcott
layout: post
guid: 'https://www.jessewolcott.com/?p=125'
permalink: /building-a-simple-lamp-web-app/
categories:
    - General
---

I work with laptops at work, and each laptop has a combination lock. Among the team, we share an Excel document on Sharepoint, and its a little bit cumbersome to search through that.

I saw this as an opportunity to build a web app. I dusted off my VMware fusion and brought up a 32-but Ubuntu VM. Started it off with 1 processor core and 2 GB of RAM. I placed the VM on a USB hard drive, since my laptop’s storage is at a premium.

Just picked a few packages during the NetInstall, LAMP, Basic Server, and OpenSSH server.

![](/assets/img/2013/06/wpid-Screen-Shot-2013-06-01-at-2.26.21-PM.png)

So after the install, I minimized the VM and went and ate an apple. For what its worth, Fuji apples are not as good as Gala.

After I did the install, I definitely cheated on importing my data from CSV into MySQL. I used a program called [Sequel Pro](http://www.sequelpro.com/) to set up my database, tables, and import the info, as well as pare down the permissions on the user I set up for the purposes of reading the data.

After I did that, I made two php files, one to display the search bar form, and the other to display the results. Here they are!

The search form page:

![](/assets/img/2013/06/wpid-Screen-Shot-2013-06-01-at-4.02.47-PM.png)

So you can see, all this really does is create the form, and set the name “keyname.”

The search page does all the heavy lifting:

![](/assets/img/2013/06/wpid-Screen_Shot_2013-06-01_at_4.04.43_PM.png)

And I say “heavy lifting,” even though its very small. So, the first lines say where the database is, how to connect, and which table we’re even looking at.

After that, we grab the keyname that we set in the search form, then we query the DB, and show the results. That was easy!

Next up… Adding a lot of records at once via CSV import, and stylizing the site! Maybe this afternoon? No promises.