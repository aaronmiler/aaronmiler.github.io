---
layout: post
title: "Making the ST/STT Shortcut work with Sublime Text 3"
date: 2013-10-22 22:08
comments: true
categories: ZSH, Z-shell, Sublime Text 3
---

I recently made the switch to Sublime Text 3. When I did this I finally removed the Sublime Text 2 application from my computer so I would quit having two instances of Sublime Text open at the same time. 

<!-- more -->

When I did this, this happened.
![Broken Command](/images/broken-zsh.png)

Whoops, I broke one of my favorite short cuts. Oh-My-ZSH has a shortcut to open a file/directory in Sublime Text.

You can run `st` to open a file, or `stt` to open the current directory in Sublime Text.

After the upgrade I broke that shortcut. The Sublime Text 3 application file name is just `Sublime Text.app` instead of Sublime Text 2 shortcut of `Sublime Text 2.app`. 

To fix it I simply went into the Sublime Text 2 plugin within ZSH (found here `~/.oh-my-zsh/plugins/sublime`) from this:
```
local _sublime_darwin_paths > /dev/null 2>&1
_sublime_darwin_paths=(
	"/usr/local/bin/subl"
	"$HOME/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl"
	"$HOME/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl"
	"/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl"
	"/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl"
)
```

to this:
```
local _sublime_darwin_paths > /dev/null 2>&1
_sublime_darwin_paths=(
	"/usr/local/bin/subl"
	"$HOME/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl"
	"$HOME/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl"
	"/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl"
	"/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl"
)
```

The only small change I had to make was line 4, and 6, and just like that, one of my favorite ZSH shortcuts is fixed! If your Sublime Text 3 application is named `Sublime Text 3.app` I would assume that you'd just have to change the 2, to a 3, and that would fix the problem just as easily.

Hooray!