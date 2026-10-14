is because Linux sometimes keeps changes to files in memory before it writes them to disk; it’s making sure that the files on the floppy are up-to-date. Simply wait until the light goes off before you remove the floppy from the drive.

# 24.4 Using Data CDs

As with a floppy disk, before you can use a data CD (“compact disc”) on your system, you must first mount it on an empty directory. You then unmount it from the directory before you can eject the CD from the CD drive (you can also eject the disc using software—see Recipe 22.1.6 [Ejecting an Audio CD], page 480).

**NOTES:** To use audio CDs, see Chapter 22 [Audio Compact Discs], page 477.

# 24.4.1 Mounting a Data CD

To mount a data CD on the system, use mount with the `/cdrom` option.⁴

⇒ To mount a data CD on the system, type:

```
$ mount /cdrom [RET]
```

This command makes the contents of the data CD available from the `/cdrom` directory tree. You can use any Linux file command on the files and directories on a data CD, but you can only write to one if it is a CDRW disc.

Like the `/floppy` directory, the use of the `/cdrom` directory is a standard practice and convenient, but not necessary—you can mount disks in whatever empty directory you like. (You could even, for example, mount discs from the CD drive to `/floppy` and mount floppy disks to `/cdrom`, but why would anyone do that!)

To mount a data CD to a specific directory, use mount and give as arguments the name of the device file in `/dev` corresponding to the CD drive, and the name of the directory to mount to. This directory must already exist on the filesystem, and it must be empty. If it doesn’t exist, use mkdir to create it first (see Recipe 5.1.2 [Making a Directory], page 130).

Most Linux systems are set up so that the device file of the first CD drive is `/dev/cdrom`, but the name of the device file may be different, especially if you have a SCSI CD-ROM drive.

> ⁴ This works if your administrator has set up the CD drive filesystem for user access—see Recipe A.6.3 [Letting Users Access Hardware Peripherals], page 718.