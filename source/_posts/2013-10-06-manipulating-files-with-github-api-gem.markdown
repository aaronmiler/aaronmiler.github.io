---
layout: post
title: 'Manipulating Files with the GitHub API Gem'
date: 2013-10-06 15:27
comments: true
categories: GitHub API Gem
---

I've been building an application, that is for creating, managing and organizing all those little bits of code you have floating around in your brain. Every piece of knowledge you save within the application gets saved to GitHub in your own personal repository.
<!-- more -->

I'm using two different Gems to interact with the GitHub API. I'm using the [GitHub API Gem](https://github.com/peter-murach/github) by Piotr Murach, as well as the [Octokit](https://github.com/octokit/octokit.rb) gem which is maintained by GitHub. Most of the interaction I'm doing with the GitHub API is with Piotr's gem, however the Octokit gem has new features implemented faster. 

A pivotal piece of this application, is the ability to create, remove, and update files. So being more comfortable with Pitor's gem, I decided to use it for the file manipulation. 

I was able to find some [documentation in the Github](https://github.com/peter-murach/github/wiki#githubapi-committing-file) repo outlining how to create a file. However, as it turns out, the documentation is very dated.

So I took matters into my own hands and looked at the source code to figure out what's going on. Finally after hours of banging my head against the wall, I found the solution I was looking for. 

My gift to you, is what you need to create/update/remove a file using Pitor Murach's Github_API Gem.


All Methods use the Github Repo Contents method to interact with the Repo Contents API
```ruby
github = Github::Repos::Contents.new  :user => 'username',
  :oauth_token => 'oauth_token',
  :repo => 'repo_name'
```
### Creating a File
```ruby
github.create 'username', 'repo_name', 'full_path_to/file.ext',
  :path => 'full_path_to/file.ext',
  :message => 'Your commit message',
  :content => 'The contents of your file'
# Content is all Base64 encoded to/from the API, and when you create a file it encodes it automatically for you
```
### Update a File
```ruby
# First you need to find the file so you can get the SHA you're updating off of
file = github.find :path => 'full_path_to/file.ext'
# Then update the file just like you do with creating
github.update 'username', 'repo_name', 'full_path_to/file.ext',
  :path => 'full_path_to/file.ext'
  :message => 'Your commit message',
  :content => self.markdown,
  :sha => file.sha
```
### Removing a File
```ruby
# First you need to find the file so you can get the SHA you're removing
file = github.find :path => 'full_path_to/file.ext'

github.delete 'username', 'tome-of-knowledge', 'full_path_to/file.ext',
  :path => 'full_path_to/file.ext',
  :message => 'Your Commit Message',
  :sha => file.sha
```

There you have it. I plan to send in a pull-request to update the documentation. Hope this saves someone some time. 