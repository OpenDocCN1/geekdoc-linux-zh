If the permissions were set correctly, the pub directory should be the only directory that shows any files under it. To verify this change, change directories to etc and list the contents.

```
ftp> cd etc
250 CWD command successful.
ftp> PORT command successful.
200 Opening ASCII mode data connection for directory listing.
total 0
226 Transfer complete.
```

By setting the permissions to execute only on the directories bin, lib, and etc, you cannot see any files in that directory. If the permissions were set to read or write/access, it would be possible to see the passwd file in the /etc directory, allowing a user to get a copy of the encrypted password file. Although this file doesn't contain passwords, it will give you user information about the system that could aid in hacking attempts.

Now that you have verified the server is relatively secure, change directories to /pub and list the contents of that directory.

```
ftp> cd pub
250-Please read the file README
250- it was last modified on Sun Sep 2 19:25:47 2001 - 1 day ago
250 CWD command successful.
ftp> ls
200 Opening ASCII mode data connection for directory listing.
total 552
-rw-r--r-- 1 root 50 100 Sep 2 19:25:47 README
-rw-r--r-- 1 root 50 8 Sep 3 07:03:33 configuration
-rw-r--r-- 1 root 50 8 Sep 3 07:03:33 temp.txt
-rw-r--r-- 1 root 50 15798 Sep 3 10:29:18 tftp-0.17-14.i386.rpm
-rw-r--r-- 1 root 50 26011 Sep 3 10:30 tftp-
server-0.17-14.i386.rpm
-rw-r--r-- 1 root 50 219332 Sep 3 10:29:00 wu-ftpd-
2.6.1-18.i386.rpm222 Transfer complete.
```

To transfer all RPM files to your local machine, issue the mget *.rpm command.

```
ftp> mget *.rpm
local: tftp-0.17-14.i386.rpm remote: tftp-0.17-14.i386.rpm
200 PORT command successful.
150 Opening ASCII mode data connection for tftp-0.17-14.i386.rpm
(15798 bytes).###########
```