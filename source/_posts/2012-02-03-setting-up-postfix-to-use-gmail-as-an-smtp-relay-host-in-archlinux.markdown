---
layout: post
title: "setting up postfix to use gmail as a smtp relay host in archlinux"
date: 2012-02-03 10:55
comments: true
categories: 
---

Setting up a MTA (mail transfer agent) to use gmail as a smtp relay host seemed to be a daunting task for me.
The amount of options you can configure postfix with would fill up a book.

I came across Matthew Hawthorne's [excellent post](http://mhawthorne.net/posts/postfix-configuring-gmail-as-relay.html) on how to do exactly this.
I will repeat his post here, modifying it slightly for archlinux.

Step 1, let's install postfix.

```
# pacman -S postfix
```

Step 2, append the following to */etc/postfix/main.cf* which will configure postfix for use with gmail.

```
# sets gmail as relay
relayhost = [smtp.gmail.com]:587

#  use tls
smtp_use_tls=yes

# use sasl when authenticating to foreign SMTP servers
smtp_sasl_auth_enable = yes 

# path to password map file
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd

# list of CAs to trust when verifying server certificate
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt

# eliminates default security options which are incompatible with gmail
smtp_sasl_security_options =
```

Step 3, create a file */etc/postfix/sasl_passwd* and add your gmail credentials.

```
[smtp.gmail.com]:587  username:password
```

Step 4, create a postfix lookup table at */etc/postfix/sasl_passwd.db* by running the following command.

```
# postmap /etc/postfix/sasl_passwd
```

Step 5, start the postfix daemon.

```
# rc.d start postfix
```

Step 6, run the following command to test.

```
$ echo 'hello world!' | mail -s 'first email' username@gmail.com
```

If you set up everything correctly, you should have sent out an email out to *username@gmail.com*.

Bonus: you can control where your local mail gets forwarded to by creating a *~/.forward* file and adding your email to the file so that local mail will get sent to you.
Check out the man page for aliases(5) for more info.
