
You may be surprised to see that the screen says this is a rescue disk. After install you can use your boot CDs or disks to repair the system installation. The available options on this screen are as follows:

- <ENTER> — Starts the installation
- F1 — Installation help
- F3 — Boot methods
- F10 — Copyright information

The F3 function shows the possible boot methods for recovery or installation. The options are as follows:

- **linux** — Start the default installation.
- **ramdisk0** & **ramdisk1** — Start the installation and read the ramdisk from disk 0 or 1. This is used in recovery and loads a file system into a _ramdisk_, which is a piece of memory that looks like a normal disk.
- **floppy0** & **floppy1** — Start the installation and mount the disk in the first or second floppy drive.
- **rescue** — Boot and mount any volume as the root file system. You must give an option to specify the root volume to mount (for example, _rescue root=/dev/hda1_).

## Base system configuration and installation

Once the Linux kernel has loaded you will be presented with the release notes for this version. During the setup you have access to other consoles for information. Table I-4 shows the consoles.

| Console Number | Purpose |
| :--- | :--- |
| Alt-1 | Setup program |
| Alt-2 | Shell prompt |
| Alt-3 | Debug messages |
| Alt-4 | Kernel messages |

The release notes will tell you which kernel the installation was built using, as well as any other important notes about this installation. The Debian installation follows a certain flow, but gives you the option of doing things out of order if needed in certain situations. Figure 1-21 shows the configuration options. The next step is given as the default whenever you are brought back to the menu. In this case, it is asking you to configure your keyboard. Choose the type of keyboard that your system uses.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_75_0.png)

Figure 1-21: Main Menu

### Disk setup

The next step is to partition and set up the data volumes and swap partitions, as shown in Figure 1-22.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_75_1.png)

Figure 1-22: Disk drive selection

Choose the hard disk you want to partition. Depending on your system configuration you may need to heed the warning in the LILO Limitations screen, as shown in Figure 1-23. As discussed previously in this chapter, some systems cannot boot if the Linux kernel is stored beyond the 8GB barrier on a hard disk, or past cylinder number 1023. New versions of LILO allow you to boot from any point on the drive, if your system has a BIOS that is new enough. If your system does not support this, or if you are just unsure, make a /boot partition below the 8GB barrier.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_76_0.png)

Figure 1-23: LILO Limitations screen

Debian uses `cfdisk` to handle partitioning. Set up your partitions as you see fit. For lab purposes it is probably a good idea to split up your volumes so you get experience with more than just single volume systems. A good method for splitting the disk is to put /home, /tmp, and /var on separate partitions. You can also put /usr on a separate partition, but be sure to give it at least a gigabyte of disk space so you have room for software installations later. Don’t forget to make a swap partition!

Once cfdisk is completed, you will be prompted to initialize the swap partition(s), as shown in Figure 1-24.

Any time you initialize a new partition in the Debian install you will be prompted to perform a bad block check. This writes some data to every sector on the disk and then reads it to make sure it is the same. If the read data is different, then the sector is marked as bad. Modern disk controllers can now handle bad blocks automatically, and as this process can take a very long time, you can normally skip this test. But, if the hardware is older or questionable, it does not do any harm to run the test. After the test you can confirm the disk initialization, which will destroy any data. Figure 1-25 shows the bad block test screen.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_77_0.png)

Figure 1-24: Swap selection

![](img/96d9ccd181675a8ae8b6a1146c919d2b_77_1.png)

Figure 1-25: Bad block test

The next several screens walk you through initializing the data volumes. You have the option of disabling some features of the ext2 file system used, if you need to access them from a Linux kernel older than 2.2. Normally this is not needed. Figure 1-26 shows the Pre-2.2 Kernel Compatibility screen.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_78_0.png)

Figure 1-26: Pre-2.2 Kernel Compatibility screen

After initialization you will be prompted to mount this new file system as root ("/"). This screen is shown in Figure 1-27. If this is the correct partition to be root, choose Yes. If not, choose No. Once back at the main menu you can go through and initialize any other partitions you need. Once you have mounted a partition as root, you will be prompted to mount the others in standard locations as you initialize them.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_78_1.png)

Figure 1-27: Mount point selection

## Kernel and module installation

The next phase of the installation is to install the Linux kernel and device driver modules needed by the system. You are prompted for the location from which to install the kernel and modules. This is useful if you need a special kernel or modules not included on the CD-ROM.

Unless you are doing anything special, such as installing from an archive you created yourself that uses nonstandard paths, you should just accept the defaults for the archive path screens. Next, choose the correct modules for your system, as shown in Figure 1-28. It is important to pick the correct drivers so your system can be configured correctly. If you do not load a network driver here, you will have to manually configure the network after the install. You will also be given a chance to add any module options, if needed.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_79_0.png)

Figure 1-28: Module selection (implied context, original text lacks explicit caption but image is present)

## Network configuration

If you loaded a driver for a network card, the next step in the installation is to configure your network. The first option is your computer's hostname. This is the host-name only, not combined with the domain name. For example, if my computer is known as `norbert.the-nashes.net`, the hostname would just be `norbert`. Figure 1-29 shows the hostname configuration screen.

If your network interface will be configured automatically using DHCP or BOOTP, enable that here. If you choose automatic configuration, you may skip to the next section. Figure 1-30 shows the Automatic Network Configuration screen.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_80_0.png)

Figure 1-29: Hostname configuration

![](img/96d9ccd181675a8ae8b6a1146c919d2b_80_1.png)

Figure 1-30: Automatic Network Configuration screen

The next several screens prompt you for basic host information such as IP address, netmask, default gateway, domain name, and DNS servers. Multiple DNS servers should be entered in a list with spaces separating them, as shown in Figure 1-31. For example, you would enter them as follows: `1.2.3.4 1.2.3.5 1.2.3.6`

If you are setting up a lab to practice on, you can use the following network configuration:

- IP address: 192.168.1.1
- Netmask: 255.255.255.0
- Broadcast address: 192.168.1.255
- Network address: 192.168.1.0

The gateway and DNS settings can be left blank.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_81_0.png)

Figure 1-31: Network configuration (implied context, original text lacks explicit caption but image is present)

## Base system installation

The next section installs the base system. These are configuration files, basic system tools, directory structures, and anything else that every Linux system requires. You are prompted for the source location since it may be different from the kernel and module source location if you used third-party install disks to install the kernel and modules. Again, in most cases you can take the defaults for the archive paths. Figure 1-32 shows the base system installation.

The base system configuration begins with the time zone selection screen, as shown in Figure 1-33. You will also be prompted as to whether the system clock is set to UTC.
