If you wanted to list the contents of the root directory /, you would type:

```
> ls /
CDROM          lib
bin            priv
core           tmp
dev            vmunix
etc            usr
include        var
```

Everything here except for vmunix, which is the piece of software at the heart of UNIX, and core, which is an error file that really should be thrown away, are directories.

> **Filename Facts** Remember that UNIX filenames, and consequently commands, are case-sensitive. UNIX alphabetizes the capitals before the lowercase. This is why CDROM appears before bin.

How can you tell that they are directories? Use option ls to ask it for more information in the listing, specifically the "long" option.

Issue the command as: ls -l <directory name>.

```
> ls -l /
 total 14
dr-xr-xr-x 2 root 512 Jan 8 1995 CDROM
lrwxrwxr-x 1 root 7 Dec 7 1994 bin -> /usr/bin
-r--r--r-- 1 root 8503728 Oct 25 20:16 core
drwxr-xr-x 3 root 11264 Nov 7 13:02 dev
drwxr-xr-x 11 root 3072 Nov 7 13:01 etc
drwxr-xr-x 46 root 2560 Jan 11 1995 include
drwxr-xr-x 23 root 4096 Oct 13 16:29 lib
drwxr-xr-x 4 root 512 Jul 4 1997 priv
drwxrwxrwx 3 root 512 Nov 24 00:30 tmp
-rwxr-xr-x 1 root 1382769 Aug 12 12:57 vmunix
drwxr-xr-x 29 root 1024 Oct 27 17:53 usr
lrwxrwxr-x 1 root 8 May 21 1995 var -> /usr/var
```