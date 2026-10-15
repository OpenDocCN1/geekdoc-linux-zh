
+   10. Writing and administering malware-fighting programs

+   11. Integrating the system with cloud storage and computing, or implementing a full UNIX, Apache, MySQL, Python (UAMP) stack

To extend some of the system administration topics covered in this book so that they are reflective of modern UNIX systems, we provide two additional chapters as follows: Chapter 24 on ZFS details how a modern UNIX file system can be utilized to efficiently manage system and user files; Chapter 25 on virtualization methodologies shows PC-BSD Jails, Solaris 11 Zones, and VirtualBox virtual machines (VMs). These two additional chapters show how to implement further levels of system security, as well as to expedite the system administration techniques and methods shown in this chapter.

## 23.2 DOING A FRESH INSTALL FROM ISO-CREATED DVD MEDIA AND PRELIMINARY SYSTEM CONFIGURATION

This section assumes that you have already obtained and burned to disk the ISO file of the DVD media for PC-BSD or Solaris, and that your system is a 64-bit, X86 architecture computer with at least one entire hard disk that you are willing to install the UNIX system on. If you have not obtained a DVD or do not have a 64-bit computer, you should follow the online documentation at www.pcbsd.org or www.oracle.com to get the ISO image of the DVD media, or use an earlier release of either of the software systems that are designed for 32-bit machines. "Obtaining the DVD media" means downloading an ISO file for the release of the software you want to use, and then burning that ISO image to a DVD. We do not give instructions here for that process. Be aware that some of the systems administration tasks illustrated for PC-BSD and Solaris are done in a different way in earlier releases of the software!

This section also assumes that you will not be permanently running the "live" version of either of the UNIX systems from persistent or nonpersistent media, like a USB drive or CD/DVD.

A few words about ISO files and media at this point would be instructive. We have chosen to do our installs in this chapter from DVDs created by burning ISO files downloaded from both www.pcbsd.org and www.oracle.com. That is because the vast majority of desktop, server, and laptop computers being sold today, and that have been sold for the past 15 years, come equipped with a DVD drive as standard. This may change in the future, where the predominant form of removable media hardware may become something else, such as USB 3.0 thumbdrives, for example. It is presently possible to use a downloaded ISO file for the installation of the operating systems placed on a USB external medium, but we chose not to use this method. If you want to use this method, you can if it fits your use case, hardware requirements, and data storage model, and most importantly, is convenient and easy for you.

Also, as shown in Chapter 25, it is possible to use the downloaded ISO file without burning it to DVD media to install the operating system into a VM environment. And you can use the downloaded ISO file in this chapter as well to directly install the operating system

without using DVD media. Again, the method of installation you choose is your personal preference, based upon what works best for you on your particular computer hardware, what your use case is, and how you store your data.

If you want to install either PC-BSD or Solaris in a virtual environment, so that it runs simultaneously with some other operating system on your computer's hardware, we give specific instructions on how to do this in Chapter 25, “Virtualization Methodologies.” In Chapter 25, Section 4.5, we give the specifics of installing PC-BSD and Solaris as “guest” operating systems on Ubuntu Linux and Windows hosts, using VirtualBox.

### 23.2.1 Preinstallation Considerations

Each of the UNIX systems we will show an installation of, PC-BSD and Solaris, have minimum hardware and driver requirements that can be determined before you begin an install. These hardware requirements are listed in the documentation online for each of the systems. Once you have determined that your computer system hardware meets or exceeds those minimum requirements, the following questions suggest some other important considerations you can make over and above the default installation choices before proceeding with the installation:

-   1. How many hard disks does your computer have, and how are you planning to use the Zettabyte File System (ZFS) on those disks? For example, if you only have one hard disk drive, that will be the bootable system disk and the file system data disk. If you have two or more hard disk drives, will you mirror the bootable system disk and all other data from the main drive on the other drives? In PC-BSD, mirroring on two or more disks can be accomplished at system installation.

Most importantly, if your hardware can support multiple hard drives, we recommend that you install the operating system on one hard drive (preferably a solid state drive [SSD]), and all of the user data on another single disk or an array of hard disk drives. That way, if the operating system and its bootable hard disk drive become corrupted or unusable for some reason, your user data is on a separate hard disk or array of hard disks. As shown in Section 23.7.3.1, which deals with the most practical methods of operating system upgrades, you can then simply replace the operating system hard disk and reinstall either the current version of the operating system or a newer version. You can then use the ZFS facilities to reattach the data hard drives to the new operating system and its hard disk drive. This is highly valuable not only for desktop computers but also server-class systems as well. The way that your data is deployed on your disks is a critical design consideration when you are building your system, and is highly dependent on the particular use case that is guiding it.

-   2. Do you have a wireless connection to a LAN and the Internet? A wired connection through DHCP is automatically done in both systems during the default install.

-   3. How many users are you going to initially establish at installation, and what are their user profiles going to be? For example, what users will have administrative privileges other than yourself, and what kind of security will each profile have? Also, what user
