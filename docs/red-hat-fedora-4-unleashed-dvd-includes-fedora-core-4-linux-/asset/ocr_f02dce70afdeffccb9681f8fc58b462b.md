Here are some of the most commonly used installation methods:

+   - **CD-ROM/DVD**—Using a compatible CD-ROM or DVD drive attached to the computer (laptop users with an external CD-ROM drive will need PCMCIA support from a driver disk image included under the first CD-ROM’s *images* directory).

+   - **DOS**—By using LOADLIN, you can boot to a Linux install by pointing LOADLIN to use a Fedora installation kernel and ramdisk. Run the DOS batch file, `autoboot.bat`, found under the `dosutils` directory on the first Fedora CD-ROM or DVD.

+   - **Network File System (NFS)**—You can install Fedora from a remotely mounted hard drive containing the Fedora Core software. To do this installation, you need to have an installed and supported network interface card, along with a boot floppy with network support. (You learn how to make boot floppies later in this section of the chapter.)

+   - **File Transfer Protocol (FTP)**—As with an NFS install, installation via FTP requires that the Fedora software be available on a public FTP server. You also need an installed and supported network interface card, along with a boot floppy with network support.

+   - **Hypertext Transport Protocol (HTTP)**—As with the FTP and NFS installs, installation via HTTP requires that the Fedora software be available on an accessible website. You also need an installed and supported network interface card, along with a boot floppy with network support.

+   - **Installation via the Internet**—If you have the bandwidth, it may also be possible to install Fedora via the Internet; however, this method might not be as reliable as using a Local Area Network (LAN) because of availability and current use of Fedora Project or other servers on mirror sites.

+   - **A hard drive partition**—By copying the `.iso` images to a hard drive partition, you can then boot to an install.

+   - **Preinstalled media**—It is also possible to install Linux on another hard drive and then transfer the hard drive to your computer. This is handy, especially if your site uses removable hard drives or other media.

> **NOTE**
> 
> More esoteric installations may be possible. Some Linux distributions support booting to an install via a Zip drive, via the Parallel Port Internet Protocol (PLIP), and even a null-modem cable supporting the Serial Line Internet Protocol (SLIP) or Point-to-Point Protocol (PPP). Browse to http://www.tldp.org and read Gilles Lamiral’s PLIP install HOWTO to see how to install Red Hat 7.0 using your PC’s parallel port. Once installed, you can then try to upgrade to Fedora.

After booting and choosing to use either a graphical or text-based install interface, the installation procedure is nearly the same for each type of install. Chapter 3 walks you through a typical CD/DVD-based installation.