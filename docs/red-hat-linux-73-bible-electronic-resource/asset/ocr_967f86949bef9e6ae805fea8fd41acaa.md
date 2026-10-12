+   *   Server — A Server installs the software packages that you would typically need for a Linux server (for example, Web server, file server, and so on). This type of install does not install the X Window System by default (so you need to either add X when you select packages or you’d better know how to use the shell). This type of install also erases all hard disks and assigns all disks to Linux by default.

> CAUTION: This is a big one. In case you didn’t catch the previous paragraph, Server installs erase the whole hard disk by default! If you have an existing Windows partition that you want to keep, change the Automatic Partitioning option that appears next to either only remove the Linux Partitions or to only use existing free space.

+   *   Laptop — A Laptop install is similar to a Workstation install. The primary differences between the two are that the Laptop install includes PCMCIA support, IRDA (infrared) utilities, and wireless tools.
+   *   Custom System — You are given the choice of configuring your own partitions and selecting your own software packages.

> NOTE: If you are at all computer literate, I recommend choosing Custom System install. It will give you a better feel for what is going on with your installation.

At this point, the procedure will continue through a Custom System installation. If you are doing a Workstation installation, you can indicate that you want to do automatic partitioning, then skip to the Configure Networking step. If you select Server installation, you can indicate that you want to erase the entire disk, then skip to the Configure Networking step. For Custom System installs, continue on.

8.  Choose your partitioning strategy. You have three choices related to how your disk is partitioned for Red Hat Linux installation:

+   *   Have the installer automatically partition for you — With this selection, all Linux partitions on all hard disks are erased and used for the installation. The installation process automatically handles the partitioning.
+   *   Manually Partition with Disk Druid — With this selection, the Disk Druid utility is run to let you partition your hard disk. This interface is more intuitive than fdisk’s.
+   *   Manually Partition with fdisk [experts only] — With this selection, the fdisk utility is run to let you partition your hard disk. This interface is more appropriate for seasoned Linux/UNIX users.

Click Next to continue.

9.  Choose partitioning. If you selected to have the installer automatically partition for you, you can choose from the following options:

> NOTE: If you selected to use Disk Druid or fdisk for partitioning, refer to the section on partitioning your hard disk later in this chapter for details on using those tools.