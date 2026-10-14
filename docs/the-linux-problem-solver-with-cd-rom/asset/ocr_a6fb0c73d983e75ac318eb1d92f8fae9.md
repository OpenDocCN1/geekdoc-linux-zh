You can employ -U user to change the user (the default is your log-in name). It asks you for a password unless you specify the -P passwd option. If you're trying to access a guest share, you can specify an empty password or just press ENTER at the password prompt. Upon success, smbclient gives you a prompt like this:

```
Domain=[MYWRKGRP] OS=[Unix] Server=[Samba 2.0.6]
smb: \>
```

From there, you can use commands similar to ftp's put, mput, get, mget, and so on. Use help to get a full list.

If you want to use shares on Windows machines on a regular basis, you should consider the SMB filesystem available in the Linux kernel. To use it, first get your kernel to support smbfs by either compiling it into the kernel or building and loading it as a module (the latter option is preferable—see Chapter 7). Then look in your SAMBA package for an smbmount program that combines the smbclient and mount programs:

```
# smbmount '\\SERVER\SHARE' -c 'mount /mnt' -U user -P password
```

Relevant man pages: smbclient (1), smbmount (8)

# 4.3 Netatalk

To get your Linux machine to speak AppleTalk, you need two things: kernel support for AppleTalk low-level protocols, and the server programs that provide services (such as filesharing and printing) to clients. AppleTalk has a number of low-level protocols (transport mechanisms), but the most common on local networks is DDP running over Ethernet. There's a kernel configuration option for this under "Networking options"; it's called AppleTalk DDP, and you should configure it as a module as described in Chapter 7.

The Netatalk package deals with the services. Its main facilities are file-sharing and printing for servers and clients, but it also includes a few utilities for looking up names and converting Macintosh-style files. The original Netatalk package has not been modified for some time, but a new version with many enhancements called Netatalk-asun is now available. This book assumes you have the enhanced package. In addition to the version on the included CD-ROM in support/atalksamba, you'll find it (at least at the time we wrote this book) at ftp://ftp.u.washington.edu/public/asun/.

Unfortunately, Netatalk's included documentation is on the skinny side; the manual pages only describe command-line options, with very little description of configuration files.

After you've built the AppleTalk kernel module (appletalk.o), use insmod on it. The kernel generates a message such as this:

```
NET4: AppleTalk 0.18 for Linux NET4.0
```