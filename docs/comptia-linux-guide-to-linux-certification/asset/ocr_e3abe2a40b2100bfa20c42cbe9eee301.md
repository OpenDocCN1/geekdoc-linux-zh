5 blocks
[root@server1 ~]# _

To view the verbose table of contents of this archive, you can use the following command:

```
```
[root@server1 ~]# cpio -vitB -I /dev/st0
drwxr-xr-x  2 root  root          0 Jul 27 13:40 /root/sample
-rw-r--r--  1 root  root      20239 Jul 21 08:15 /root/sample/samplefile
-rw-rw-r--  1 root  root         574 Jul 21 08:18 /root/sample/samplefile2
5 blocks
[root@server1 ~]# _
```
```

Following this, you can extract the archive on /dev/st0, creating directories and overwriting files as needed by using the following command:

```
```
[root@server1 ~]# cpio -vicd uB -I /dev/st0
/root/sample
/root/sample/samplefile
/root/sample/samplefile2
5 blocks
[root@server1 ~]# _
```
```

Like tar, the cpio command can be used to create an archive on a file on the filesystem; to do this, simply specify the filename after the -O option. To create an archive called /root/sample.cpio that contains the files from the directory /root/sample, using a block size of 5 Kb as well as a common header, and to view the results, you can issue the following command:

```
```
[root@server1 ~]# find /root/sample | cpio -vocB -O /root/sample.cpio
/root/sample
/root/sample/samplefile
/root/sample/samplefile2
5 blocks
[root@server1 ~]# ls -l sample.cpio
-rw-rw-rw-  1 root  root      25600 Jul 27 13:45 sample.cpio
[root@server1 ~]# _
```
```

As with the tar utility, cpio archive filenames need not have an extension to identify their contents. However, it is good practice to use extensions, as shown with /root/sample.cpio in the preceding example.

# ## Using dump/restore

Like tar and cpio, the dump command can be used to back up files and directories to a device or to a file on the filesystem, and the restore command can be used to restore those files and directories. However, dump and restore can only work with files on ext2, ext3, and ext4 filesystems.

![](bbox=[0.15, 0.81, 0.25, 0.88])

The dump and restore commands are not installed on Fedora 20 or Ubuntu Server 14.04 by default. To install them from a software repository on the Internet, you can run the yum install dump command as the root user on Fedora 20, or the apt-get install dump command as the root user on Ubuntu Server 14.04.