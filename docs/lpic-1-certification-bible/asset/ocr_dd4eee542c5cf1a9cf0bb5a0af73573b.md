**18. How many primary and extended partitions are allowed on a hard disk?**
A. 1
B. 2
C. 3
D. 4

**19. How many primary partitions are allowed on a hard disk?**
A. 1
B. 2
C. 3
D. 4

**20. Before a file system can be examined using fsck it must first be ___________.**

# ## Scenarios

+   1. There was recently a power loss that caused your computer to be shut down improperly. When you rebooted, the `fsck` utility was run automatically. Now the system works, but some of the files that were stored in your home directory are now missing. How would you locate these files?

+   2. There was recently a power loss that caused your computer to be shut down improperly. Now you get errors about a corrupt superblock on the drive. How would you recover from this problem?

# # Lab Exercises

# **Lab 5-1 Creating and using a file system**

In this lab you will create a new partition and file system and configure it to be mounted when the system boots.

+   1. Use `fdisk` to create a new partition.

```
```
# fdisk /dev/hda
The number of cylinders for this disk is set to 2495.
There is nothing wrong with that, but this is larger than
1024,
and could in certain setups cause problems with:
 1) software that runs at boot time (e.g., old versions of
 LILO)
```
```