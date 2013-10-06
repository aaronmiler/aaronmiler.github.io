---
layout: post
title: "Interacting with the GitHub API"
date: 2013-10-06 15:27
comments: true
categories: GitHub API Gem
---

I've been building an application, that is for creating, managing and organizing all those little bits of code you have floating around in your brain. Every piece of knowledge you save within the application gets saved to GitHub in your own personal repository.
<!-- more -->

I went back and fourth on how I wanted to build this application. But I finally decided to go with a Rails powered application for this project.

I'm using two different Gems to interact with the GitHub API. I'm using the [GitHub API Gem](https://github.com/peter-murach/github) by Piotr Murach, as well as the [Octokit](https://github.com/octokit/octokit.rb) gem which is maintained by GitHub. Most of the interaction I'm doing with the GitHub API is with Piotr's gem, however the Octokit gem has new features implemented faster. 

There are two ways you can make calls to the GitHub API. You can make anonymous calls, or you can make calls on behalf of a user. When making calls on behalf of a user you need to pass their OAUTH key along with the call you are making.

When you ask for permission to access somebody's GitHub information, it reroutes them back to your application with a code. However this code isn't the OAuth token. It's a code that you must send back as a POST request back to GitHub, in order to get the users OAuth key. 

The problem I had after that, was it didn't appear either of the gems had a way to tell what user was currently logged in, yet the GitHub API seemed to provide a similar method. So I implemented a temporary solution using the rest-client gem.

``` ruby
@github = Github.new client_id: ENV['GITHUB_ID'], client_secret: ENV['GITHUB_SECRET']
access_token = @github.get_token params['code']
session[:token] = access_token.token
session[:credentials] = JSON.parse(RestClient.get "https://api.github.com/user?access_token=#{session[:token]}")
```

This makes a simple call to the GitHub API in order to find out which user I'm currently interacting with. Since when you're making calls to a repository you need to know who the user is this makes or breaks the application.

All in all working with the GitHub API proved to be a very nice experience. I was able to make an application that created/updated/deleted files in a matter of a couple of weeks. I'm very close to "done" with it, and I can't wait to let it out in to the wild.