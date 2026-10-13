```
<META HTTP-EQUIV="content-type" CONTENT="text/html; charset=iso-8859-1">
<META NAME="keywords" CONTENT="Sherlock Holmes,Arthur Conan Doyle,Dr. Watson,John Watson,Sherlockian,Baker Street,221b,Moriarty,detective,mystery,London,England,Jeremy Brett,Christopher Plummer,Scotland Yard">
<META NAME="description" CONTENT="A reader-friendly library of some of the best Sherlock Holmes stories, as written by Arthur Conan Doyle and narrated by Dr. Watson. Inspired by the work of Project Gutenberg. Note: Site won't work with Netscape 4.x">
<META NAME="ROBOTS" CONTENT="ALL">
<TITLE>The Adventures of Sherlock Holmes, by Arthur Conan Doyle</TITLE>
```

Simple in concept, and simple in execution, virtual hosts are a “killer app” for Unix as an Internet server. As a system administrator, it’s your job to configure and maintain this sort of setup if you’re with an ISP or any other firm that serves up Web sites, and as such, it should be a relief that it’s so straightforward.

Having run different Web hosting servers for almost 10 years now (rather amazing, really!), my experience leads me to two strong recommendations:

+   1. Put all the Web sites on a different partition or different physical disk. It helps manage disk space and maintain quotas for customers (see Hour 12, “Managing Disk Quotas,” for more details on how you might set up a simple Web hosting disk usage quota).
+   2. Set up aliases so that when users connect to the server, they’re either dropped directly into their Web hosting account (not a bad strategy, all in all—just set the home directory to /web/sherlockworld, for example), or so that they have a link directly in the home directory that takes them to the appropriate place on the filesystem (perhaps public_html, to be consistent with other hosting firms).

If you can avoid it, don’t let people have telnet or ssh access to the system. Set them up with ftp (see Hour 19, “Running Internet Services”) and, again, have their home directory be their Web directory, too.

A few minutes of organization and proper setup and you can easily manage a server hosting hundreds of Web sites.

# Keeping Your System Secure

The preceding comments about trying to sidestep granting your users telnet or ssh access to the system is the tip of a much bigger iceberg: Unix system security.

Although we clearly do not have sufficient space (or time) left to discuss this topic in any extensive manner, it is worthwhile to wrap up Teach Yourself Unix System Administration in 24 Hours with a brief foray into the world of system and server security.