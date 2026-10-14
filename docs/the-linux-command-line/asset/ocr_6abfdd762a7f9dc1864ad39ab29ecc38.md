```
Fedora      7      05/31/2007
Ubuntu      7.04   04/19/2007
SUSE        10.2   12/07/2006
Ubuntu      6.10   10/26/2006
Fedora      6      10/24/2006
Ubuntu      6.06   06/01/2006
SUSE        10.1   05/11/2006
Fedora      5      03/20/2006
```

By specifying -k 3.7 we instruct sort to use a sort key that begins at the seventh character within the third field, which corresponds to the start of the year. Likewise, we specify -k 3.1 and -k 3.4 to isolate the month and day portions of the date. We also add the n and r options to achieve a reverse numeric sort. The b option is included to suppress the leading spaces (whose numbers vary from line to line, thereby affecting the outcome of the sort) in the date field.

Some files don’t use tabs and spaces as field delimiters; for example, the /etc/passwd file:

```
[me@linuxbox ~]$ head /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534: sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
```

The fields in this file are delimited with colons (:), so how would we sort this file using a key field? sort provides the -t option to define the field separator character. To sort the passwd file on the seventh field (the account’s default shell), we could do this:

```
[me@linuxbox ~]$ sort -t ':' -k 7 /etc/passwd | head
me:x:1001:1001:Myself,,,:/home/me:/bin/bash
root:x:0:0:root:/root:/bin/bash
dhcp:x:101:102::/nonexistent:/bin/false
gdm:x:106:114:Gnome Display Manager:/var/lib/gdm:/bin/false
hplip:x:104:7:HPLIP system user,,,:/var/run/hplip:/bin/false
klog:x:103:104::/home/klog:/bin/false
messagebus:x:108:119::/var/run/dbus:/bin/false
```