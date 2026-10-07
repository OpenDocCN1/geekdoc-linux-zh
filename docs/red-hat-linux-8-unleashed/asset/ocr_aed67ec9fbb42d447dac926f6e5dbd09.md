File recovery isn’t something to be attempted without preparation and practice because both will improve your chances of recovering more of the data. The Ext2fs Undeletion mini-HOWTO (http://www.tldp.org/HOWTO/mini/Ext2fs-Undeletion.html)has been written to detail the process. It requires some practice before you would be ready to use it in the real world.

> If you want to experiment with learning to restore files, use the information in the Examples section of Chapter 10 to create a loopback filesystem to experiment with. Using that, you can safely delete and undelete files without taking a chance on damaging your system by inadvertently changing critical files or deleting directories.

# Reformatting with the -S Option When Experiencing Unrecoverable Filesystem Errors

In attempting to recover data from a damaged disk with filesystem errors that can’t be fixed with fsck, you run the mkefs command with the -S option like this (if you are having trouble with the ext2 partition on /dev/sda1)

```
# mkefs -S /dev/sda1
```

The -S argument writes new superblock information, but doesn’t write new nodes; this might make the missing data salvageable, or it might not depend on the damage. You must run e2fsck on the unmounted partition after using the mkefs command in this manner.

Because a directory is a file as well, the same techniques for file recovery can be used to recover directory entries. The Ext2fs Undeletion of Directory Structures mini-HOWTO (http://www.tldp.org/HOWTO/mini/Ext2fs-Undeletion-Dir-Struct/index.html) is written as a companion to the Ext2fs Undeletion mini-HOWTO—both of which should be on everyone’s reading list if you want to successfully delete any files. The manual technique described in the HOWTOs is too long and complex to be covered in this book.

# Undeleting Using mc

The Midnight Commander can use of a virtual filesystem and includes an undelete filesystem that can be used on ext2/3 partitions. The mc utility is an interface to the ext2fs library, and the virtual filesystem handles for the nitty-gritty details of the filesystem that the previous paragraph alluded to. With any simplified solution to complex issues, mc must make some assumptions for you that might result in less data recovered than if you use the manual method. For that reason, using mc for recovering deleted files is not a standard method.