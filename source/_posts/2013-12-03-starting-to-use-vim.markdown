---
layout: post
title: "Starting to use Vim"
date: 2013-12-03 21:49
comments: true
categories: [Vim,Environment,Worflow]
---

I've started to use Vim. 

I feel incredibly inefficient right now. But I know, that with time I will learn how to efficiently edit with Vim.
<!-- more -->

There are a couple of things I need to figure out.

- How to open/edit new files more efficiently
- How to browse a projects file structure
- How to efficiently execute commands from Vim (Git, RSpec and such)

I'm still quite used to using Sublime Text at this point. One of the things I miss the most is the Command+T shortcut. This brought up a dialog where you could start typing part of the path or filename. It would then autocomplete the file for you, and you could open it. When you knew what you were looking for this resulted in very quick file opens.

I have set a couple of useful shortcuts for Vim that have helped me in the learning process though. For example:

```
" Don't use the arrow keys
noremap <up>    :echoerr 'USE K TO GO UP'<CR>
noremap <down>  :echoerr 'USE J TO GO DOWN'<CR>
noremap <left>  :echoerr 'USE H TO GO LEFT'<CR>
noremap <right> :echoerr 'USE L TO GO RIGHT'<CR>
```

When I first started I found myself drifting to the arrow keys every now and again. This makes it so every time I try to use the arrow keys, I get a nice red error in vim that tells me to use the actual navigation command for that.

Another thing I found helpful was this shortcut
```
" Remap jk to leave insert mode
imap jk <ESC> 
```

This allows me to exit insert mode very easily.

The learning curve is steep, but I know that with time will come Vim Mastery.

What I'm really looking forward to, is the super speedy vim editing I've seen from others live coding at conferences.
