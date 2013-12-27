---
layout: post
title: "Switched to rbenv"
date: 2013-12-27 15:14
comments: true
categories: Workflow, rbenv
---

I switched from using RVM to rbenv not too long ago. I'm pretty happy with the switch, and I think I'm better off. There are a couple of reasons that made me switch.

<!-- more -->

- Quick Switching between Ruby Versions
- Upgrade with Git
- Lightweight
- Reliable

I was using RVM for the longest time, because it is what most everybody recommended. However, I had seen the .ruby-version files throughout other projects, and was wondering why people liked [rbenv](https://github.com/sstephenson/rbenv) so much.

Then all of the sudden I started having troubles while switching ruby versions with RVM. My gems got all wonky, and it just became a chore, where I found myself uninstalling my ruby and then reinstalling it just to get it to work properly.

So I switched to rbenv. The switch was super easy, all I had to do was this:

*Note: You can install it with Brew, but I wanted more control, so I installed it this way*

``` bash
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
# I use ZSH so I'm adding this to my .zshrc, if you use bash it should be your .bash_profile
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
```

I then installed [ruby-build](https://github.com/sstephenson/ruby-build) which is used to compile and install the different versions of ruby. It's just as easy to install

``` bash
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
```

Now, you should be able to relaunch your terminal, and run `rbenv install --list` to see all the ruby versions that are availible for install. After that, it's just as simple as running `rbenv install 2.0.0-p427' to install Ruby 2.0.0

After you install a ruby version you can do a couple of different things.

``` bash
rbenv global 2.0.0-p247 # Set the Global Ruby version
rbenv local 1.9.3-p385
# Sets the local Ruby Version, also creates a .ruby-version file
# and will automatically switch to that version when in that directory
```

The quick switching between ruby versions is the main reason I like using rbenv so much.