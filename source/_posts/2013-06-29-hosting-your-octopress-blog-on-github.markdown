---
layout: post
title: "Using Octopress and Github to Host My Website"
date: 2013-06-29 20:47
comments: true
categories: blogging github octopress
---

Last week I started building my site on Octopress. Coming from Jekyll everything was rather familiar. While developing my site, I listened to a great podcast, called "Jekyll and CMS-less websites with Young Hahn and Dave Cole" on The Web Ahead. I won't attempt to summarize it as there is so much covered, and it really got me excited about using Jekyll. If you haven't listened to it, you can listen to it [here](http://5by5.tv/webahead/54). <!-- more --> As I got closer to finishing my site, I started to wonder about how I was going to host it. With my initial Jekyll set up I had just uploaded the static files to a Digital Ocean VPS and called it a day. But the Jekyll podcast got me thinking about hosting my site on GitHub pages for free, so I gave it a shot. 

Very quickly I realized how easy it was to throw my site up on github pages. The directions for all of the pieces are a little scattered, so I figured I'd put them all here for other Internet goers to enjoy.

### Setting up your GitHub Repo.

[Github Pages](http://pages.github.com/) allows you to host static content on GitHub for free. There are two different type of GitHub Pages. There are Project Pages, and User/Orginization pages. The User/Orinization pages must follow this formation _username/username.github.io_ and you can only create your own User/Org pages, you can't take somebody else's name. Project Pages behave a little differently. All you have to do for any given project is add a branch called gh-pages and that is the branch that GitHub will use to build the site. The User/Org page can be accessed from http://username.github.io while the project pages are accessed from http://username.github.io/project. 

### Setting up your Octopress

Out of the box Octopress is already all wired up to deploy to GitHub, all you have to do is give it the destination. All you have to do is:

  - Run _rake setup_github_pages_
  - Paste in your repo URL

Octopress will then detect if its a User/Org repo, or a project page repo, and create the branches accordingly. If it's a user/org repo it will create your master branch, if it is a project page it will create the gh-pages branch for you.

### Deploying to GitHub

As if this wasn't easy enough already, this part was just a breeze. All it takes, is running two simple commands

```
rake generate
rake deploy
```

That's it. Octopress will push your blog to gitHub, and GitHub will build your pages. Since you're pushing static files to GitHub, you don't have to wait for it to compile the page like you would if it were pushing Jekyll source to gitHub. 

### Adding your custom domain name

GitHub makes this almost too easy. First go into your DNS settings and point your domain name to ```204.232.175.78```. Then in the root of your site, add a file called CNAME. My cname file looks like this
```
aaronmiler.com
```

It's that easy. GitHub will set up some automatic redirects such as redirecting www.aaronmiler.com to aaronmiler.com, and it will also redirect traffic from aaronmiler.github.io to aaronmiler.com.

I was blown away by how easy this was. I've often at work created very small rails apps for simple sites, or resorted to using Wordpress. After using Octopress, and Jekyll to push my content to GitHub. I think I have now found my new work flow for smaller sites. 