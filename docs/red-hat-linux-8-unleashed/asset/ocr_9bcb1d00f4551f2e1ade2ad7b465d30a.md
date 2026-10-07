# CHAPTER 3 Installing Red Hat Linux

To use this installation method, your computer must support booting from CD-ROM, and the CD-ROM drive must be recognizable by the Linux kernel. You can verify this by checking your BIOS and then booting your PC.

In the past, booting the Red Hat installer using CD-ROM drives required a kernel patch, but this should no longer be a problem; see Table 3.1 in this chapter, which lists a driver image used to support older drives.

# Booting to an Install from DOS

As previously mentioned, you can use a DOS utility as LOADLIN (or BOOTLIN) to either directly boot an install from the CD-ROM or to load the Red Hat Linux install kernel.

See the desutils directory on the first Red Hat Linux CD included with this book, and read the README file under the dentists directory for an overview of the DOS utilities. The directory contains a one-line DOS batch file (.bat file) that can help boot to an install:

```
loadlin autoboot\ vmlinuz initrd=**autoboot\initrd.img
```

In this example, the LOADLIN command will boot the Red Hat Linux kernel residing under the desutils/autoboot directory, and then load the installation software to launch an install.

# Making an Installation Boot Diskette

Your Red Hat Linux installation can be started using a boot floppy. A boot floppy can be used to boot the Red Hat CD-ROM on older CD-ROM drives. A boot floppy can also be used to start a Red Hat installer over a network when the PC does not have a CD-ROM drive but has a network interface card (NIC). Boot floppies are created from floppy images (.img files). These images are contained in the images directory on the first Red Hat CD-ROM.

Red Hat provides a number of images, as listed in Table 3.1.

TABLE 3.1 Red Hat Linux Boot and Driver Disk Images
| Name | Description |
| :--- | :--- |
| boot.img | Enabling boot using CD-ROM or hard partition |
| bootnet.img | install via FTP, HTTP, or NFS |
| pcmcia.img | Boot install using PCMIA hardware (requires the pcmciadd.img) |
| pcmciadd.img | PCMIA driver disk with support for SCSI, network, and other adapters |
| drblock.img | Utility image containing various hardware drivers |
| drnnet.img | Additional network drivers |
| oldcdrom.img | Support image for booting using old CD-ROM drives |
| images/pxeboot | Directory containing a PXE-enabled Linux kernel and RAM-disk images to support network booting