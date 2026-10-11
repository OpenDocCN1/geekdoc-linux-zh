![](bbox=[0.15, 0.13, 0.23, 0.18])

# **NOTE**

If your Internet connection is slow, you can instead use the `get file3.gz` command. The FTP service automatically compresses file3 with the gzip utility before transmission.

Similarly, to change the current directory on the remote computer to /root/stuff and upload a copy of file4 from the current directory on the local computer to it, as well as view the results and then exit the ftp utility, you can use the following commands at the ftp> prompt:

```
ftp> cd stuff
250 CWD command successful.
ftp> pwd
257 "/root/stuff" is current directory.
ftp> mput file4
mput file4? y
227 Entering Passive Mode (192,168,0,1,70,109)
150 Opening BINARY mode data connection for file4.
226 Transfer complete.
929 bytes sent in 0.00019 seconds (4.8e+03 Kbytes/s)
ftp> ls
227 Entering Passive Mode (192,168,0,1,235,35)
150 Opening ASCII mode data connection for directory listing.
total 8
-rw-r--r--    1 root    root        929 Aug 14 09:26 file4
226 Transfer complete.
ftp> bye
[root@server1 root]#
```

# ## Accessing Files with NFS

Although not as common as FTP, the Network File System (NFS) is another common method for transferring files among UNIX and Linux computers. To access files using NFS, you simply mount a directory from a remote computer on the network that has the NFS daemons started to a local directory. Simply specify the nfs filesystem type, server name or IP address, remote directory, and local directory as arguments to the mount command. For example, to mount the /var directory on the remote computer named nfs.sampledomain.com (IP address 192.168.0.1) to the /mnt directory on the local computer using NFS and view the results, you can use the following commands:

```
[root@server1 root]# mount -t nfs nfs.sampledomain.com:/var /mnt
[root@server1 root]# mount
/dev/hda1 on / type ext3 (rw)
none on /proc type proc (rw)
```