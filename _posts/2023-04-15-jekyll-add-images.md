---
layout: post
title: Wordpress To Jekyll, Pt2 - The Assets
author: jesse.wolcott
---
Ok, you've got your website moved over to GitHub pages, and now you need to move your content from Wordpress over to GitHub Pages. If you are using this as a personal blog, it seems very reasonable to need to include attachments, pictures, etc. Thankfully, there is a super straightforward way to sort that out! When you first migrate your site over to GitHub you may notice that your images and media are still working. Thats because its still linking to your old webhost!

**This is part 2 of a multi-part series covering migrating from Wordpress to Jekyll and GitHub Pages. [Part 1 is here]({% post_url 2023-04-08-Wordpress-to-Jekyll %})**

1. Curse at the wordpress-to-jekyll exporter. This is important, as you will want to warm up for when you do it later.
2. Create a folder in your repository called "assets"
3. In that folder, create another folder called "img"
4. Navigate to your Wordpress install, and find the ```wp-content``` folder. Inside of that, you should see another folder called ```uploads```. There should be folders split by year. Copy all of those over to ```/assets/img/```.
5. In your posts, the URL for all of these images is malformed, (see step 1). The easiest way that I have found, without writing something to parse all the weird and terrible image names I've used over the years, is to go through my posts and update the links. I use VSCode for this (and many other things). Inside the post, press CTRL-H to bring up the Find and Replace menu. Put the first part of your link in the top line, and ```/assets/img/``` in the bottom. You can press the "Replace All" button (or use CTRL-ALT-ENTER) to update the links. 
![vscode](/assets/img/2023/04/vscode1.png)
6. If there are thumbnails, the URL is REALLY misformed. What you need to know when looking at these is that this is the proper format for an image:
    ```![vscode](/assets/img/2023/04/vscode1.png)```
7. After piling through all of your posts, probably deleting a few if they were cringey, you're good. Before you commit, you will probably want to clean up your images folder to remove all the thumbnails. You can use this gist to do that (set your local repo in the script): [Link to Gist](https://gist.github.com/jessewolcott/35af044b46897eefcc3c2fbb5de759a3)
8. After the thumbnail cleanup, you may want to remove all the empty folders for cleanliness sake. You can use this gist to do that: [Link to Gist](https://gist.github.com/jessewolcott/3ea411ca745730f9b085ea6fd8d8af00)

Next up, we'll worry about DNS. I took this opportunity to go through my posts and make sure that nothing looked out of place. There were a few wayward gross HTML bits that I cleaned up, and a I'm certain a few characters are malformed. It will all work itself out! 