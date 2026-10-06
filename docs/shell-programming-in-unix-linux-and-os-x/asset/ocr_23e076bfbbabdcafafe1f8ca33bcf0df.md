# Skipping Fields

If you had to sort your data file by the y value—that is, the second number in each line—you could tell sort to start with the second field by using the option

instead of -n. The -k says to skip the first field and start the sort analysis with the second field of each line. Similarly, -k5 would mean to start with the fifth field on each line and then sort the data numerically.

```
$ sort -k2n
14 -9
23 2
15 6
-5 11
2
5 27
3 33$
```

Fields are delimited by space or tab characters by default. If a different delimiter is to be used, the -t option must be used.

# The -t Option

As mentioned, if you skip over fields, sort assumes that the fields are delimited by space or tab characters. The -t option can indicate otherwise. In this case, the character that follows the -t is taken as the delimiter character.

Consider the sample password file:

```
$ cat /etc/passwd
root:0:0:root:/bin/bash
steve:200:100:/users/steve:/usr/bin/ksh
bin:x:13::The owner of system files:
cron:1:1:Cron Daemon for periodic tasks:
george:75:75:/users/george:/usr/lib/rhs
pat*:300:300:/users/pat:/usr/bin/ksh
uucp:nc83CISI2M:5:/usr/spool/public/lib/uuc/uucoico
asg*:6:6:The Owner of Assignable Devices:
sysinfo*:1:10:10:Access to System Information:/usr/bin/sh
mail:301:301:/usr/mail:
$
```

If you wanted to sort this file by username (the first field on each line), you could just issue the command
sort /etc/passwd