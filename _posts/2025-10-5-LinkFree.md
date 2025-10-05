---
layout: post
title: LinkFree and NFC 
author: jesse.wolcott
---

I was targetted for marketing on this NFC enabled card thing (https://dot.cards/). Combining that with a Linktr.ee site, or something similar, seems like a great idea for all professional networking situations. Apple introduced the ability to touch phones and exchange contact info, which is really good, but it exchanges your REAL vcf, which, for me, has loads more info than I want to exchange professionally. So, what can we do?

I'm a huge fan of micro-vps (Virtual Private Server) to host critical but beneficially air-gapped servers for stuff like this. My friends over at [LowEndTalk](https://lowendtalk.com) are always selling teeny-tiny VPS for cheap as can be. I got the vps for this project for $9 for a year of service. Its certainly no beefcake, but it provides a very simple NGINX server with some basic protections, so it doesn't need to be powerful (as much as I'd like the idea of the general public beating up my personal contact info, I garner no such fame). 

# Server Setup

Your VPS host should provide you an IPv4 address. You'll need that to make the A Record on your DNS provider. I'm using a subdomain on my domain (https://links.jessewolcott.com), so its free, and I set it up through the porkbun web UI.

We need super basic stuff on here, so once you get your vps (I chose an LTS Ubuntu release), SSH into it and do the following:

```bash
# updates
sudo apt update && sudo apt upgrade -y

# Install Nginx
sudo apt install nginx -y

# Start and enable Nginx
sudo systemctl start nginx
sudo systemctl enable nginx

# Verify web server status
sudo systemctl status nginx

# Install Certbot and Nginx plugin
sudo apt install certbot python3-certbot-nginx -y

# Obtain and install certificate for your domain (include -d www.whatever.domain.com if needed)
sudo certbot --nginx -d links.jessewolcott.com 

# Test renewal (Certbot adds a cron job; run this to verify)
sudo certbot renew --dry-run

# Install Fail2Ban
sudo apt install fail2ban -y

# Start and enable
sudo systemctl start fail2ban
sudo systemctl enable fail2ban

# reboot
reboot

```

# Webpage Setup

I made use of the open-source project [Linkfree](https://github.com/MichaelBarney/LinkFree) to create a static webpage for this. Well, thats inaccurate, I ripped off the structure and formatting and didn't like any of the themes and didn't like that i had to link the picture and that the stylesheet was separate, so I glommed it all together in one file and made a generator.

[So check out this powershell generator to create your page](https://github.com/jessewolcott/LinkFreePageGenerator). Once you have that file, simply upload it to /var/www and you're all set! 

# NFC Tag Setup

Now, to bring it all together! Download [NFC Tools](https://apps.apple.com/us/app/nfc-tools/id1252962749) on your iPhone, and pick up some [NFC Tags from Amazon](https://www.amazon.com/dp/B077W8SN1Q?th=1). I bought these little keychain ones, but there are stickers and cards and all manners of these things and they're really cheap. 

Open up NFC Tools, and go to "Write", then "Add a record". Go to "URL/URI" and enter your link, then click write, and put your tag up to it. DONE! Now, when you wave your NFC tag near an NFC-capable phone, you'll see this:

![iOS Screenshot](/assets/img/2025/10/20251005_152929000_iOS.jpg)