with graphical user interfaces and other features to simplify backups. Here are some well-known commercial back up utilities for Linux:

+   BRU: A back up and restore utility from the TOLIS Group, Inc. (www.tolisgroup.com)
+   LONE-TAR: Tape back-up software package from Lone Star Software Corp. (www.cactus.com)
+   Arkeia: Back up and recovery software for heterogeneous networks from Arkeia (www.arkeia.com)
+   Bare Metal Plus: Back up and recovery software from UniTrends (www.unitrends.com)
+   Brightstor ARCserve Backup for Linux: Data-protection technology for Linux systems from Computer Associates (www3.ca.com/solutions/product.asp?id=3370)

# Using the tape archiver — tar

You can use the tar command to archive files to a device, such as a floppy disk or tape. The tar program creates an archive file that can contain other directories and files and (optionally) compress the archive for efficient storage. The archive is then written to a specified device or another file. In fact, many software packages are distributed in the form of a compressed tar file.

The command syntax of the tar program is as follows:

```
tar options destination source
```

Here, options are usually specified by a sequence of single letters, with each letter specifying what tar does. The destination is the device name of the back up device. And source is a list of file or directory names denoting the files to back up.

# Backing up and restoring a single-volume archive

For example, suppose you want to back up the contents of the /etc/X11 directory on a floppy disk. Log in as root, place a disk in the floppy drive, and type the following command:

```
tar zcvf /dev/fd0 /etc/X11
```

The tar program displays a list of filenames as each file copies to the compressed tar archive on the floppy disk. In this case, the options are zcvf,