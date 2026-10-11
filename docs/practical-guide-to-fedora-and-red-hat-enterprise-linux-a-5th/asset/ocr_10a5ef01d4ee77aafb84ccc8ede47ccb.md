# EMAIL

Email enables you to communicate with users on the local system and, if the installation is part of a network, with other users on the network. If you are connected to the Internet, you can communicate electronically with users around the world.

Email utilities differ from **write** in that email utilities can send a message when the recipient is not logged in. These utilities can also send the same message to more than one user at a time.

Many email programs are available for Linux, including the original character-based **mail** program, Mozilla/Thunderbird, **pine**, mail through **emacs**, KMail, and **evolution**. Another popular graphical email program is **sylpheed** (sylpheed.sraoss.jp/en).

Two programs are available that can make any email program easier to use and more secure. The **procmail** program (www.procmail.org) creates and maintains email servers and mailing lists; preprocesses email by sorting it into appropriate files and directories; starts various programs depending on the characteristics of incoming email; forwards email; and so on. The GNU Privacy Guard (GPG or GnuPG, page 1048) encrypts and decrypts email and makes it almost impossible for an unauthorized person to read.

Refer to Chapter 20 for more information on setting email clients and servers.

If your system is part of a LAN, you can generally send email to and receive email from users on other systems on the LAN by using their usernames. Someone sending Alex email on the Internet would need to specify his *domain name* (page 1080) along with his username. Use this address to send email to the author of this book: **mgs@sobell.com**.

# TUTORIAL: CREATING AND EDITING A FILE USING **vim**

This section explains how to start **vim**, enter text, move the cursor, correct text, save the file to the disk, and exit from vim. The tutorial discusses three of the modes of operation of vim and explains how to switch from one mode to another.

# The full version of **vim** is not installed by default

By default, Fedora/RHEL systems install a minimal build of vim that is run by the command **vi** (see the tip on the next page). The commands **vim** and **vimtutor** do not work. Working as **root** (page 408), give the following yum (page 500) command to install the full version of vim:

```
yum install vim-enhanced
```

You can use the minimal build of vim to work through the examples in this chapter: Substitute the command **vi** for **vim** in the examples.

In addition to working with this tutorial, you may want to try vim’s tutor, named **vimtutor**: Give its name as a command to run it.