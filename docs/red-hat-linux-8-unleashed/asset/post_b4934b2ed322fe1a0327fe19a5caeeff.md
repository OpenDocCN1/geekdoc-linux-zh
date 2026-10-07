
Remember: Red Hat Linux requires at least a root (/) and swap partition. The swap partition should be at least twice as large as the amount of installed memory in order to assure system performance if you run a lot of programs or host many users. Figure 3.10 shows a simple, completed partitioning scheme with a separate /home partition on a server using a 5GB hard drive.

![](img/446debe023486a07fde575245cf7a3ff_106_0.png)

**FIGURE 3.10** Review the partitioning scheme for your hard drive.

Take a moment to review your partitioning scheme. If you are not satisfied with the partitioning, you can make changes by selecting a partition and then using the Edit button to change the partition's information (such as mount point or type of filesystem). Use the Delete button to delete the partition entry and free up partition space. You can then use the New button again to create partitions in the space that is now free. When satisfied, use the OK button to continue the installation.

## Choosing, Configuring, and Installing the Boot Loader

After you choose OK to accept the partitioning scheme, a screen appears asking you to select a boot loader for booting Red Hat Linux (see Figure 3.11). This screen also enables you to choose not to use a boot loader (booting from floppy, a commercial utility, a DOS partition, or over a network). Review “Choosing a Boot Loader,” shown previously in this chapter, for more information on making this choice.

Select the desired boot loader (we will use GRUB for our install here), and then use the OK button.

You're asked if you'd like to add any kernel arguments before booting Linux (as shown in Figure 3.12). Kernel arguments are used to enable or disable various features of Linux at boot time. If you install the source to Red Hat Linux kernel, you'll find documentation about the more than 200 kernel arguments in the file `kernel-parameters.txt` under the `/usr/src/linux-2.4/Documentation` directory.

 CHAPTER 3 Installing Red Hat Linux

Red Hat Linux (C) 2002 Red Hat, Inc.

![](img/446debe023486a07fde575245cf7a3ff_107_0.png)

FIGURE 3.11 Select whether you want to use a boot loader, and if so, which type.

Red Hat Linux (C) 2002 Red Hat, Inc.

![](img/446debe023486a07fde575245cf7a3ff_107_1.png)

FIGURE 3.12 Enter any desired kernel arguments to be passed by the boot loader.

Enter the arguments in the dialog box or use the OK button to continue. Note that if the Red Hat installer detects a CDRW (Read/Write) drive, you might see a Linux kernel argument such as hdc=ide-scsi implemented to support the use of the drive under SCSI emulation. This emulation is used to support CD write and erase operation while using Linux. See Chapter 4, "Post-Installation Configuration," to see how to install, and use CDRW drives with Red Hat.

> NOTE
> You can also use the hdc-ide-scsi kernel argument later after installing Red Hat Linux by editing the LILO or GRUB configuration files. See Chapter 24 for details. Editing these files can be dangerous, though, be sure to read all the information (and warnings) in Chapter 24.

Highlight the OK button and press Enter to see the screen shown in 3.13. Here, you're asked if you'd like to use a preboot password. If you choose to use this option, you will need to enter a password at the GRUB boot screen (see the section “Login and Shutdown” at the end of this chapter for information on graphical logins). Carefully note the password! It does not have to be the same password used to log in Red Hat, but if you password boot protecting your computer's BIOS and use a boot loader password here, you will subsequently need to enter three passwords (BIOS, boot loader, and login) to access Red Hat Linux. Type a password of at least eight characters twice (once on each line); then highlight the OK button and press Enter.

![](img/446debe023486a07fde575245cf7a3ff_108_0.png)

**Figure 3.13** You may enter a boot loader password.

You can graphically edit the loader's configuration file, as shown in Figure 3.14, to add or remove features of booting other operating systems. The default (and only) operating system to boot should be Red Hat Linux if you wiped your internal hard drive, however, you can configure a dual-boot system during the install or later when using Red Hat Linux to support booting another installed operating system residing on a different partition. Use the OK button to configure and install the boot loader.

You're asked where you want to install the boot loader, as shown in Figure 3.15. GRUB and LILO are typically installed in the MBR of the first IDE hard drive in a PC. However, the boot loader can also be installed in the first sector of the Linux boot partition, or even not installed on the hard drive (in which case, you'll need to create a boot floppy during the install; see “Create a Boot Disk,” later in this chapter). Note that you can also backtrack through the install process to change any settings. Select a location and use the OK button to continue.

 CHAPTER 3 Installing Red Hat Linux

![](img/446debe023486a07fde575245cf7a3ff_109_0.png)

FIGURE 3.14 Configure and select which operating system to be booted by.

## Boot Loader

![](img/446debe023486a07fde575245cf7a3ff_109_1.png)

FIGURE 3.15 Select where you'd like to install the boot loader.

## Network Configuration

If you have an network adapter, you are asked for network details, as shown in Figure 3.16. Red Hat Linux can be set to automatically configure networking upon booting. Note that you can also configure networking following installation using Red Hat's graphical tool (see Chapter 13).

Red Hat Linux (C) 2002 Red Hat, Inc.

![](img/446debe023486a07fde575245cf7a3ff_110_0.png)

FIGURE 3.16 Select or enter networking information.

> NOTE
> Red Hat Linux finds more than one interface installed on your computer, you might be asked to configure a second device. This might be the case, for you are installing Red Hat on a computer that will serve as a gateway or firewall. If you configure more than one interface, the device named eth0 will be the first interface when you start Red Hat. After making your selection, press Enter.

![](img/446debe023486a07fde575245cf7a3ff_110_1.png)

FIGURE 3.17 Give your new Red Linux system a hostname.

## Firewall and Security Configuration

Figure 3.18 shows the Red Hat installer Firewall Configuration dialog, which offers an opportunity to set default security policies for the new server. Protecting your system using a firewall is especially important if your server is connected to a network (although it is best to first install Red Hat, set security policies, and then connect to a network). These settings in this installation screen determine how remote computers or users will be able to access your server. You can change these policies after finishing the install and logging in to Red Hat.

![](img/446debe023486a07fde575245cf7a3ff_111_0.png)

**Figure 3.18** Select a desired security level.

If you have a general idea of how to protect your computer, use the dialog box shown in Figure 3.18 to set a security level.

- Choosing No Firewall setting isn't recommended; use this setting only if Red Hat will be used as a non-networked workstation.
- The Medium setting might be acceptable for use on an intranet protected by a firewall and served by an Internet gateway.
- Definitely use a High security level if you plan to have your server attached directly to the Internet to install.

> NOTE
> Note that you can also manually configure security settings after installing Red Hat Linux using the text-based lokkit command, redhat-config-securitylevel client, or graphical gnome-lokkit client. See Chapter 13 for details on how to protect your Red Hat system using these clients and various security settings.

Use the Customize button to configure allowable services, as shown in Figure 3.19.
