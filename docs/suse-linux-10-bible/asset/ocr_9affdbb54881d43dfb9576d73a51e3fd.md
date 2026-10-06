# 100 Part I SUSE Linux Basics

a directory is permanently associated with that specific filesystem. For example, if you want to store the /var hierarchy on a different disk, you would mount it permanently outside of /mnt.

The mount command -t option enables you to specify the type of filesystem that you are mounting but is unnecessary in many cases the kernel tries to automatically sense the filesystem. If the kernel cannot determine the filesystem type automatically and you are unsure of the type of filesystem that is located on a device, you can use the guefstype utility, which enables the superblock on a specific partition to determine the type of filesystem that it contains. You can then explicitly identify the type of filesystem that a partition contains by using the -t type option when you issue the mount command.

# Mount Options

Depending on the type of filesystem you are using, you can pass mount options that impact the way the filesystem is used. These are functional parameters that change the way that the filesystem works or provide optimizations for specific scenarios.

This section provides an overview of the most significant mount options that are available for the EXT2/EXT3 and ReiserFS filesystems, as well as a discussion of some general mount options that can be useful regardless of the type of filesystem you are using. The online page for the mount command provides complete information about all the general and filesystem-specific options that are supported by the mount command.

# Common EXT2 and EXT3 Mount Options

As discussed in the chapter, the EXT2 and EXT3 filesystems share the same basic data structures and differ only in terms of whether a journal is present (and the journaling is enabled in the superblock). For this reason, they also share a large list of mount options that can be used with either. Of these, the most significant is the sb option, which enables you to use an alternate superblock to use when checking the consistency of the filesystem fsck utility.

As shown in Listings 3-6 and 3-7, a backup superblock are created when EXT2 or EXT3 filesystem is created. A superblock is the cornerstone of a Linux filesystem and provides key information about a filesystem such as the number of free inodes, a pointer to the list of free blocks, and various attributes that specify the configuration of that particular filesystem. The size of a filesystem determines the number of backup superblocks created by the mkfs.ext2 or mkfs.ext3 utilities you created the filesystem.

Backup superblocks are useful when the primary superblock for a filesystem (generally the first 512 bytes of the filesystem) has become corrupted or otherwise damaged. If a filesystem's primary superblock has become corrupted, you must