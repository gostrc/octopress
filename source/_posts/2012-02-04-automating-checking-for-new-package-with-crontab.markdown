---
layout: post
title: "automating checking for new packages with crontab"
date: 2012-02-04 21:30
comments: true
categories: 
---

You might have some command you repeatedly type to check its output.
I occasionally check for new package updates using tagurit and urlwatch which I mentioned in a previous post.
The problem is that it can get tedious running those commands over the terminal every day or week.
Let's automate this.

Setting up cron to run a scheduled command is the perfect solution.
So let's do it.

I will be doing this on archlinux but it should be the same on any computer with the same software installed.

First of all, you have to have the crond daemon running for this to work.
It is turned on by default on archlinux so we already have that working.

Next, we need to edit our crontab file by running:

```
$ crontab -e
```

Then for my example, I want to run urlwatch and tagurit every day at 6am and 6pm.
After I check crontab(5) to check the format of the file, I type the following in:
```
0 6,18 * * * urlwatch
0 6,18 * * * tagurit
```

This will run every day, every time our computer is turned on.
Cron will also send us a message to our local mail account if there is any output from the commands it ran.

Since I want it to deliver it to my gmail account, we first need to set up a postfix daemon to use gmail as a smtp relay host.
I covered that in a previous blog post.
I also covered how to set up a *~/.forward* file in the previous blog post in the bonus section.
The *~/.forward* file will route all our local messages to the specified email.
If you haven't done so already, please set that up.

You should now be automatically running and receiving commands via cron!
