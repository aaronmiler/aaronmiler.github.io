---
layout: post
title: "Reload Chrome from Vim"
date: 2014-03-17 20:06
comments: true
categories: [Vim,Chrome,Shortcuts,Workflow]
---
As my proficiency in vim increases. I've started looking for little short cuts. At the office, I have two monitors, and do some front end development from time to time. The annoying thing about it, is ever since I've switched to vim, I find CMD+Tabbing out of the terminal exceedingly annoying.

<!-- More -->
Then, I happened upon [Chrome CLI](https://github.com/prasmussen/chrome-cli) which allows you to send commands to chrome from the command line.

One of the commands that is particularly useful, is the `Reload active tab` command. Which is issued with `chrome-cli reload`

Another thing that I recently learned, is that you can issue commands to the terminal from Vim as well. All you have to do is prepend your command with a bang (!) and you can issue any command, such as `!open .` to open the current directory in the finder. Which I use quite frequently.

With these two factoids in my brain, I was able to create a line in my Vim RC file to reload the active chrome tab with a simple keystroke.

Now, when you enter in a shell command into Vim, it pops you out of vim, and waits for input to proceed. So what this command does is this.

``` vim
" Reload the active chrome tab
:! chrome-cli reload
" Press Enter to execute
<CR>
" Press Enter again to pop back into Vim
<CR>
```

Here is what it looks like when it's mapped to my leader shortcut

``` vim
map <Leader>r :! chrome-cli reload<CR><CR>
```

This allows me to put Vim on one monitor, and chrome on the other. So I can just save, then hit `<Leader>+r` to reload the tab without leaving Vim.

I'm tempted to add a save before the reload in order to lessen the keystrokes even more, but I haven't been annoyed enough quite yet.
