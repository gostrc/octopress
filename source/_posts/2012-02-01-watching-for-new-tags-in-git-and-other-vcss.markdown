---
layout: post
title: "Watching for new tags in git and other VCSs"
date: 2012-02-01 09:57
comments: true
categories: 
---

*Background*

As any packager will tell you, part of the work involves updating a package to the latest version.
This is especially true for a distro like [archlinux](http://www.archlinux.org/) where it is known for its extremely up to date, stable packages.

I maintain a couple of packages for archlinux and it is important for me to check for new versions of a package.
When I first started packaging, I manually checked for new packages by going to the package's website and verifying that there was no new version.
This got tedious, and repetitive very fast. This was about the time I came across [urlwatch](http://thp.io/2008/urlwatch/).

Urlwatch is a tool that watches websites and commands for changes since you last ran them.
This allowed you to initially take some time to set it up.
Then each subsequent run will fetch all the webpages and diff them against the previous versions it has in its cache.
This was better and made me actually want to check for new versions. Except this came with its own problems:

1. Lots of false positives due to dynamic content (e.g., ratings, user comments, etc.)
2. You need to write filters on a per site basis to minimize false positives.
3. Mercurial (hg) repositories require you to have a full copy of the repository locally to list out all the tags.

I know that upstream projects that use version control systems (git, svn, hg, ...) usually create tags whenever they create a new release.
I realized that checking for new tags would probably be the best way to check for new package versions since you might even get notified before any news item is even released.

*Tagurit*

As a result of the above limitations/frustrations with urlwatch, I decided to write a small tool in ruby called tagurit.
One benefit this brought was simple configuration which meant you only had to paste the url to the repository and the tool does the rest.
Also, false positives are practically nonexistent, besides development version tags.

I use this tool quite often and it does its job perfectly.
There are still situations were something like urlwatch is required to check for new versions of a package:

1. Upstream doesn't use a version control system.
2. Upstream doesn't properly use the VCS and doesn't use tags.
3. Upstream uses an unsupported VCS (not git, svn, or hg).

The 1st and 2nd items can't be addressed by me.
But the 3rd item is because I don't maintain any packages that use another VCS.
If you want support for a new VCS type that supports tags, I would be happy to look into it if you open a feature request on github.

Checkout tagurit on [github](https://github.com/gostrc/tagurit), or [rubygems](https://rubygems.org/gems/tagurit).
