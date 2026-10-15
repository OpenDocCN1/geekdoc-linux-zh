multiple-booting systems where you can use any suitable boot loader which is capable of booting multiple operating systems. I chose GRUB in this guide for three specific reasons: 1) GNU GRUB is the "default" boot loader in Red Hat distribution releases currently. 2) As mentioned in the 'Release Notes' of Red Hat Linux 8.0, the use of LILO is deprecated and the package would be removed from one of its future releases. 3) GRUB is a very powerful (x86) PC-compatible boot loader which supports a number of operating systems "directly" and other proprietary ones too via "chain-loading" for booting them. Thus, GRUB is used instead of other boot loaders.

11. **I have older Red Hat, FreeBSD and OpenBSD distributions and/or releases. Will they work?**

I am sure they would with a few modifications at places. All steps mentioned should behave in a normal manner if you are using Kernel 2.2.x or higher (for Linux). For FreeBSD users, if you are using not earlier than 4.X–RELEASES, there should not be any problems whatsoever. Just take a deep breath, and start doing as given in this guide. If in case, at some place it does "not" work, make sure you are using the right step and commands etc. Most times, it is human error rather than computer-related error which lets big servers and networks down. Always remember this!

12. **I would like to have access to good resources on Linux and FreeBSD. Could you suggest a few?**

Yes, definitely I could. There is a lot of very good technical information on all the "open-source" operating systems out there on the Internet. For Linux, make sure you often visit http://www.linuxgazette.com, http://www.linuxfocus.org, http://www.linux.com and a host of others. Besides, "The Linux Documentation Project" (TLDP) provides excellent resources on all topics related to GNU/Linux. As for printed books, these are some of my absolute favorites: Red Hat Linux 8.0 Bible, Understanding the Linux Kernel, Modern Operating Systems, Linux Kernel Programming, The FreeBSD Handbook at http://www.freebsd.org, The Design of the UNIX Operating System, The Design and Implementation of the 4.4BSD Operating System. That would be enough for the time-being!

13. **I have a few suggestions, new ideas and exciting comments. Can I send them to you?**

Without asking, please do. Only by hearing from others, I can make this guide a better one in the near future. So, drop a line if you want to.

14. **I have "installation-specific" questions/queries or something "failed" or "this quite didn't work"? Can I send these reports to you?**

Of course do. But please be patient, cause I am busy with lots of things at my university; tests, exams, assignments, dating my "infinitely patient FreeBSD-compatible rock-stable girlfriend", maintaining this guide, other Linux assignments etc. So, I cannot promise to get back to you immediately. I need some time solving your problems.