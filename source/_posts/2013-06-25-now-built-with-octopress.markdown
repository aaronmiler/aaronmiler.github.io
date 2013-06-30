---
layout: post
title: "Now Built with Octopress"
date: 2013-06-25 22:31
comments: true
categories: 
---
I've deployed my new blog using Otopress. I had been using Jekyll for the past couple of weeks, but I found very quickly that making changes, then rebuildling/testing was very time consuming, and rather annoying. One nice thing about Octopress is that I can simply run the server like I would a rails application and it will pay attention to changes and rebuild the site as needed.
<!--more-->
In the process of moving to Octopress I did have to fix some things on my local development environment. I kept getting an error from RVM that the GCC compiler wasn't working, and it was unable to create executables. After looking around stack overflow it seemed like a simple xCode issue. So I tinkered with that for a while.

After about a half hour of tinkering, I realized I wasn't really going anywhere with this. I'm a huge advocate for Railsinstaller. If I need to get a machine up and running with rails quickly, that is always the route I take. However it seemed that some of the defaults that Railsinstaller used when I put it on my system kind of backed my RVM into a corner, and I was unable to update. Now Railsinstaller comes with a uninstallation option, so I simply uninstalled it, and reinstalled RVM with the normal install command. 

In almost no time RVM installed with no gotchas, and Rails 4.0 was installed successfully. It was a rather quick and painless fix, and hopefully now I'll have a little bit more freedom with my RVM installation.