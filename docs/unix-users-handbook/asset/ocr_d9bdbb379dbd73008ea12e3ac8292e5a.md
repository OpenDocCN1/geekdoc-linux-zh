```
$ paste llsum.out ll.out
FILENAME             SIZE      total 792
README               810      -rwxrwxrwx
backup_files         3408     -rwxrwxrwx
biography            427      -rwxrwxrwx
cshtest              1024     drwxr-xr-x
gklll                1855     -rwxrwxrwx
gkill.out            191      -rw-r--r--
hostck               924      -rwxrwxrwx
ifstat               1422     -rwxrwxrwx
ifstat.int            2147    -rwxr-xr-x
ifstat.out             723     -rw-r--r--
intros               54018    -rw-r--r--
introux              52476    -rwxrwxrwx
letter               23552    -rw-r--r--
letter.auto          69632    -rw-r--r--
letter.auto.recover  71680    -rw-r--r--
letter.backup        23552    -rw-r--r--
letter.lck            57      -rw-rw-rw-
letter.recover      69632     -rw-r--r--
ll.out               1057     -rw-r--r--
llsum                1267     -rwxrwxrwx
llsum.orig           1267     -rwxr-xr-x
llsum.out            1657     -rw-r--r--
llsum.tomd.out       1356     -rw-r--r--
psg                  670      -rwxrwxrwx
psg.int              802      -rwxr-xr-x
psg.out              122      -rw-r--r--
sam_adduser          1010     -rwxrwxrwx
tdolan               1024     drwxr-xr-x
trash                4554     -rwxrwxrwx
trash.out            329      -rw-r--r--
typescript           679      -rw-r--r--
$

```

![](bbox=[0.89, 0.08, 0.98, 0.17])

This has produced a list that includes FILENAME and SIZE from llsum.out and permissions from ll.out.

![](bbox=[0.89, 0.7, 0.98, 0.8])

If both the files have the same first field, you can use the join command to merge the two files:

![](bbox=[0.89, 0.79, 0.98, 0.89])

The following is a summary of the paste and join commands, with some of the more commonly used options: