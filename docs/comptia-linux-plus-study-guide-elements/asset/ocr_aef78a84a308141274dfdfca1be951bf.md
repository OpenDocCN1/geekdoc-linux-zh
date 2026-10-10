# The Boot Method

Linux installer programs run within Linux itself. This means that in order to install Linux, you must be able to boot a small Linux system, which is provided by the distribution maintainer. This system is useful only for installing Linux and sometimes for doing emergency maintenance. It typically fits on one or two floppy disks or can boot from a bootable CD-ROM.

Modern BIOSs include options for the selection of a boot medium. Typical choices include the floppy disk, CD-ROM drive, PATA hard disk, SATA hard disk, SCSI hard disk, and USB media. In addition, some network cards include BIOSs that enable a computer to boot from files stored on a server. In theory, any of these media can be used to boot a Linux installer.

Although many boot methods are possible, the most common method by far is to use a bootable CD-ROM or DVD-ROM. If you buy a boxed Linux package, it will come with a bootable disc; or you can download an image from the distribution's Web site, burn it, and boot it.

In the past, floppy disks and booting from DOS or Windows were common methods of launching an installer. These methods have fallen by the wayside, but it’s conceivable you’ll still run into them, particularly on old, small, or specialized distributions.

Ultimately, the boot method is unimportant, because the same installation programs run no matter what method you choose. Pick the boot method that’s most convenient for your hardware and the form of installation medium you’ve chosen.

# Installation Media

The installation medium is the physical form of the source of the Linux files. These are the most common choices:

+   **Optical discs** If you buy Linux in a store or from an online retailer, chances are you’ll get an optical disc. In fact, most distributions come on multiple CD-ROMs or a single DVD-ROM. Optical disc installations tend to be quick. Most distribution maintainers offer CD-ROM and DVD-ROM image files that you can burn to CD-Rs yourself. To find optical disc image files, check `http://iso.linuxquestions.org`, `ftp://sunsite.unc.edu/pub/linux/distributions` or your chosen distribution's Web or FTP site.

+   **Network** If you have a fast network connection, many distributions enable you to install via network connections. You must typically download a small image file for a boot CD-ROM, burn that image to disc, and boot it. This boot disc has only a minimal software set, so when you install from the network, you’ll download only what you want to install. The drawback to network installations is that they tend to be slower than installs from CD-ROMs. They require more information from the user, and so they can be more difficult for a new user to get working. They can also fail midway if a network connection goes down or a server stops responding. Network installations may use any of several protocols to transfer files, including FTP, HTTP (Web), SMB (Windows file sharing), and NFS (Unix/Linux file sharing). Precisely which protocols are supported varies from one distribution to another.