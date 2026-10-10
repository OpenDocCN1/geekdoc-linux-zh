The three files with the date appended (7/12/00 time 15:04) to the end of the filename were produced by the **fbackup** command issued earlier. The date appended to the end of the file can help in the organization of backup files. We could restore any or all of these files with **frestore** from the file that contains the backup information (*`/tmp/testbackup`*), as demonstrated earlier.

We are not restricted to performing backups to a tape drive attached to the local system. We can backup to a remote tape with **fbackup** by specifying the system name and tape drive, or file, to which we want to store the files. The following example uses **fbackup** options covered earlier and also includes the name of the system with the tape drive:

```
# fbackup -f tapesys:/dev/rmt/0m -i /var/tmp -v
fbackup(1004): session begins on Wed Jul 12 15:56:22 2000
fbackup(3507): volume 1 has been used 1 time(s) (maximum: 100)
fbackup(3024): writing vol 1 to output file tapesys:/dev/rmt/0m
1: /
2: /var
3: /var/tmp
4: /var/tmp/AAAA1812 0
5: /var/tmp/AAAA1992 0
6: /var/tmp/BEQ19522 19
7: /var/tmp/DCB19522 0
8: /var/tmp/DBC19522 0
9: /var/tmp/ISPX19522 0
.
.
.
73: /var/tmp/eaaa13306 1
74: /var/tmp/ems_inittab.old 2
75: /var/tmp/envd.action2 1
76: /var/tmp/envd.action5 1
77: /var/tmp/inet.conf.old 9
78: /var/tmp/net19522 1799
79: /var/tmp/swagent.log 16
fbackup(1005): run time: 43 seconds
fbackup(3055): total file blocks read for backup: 1974
fbackup(3056): total blocks written to output file ori:/dev/rmt/0m: 0
#
```

This command performs the backup of */var/tmp* on system *or1* by sending the files to the tape drive on system *tapesys*. We could have used many additional options to **fbackup** as demonstrated in earlier examples, but I wanted to keep the example simple so that it would be easy to see the remote tape drive specification.