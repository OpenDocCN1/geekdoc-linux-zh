![](bbox=[0.12, 0.07, 0.72, 0.42])

*Figure 3-5: The /etc/fstab file contains partition and filesystem settings.*

# ## The mkfs Command

![](bbox=[0.75, 0.49, 0.91, 0.55])

The *mkfs command* is used to build a Linux filesystem on a device, which is usually a hard disk partition. The following table lists some options of the mkfs command and their description.

| Option | Allows You To |
| :--- | :--- |
| -v | Produce verbose output, where the output message will keep changing constantly as the program is processing. |
| -V | Produce verbose output, including all filesystem specific commands that are executed. |
| -t fstype | Specify the type of filesystem to be built. |
| fs-options | Pass filesystem specific options to the filesystem builder. |
| -c | Check the device for bad blocks, before building the filesystem. |
| -l file name | Read the list of bad blocks from a specified file. |

# ### Building New Linux Filesystems Using the mkfs Commands

The *mkfs* commands are used to build a new Linux filesystem. The different *mkfs* commands are given in the following table.