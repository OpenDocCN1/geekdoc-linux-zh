```
[root@localhost /usr]# ls -la
total 144
drwxr-xr-x  21 root  root  4096 Apr  1 02:29 .
drwxr-xr-x  17 root  root  4096 Apr  1 02:11 ..
drwxr-xr-x   8 root  root  4096 Mar  6 08:20 X11R6
drwxr-xr-x   2 root  root 28672 Apr  1 02:45 bin
drwxr-xr-x   2 root  root  4096 Apr  1 02:43 dict
drwxr-xr-x 224 root  root 8192 Apr  1 02:45 doc
drwxr-xr-x   2 root  root  4096 Feb  6  1996 etc
drwxr-xr-x   2 root  root  4096 Apr  1 02:43 games
drwxr-xr-x   4 root  root  4096 Apr  1 02:16 i386-redhat-linux
drwxr-xr-x   3 root  root  4096 Apr  1 02:29 i486-linux-libc5
drwxr-xr-x  57 root  root 8192 Apr  1 02:45 include
drwxr-xr-x   2 root  root 8192 Apr  1 02:23 inf eros
drwxr-xr-x   7 root  root  4096 Apr  1 02:29 kdeeros
drwxr-xr-x  55 root  root 16384 Apr  1 02:45 lib
drwxr-xr-x   6 root  root  4096 Apr  1 02:37 libexec
drwxr-xr-x  11 root  root  4096 Apr  1 02:11 local
drwxr-xr-x   2 root  root 16384 Apr  1 02:09 lost+found
drwxr-xr-x  12 root  root  4096 Apr  2 04:02 man
drwxr-xr-x   2 root  root  4096 Apr  1 02:45 sbin
drwxr-xr-x  67 root  root  4096 Apr  1 02:43 share
drwxr-xr-x   4 root  root  4096 Apr  1 02:29 src
lrwxrwxrwx   1 root  root    10 Apr  1 02:11 -> ../var/tmp
[root@localhost /usr]#
```

**Figure 17.1** The contents of /usr in Red Hat Linux.

+   6. In this virtual terminal, type "ls -la /usr". You should get something similar to what is shown in Figure 17.1.
+   7. Change back to the exports file.

+   8. The goal here is to offer the entire /usr hierarchy for export except for /usr/local, because this directory is for use by individual machines. NFS allows you to export a directory either with all of its subdirectories or with none. No "except" functionality is available, unfortunately. So, you add a line for each of the subdirectories except for /usr/local. What you end up with might be similar to the following:

```
/usr/bin		*.animals.org(secure,ro)
/usr/dict		*.animals.org(secure,ro)
/usr/doc		*.animals.org(secure,ro)
/usr/etc		*.animals.org(secure,ro)
/usr/games		*.animals.org(secure,ro)
/usr/i386-redhat-linux	*.animals.org(secure,ro)
/usr/i486-linux-libc5	*.animals.org(secure,ro)
/usr/include	*.animals.org(secure,ro)
```