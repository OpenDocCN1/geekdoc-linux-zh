> **NOTE:** If you keep the GRUB boot loader, you have the option of adding a GRUB password. The password protects your system from having potentially dangerous kernel options sent to the kernel by someone without that password. This password can be different from the root password you are asked to enter later. GRUB and LILO boot loaders are described later in this chapter.

The names shown for each bootable partition will appear on the boot loader screen when the system starts. Change a bootable partition name by clicking it and selecting Edit. To change the location of the boot loader, click “Configure advanced boot loader options” and continue to the next step. If you do not want to install a boot loader (because you don’t want to change the current boot loader), click “Change boot loader” and select “Do not install a boot loader.” (If the defaults are okay, skip the next step.)

**12.** **Configure advanced boot loader.** To choose where to store the boot loader, select one of the following:

+   * **Master Boot Record (MBR)** — This is the preferred place for GRUB. It causes GRUB to control the boot process for all operating systems installed on the hard disk.

+   * **First Sector of Boot Partition** — If another boot loader is being used on your computer, you can have GRUB installed on your Linux partition (first sector). This lets you have the other boot loader refer to your GRUB boot loader to boot Fedora Core.

You can choose to add kernel parameters (which may be needed if your computer can’t detect certain hardware). If some piece of hardware is improperly detected and preventing your computer from booting, you can add a kernel parameter to disable that hardware (for example, add `nousb`, `noacpi`, `nopcmcia`, or `noap`). You can select to use linear mode (which was once required to boot from a partition on the disk that is above cylinder 1024, but is now rarely needed).

> **NOTE:** For more information on GRUB, refer to the section on boot loaders later in this chapter.

**13.** **Configure networking.** At this point, you are asked to configure your networking. This applies only to configuring a local area network. If you will use only dial-up networking, skip this section by clicking Next. If your computer is not yet connected to a LAN, you should skip this section.

Network address information is assigned to your computer in two basic ways: statically (you type it) or dynamically (a DHCP server provides that information from the network at boot time). One Network Device appears for each network card you have installed on your computer. The first Ethernet interface is `eth0`, the second is `eth1`, and so on. Repeat the setup for each card by selecting each card and clicking Edit.

> **CROSS-REFERENCE:** Refer to Chapter 15 for descriptions of IP addresses, netmasks, and other information you need to set up your LAN and to Chapter 16 for information related to domain names.

With the Edit Interface eth0 dialog box displayed, add the following: