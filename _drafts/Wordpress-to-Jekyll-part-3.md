---
layout: post
title: Wordpress To Jekyll, Pt3 - The DNS
author: jesse.wolcott
---

The final piece to really *replace* Wordpress is to point your DNS to GitHub Pages.

GitHub gives us a [step by step guide](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) on how to do this. I am dumb, and it took me a while to sort this out, as DNS in web hosting is not something I deal with frequently. Lets do it!

1. Head over to your webhost. Mine is Dreamhost.
2. Remove your hosting (if it exists). Wait for those changes to propegate. 
3. Add a CNAME record to your domain for www to <username>.github.io
4. 