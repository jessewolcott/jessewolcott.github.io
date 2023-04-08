---
id: 151
title: 'Workflowy, and How I’d Improve It'
date: '2013-06-14T23:35:35-04:00'
author: jesse.wolcott
layout: post
guid: 'https://www.jessewolcott.com/?p=151'
permalink: /workflowy-and-how-id-improve-it/
categories:
    - General
---

I sent an email to the [Workflowy](http://www.workflowy.com) people, and it said this:

> Hi there!
> 
> Do you guys plan any email or IFTTT integration any time soon?
> 
> I don’t mean to be like this, but I’d totally go pro if that was a thing.

And I don’t mean to be that guy. I will likely go pro in Workflowy if it continues to be my main workflow, because I like it. I like the outline format, and its really hit the spot for me, because it’s a clever cross between to-do list, outliner, and mind mapping tool. Its pretty great. There is a limitation of 250 items, which is removed by “Pro” status. I really like Workflowy, and just need to make sure that it’s a cornerstone in my life before I commit. If anyone knows anything about my workflow professional, they’ll know that I rabidly proselytize [Evernote](http://www.evernote.com), and I’ve been a pro member there for years, despite not using a ton of bandwidth, purely so that I can support the product. I want Evernote to flourish and be around forever. If Workflowy does the same thing, I’ll throw my $40 a year at that, too. So, as any outgoing, awesome company would do, they fired back:

> What are the main types of things you want to import?

So, what **would** I do to improve it? There are a few things that could be baseline features, or pro features. Without knowing what the backend is, I can only speculate, and hope. Let’s say we have a Workflowy doc (Spoilers: we do).

[![image](https://www.jessewolcott.com/wp-content/uploads/2013/06/image_thumb.png "image")](https://www.jessewolcott.com/wp-content/uploads/2013/06/image.png)

## Email Submission

Any automated process can send email.. and that’s fantastic. Its not complicated, and, more to the point, its easy to manipulate it through most any method. Any BASH, perl, python, applescript, VBS, powershell, etc script can send email.

Using an open and close character could identify the hierarchy of the submission. Using common characters could be problematic for scripting, and while a feature could be designed with disregard towards scripting, I think that “what if’s” should be considered. IFTTT is a big deal, after all.

So, with our example above, if we wanted to create this via email, we should be able to do the following:

> Send an email to jesse.wolcott@prousers.workflowy.com
> 
> Subject: (Workflowy Suggestions)&gt;(Submit via email)&gt;(Item with a note)
> 
> Body of Email: Note Contents.

Now, this is just a rough idea. There aren’t too many scripting languages that can’t handle &gt;’s and parentheses, when called specifically.

## PDF / Attachment Support

Obviously when we start getting to this point, things get a little hairy, because you really have to start worrying about quotas, and massive amounts of disk space. In the world of task lists and to-do’s, basic support for PDF and DOC import is pretty crucial.

I think that a lot can be done, if we view Workflowy as a task manager, it’s a very different situation than that of a mind-mapper…For instance, lets consider the follow situation: A user puts an Arduino on their propane gas tank. When it gets to a certain level, email support could add a to-do to your Workflowy to pick up propane. This may be obscure, but lots of stuff like this could be used. If you’re monitoring a datacenter’s temperature, you could use Workflowy with email support to catalog alerts for when the datacenter reached a certain temperature. Workflowy’s creators may have a different vision for what people will end up using it for, I’m not sure… But they’ve left it very open to interpretation on the user’s end!

The possibilities are endless!