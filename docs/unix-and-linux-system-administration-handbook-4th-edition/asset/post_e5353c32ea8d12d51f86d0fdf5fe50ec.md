
# EMC NetWorker

Storage behemoth EMC acquired Legato NetWorker back in 2003. At the time, Veritas and Legato were the two market leaders for enterprise backup.

Pros:
- Competitively priced
- Server software can run on each of our example platforms
- Supports diverse client platforms
- Slick, integrated bare-metal restorations

Cons:
- Significant overlap among EMC products

## Other alternatives

W. Curtis Preston, author of the O'Reilly book Backup & Recovery, maintains a web page about backup-related topics (disk mirroring products, advanced filesystem products, remote system backup products, off-site data-vaulting products, etc.) at backupcentral.com.

## 10.10 RECOMMENDED READING

PRESTON, W. CURTIS. Backup & Recovery: Inexpensive Backup Solutions for Open Systems. Sebastopol, CA: O'Reilly Media, 2007.

## 10.11 EXERCISES

E10.1 Investigate the backup procedure used at your site. Which machines perform the backups? What type of storage devices are used? Where are tapes stored? Suggest improvements to the current system.

E10.2 What steps are needed to restore files on a system that uses Bacula? How do you find the right tape?

E10.3 Given the following output from df and /etc/dumpdates, identify the steps needed to perform the three restores requested. Enumerate your assumptions. Assume that the date of the restore request is January 18.

df output from the machine khaya.cs.colorado.edu:

```
/dev/hda8    256194   81103   161863   33% /
/dev/hda1    21929    4918    15879   24% /boot
/dev/hda6   3571696  24336  3365924   1% /local
/dev/hda10  131734    5797   119135   5% /tmp
/dev/hda5  1815580 1113348  610004   65% /usr
/dev/hda7   256194   17013   225953   7% /var
```

/etc/dumpdates from khaya.cs.colorado.edu:

```
/dev/hda8   2 Sun Jan 17 22:59:23 2010
/dev/hda6   3 Sun Jan 17 22:51:51 2010
/dev/hda7   3 Sun Jan 17 22:50:24 2010
/dev/hda5   9 Sun Jan 17 22:46:25 2010
/dev/hda5   1 Tue Jan 12 22:45:42 2010
/dev/hda7   0 Tue Jan 12 23:14:47 2010
/dev/hda6   1 Tue Jan 12 23:14:32 2010
/dev/hda8   1 Tue Jan 12 23:14:17 2010
/dev/hda6   0 Sun Jan 10 22:47:31 2010
/dev/hda1   1 Fri Jan  8 22:16:05 2010
/dev/hda7   1 Thu Jan  7 22:08:09 2010
/dev/hda1   4 Sun Jan  3 22:51:53 2010
/dev/hda7   2 Thu Dec 24 22:53:52 2009
/dev/hda5   0 Tue Nov  3 22:46:21 2009
/dev/hda1   0 Mon Sep 21 22:46:29 2009
/dev/hda8   0 Mon Aug 24 23:01:24 2009
/dev/hda1   3 Wed Jul 29 22:52:20 2009
/dev/hda6   2 Wed Jul 29 23:01:32 2009
```

- a) "Please restore my entire home directory (/usr/home/clements) from some time in the last few days. I seem to have lost the entire code base for my senior project."
- b) "Umm, I accidentally did a sudo rm -rf * on my machine khaya. Could you restore all the filesystems from the latest backups?"
- c) "All my MP3 files that I have been collecting from BitTorrent over the last month are gone. They were stored in /tmp/mp3/. Could you please restore them for me?"

E10.4 Design a backup plan for the following scenarios. Assume that each computer has a 400GB disk and that users’ home directories are stored locally. Choose a backup device that balances cost vs. support needs and explain your reasoning. List any assumptions you make.

- a) A research facility has 50 machines. Each machine holds a lot of important data that changes often.
- b) A small software company has 10 machines. Source code is stored on a central server that has 4TB of disk space. The source code changes throughout the day. Individual users’ home directories do not change very often. Cost is of little concern and security is of utmost importance.
- c) A home network has two machines. Cost is the most important consideration, and the users are not system administrators.

E10.5 Design a restore strategy for each of the three situations described in Exercise 10.4.

E10.6 Write Bacula configuration statements that implement the backup plans you came up with for Exercise 10.4.

E10.7 Outline the steps you would take to perform a dump to a remote tape drive through a secure SSH tunnel.
