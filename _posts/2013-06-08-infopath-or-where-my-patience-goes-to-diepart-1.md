---
id: 144
title: '“InfoPath” or “Where my patience goes to die”–Part 1'
date: '2013-06-08T22:33:27-04:00'
author: jesse.wolcott
layout: post
guid: 'https://www.jessewolcott.com/?p=144'
permalink: /infopath-or-where-my-patience-goes-to-diepart-1/
categories:
    - General
    - Howto
    - Microsoft
---

I’ve known about Microsoft’s InfoPath for a while, and as a part of most MS Office installs, its not a super huge mystery that it *exists*. Its existence, though, is questionable. I’m trying to figure out WHY it exists.

Clearly, it was meant for some database integration, as well as form creation, and its meant to interact with SharePoint at some level. I’ve taken up two challenges to try to teach myself InfoPath design, a bit about implementation, and, maybe most importantly, some of its limitations.

## Challenge 1: Simple Email Form with Attachment

My initial inclination whenever I need to email something with checkboxes is to make a web form, with very simple email backend. However, as I just installed Office 2013, I wanted to see if I could make a go at using MS’s provided tools, and maybe learn something in the process.

So, after opening InfoPath Designer 2013, it becomes immediately clear that you need to know what you’re doing straight away. There likely will not be hand-holding here. I want to create an email form so that I can QA new user setups at work; something prone to disaster, with many steps and places for us to trip up.

![Screenshot_060613_035810_PM](/assets/img/2013/06/Screenshot_060613_035810_PM.jpg)

At this point, I should tell you that I used a Windows Mobile phone for a bit, and I thought to myself “Wow, this way of flattening everything and using contrasting colors with tons of white space doesn’t really work for me.” This app is like, full on Windows 8 style. I don’t much care for that.

So after I get into the “design” aspect, the first thing, I’m told, I need to do is set up a data connections. What data connections, you might ask? Well, this is an email form, so that is our data connection. What? You run through the wizard, and select “As an email message” as your “destination for submitting data.” I’m not sure I would have worded that in such a confusing way.

Its important to note that we *will absolutely be coming back and changing this connection*. After you select email, you’ll see some familiar fields, along with the formula button.

![Screenshot_060613_041035_PM](/assets/img/2013/06/Screenshot_060613_041035_PM.jpg)

Fill out your submission email, and click next. We’ll update the subject later. After that, you need to get busy designing your form. I’m going to put checkboxes with labels and text entry fields. I’m not going to teach you how to drag and drop fields, but, essentially, under the “home” tab, there are controls. You can drag them. The radio button one confounds me, and I’m not sure how a UX designer tried that and said “yeah, that’s the sweet spot.” Additionally, I’m perplexed that everywhere in the UX got the 2013 / Windows 8 / Obnoxious White Space treatment except the wizards. That is curious.

Each checkbox, text field, or other control you enter should be named properly. Name the field something that you can identify in a list of 100 controls without following the workflow of what-goes-where. If you’re in a section of your form marked “Telephone,” don’t use a field called “type” because that could mean darn near anything when you look at a list of field names.

After you navigate through the horror that is InfoPath Page Layout, and set all your fields, you’re left with your form in its raw form, like so:

![Screenshot_060713_111335_AM](/assets/img/2013/06/Screenshot_060713_111335_AM.jpg)

To anyone concerned, I don’t think this contains any information that is not publicly shareable.

So, remember how I said we’d go back to the Data Connections? Well, now its time to set up this email to be useful! Open up your Data Connections, select your Email Submission, and click “Modify.” For this form, for me, I’m going to email this to a couple different places, including our ticket system. When you open the Data Connection wizard, its important to note that the data fields here are **FOR SHOW ONLY**. Don’t put info in there, it doesn’t work. No, I’m not sure why.

![Screenshot_060713_112208_AM](/assets/img/2013/06/Screenshot_060713_112208_AM.jpg)

So, you MUST click the function button to enter ANYTHING in this. We can do any sort of math we’d like, but mostly, we just want to use the CONCAT() function with our field names to make some sense of this. See where I’m going with this? You don’t have to concat if you don’t need to. SetupTech, in my example, should be an email address, so that can just be defined. If it needs to be more than that, you can just concat spaces. Check out mine:

![Screenshot_060713_011544_PM](/assets/img/2013/06/Screenshot_060713_011544_PM.jpg)

So now, we can click through, and name our submission (it might still be named from earlier) and save it. You should save your work, now, and press F5, which will open InfoPath Filler (which is the best name they could think of, I’m sure). After you complete the form, you can click submit, and it will go through the motions of sending the email. Important note here, you have to use Outlook, nearest I can tell. In my example, above, I’m also emailing our ticket system to update the new-hire ticket with the contents of the form. Because, predictably, the ticket system has a giant issue with HTML email updates, I’ll likely change this one to attach the form, which, for whatever reason, it handles well.

Also, InfoPath, throughout its existence, has been plagued with the inability to work with its former versions… As in this form likely won’t open in InfoPath 2010 or 2007. “But Jesse,” you plead, “Its just a form! Surely this is just XML in the backend, and filling out a form is one of the first things a data management system should be able to do flawlessly!” But then you remember this is a Microsoft product, and integration from end to end isn’t actually end to end, but its like, end to half way, then another connected system. Actually, it’s a lot like the Baltimore, MD mass transit system. The Light-rail trains don’t go where most people need to go, the subway exists for a reason unknown to most, and the buses, the turtle of the mass transit system, are the connectors to everywhere in the city. I can’t figure out what Microsoft’s bus-system is. Maybe AD? Maybe. I can’t tell.

More InfoPath fun in the future. I need to get this thing cranking out forms into SharePoint document libraries, which is an option. I asked our SharePoint admin create a document library for me to test with, and it went like this:

## ![Screenshot_060813_062909_PM](/assets/img/2013/06/Screenshot_060813_062909_PM.jpg)

This is indicative of the level of hilarious that my team members are used to. Oh, and the document library works fine, its properly specified in InfoPath, and it doesn’t submit. I love learning Microsoft products!!!1