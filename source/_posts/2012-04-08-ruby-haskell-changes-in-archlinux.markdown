---
layout: post
title: "ruby haskell changes in archlinux"
date: 2012-04-08 00:33
comments: true
categories: 
---

Since the last post in this blog, I have been busy with cleaning up ruby and haskell support in archlinux.
Specifically changing the default gem install location for ruby and switching haskell away from the haskell-platform for archlinux.

The main change I have made to ruby was changing the default gem install location to ~/.gem/
This change is there to separate pacman installed gems which are installed to /usr/lib/ruby/gems/ and gem installed gems which are now installed to ~/.gem/
The transition has been rather smooth for such a major default change and there were expected problems, but no serious problems have occurred.
The main problem that some users faced was that they were unaware of the change, didn't read the messages, and wondered why sudo gem install foo installed to /root/.gems/

For haskell, I mainly worked on first removing haskell-platform and all of its packages from the extra repository, and then upgrading ghc to the latest stable release.
Although most distros choose to use the haskell-platform, it makes less sense to do this in archlinux since it advertises itself as a rolling release distro which uses the latest stable version of software.
Dropping the haskell-platform has removed a lot of haskell packages from extra and has freed us from having to use the same ghc version as the haskell-platform.
The only packages remaining in extra are ghc and cabal-install along with their dependencies.
There have been a few problems that users encountered, but the most common was that they were unaware that the haskell-platform has been removed.
I did announce the removal, but some people just don't read the mailing list.

Both of these changes are a step in the right direction for archlinux in my opinion.
Hopefully the changes make using these languages a better experience in the long run for arch users.
