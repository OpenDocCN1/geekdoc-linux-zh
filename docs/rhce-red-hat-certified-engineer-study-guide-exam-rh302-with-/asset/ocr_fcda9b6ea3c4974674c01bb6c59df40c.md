# Chapter 20 • Working in Single-User and Rescue Mode

However, in Red Hat Linux 6.1 and later, the standard installation media provide for rescue mode, no special floppy disk is required. Nevertheless, many Red Hat Linux users prefer the Red Hat Linux 6.0 approach to rescue mode. If you have a Red Hat Linux 6.0 distribution CD-ROM, you can follow the procedure in the next subsection to use the Red Hat Linux 6.0 rescue facility.

To use the Red Hat Linux 6.1 rescue facility, boot the system by using the installation floppy disk or the installation CD-ROM. In response to the boot prompt, reply `linux rescue`.

The rescue facility will ask you to choose your language and keyboard style. It will then attempt to locate the RPMs and base directories of the Red Hat Linux distribution media. If the system's CD-ROM drive contains a distribution CD-ROM, the system will enter rescue mode. Otherwise, the rescue facility will prompt you for the location of these directories, which may be a CD-ROM drive or local hard drive. Generally, you should insert an installation CD-ROM in the CD-ROM drive and direct the rescue facility to that device. However, if the system contains a readable file system directing the rescue facility to the partition on which the file system resides.

> You can use a bootnet.img floppy as a rescue disk, obtaining the rescue environment from a suitably configured NFS server.

![](bbox=[0.137, 0.513, 0.203, 0.569])

# Using the Red Hat Linux 6.0 Rescue Facility

The Red Hat Linux 6.0 rescue facility is not supported by Red Hat Linux 6.2 and later. Therefore, use of the Red Hat Linux 6.0 rescue facility is no longer allowed during the RHCE exam. However, if you're responsible for administering Red Hat Linux 6.0 systems, you need to know how to use this facility.

To use the Red Hat Linux 6.0 rescue facility, you must create a boot disk and rescue disk from images on the Red Hat Linux distribution CD-ROM. Alternatively, you can use your system's boot disk and create only the rescue disk.

# Creating the Boot Disk

To create a boot disk from the image on the Red Hat Linux distribution CD-ROM, insert the media, mount the CD-ROM as /mnt/cdrom, and issue the following command:

```
dd if=/mnt/cdrom/images/boot.img of=/dev/fd0
```