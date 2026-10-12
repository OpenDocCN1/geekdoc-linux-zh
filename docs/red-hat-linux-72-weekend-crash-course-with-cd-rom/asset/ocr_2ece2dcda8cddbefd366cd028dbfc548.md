# Session 22—Understanding How Red Hat Linux Boots

This says that init should execute the command `/etc/rc.d/rc` 5 and wait until that command completes.

The /etc/rc.d/rc script is somewhat complicated. Here is how it works:

+   - It changes to the directory corresponding to the run level. For example, to change to run level 5, the script changes to the /etc/rc/rc5.d directory.
+   - In the directory that corresponds with the run level, it looks for all files that begin with a 1 and executes each of them with a stop argument. This kills currently running processes. Then it locates all files that begin with an S and executes each file with an argument of start. This starts the processes needed for the specified run level.

To see what gets executed at run level 5, type the command `ls -l /etc/rc.d/rc5.d`. The output, shown in the following listing, is truncated because it is repetitive:

```
ls -l /etc/rc.d/rc5.d
total 0
lrwxwxwxwx    1 root     root    15 Aug 14 16:24 K01pppoe -> ../init.d/pppoe
lrwxwxwxwx    1 root     root    14 Aug 14 16:08 K051snd -> ../init.d/finnd
lrwxwxwxwx    1 root     root    13 Aug 19 22:18 K20nfs -> ../init.d/nfs
lrwxwxwxwx    1 root     root    16 Aug 14 16:24 K20rstatd -> ../init.d/rstatd
lrwxwxwxwx    1 root     root    17 Aug 14 16:24 K20ruserd -> ../init.d/ruserd
lrwxwxwxwx    1 root     root    16 Aug 14 16:24 K20rwalld -> ../init.d/rwalld
lrwxwxwxwx    1 root     root    16 Aug 14 16:24 K20rwhod -> ../init.d/rwhod
...part of listing deleted...
...
.
.
.
....init.d/sendmail
lrwxwxwxwx    1 root     root    18 Aug 14 16:26 S80sendmail -> ../init.d/sendmail
lrwxwxwxwx    1 root     root    13 Aug 14 16:07 S85pam -> ../init.d/gpm
lrwxwxwxwx    1 root     root    15 Aug 14 15:58 S85htpd -> ../init.d/htpd
lrwxwxwxwx    1 root     root    13 Aug 14 15:58 S90x -> ../init.d/xfs
lrwxwxwxwx    1 root     root    17 Aug 14 15:55 S95anacron -> ../init.d/anacron
lrwxwxwxwx    1 root     root    19 Aug 14 16:16 S991inxconif -> ../init.d/linuxconif
lrwxwxwxwx    1 root     root    11 Aug 14 15:56 S991ocal -> ../rc.local
```

As the output shows, all files with names starting with K and S are symbolic links to scripts that reside in the /etc/rc.d and /etc/init.d directories. In fact, the /etc/rc.d/rc script executes these files exactly in the order that they appear in the directory listing.

> Note that the last file in the directory listing is a symbolic link to the ../rc.local script. This means that /etc/rc.d/rc.local is executed after all other scripts. So you can place in that script any command you want executed whenever your Linux system boots.