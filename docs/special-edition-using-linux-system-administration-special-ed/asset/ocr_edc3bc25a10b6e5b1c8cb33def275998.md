+   - The applications in the bin directory should have permission set to 111: Execute for all users.
+   - The etc directory (that is, /home/ftp/etc/ in all the examples in this chapter) should be owned by the root user and the group root or wheel.
+   - The etc directory’s permissions should be 111: Execute for all users.
+   - The passwd and group files in the etc directory must have 444 as their permission: Readable by all users.
+   - The lib directory (that is, /home/ftp/lib/ in all the examples in this chapter) should be owned by the root user and the group root or wheel.
+   - All files in the lib directory should have 555 as their permission: Readable and executable by all users.
+   - The pub directory (that is, /home/ftp/pub/ in all the examples in this chapter) should be owned by the root user or the user who is assigned to maintain the archive.
+   - The pub directory’s permission should be 555: Readable and executable by all users.

The following directory listings show file and directory permissions from the anonymous FTP user’s directory on a sample FTP site:

```
 # cd /home/ftp
 # ls -l
 d--x--x--x  2 root     root          1024 Nov 11 21:14 bin
 d--x--x--x  2 root     root          1024 Nov 11 21:14 etc
 d--x--x--x  2 root     root          1024 Nov 11 21:14 lib
 dr-xr-xr-x  2 root     root          1024 Nov 11 21:14 pub
 # ls -l etc
 -r--r--r--  1 root     root            29 Nov 10 20:26 group
 -r--r--r--  1 root     root            91 Nov 10 20:25 passwd
 # ls -l bin
 -r-x--x--x  1 root     wheel        50148 Nov 10 20:20 ls
 # ls -l lib
 -r-xr-xr-x  1 root     root        342206 Nov 10 22:29 ld-2.1.1.so
 lrwxrwxrwx  1 root     root            11 Nov 10 22:29 ld-linux.so.2 -> \
 ld-2.1.1.so
 -r-xr-xr-x  1 root     root       4016683 Nov 10 22:30 libc-2.1.1.so
 lrwxrwxrwx  1 root     root            13 Nov 10 22:30 libc.so.6 -> \
 libc-2.1.1.so
 -r-xr-xr-x  1 root     root       364235 Nov 10 22:38 libnsl-2.1.1.so
 lrwxrwxrwx  1 root     root            15 Nov 10 22:40 libnsl.so.1 -> \
 libnsl-2.1.1.so
 -r-xr-xr-x  1 root     root       239464 Nov 10 22:39 libnss_files-2.1.1.so
 lrwxrwxrwx  1 root     root            21 Nov 10 22:39 libnss_files.so.2 -> \
 libnss_files-2.1.1.so
```

# TESTING YOUR ANONYMOUS FTP SERVER

When you have configured WU-FTPD for anonymous access, double-check that it is running properly. To do this, use the FTP client included with your Linux distribution to connect to the new FTP server and log in as the anonymous user. Once connected, you need to test several things: