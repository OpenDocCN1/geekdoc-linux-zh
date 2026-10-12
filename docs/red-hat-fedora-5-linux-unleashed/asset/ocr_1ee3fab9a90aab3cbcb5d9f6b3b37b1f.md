come in handy if you need to perform troubleshooting. You can also use the list as a post-installation check-off sheet to see how well Fedora works with your system.

# # Preparing for the Install Process

The basic steps in installing Fedora are to plan, install, and configure. You have to decide how to boot to an install and how much room to devote to Linux. Then perform the install (a sample step-by-step installation is discussed in Chapter 3, “Installing Fedora”) and afterward, configure your system to host new users and specific software services. Much of the initial work is done during the install process because the installer, Anaconda, walks you through partitioning, configuring the desktop, and configuration of any recognized network adapter.

There are many different ways to install Fedora Core, and selecting an installation method might depend on the equipment on hand, existing bandwidth, or equipment limitations. Here are some of the most commonly used installation methods:

+   - **CD-ROM/DVD**—Using a compatible CD-ROM or DVD drive attached to the computer (laptop users with an external CD-ROM drive will need PCMCIA support from a driver disk image included under the first CD-ROM's `images` directory).

+   - **DOS**—By using LOADLIN, you can boot to a Linux install by pointing LOADLIN to use a Fedora installation kernel and ramdisk. Run the DOS batch file, autoboot.bat, found under the dosutils directory on the first Fedora CD-ROM or DVD.

+   - **Network File System (NFS)**—You can install Fedora from a remotely mounted hard drive containing the Fedora software. To perform this installation, you must have an installed and supported network interface card, along with a boot floppy with network support. (You learn how to make boot floppies later in this section of the chapter.)

+   - **File Transfer Protocol (FTP)**—As with an NFS install, installation via FTP requires that the Fedora software be available on a public FTP server. You also need an installed and supported network interface card, along with a boot floppy with network support.

+   - **Hypertext Transport Protocol (HTTP)**—As with the FTP and NFS installs, installation via HTTP requires that the Fedora software be available on an accessible website. You also need an installed and supported network interface card, along with a boot floppy with network support.

+   - **Installation via the Internet**—If you have the bandwidth, it might be possible to install Fedora via the Internet; however, this method might not be as reliable as using a Local Area Network (LAN) because of availability and current use of The Fedora Project or other servers on mirror sites.

+   - **A hard drive partition**—By copying the `.iso` images to a hard drive partition, you can then boot to an install.