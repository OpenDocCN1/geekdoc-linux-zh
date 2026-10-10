Next, enter the cylinder number the partition will end with (or type the specific number of megabytes or kilobytes you want: for example, +50M or +1024K). You just created an ext3 Linux partition. Again, this change isn’t permanent until you write the changes.

+   *   **Change the partition type** — Press **t** to choose the type of file system. Enter the partition number of the partition number you want to change. Type the number representing the file system type you want to use in hexadecimal code. (Type **L** at this point to see a list of file system types and codes.) For a Linux file system, use the number 83; use 82 for a Linux swap partition. For a Windows FAT32 file system, you can use the letter b.
+       *   **Display the partition table** — Throughout this process, feel free to type **p** to display (print on the screen) the partition table as it now stands.
+       *   **Saving and quitting** — If you don’t like a change you make to your partitions, press **q** to exit without saving. Nothing will have changed on your partition table.

Before you write your changes, display the partition table again and make sure that it is what you want it to be. To write your changes to the partition table, press **w**. You are warned about how dangerous it is to change partitions and asked to confirm the change.

An alternative to the `fdisk` command is `sfdisk`. The `sfdisk` command is command line–oriented. Type the full command line to list or change partitions. (See the `sfdisk` man page for details. Note that this command has some limitations in that it was not designed for GUID partition tables or large partitions.)

# Tips for creating partitions

Changing your disk partitions to handle multiple operating systems can be very tricky, in part because each operating system has its own ideas about how partitioning information should be handled, as well as different tools for doing it. Here are some tips to help you get it right.

+   *   If you are creating a dual-boot system that includes Windows, try to install the Windows operating system first. Otherwise, the Windows installation may make the Linux partitions inaccessible.
+   *   The `fdisk` man page recommends that you use partitioning tools that come with an operating system to create partitions for that operating system. For example, the DOS `fdisk` knows how to create partitions that DOS will like, and the Fedora `fdisk` will happily make your Linux partitions. On your hard disk is set up for dual boot, however, you should probably not go back to Windows-only partitioning tools. Use Linux `fdisk` or a product made for multiboot systems (such as Partition Magic).
+   *   You can have up to 63 partitions on an IDE hard disk. A SCSI hard disk can have up to 15 partitions. You probably won’t need nearly that many partitions.

If you are using Fedora as a desktop system, you probably don’t need a lot of different partitions within your Linux system. There are, however, some very good reasons for having