This command dumps DOS from system memory and starts the Linux installation program.

If neither of these things worked, you'll need to create an installation floppy disk to boot your system. The information to make the floppy is on the CD-ROM as well as in the following steps.

To make an installation floppy disk, follow these steps from an existing DOS system. These steps apply to making a 1.44MB diskette on floppy drive A: Using another size or location of floppy drive is also possible and is described in the README file on the CD-ROM:

+   1. Insert the accompanying OpenLinux Lite CD-ROM into your CD-ROM drive.
2. Insert a blank floppy disk.

+   3. Enter this command (changing the drive letter to match the CD-ROM drive in your system):

```
E:\COL\TOOLS\RAWWRITE
```

+   4. Enter the drive letter for your floppy drive.

+   5. Enter the name of the installation floppy image on the CD-ROM:

```
E:\COL\LAUNCH\FLOPPY\INSTALL.IMG
```

If you want to create the floppy from an existing Linux system, you can use the dd command instead:

```
dd if=/mnt/cdrom/col/launch/floppy/install.img of=/devfd0
```

> The install.img file is a disk image. This type of file is an exact copy of everything that needs to be on the installation disk. The latest, greatest installation disk images may not be on the accompanying CD-ROM because updates occur frequently. Later images may include additional security fixes, hardware support, or updates. If you're concerned about hardware support or having the latest security information, check the Caldera Web site. There may be a later installation disk image.

You may also want to make a modules disk from the disk image in the same directory. The modules disk contains all the extra kernel modules that you might need to recognize your hardware. It's fairly common to need a modules disk, and it saves the trouble of coming back to this point and restarting if you make the modules disk when you make the installation disk.