---
layout: post
title: "Manage your dotfiles with deploydots"
date: 2012-02-02 10:26
comments: true
categories: 
---

I recently folded in and joined the masses that manage their dotfiles through git.
There were many available tools, but I was surprised that none of the tools for managing your dotfiles folder did what I wanted:

1. I wanted a seperate tool.
2. Symlinking files, making folders.
3. Have the toplevel files in the dotfiles folder not have a '.' in front of them.

For the 1st point, I wanted this to be able to have a definitive source to get the tool instead of having to rely on a homegrown script put into the directory as an afterthought.
The 2nd point was to keep ~/dotfiles from getting cluttered with temporary files, logs, and such.
The 3rd point is so that I can simply run "ls" to see the available folders.
An added benefit from the 3rd point was that ~/.git wouldn't conflict with ~/dotfiles/.git.

You can find deploydots at [github](https://github.com/gostrc/deploydots), and [rubygems](https://rubygems.org/gems/deploydots).

Also, you can find my dotfiles at [github](https://github.com/gostrc/dotfiles).

Side note for weechat users.
Weechat currently overwrites the symlinks every time you quit or save the config files.
I opened a task report for this behavior at the [weechat tracker](https://savannah.nongnu.org/task/?11779).
