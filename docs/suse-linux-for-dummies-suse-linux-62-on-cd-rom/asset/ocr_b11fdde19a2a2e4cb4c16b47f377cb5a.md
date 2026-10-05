# Chapter 13: File System Management

When you are finished with configuring mount points for new partitions, press the Esc key to get back to the main YaST menu and select Exit YaST.

# Reforming Corrupted File Systems

File systems can be corrupted by anything from a driver error to a hardware-crash. The fsck utility can check the file system's consistency, report errors, and make some repairs. Normally, the fsck program is called automatically when the system boots. Therefore, if your system crashes, fsck runs on all file systems that were mounted when the system crashed.

The repairs that fsck can perform are limited to structural repairs of the file system and its data components. fsck can't help if you have corrupted data in a structurally intact file. Also remember that, except for the root file system, fsck runs only on unmounted file systems. You must make sure that the system is in single-user mode to use fsck on the root file system.

Here's the syntax for the fsck command:

```
fsck (options) filesystem
```

where filesystem names the block special file where the file system resides. If filesystem is omitted, the fsck utility checks all file systems listed in the /etc/fstab configuration file. If the fsck utility finds any errors, it prompts you for input on what to do about them. For the most part, you simply agree with whatever the program suggests.

The fsck command has the following options:

+   - p Preen the file system. Perform automatic repairs that don't change the contents of files.
- n Answer no to all prompts and only list problems; don't repair them.
- y Answer yes to all prompts and repair damage regardless of severe.
- f Force a file system check.

A lot of people run the fsck command with the -y option. If you run fsck with the -p option, some steps are automatically performed for you. Lost files are placed in the log+found directory, zero-length files are deleted, and missing blocks are placed back on the list of free blocks, which are blocks still available for filling with data, among other things.