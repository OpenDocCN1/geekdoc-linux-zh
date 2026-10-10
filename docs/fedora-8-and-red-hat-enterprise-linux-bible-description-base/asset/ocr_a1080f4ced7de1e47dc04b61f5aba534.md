- **Saving and quitting** — If you don't like a change you make to your partitions, press q to exit without saving. Nothing will have changed on your partition table. Before you write your changes, display the partition table again and make sure that it is what you want it to be. To write your changes to the partition table, press w. You are warned about how dangerous it is to change partitions and asked to confirm the change.

An alternative to the fdisk command is sfdisk. The sfdisk command is command line-oriented. Type the full command line to list or change partitions. (See the sfdisk man page for details.)

# ## Tips for creating partitions

Changing your disk partitions to handle multiple operating systems can be very tricky. Part of the reason is that each different operating system has its own ideas about how partitioning information should be handled, as well as different tools for doing it. Here are some tips to help you get it right.

+   - If you are creating a dual-boot system, particularly for Windows ME or Windows XP, try to install the Windows operating system first. Otherwise, the Windows installation may make the Linux partitions inaccessible.
+   - The fdisk man page recommends that you use partitioning tools that come with an operating system to create partitions for that operating system. For example, the DOS fdisk knows how to create partitions that DOS will like, and the Fedora or RHEL fdisk will happily make you Linux partitions. Once your hard disk is set up for dual boot, however, you should probably not go back to Windows-only partitioning tools. Use Linux fdisk or a product made for multiboot systems (such as Partition Magic).
+   - You can have up to 63 partitions on an IDE hard disk. A SCSI hard disk can have up to 15 partitions. You probably won't need nearly that many partitions.

If you are using Fedora or RHEL as a desktop system, you probably don't need a lot of different partitions within your Linux system. There are, however, some very good reasons for having multiple partitions for Linux systems that are shared by a lot of users or are public Web servers or file servers. Multiple partitions within Fedora or RHEL offer these advantages:

+   - **Protection from attacks** — Denial-of-service attacks sometimes take action that tries to fill up your hard disk. If public areas, such as /var, are on separate partitions, a successful attack can fill up a partition without shutting down the whole computer. Because /var is the default location for Web and FTP servers, and therefore might hold a lot of data, often entire hard disks are assigned to the /var file system alone.
+   - **Protection from corrupted file systems** — If you have only one file system (/), corruption of that file system can cause the whole Fedora or RHEL system to be damaged. Corruption of a smaller partition can be easier to correct and can often allow the computer to stay in service while the corruption is fixed.