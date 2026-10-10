partition. The design behavior for tune2fs when the file system is mounted is to create the journal file called . journal, a hidden file. A file in Linux preceded with the period ( . ) is considered a hidden file; most Linux command line file utilities silently ignore files of this type. From Listing 9-7, we can see that the 1s command was invoked with the - a flag, which tells the ls utility to list all files.

# **Listing 9-7**

**ext3 Journal File**

```
```
$ ls -al /mnt/flash
total 1063
drwxrwxrwx  15 root root    1024 Aug 25 19:25
drwxr-xr-x   5 root root    4096 Jul 18 19:49 ..
drwxr-xr-x   2 root root    1024 Aug 14 11:27 bin
drwxr-xr-x   2 root root    1024 Aug 14 11:27 boot
drwxr-xr-x   2 root root    1024 Aug 14 11:27 dev
drwxr-xr-x   2 root root    1024 Aug 14 11:27 etc
drwxr-xr-x   2 root root    1024 Aug 14 11:27 home
drwxr-xr-x   1 root root   1048576 Aug 25 19:25 .journal
drwxr-xr-x   2 root root    1024 Aug 14 11:27 lib
drwxr-xr-x   2 root root    12288 Aug 14 11:27 lost+found
drwxr-xr-x   2 root root    1024 Aug 14 11:27 proc
drwxr-xr-x   2 root root    1024 Aug 14 11:27 root
drwxr-xr-x   2 root root    1024 Aug 14 11:27 sbin
drwxr-xr-x   2 root root    1024 Aug 14 11:27 tmp
drwxr-xr-x   2 root root    1024 Aug 14 11:27 usr
drwxr-xr-x   2 root root    1024 Aug 14 11:27 var
```
```

Now that we have created the journal file on our Flash module, it is effectively formatted as an ext3 file system. The next time the system is rebooted or the e2fsck utility is run on the partition containing the newly created ext3 file system, the journal file is automatically made invisible. Its metadata is stored in a reserved inode set aside for this purpose. As long as you can see the . journal file, it is dangerous to modify or delete this file.

It is possible and sometimes advantageous to create the journal file on a different device. For example, if you have more than one physical device on your system, you can place your ext3 journaling file system on the first drive and have the journal file on the second drive. This method works regardless of whether your physical storage is based on Flash or rotational media. To create the journaling file system from an existing ext2 file system with the journal file in a separate partition, invoke tune2fs in the following manner:

```
```
# tune2fs -J device=/dev/sda1 -J /dev/sdb1
```
```