line-based editor: This is one of the oldest mail clients for Linux, and most distributions include `mail`. Start the `mail` client, like this:

```
$ mail
$ mail
Mail version 8.1 6/6/93.  Type ? for help.
"./var/spool/mail/tbball": 18 messages 1 new

1 MAILER-DAMON@ux.or  Wed May 9 13:03 12/505  "DON'T DELETE THIS MES"
2 tbbarg@pop.mail.rcn  Thu Mar 23 23:18 1552/115498 "Re: Back At You!"
3 bbelle@ch.com  Tue Jun 27 09:41 104/3131 "MS Haiku"
4 slashdot@slashdot.or  Tue Sep 12 14:08 42/1690 "Slashdot user password"
5 Forum.Help@PDUBuzz.c  Sat Oct 28 11:22 40/1564 "Your UserName and Pass"
6 morely@sourceforge.  Sat Dec 16 00:15 39/1530 "SourceForge Account R"
7 Harsh@2aa0l.com  Tue Jan 2 23:06 42/1400 "New Cell Number"
8 hduff2@worldnet.att.  Fri Mar 2 10:40 100/3778 "Re: Maximum Linux"
9 nbast@inopnet.com  Sun Mar 25 22:46 58/2440 "Re: OS X and Linux"
10 ctaul@beesomeganlewis  Mon Apr 30 16:18 55/3075 "It's Post Time"
11 J15240-R6916@lmail.co  Mon Apr 30 16:56 153/3339 "LinuxWorld Conference"
12 Rencich&comdt.usc@y.u  Tue May 1 11:24 120/3530 "Re: boat stuff"
13 dennis@ls.net  Thu May 3 09:25 90/3731 "[novalg] Linuxfest i*"
14 Jbodmer@acrf.dhns.gov  Fri May 4 16:54 79/3312 "...no subject..."
15 Redlate@redat.rgc2.n  Mon May 7 20:36 1734/61398 "Under the Brim | Red"
16 service@microsoft.co  Tue May 8 10:23 97/4025 "Microsoft Order Compl"
17 steeve@brightchand.  Tue May 10 12:53 58/2554 "Action Required to Ac"
>N 18 Service@bytargus.co  Wed May 9 13:06 50/1709 "Targus.com - Order No"&
```

Current messages will be listed in numerical order. Note that a new message will be prefaced by a capital N. The prompt, an ampersand (&), is used as a one-letter command line. The following are typical mail commands:

+   ?	Display help
+   	d	Delete messages	e	Edit messages
+   	i	Escape to a shell
+   	h	Print out message headers
+   	n	Go to and type next message
+   	q	Quit, saving unresolved messages in mbox
+   	R	Reply to message senders
+   	x	Quit, do not remove system mailbox