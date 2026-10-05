To check for a Trojan horse, examine the filesystem periodically for files
setuid (page 420) permission. The following command lists these files:

Listing setuid files `sudo find / -perm 4000 -exec ls -lh {} \; 2> /dev/null`

```
-rws-xr-x 1 root 125K 2015-03-26 11:24 /usr/bin/sudoedit
-rws-xr-x 1 root 14K 2010-03-21 15:12 /usr/bin/arping
-rws-xr-x 1 root 31K 2010-01-26 09:09 /usr/bin/chsh
-rws-sr-x 1 daemon daemon 42K 2010-03-04 18:35 /usr/bin/at
-rws-xr-x 1 root 36K 2010-01-26 09:09 /usr/bin/chfn
-rws-xr-x 1 root 37K 2010-01-26 09:09 /usr/bin/passwd
-rws-xr-x 1 root 1lpadmin 2010-04-09 08:13 /usr/bin/lpassword
```

This command used to find all files that have their setuid bit set (mode 4000).
The hyphen prefix causes the command to find any file that has this bit set,
regardless of how the other bits are set. The output sent to /dev/null does not clutter the screen.

Another way a Trojan horse can enter a system is via a ~/.bashrc (page 488)
. A bogus sudo command or alias in this file can capture a user's password,
which may then be used to gain root privileges. Because a user has write permission
to this file, any program the user executes easily modify it. The best way to
this type of Trojan horse from entering a system is to run software only from
s you trust.

You can set up a program, such as AIDE (Advanced Intrusion Detection Environ-nment), that will take a snapshot of the system and periodically check files for-changes. For more information see sourceforge.net/projects/

# GETTING HELP

The Ubuntu distribution comes with extensive documentation (page 136).
For example, the Support tab on the Ubuntu home page (www.ubuntu.com/sup-port) and the Ubuntu wiki (wiki.ubuntu.com) point to many useful sources of-port that can also find help on the System
Administrators Guide site (www.sage.org). The Internet is another rich source of
information on managing a Linux system; refer to Appendix B (page 1099) and
the author's home page (www.sobell.com) for pointers to useful sites.

You need not act as an Ubuntu administrator in isolation; a large community of
Linux/Ubuntu experts is willing to assist you in getting the most out of your.
You will get better help if you have already tried to solve a problem by yourself
reading the available documentation. If you are unable to solve a problem by consult-ing the documentation, a well-thought-out question posed to the appropriate news-group, such as comp.os.linux.misc, or mailing list can often generate useful