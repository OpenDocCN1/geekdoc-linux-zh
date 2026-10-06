# Part I: Getting Started in Fedora and RHEL

+   - **Create a partition** — If you have free space, you can add a new partition. **Type n** and you are asked to enter *l* for a logical partition (5 or over) or *p* for a primary partition (1–4). Enter partition number from the available range. Choose the first cylinder number from those available. (The output from `fdisk` earlier will show you cylinders being used under the Start and End columns.)
- Next, enter the cylinder number the partition will end with (or type the specific number of megabytes or kilobytes you want: for example, +50M or +1024K). You created an ext3 partition. Again, this is not permanent until you write the changes.
- **Change the partition type** — Press *t* to choose the type of file system. Enter the partition number of the partition you want to change. Type the number representing the file system you want to use in hexadecimal. (Type *L* at this point to see a list of file types and codes.) Use number 83; use 82 for a Linux swap partition. For a Windows FAT32 file system, you can use the letter b.

+   - **Display the partition table** — Through this process, free to type *p* to display (on the screen) the partition table as it stands.

+   - **Saving and quitting** — If you don't like a change to your partitions, press *q* to exit without saving. Nothing will have changed on your partition table.

Before you write changes, display the partition table and make sure that it is what you want it to. To write your changes to the partition table, press *w*. You are warned about how dangerous it is to change partitions and confirm the change.

An alternative to the `fdisk` command is `sfdisk`. The `sfdisk` command is command-oriented. Use the full command line to list or change partitions. (See the `sfdisk` man page for details.)

# Tips for creating partitions

Changing your partitions to handle multiple operating systems can be very tricky. Part of the reason is that each operating system has its own ideas about how partitioning is handled, and as well different tools to do it. Here are some tips to help you get it right.

+   - If you are creating a dual-boot system that includes Windows, to install the Windows operating system first. Otherwise, the Windows installation may make the Linux partitions inaccessible.
- The `fdisk` man page recommends that you use tools that come with an operating system to create partitions for that operating system. For example, the DOS `fdisk` knows how to create partitions that DOS will be like, and the Fedora or RHEL `fdisk` will happily make Linux partitions. Once your hard disk is set up for boot, however, you should probably not go back to Windows-only partitioning tools. Use Linux `fdisk` or a product made for multiboot systems (such as Partition Magic).