+   Automatically partition — With this selection, all Linux partitions on all hard disks are erased and used for the installation. The installation process automatically handles the partitioning. (It does give you a chance to review your partitioning, however.)

+   Manually partition with Disk Druid — With this selection, the Disk Druid utility is run to let you partition your hard disk.

Click Next to continue.

+   Choose partitioning. If you selected to have the installer automatically partition for you, you can choose from the following options:

> NOTE: If you selected to use Disk Druid for partitioning, refer to the section on partitioning your hard disk later in this chapter for details on using those tools.

+   Remove all Linux partitions on this system — Windows and other non-Linux partitions remain intact with this selection.

+   Remove all partitions on this system — This erases the entire hard disk.

+   Keep all partitions and use existing free space — This only works if you have enough free space on your hard disk that is not currently assigned to any partition.

If you have multiple hard disks, you can select which of those disks should be used for your Fedora Core installation. Turn the Review check box on to see how Linux is choosing to partition your hard disk. Click Next to continue.

After reviewing the Partitions screen, you can change any of the partitions you choose, providing you have at least one root (/) partition that can hold the entire installation and one swap partition. A small /boot partition (about 100MB) is also recommended.

The swap partition is often set to twice the size of the amount of RAM on your computer (for example, for 128MB RAM you could use 256MB of swap). Linux uses swap space when active processes have filled up your system’s RAM. At that point, an inactive process is moved to swap space. You get a performance hit when the inactive process is moved to swap and another hit when the process restarts (moves back to RAM). For example, you might notice a delay on a busy system when you reopen a Window that has been minimized for a long time.

The reason you need to have enough swap space is that when RAM and swap fill up, no other processes can start until something closes. Bottom line: add RAM to get better performance; add swap space if processes are failing to start. Red Hat suggests a minimum of 32MB and maximum of 2GB of swap space.

Click the Next button (and select OK to accept any changes) to continue.

+   Configure boot loader. All bootable partitions and default boot loader options are displayed. By default, the install process will use the GRUB boot loader, install the boot loader in the master boot record of the computer, and choose Fedora Core as your default operating system to boot.