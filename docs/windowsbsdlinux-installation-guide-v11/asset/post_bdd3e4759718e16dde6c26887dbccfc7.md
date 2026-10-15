
editor. Readers must note: Typing "quit" means to exit the editor saving the changes and "exit" means to exit the editor without saving any changes. So, we do a "quit", not an "exit".

- 13. Next the disk label which defines the layout of the OpenBSD file systems must be set up. The installation script will invoke an interactive editor allowing you to do this. I create a swap of about a few thousand bytes, and provide the rest to the "a" partition i.e. to the "root" directory on the filesystem. The install program will now label your disk and ask which file systems should be created on which partitions. It will automatically select the 'a' partition to be the root file system. Next it will ask for which disk and partition you want a file system created on.

- 14. After all your file systems have been created, the install program will give you an opportunity to configure the network. Next, you are prompted to configure your network interfaces, default route, IP address of the primary name server, and the host table.

- 15. Once all these done, you will be able to extract the distribution sets onto your system. When installing from a CD-ROM, you will be asked which device holds the distribution sets. This will typically be "cd0". Next you will be asked which partition on the CD-ROM the distribution is to be loaded from. This is normally partition "a".

- 16. Next you will have to identify the file system type that has been used to create the distribution on the CD-ROM, this can be either FFS or ISO CD9660. The OpenBSD CD distribution uses the CD9660 format.

- 17. You will also have to provide the relative path to the directory on the CD which holds the distribution, for the i386 this is "/3.2/386".

- 18. When all the selected distribution sets has been extracted, you will be allowed to select which time zone your system will be using, all the device nodes needed by the installed system will be created for you and the file systems will be unmounted. For this to work properly, it is expected that you have installed at least the "base32", "etc32", and "bsd" distribution sets.

- 19. A message will appear on your screen telling you that OpenBSD 3.2 operating system has been successfully installed on your computer. Type in halt to halt the system and reboot.

- 20. When I reboot for the first time, I get the following prompt on the screen: F1 DOS, F2 BSD, each in one line. I press the F1 functional key to boot into Windows 98 (SE) and check whether everything is working perfectly or not. As it so happens, it does! Then I reboot and this time, I press F2, which logs me into OpenBSD 3.2.

- 21. Depending on the configuration of your computer, you will receive bootup messages on your screen when you boot into OpenBSD for the first time. Though the messages scroll off the screen rather fast for you to read anything productive, you can always read it later by using the "/sbin/dmesg | more" command. Finally, you will arrive at the login prompt. Login using the username/password you set during installation. Check if everything is in place or not and try exploring the new system.

- 22. Readers must note: So, that is all with OpenBSD this time. We still have Linux to install and configure. So, for doing this and more, we proceed to the next chapter. Chapter 6: Installing Red Hat Linux 7.3 (Valhalla).

## 3.5 Installing NetBSD 1.6.1

This Chapter focuses on installing NetBSD 1.6.1 and multi-booting the system so that it can coexist successfully with the already existing Windows operating system on the computer. Like the Windows, FreeBSD and OpenBSD installations, it too focuses on a CD-ROM based installation. Experts may proceed as usual without help, as for the newbies out there, make sure you check out the documentation available on the NetBSD Homepage at http://www.netbsd.org. These and other documentation available on the NetBSD 1.6.1 CD-ROM provides exhaustive and extensive coverage of all aspects related to NetBSD. Make sure you grab as much information as you can from this site before proceeding with this guide.

**Note:** I hereby assume the reader executing this Chapter possesses a sound understanding and knowledge of BSD-style hard disk partitioning and labeling schemes, device naming conventions and so on before proceeding any further. If in case you have no idea at all of what I am talking about or in general of NetBSD, I strongly suggest you to go back to the Chapter covering FreeBSD.

A few significant points to remember: NetBSD labels hard disks similar to OpenBSD with /dev/wd0 for the first hard disk, /dev/wd1 for the second hard disk and so on. NetBSD disklabel allows up to 16 partitions. It can detect and represent all primary partitions that exist on the hard disk. NetBSD disklabel though sees all partitions within an extended partition but it does not list the extended partition container. Readers must note that NetBSD reserves the c: partition which represents the entire hard disk. i: through p: are reserved for partitions belonging to other operating systems other than NetBSD (for example Windows or Linux partitions), with a:, b: and d: – h: available for NetBSD specific partitions.

### Summary of Installation Steps

For a complete step-by-step coverage of NetBSD installation, please consult the documentation available on the NetBSD Project web-site. As in the previous Chapter, here also, I would be mentioning only the significant steps for the installation. Use these steps to install NetBSD on your computer and configure it for "multiple-booting":

- 1. Right now, we have a computer running Microsoft Windows OS. On my PC, it is Windows 98 (SE). I put a bootable NetBSD 1.6.1 CD-ROM in the CD-ROM drive and reboot the system.
- 2. The computer boots, reads the CD-ROM, displays the usual hardware probing messages on the screen and presents you with an installation program. Readers must note: There are several ways to install NetBSD onto a disk. The easiest way, should your computer support it, is to boot off the CD-ROM. Otherwise, you can boot from a 3.5" 1.44MB floppy disk. You should now be ready to install NetBSD.
- 3. The blue-colored NetBSD 1.6.1 Installation Tool is called sysinst. At the very beginning, you receive a "Welcome to sysinst" screen. Select the option "Install NetBSD to hard disk" and press enter.
