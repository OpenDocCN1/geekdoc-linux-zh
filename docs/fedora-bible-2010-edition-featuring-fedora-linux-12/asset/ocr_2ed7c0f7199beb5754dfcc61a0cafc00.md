when active processes have filled up your system’s RAM. At that point, an inactive process is moved to swap space. You get a performance hit when the inactive process is moved to swap and another hit when the process restarts (moves back to RAM). For example, you might notice a delay on a busy system when you open a window that has been minimized for a long time.

The reason you need to have enough swap space is that when RAM and swap fill up, no other processes can start until something closes. Bottom line: add RAM to get better performance; add swap space if processes are failing to start. The Fedora Project suggests a minimum of 32MB and maximum of 2GB plus the amount of RAM of swap space. For example, if you have 4GB of RAM, make the swap size 6GB.

Click the Next button (review partitions that are being reformatted and select Write changes to disk *if* the changes are acceptable) to continue.

+   10. **Configure boot loader.** All bootable partitions and default boot loader options that are detected are displayed. By default, the install process will use the GRUB boot loader, install the boot loader in the master boot record of the computer, and choose Fedora as your default operating system to boot.

> **NOTE:** If you keep the GRUB boot loader, you have the option of adding a GRUB password. The password protects your system from having potentially dangerous kernel options sent to the kernel by someone without that password. This password can and should be different from the root password you are asked to enter later. The GRUB boot loader is described later in this chapter.

The names shown for each bootable partition will appear on the boot loader screen when the system starts. Change a bootable partition name by clicking it and selecting Edit. To change the location of the boot loader, click “Change device” and select where to install the boot loader. If you do not want to install a boot loader (because you don’t want to change the current boot loader), click “No boot loader will be installed.” (If the defaults are okay, skip the next step.)

+   11. **Change device.** If you selected to configure advanced boot loader options, you can now choose where to store the boot loader. Select one of the following:

+   *   **Master Boot Record (MBR)** — This is the preferred place for GRUB. It causes GRUB to control the boot process for all operating systems installed on the hard disk.
+   *   **First Sector of Boot Partition** — If another boot loader is being used on your computer, you can have GRUB installed on your Linux partition (first sector). This lets you have the other boot loader refer to your GRUB boot loader to boot Fedora. If you take this option, you will need to modify your other boot loader to point to your Fedora partition (or you won’t be able to boot the Fedora you are installing).

+   12. **Install classes.** For a new install, the installer automatically selects a set of basic software to install. In addition to *that* set, you can choose one or more of the following groups of software, referred to as *tasks*. For each of these installation tasks, you have the opportunity to install a set of preset packages or customize that set: