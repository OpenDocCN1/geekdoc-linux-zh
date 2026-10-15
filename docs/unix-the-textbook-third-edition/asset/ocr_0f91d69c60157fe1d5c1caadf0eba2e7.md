```
226 Directory send OK.
ftp> get kernel.txz
local: kernel.txz remote: kernel.txz
229 Entering Extended Passive Mode (|||61444||).
150 Opening BINARY mode data connection for kernel.txz (77467572 bytes).
100% |******************************************| 75651 KiB 174.60 KiB/s
00:00 ETA
226 Transfer complete.
7746752 bytes received in 07:13 (174.48 KiB/s)
ftp> ll s
kernel.txz
ftp> quit
421 Timeout.
%
```

Once you have established an ftp connection, most sites put you in binary mode so that you can transfer non-ASCII files, such as files containing audio and video clips. You can explicitly put the ftp session into binary mode by using the binary command, which ensures proper file transfer. You can revert to ASCII mode by using the ascii command.

In the following in-chapter exercise, you will use the ftp command to transfer a file from a remote host on the Internet.

# EXERCISE 11.19

Establish an anonymous ftp session with the host ftp.FreeBSD.org and transfer all the files related to release 10.1 into your system by using the mget command.

# 11.8.9 Remote Copy

You can use the ftp command to transfer files to and from a remote host on another network, but doing so requires that you log on to the remote host. You can use the rcp (remote copy) command to copy files to and from a remote machine on the same LAN, without logging on to the remote host. This command is not needed in a local area environment if you are using a network-based file system such as the Network File System (NFS). In this case, the storage of your files is completely transparent to you, and you can access them from any host on your network, without specifying the name of the host that contains them. The following is a brief description of the command.

# SYNTAX

```
rcp [options] [host:]sfile [host:]dfile
rcp [options] [host:]sfile [host:]dir
```

Purpose: To copy sfile to dfile