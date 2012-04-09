---
layout: post
title: "distribution vs language package managers"
date: 2012-04-08 09:56
comments: true
categories: 
---

I have noticed a lot of confusion and differing views around which is better, using the distribution's package manager or using the package manager that comes with a certain programming language.
I have thought about this problem a lot recently since I had to make some decisions about it recently.
This post is about my opinions on the topic.

I am for using a 3rd party package manager to manage packages provided by a 3rd party repository.
The following are reasons for using a 3rd party package manager:

1. The 3rd party package manager already has access to the whole repository, so you will be able to install all the packages.
2. Upstream usually knows the best way or can be configured to act in the best interest of the user.
3. This lessens the burden of the distro package managers. Why repackage something that is already packaged?

The first point states that since the 3rd party package manager was specifically built to access and install from the 3rd party repository (e.g. gem for rubygems), it will be able to install any package from that repository.
This is contrary to using the distro's package manager, where package maintainers now have the burden to repackage all packages provided by the 3rd party repository.
In practice, I have yet to be shown a distro that successfully, and fully repackages a 3rd party repository that has it's own package manager.
For example, debian provides a lot of official packages for rubygems, yet from my own personal experience, people who use ruby and debian actively avoid debian's ruby's gem packages because they are either too outdated or because there are some packages which haven't been repackaged by debian.

The second point states that if you use the 3rd party package manager, you will most likely find the same behavior across all distros that use that package manager.
Upstream also can change and restructure formats and be able to easily adapt to the changes.
They are providing a common platform to access their repository across all distros.

The third and final point I have is that there would be a *huge* duplication of effort in my opinion if a distro decided to repackage a 3rd party repository successfully.
For example, rubygems.org has 2398 packages that would need to be packaged to provide the same coverage as you get from gem.
This means you will increase the amount of work per 3rd party repository by a huge amount.
Even if you were to automate recreating packages for you distro's package manager, you would still have to take care of lots of edge cases where there are bugs or some kind of failures.

Another thing to consider is what happens when someone repackages the whole repository (or close to it) and then they leave.
This creates an unimaginable amount of old and useless packages.
A case like this already happened with archlinux a while ago with arch-haskell when the maintainers decided to stop updating archlinux's packages that repackaged haskell's packages.
Now there are about 1700 orphaned, useless, and outdated haskell packages in the AUR.

The only cases that I think justify repackaging a 3rd party package are:

1. If you want to provide a certain program that is in the 3rd party repository that you can't easily install using the 3rd party package manager.
2. It is a dependency of the first case.
3. There is no official, and obviously popular 3rd party package manager.

The first point lets a maintainer choose certain important packages which might be hard to install or are critical for some applications.
As an example, the only package that I repackage for haskell is cabal-install which is the 3rd party package manager for haskell.
This will give people the option to easily install the 3rd party package manager which might not be obvious to install using other means.

The second point is a prerequisite for the first case, there's usually no way around it if it's a dependency.

The third point is to cover cases where the packages might have a central location, but it might not be the only place to get the packages from.
Also if the package manager doesn't do a good job of building and cleanly installing the 3rd party packages.

I have been packaging python packages for a while, and have avoided using pip to install python packages, mainly because at the time when I was learning python, using pip wasn't very popular.
I might consider switching over to it after doing some investigation into how it works and how it can be configured.

Hopefully this post helps others and helps me organize my thoughts on the topic.

Cheers!

**update:**
I have reviewed the current situation with python and pip on archlinux and I prefer using pacman for python packages now.
The reason is that there are already so many well maintained python packages.
Also because pip doesn't support a way to easily upgrade all the packages which is something pacman provides.
If it became more gem like providing the benefits of gem over pacman, I would consider using it for everything.
Basically there is almost no incentive for me to switch, and there is a loss of functionality if I switched.
