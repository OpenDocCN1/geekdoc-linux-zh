+   - Set the time zone
+   - Set the root password and add user accounts
+   - Configure password authentication

The following sections guide you through each of these configuration steps.

# Install LILO

LILO stands for Linux Loader — a program that resides on your hard disk and starts Red Hat Linux from the hard disk. If you have Windows 95/98 on your hard disk, you can configure LILO to load these operating systems as well. LILO is also known as the bootloader.

The Red Hat installation program displays the LILO Configuration screen (see Figure 3-1), which asks you where you want to install LILO. For systems with Windows 95/98 and Red Hat Linux residing on a single hard disk, Red Hat recommends installing LILO on the master boot record.

![](bbox=[0.22, 0.5, 0.77, 0.81])

Figure 3-1
The LILO Configuration screen enables you to specify where to install LILO and whether to create a boot disk.

The first button on this screen asks if you want to create a boot disk. This is different from the installation boot disk; you can use this disk to boot your Linux system if the Linux kernel on the hard disk is damaged or if LILO — the Linux