---
title: 'Wordpress to Jekyll (with bonus Github Pages info)'
layout: post
---
After paying another too-high hosting bill, I heard a dear friend mention that he had moved his sites to AWS to minimize cost. I've hosted my site for ~12 years as a full-fledged Wordpress install, and while that has been ok, it definitely is overkill. I have used various methods to post, including blogging software that has gone EOL, and engines that convert markdown to wordpress. All of them left something to be desired. I have been writing nearly everything at work in markdown, from meeting notes, to release notes, to project plans, and it seems like MD is here to stay. Time to move, now that I have 11 months of hosting to do it! GitHub Pages is free, and I get to use markdown. Lets do it!

Presumptions:
- Windows with admin access
- Wordpress site that works

## Wordpress to Jekyll

1. Install Visual Studio Code from https://code.visualstudio.com/
2. Install git from https://git-scm.com/download/win
3. Log into your Wordpress site
4. Install the "wordpress-to-jekyll-exporter" plugin from Github or the Wordpress plugin marketplace - https://github.com/benbalter/wordpress-to-jekyll-exporter
5. Activate the plugin and click "Tools" and "Export to Jekyll". A zip file will download. You should back this up.
6. Install ruby on your machine with winget. Open a CMD prompt and type ```winget install RubyInstallerTeam.RubyWithDevKit.3.2```
7. Install Jekyll. In your CMD, type ``` gem install bundler jekyll```. If your terminal says that Gem isn't recognized, open a new terminal. If it still doesn't work, check that ruby actually installed.
8. After all that installs, run ```gem update``` just to make sure we're all up to date.
9. Using your terminal, navigate to wherever you'd like to store your blog's files. For me, I store all of my repos on another disk, in a folder called GitHub. If you intend to use Github Pages to host your new site, you must name it (username).github.io, so my path will be ```H:\GitHub\jessewolcott.github.io```. So, I'd use ```cd H:\Github``` to get there. 
10. Create a new site using your jekyll install. Run ```jekyll new jessewolcott.github.io```. If the folder already exists, make sure to add ```--force``` but be mindful that this will overwrite whatever it needs to, in that folder.
11. Once that completes, CD into your new folder, and run ```jekyll serve```. This will generate the site for local viewing, and you can hit it from http://127.0.0.1:4000 in your browser.
    - Now that this thing is running, whenever something changes in that directory, the site will be rebuilt, and you need only refresh your browser to see the changes. Neat!
12. Unzip your blog export from Step 5. You will see a folder called "posts". Inside of there are all of your blog posts from wordpress. You can copy these over to the _posts directory. Your site will rebuild and you can refresh and view it locally. Cool, right?
13. You might not have noticed if you glanced quickly, but your site is probably called "Your awesome title" and a few other places, its clear we're still rocking the default newly generated site. Navigate over to your directory and find ```_config.yaml```. Open that up in your favorite text editor. If you take a glance at your Wordpress export, it doesn't give you much, aside from URL, title and description. Fill out your ```_config.yaml``` to your liking. You may need to terminate the ```jekyll serve``` job to reload the new config.
14. All of your blog posts are on one page. This is not great. Lets fix it! Back in your terminal, type ```gem install jekyll-paginate```.
15. In your site's directory, find "Gemfile". Underneath ```gem "jekyll-feed", "~> 0.12"```, create a new line and put ```gem "jekyll-paginate"```
16. In your ```_config.yaml```, above the build settings, enter ```paginate: 5```. This will paginate every 5 posts. You can change this to your liking. 
17. In your site's directory, you should see ```index.markdown```. Rename this file to ```index.html``` and add the following code AFTER the existing info (below the last line of the "front matter", which is that section at the top.)

    ---
    # Feel free to add content and custom Front Matter to this file.
    # To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

    layout: home
    ---
    <!-- This loops through the paginated posts -->
    {% for post in paginator.posts %}
      <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
      <p class="author">
        <span class="date">{{ post.date }}</span>
      </p>
      <div class="content">
        {{ post.content }}
      </div>
    {% endfor %}
    
    <!-- Pagination links -->
    <div class="pagination">
      {% if paginator.previous_page %}
        <a href="{{ paginator.previous_page_path }}" class="previous">Previous</a>
      {% else %}
        <span class="previous">Previous</span>
      {% endif %}
      <span class="page_number ">Page: {{ paginator.page }} of {{ paginator.total_pages }}</span>
      {% if paginator.next_page %}
        <a href="{{ paginator.next_page_path }}" class="next">Next</a>
      {% else %}
        <span class="next ">Next</span>
      {% endif %}
    </div>

18. Ok, we are getting somewhere now. The site is paginated, but still shows all the rest of the posts below. If we take a look at your index in Step 17, you'll see that we are leaning on ```layout: home```. That means that we are pulling layouts from the theme. If you are using the minima theme that is installed by default with Jekyll, as I was, you'll need to update this layout. Thankfully, its easy! Head over to the theme's folder, which is installed in ```C:\Ruby32-x64\lib\ruby\gems\3.2.0\gems\minima-2.5.1\_layouts``` on my computer. Open up ```home.html``` in your text editor and comment out the part that displays the posts. It might look something like this: 
    
    <div class="home">
      {%- if page.title -%}
        <h1 class="page-heading">{{ page.title }}</h1>
      {%- endif -%}
    
      {{ content }}
    <!--
      {%- if site.posts.size > 0 -%}
        <h2 class="post-list-heading">{{ page.list_title | default: "Posts" }}</h2>
        <ul class="post-list">
          {%- for post in site.posts -%}
          <li>
            {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
            <span class="post-meta">{{ post.date | date: date_format }}</span>
            <h3>
              <a class="post-link" href="{{ post.url | relative_url }}">
                {{ post.title | escape }}
              </a>
            </h3>
            {%- if site.show_excerpts -%}
              {{ post.excerpt }}
            {%- endif -%}
          </li>
          {%- endfor -%}
        </ul>
    
        <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>
      {%- endif -%}-->
    
    </div>

19. Rebuild your site , and see that we have successfully paginated. 
20. Now, you can build your site using ```jekyll build```, and copy ```_sites``` to your web host (don't forget your WordPress media!) and you're good to go. If you're using GitHub Pages, check out the section at the bottom.

## Jekyll to GitHub Pages

So, we have our page built. It works great on a standalone server (which may be perfect if you are swapping out a Wordpress install). You still have to build your site and upload it each time you change it, and that may not be what you're looking for. Thankfully, part of the reason Jekyll exists is to publish pages to GitHub Pages (and you don't even have to build it). You basically get it set up, and then just push an .MD file, and it does its thing.

1. Log into GitHub.com and create a repo called (username).github.io. My repo is jessewolcott.github.io. Make sure its publically viewable.
2. Clone it to your local machine.
3. Copy your Jekyll site to the git folder you just created, and clone it back up.
4. You will notice that any modifications (including altering the theme) didn't take. We have to change some things to make that go. Open up your ```_config.yaml``` and comment ```gem "minima", "~> 2.5"``` by putting a # on the line. Then uncomment ```gem "github-pages", group: :jekyll_plugins```. 
5. In your terminal, run ```gem install github-pages```. Then run ```bundle update github-pages``` to make sure its up to date.
6. Once thats all sorted, copy the theme's layout folder to your site's directory (```C:\Ruby32-x64\lib\ruby\gems\3.2.0\gems\minima-2.5.1\_layouts```)
7. Commit and push and you're done!