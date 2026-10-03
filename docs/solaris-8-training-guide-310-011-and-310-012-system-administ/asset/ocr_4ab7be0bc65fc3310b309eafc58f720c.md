> NOTE
The swap -l command displays swap space in 512-byte blocks, and the swap -s command displays swap space in 1024-byte blocks. If you add up the blocks from swap -l and convert them to kilobytes, it will be less than used + available (in the swap -s output) because swap -l does not include physical memory in its calculation of swap space.

> NOTE
A crash dump is a disk copy of the physical memory of the computer at the time of a fatal system error. When a fatal operating system error occurs, a message describing the error is printed to the console. The operating system then generates a crash dump by writing the contents of physical memory to a predetermined dump device, which is typically a local disk partition. This crash dump can then be analyzed to determine the cause of the system error. By default, the dump device is configured to be an appropriate swap partition. Therefore, it’s necessary to make sure that your swap area is at least as large as your physical RAM; otherwise, the system will not have enough room to store the crash dump.

Then you can identify what changes to the system might have caused swap space usage to increase.

Keep in mind when using this command that the amount of physical memory available for swap usage changes dynamically as the kernel and user processes lock down and release physical memory.

# Setting Up Swap Space

As described in Chapter 15, “Installing a Server,” swap space is configured during software installation through the installation program. If you use the installation program’s automatic layout of disk slices and do not manually change the size of the swap slice, the Solaris installation program allocates default swap slices, as shown in Table 14.5, based on the amount of physical memory installed in your system.

TABLE 14.5

# DEFAULT SWAP SPACE ALLOCATIONS

| Physical RAM Installed | Default Swap Space Allocated |
|---|---|
| 64–127 | 64MB |
| 128–511 | 128MB |
| Greater than 512 | 256MB |

The software installation program adds entries for swap slices and files in the /etc/vfstab file. These swap areas are activated each time the system is booted by the /sbin/swapadd script.

As system configurations change, more users are added, and new software packages are installed, you might need to add more swap space. There are two methods available for adding more swap to your system:

+   - Create a secondary swap partition.
- Create a swap file in an existing UFS file system.

Creating a secondary swap partition requires additional, unused disk space. You’ll use the format command, as described in Chapter 6, to create a new partition and file system on a disk. After creating the