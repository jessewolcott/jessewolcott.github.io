---
layout: post
title: A blog for your kid
author: jesse.wolcott
---

Kids minds are so incredible. I would love to catalog everything my kid does, but it doesn't make sense to do it on my blog. If my parents had set up a blog when I was born, I'd have a lifetime of cool stuff to look back at, and I think that would be pretty neat. I wrote a whole auto-biography in 5th grade as a project, and I sure do wish I had it now. 

I blog with Jekyll on Github Pages. I have meant to do something for my son for a long time, and no time like the present to get going on AWS. I was going to use Hugo until I found out that GitHub used jekyll natively (and I didn't have to figure out how to build the site). Now that I've gotten my base all sorted, I think its time for the Hugo -> Github -> Amazon S3 blog for kiddo.

I have owned his URL for a long time (bryanwolcott.com). It has hosted a (poorly made and quickly done) static site since his inception, basically. I wonder if .com will be dumb by the time he's old enough to care. So what all needs to be done?

* Github Account
* AWS Free Tier account
    * Billing alerts with cloudwatch
    * S3 Bucket for storage 
    * Amplify for static sites
    * Cloudfront for HTTPS
* Github build workflow
* DNS Records

## Accounts
GitHub account and AWS account were easy, of course. I set up a forwarding email from his domain to my email, which enabled all the verifications required. 

## CloudWatch Billing Alerts

I set up alerts for AWS using CloudWatch, with help [from AWS's documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html). It was pretty easy. I did have to change the region from Ohio to N. East to get Billing to show up in my metrics, though.

## S3 Bucket

Head over to [AWS S3 Bucket Create](https://s3.console.aws.amazon.com/s3/bucket/create?region=us-east-1) and name your bucket. I have no interest in other people accessing this bucket, so I elected to disable ACLs. I created the bucket with all public access blocked, and I will turn on the access I need when the site needs it. I will be using Github for versioning, so I don't need that there either. The rest of the bucket config is default. 

## Hugo

Hugo is the static site generator that we are going to use, and its fairly straightforward to get going, but has a bunch of steps. This guide assumes Windows 11. If thats not you, sorry. 

1. Install Powershell 7 by opening your terminal and typing ```winget install Microsoft.Powershell```.
1. Use Winget to install Git (if you haven't already). This is done by running ```winget install Git.Git```
1. Close and reopen terminal, and open a new tab by selecting the arrow and choosing "Ubuntu". 
1. In the Ubuntu terminal, run ```sudo snap install hugo```. 
1. Navigate to wherever you would like your new site to be stored. I like to keep my repos in ```C:\Git```, so I'd navigate to that folder by running ```cd /mnt/c/Git/```. If you want to make another folder, of course, you can. We will create the repo's folder next.
1. Run ```hugo new site website``` or whatever friendly name you'd like to give the site. You'll see some text about a theme.
1. Run ```cd website``` to get into the folder of the site we just made.
1. Run ```git init``` to initialize the git project for the site.
1. Clone a theme to your site by running ```git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke```. If this fails, be sure that git is installed!
1. Run ```echo "theme = 'ananke'" >> hugo.toml``` to add the theme you just cloned to your config file.
1. Start your hugo local server to be sure you did it right, run ```hugo server```. You should see a message about navigating to http://localhost:1313. Do that, and make sure you're good to go.

## Github Desktop

I am going to teach my son to use this, so software like Github Desktop will be useful to manage the version control process. Log in through the browser, and clone your repository to Github, then commit and push your quickstart.

## Amplify 

AWS Amplify is a great solution for those of us using static website builders. It features built-in connections to Github, and we are going to make use of just that feature! 

1. Head to [AWS Amplify](https://aws.amazon.com/amplify/) and sign in.
1. Click "Get Started", then "Host your web app".
1. Select "Github" and click "Continue".
1. Run through the authorization prompts. Select your repository (mine is called "website"). Leave "Main" selected. I will not be branching this site.



A kind soul named Albert Moreno made an excellent action to publish hugo to S3, so I went ahead and forked that to kiddo's Github, just in case something happens and we need our own copy. You can find that [here](https://github.com/AlbertMorenoDEV/deploy-hugo-to-s3-action/tree/main).

Next, we will wander over to [github.com](github.com) and take a look at the settings for the website repo. On the left side, look for "Security", then "Secrets and Variables", finally "Actions".

Make sure that you have a Github repo created and cloned, and then add a folder to the cloned repo called ".github". Under that folder, create another called "workflow". In that folder, create a file called ```build.yml```. It should contain the following code:

```YAML
name: Hugo Build and Deploy to S3

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    name: Build and Deploy
    runs-on: ubuntu-latest
    steps:
      - name: Check out master
        uses: actions/checkout@master
      
      - name: Build and deploy
        uses: bryanwolcott/deploy-hugo-to-s3-action@v0.0.5
        with:
          hugo-version: 0.89.0
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

https://docs.aws.amazon.com/amplify/latest/userguide/welcome.html

## Github build workflow




