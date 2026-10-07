-L—This option gives the volume label, which is useful if you need to be reminded what the filesystem is used for; it also provides flexibility in identifying volumes in /etc/fstab.
-S—This option is a last-ditch effort for recovering a mung filesystem; it writes only the superblock and descriptors, leaving the information in the inodes unchanged. Always run fsck after using this option.

As you can see, mk2fs offers a few options to make more space available for the regular users. But that space always comes from the superuser's space for recovering damaged files. The default settings accommodate most users, so think carefully before using one of these options. Hard disks are getting less expensive all the time, so adding another might be a better solution.

Using mk2fs.ext3
to make a new ext3 filesystem, use the mk2fs command with the -j or -J option, or call the command as mk2fs.ext3 (There is no mk3fs command.) Use the tune2fs command on an existing ext2 filesystem to add journaling. (You learn how to convert an existing ext2 filesystem into an ext3 filesystem in this chapter.)

# tune2fs /dev/hdxn -j
Some arguments you can use with this command include

+   -j—This option adds an ext3 journal to the new filesystem using the default values. Note that you must be using a kernel that has ext3 support to actually make use of the journal.
-J journal-options—This option overrides the default ext3 journal parameters so that you can choose the options using the -sign=
size=journal-size—This creates a journal of journal-size megabytes. With a minimum size of 1,024 blocks, it can't be more than 102,400 blocks. There must be enough free space in the filesystem to create a journal of that size.
-device=journal—This option associates the filesystem with a journal not contained within the filesystem (one must have already been created with the command mk2fs -O journal_device journal_name); in other words, the journal and the data files don't have to be on the same device.

> NOTE
The latter two options in the arguments list are mutually exclusive.

To select the ext3 journaling mode, you must add the appropriate entry in /etc/fstab.