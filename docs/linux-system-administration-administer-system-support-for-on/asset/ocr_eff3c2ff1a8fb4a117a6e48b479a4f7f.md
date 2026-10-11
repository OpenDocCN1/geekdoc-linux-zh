```
# ls /floppy/
abba.txt b-52s.txt cheap-trick.txt fleetwood-mac.txt

```

The contents of the disk in the floppy drive show up. If you have the appropriate permissions, you can read, write, and execute (move or remove) the files.

When you're done using the floppy drive, be sure to unmount the drive before you remove the disk.

```
# mount /floppy

```

# CD-ROM Drives


Because you most likely installed Slackware Linux from a CD-ROM drive, you know that Slackware supports most CD-ROM drives. A CD-ROM drive is mounted as read-only; you cannot write to it, even as root. If your system needs a writable CD-ROM drive, refer to the "Extra Storage Drives" section.

Your CD-ROM driver should be built into your kernel. In most of the Slackware installations I've seen, the CD-ROM drivers are on the /dev/hdc drive for ATAPI and IDE. (This location varies on specific hardware setups—for example, my CD-ROM is the slave drive on the secondary controller, /dev/hdd.) You can put your CD-ROM nearly anywhere on your controller card, except where the floppy controller should be.

No matter what, the CD-ROM is recognized on the file /dev/cdrom.

If we take a long listing of the /dev/cdrom file, we get:

```
# ls -l /dev/cdrom
lrwxrwxrwx 1 root    root    8  Jun 16 20:24 /dev/cdrom -> /dev/hdc

```

The file is always a symbolic link to the drive it's on, whether IDE or SCSI device. In this case, it's on /dev/hdc, the first drive on the secondary IDE controller.

# Extra Storage Drives


Having a CD-ROM, floppy drive, and a hard drive is not enough. Sometimes you'll want to backup files or transport large amounts of data to removable media. For this, you can configure Zip drives, Jaz drives, CD writable drives, or external hard drives.

# ZIP AND JAZ DRIVES


Known support is available for Zip and Jaz drives, but remember that some of their most basic characteristics can affect your choice. Jaz drives for example, are SCSI—they can't run through a parallel port because parallel ports don't have the throughput. Zip drives, however, are available in three different versions: parallel port, SCSI, and IDE—but the IDE version is only available as internal hardware. This means it won't work for a laptop and you have to install the drive yourself.