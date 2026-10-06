# 768 Linux Administration: A Beginner's Guide

A typical invocation of restore is as follows:

```
root@server ~# restore -ivf /dev/st0
```

This will pull the dump file from the device /dev/st0 (the first SCSI tape device), print out each step restore takes, and provide an interactive session for you to decide which files from the dump get restored.

A complete file system is lost, you can re-create the file system using the mkfs.* command and then restore to populate the file system. For example, let's say your External Serial Advanced Technology (SATA) drive (/dev/sdb) fails, and you have a single partition on it (/dev/sdb1) formatted with the ext4 system. After replacing the failed drive with a new drive and partitioning it, we would re-create the file system

```
root@server ~# mkfs.ext4 /dev/sdb1
```

> CAUTION To avoid data loss, make sure you are running any of the mkfs.* commands on the proper device.

Next, we have to mount the file system at the appropriate location. We'll assume this is the /home file system, so we type the following:

```
root@server ~# mount /dev/sdb1 /home
```

Finally, with the dump tape in the SCSI tape drive (/dev/st0), we perform the restoration using the following command:

```
root@server ~# cd /home; restore -rf /dev/st0
```

> TIP If you use gzip to compress your dump, you'll need to decompress it before restore can do anything with it. Simply tell gzip to uncompress the tape device and send its output to the standard out. Standard then be piped to restore, with the -f parameter set to read from standard (stdin). Here's the command:
root@server ~# gzip -d c /dev/st0 | restore -ivf -

# tar

Chapter 3 discussed the use of tar for creating archives of files. What wasn't discussed, however, is the fact that tar was originally meant to create archives of files onto tape (tar = tape archive). Because of Linux's flexible approach of treating devices as the same, we've been using tar as a means to archive and unarchive a group of files into a single disk file. Those tar commands could be rewritten to send the files to the tape instead.