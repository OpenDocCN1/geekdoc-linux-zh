# CHAPTER 18 Secure File Transfer Protocol (FTP) Service

This is a simple example, average FTP sessions are similarly trivial. Several other commands are available during an FTP session, but they're rarely used. FTP has the capability to take scripted input and define macros that allow for a much more complicated session. Should you need to use these advanced commands, see the info text on ftp by issuing the command

$ info ftp

> TIP
The FTP info pages are much like the man (manual) pages shipped with almost every command in Linux , but generally contain much more detailed information.

Using the lftp Command for File Transfers
The lftp command can be used for file transfers using FTP, HTTP, and various secure protocols such as HTTPS and FTP if proxy is enabled. Two great features of this command are the ability to restart a stalled download in the middle of a file, as well as to start and run multiple downloads in a single session (with job control).

For example, here is a simple session showing an HTTP retrieval from a remote computer running the Apache Web server:

```
$ lftp http://192.168.2.37
cd ok, cwd=/
lftp 192.168.2.37:> ls
-rw-r--r-- -- manual/mod/core.html
-rw-r--r-- -- manual/index.html
-rw-r--r-- -- icons/apache_pb.gif
-rw-r--r-- -- poweredby.png
lftp 192.168.2.37:> get poweredby.png
1154 bytes transferred
lftp 192.168.2.37:> bye
```

The lftp command can also be used, too, as a "traditional" FTP client, but with some interesting features:

```
$ lftp 192.168.2.67 -u bball
Password:
lftp bball@192.168.2.67:> cd /d2/isos/redhot/limbo
cd ok, cwd=/d2/isos/redhot/limbo
lftp bball@192.168.2.67:> /d2/isos/redhot/limbo mget disc1 &
[0] mget "disc1" *
lftp bball@192.168.2.67:> /d2/isos/redhot/limbo jobs
[0] mget "disc1*
```