# Table 10-2 File Attributes in Linux (continued)

| File attribute code letter | Description |
|---|---|
| t | Extra data at the end of this file (that would fill only part of a disk block) will not be merged with similar partial-block data from other files). This feature is called tail-merging. It is not yet supported by ext3, but this attribute will be needed when support is fully implemented. |
| u | When the file is deleted, save its content so it can be undeleted later if needed (this attribute is not yet supported) |
| X | Used by developers working on kernel compression; it cannot be changed using chattr, but it is displayed by lsattr |
| Z | Used by developers working on kernel compression; it cannot be changed using chattr, but it is displayed by lsattr |

For example, to change the attributes of a file named timesheet to be immutable (unchangeable), you can use this command:

```
# chattr +i timesheet
```

To cause all files in a directory and its subdirectories to not have their atime field updated when they are accessed, you can use this command:

```
# chattr -R +A *
```

# Checking File Systems

The fsck utility (usually pronounced FIZZ-check) checks the integrity of your file systems, making certain that each inode is correctly linked to a file, that the blocks of each file can be found, and so forth. The fsck utility can also repair minor file system problems. fsck is a front end that uses checking programs specific to the file system type that you want to check. For example, if you run fsck on a standard ext3 file system, fsck uses the program fsck.ext2 to check the file system (ext2 and ext3 are so similar that the same program is used for both).

In older Linux systems, the fsck program was run automatically after a file system had been mounted a certain number of times (20 was the default). That is no longer the case, and fsck does not check your file systems unless you explicitly start it yourself. It's a good idea to do this every few months on a busy system to make certain no hard disk errors are creeping in.

The challenge is that fsck must be run on a file system that is not mounted. In order to check your root Linux file system, you must start your computer from a removable disk and run fsck. Conversely, if you have multiple data partitions (for example, a separate partition for the /home directory), you might be able to unmount and check that file system when users are unlikely to need access to it.