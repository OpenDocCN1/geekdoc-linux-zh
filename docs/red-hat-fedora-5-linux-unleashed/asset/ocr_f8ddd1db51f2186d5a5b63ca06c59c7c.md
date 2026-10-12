This is a simple example, but average FTP sessions are similarly trivial. Several other commands are available during an FTP session, but they are rarely used. FTP has the capability to take scripted input and define macros that allow for a much more complicated session.

> TIP
> 
> The FTP info pages are much like the man (manual) pages shipped with almost every command in Linux. More detailed information may be found in the command's source code package.

# Using the lftp Command for File Transfers

The lftp command can be used for file transfers using FTP, HTTP, and various secure protocols such as HTTPS and FTP if a remote proxy is enabled. Two great features of this command are the ability to restart a stalled download in the middle of a file transfer, as well as to start and run multiple downloads in a single session (with job control).

For example, here is a simple session showing an HTTP retrieval from a remote computer running the Apache web server:

```
```
$ lftp http://192.168.2.37
cd ok, cwd=/ 
lftp 192.168.2.37:/> ls
-rw-r-r--  --  manual/mod/core.html
-rw-r-r--  --  manual/index.html
-rw-r-r--  --  icons/apache_pb.gif
-rw-r-r--  --  poweredby.png
lftp 192.168.2.37:/> get poweredby.png
1154 bytes transferred
lftp 192.168.2.37:/> bye
```
```

The lftp command can also be used as a traditional FTP client, but with some interesting features:

```
```
$ lftp 192.168.2.67 -u phudson
Password:
lftp phudson@192.168.2.67:~> cd /d2/isos/redhat/limbo
cd ok, cwd=/d2/isos/redhat/limbo
lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> mget disc1 &
[0] mget *disc1* &
lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> jobs
[0] mget *disc1*
    'limbo-1386-disc1.iso' at 56436448 (8%) 1.08Mi/s eta:9m [Receiving data]
lftp phudson@192.168.2.67:/d2/isos/redhat/limbo> bye
[1843] Moving to background to complete transfers...
$ ps aux | grep lftp
phudson 1843 7.6 1.0 5456 2404 ? S 19:09 0:02 lftp 192.168.2.67
```
```