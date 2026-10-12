software. This is the default; if you allow GRUB to be installed here, its graphical boot menu will load when you power on or reboot your system, and it will allow you to select which operating system to load. In a server configuration, there may be choices of Linux kernels to load, but there should just be one operating system option!

# **NOTE**

SMP-based systems will start with two boot image choices. The first choice, Red Hat Linux, is set up to support multiple processors. In the event that you encounter a problem with this configuration, Red Hat Linux-up will also be available; it will utilize only one processor, but at least it will get you up and going.

If you are already using another boot loader and prefer it, then you will want to place GRUB on the first sector of the root partition. This will allow your preferred boot loader to run first and then pass control off to GRUB, should you decide to start Linux. Figuring out how to notify your preferred boot loader that there’s a new operating system available is up to you.

This screen also has an option to Force LBA32, which uses linear mode. This applies only to some SCSI drives or drives that are accessed in LBA mode, so unless you know that it applies to you, or are experimenting, leave the box unchecked.

The last option on this advanced configuration screen is a box that allows you to enter kernel parameters to be used at boot time. Most people can ignore this box. If the documentation for a particular feature or device requires you to pass a parameter here, add it; otherwise, leave it blank.

# Setting Up Networking

Now Red Hat is ready to configure your network interface cards (see Figure 2-12).

Each interface card recognized by Linux will be listed in the table at the top of your screen. Ethernet devices are listed as eth0, eth1, eth2, and so on. You can select each interface and click Edit to configure it using DHCP or to set the IP address by hand, as shown.

![](bbox=[0.35, 0.76, 0.65, 0.92])