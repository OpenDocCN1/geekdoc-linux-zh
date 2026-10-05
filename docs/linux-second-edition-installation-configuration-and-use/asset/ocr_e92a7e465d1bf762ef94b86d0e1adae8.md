# FILE TRANSFER PROTOCOL (FTP) 337

open estabablishes a connection with the host computer
(if the first attempt has failed)

put file transfers the file from the current archive into the
FTP archive

quit terminates FTP

user allows a new login (if the first attempt has failed)

# Example

The following example shows how the PPP package 2 is copied from the FTP server
ftp.redhat.com. For reasons of space, some of the texts and directories displayed on
screen have been shown. In order to improve readability, all received texts have
ented by a few characters with respect to user input.

![](bbox=[0.169, 0.386, 0.193, 0.458])

In spite of the shortened texts, the example shows that during an FTP session
vast amounts of text are displayed. Therefore, try to work in an X shell window
or in the shell mode of Emacs, where you can scroll through already displayed
text sessions. less cannot be used in FTP sessions.

```
user$ ftp.redhat.com.
Connected to speedy.redhat.com.
Please use a mirror if possible
```

FTP Site           Directory
==========           =======
ftp.gwdg.           /linux/install/redhat
...

speedy.redhat.com FTP server (Version-2.4.2-academ[BETA-9])(1)
Feb 29 15:50:44 EST 1996) ready.
Name (ftp.redhat.com:kofler): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password: > kofler@ftp.at
Welcome to the Red Hat Software Linux archive.
There are currently 72 users using the ftp archive.
Guest login ok, access restrictions apply.
Remote system type is Unix.
Using binary mode to transfer files.

```
ftp> ls
---
dwxfxxr-xr 3 root root       1024 May 24 20:26 mirrors
dwxfxxr-xr 5 506 506      1024 May 21 14:23 pnp
dwx--x--x 3 root root       1024 May 27 17:10 private
dwxfxxr-xr 15 root root       1024 Jun 5 16:16 pub
dr-xr-xr-x 3 root root       1024 Sep 9 1994 usr
```