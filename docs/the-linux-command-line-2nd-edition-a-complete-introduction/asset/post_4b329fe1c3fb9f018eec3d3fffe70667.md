
drives, we can manage those devices, too. Preparing a blank floppy for use is a two step process. First, we perform a low-level format on the diskette, and then create a file system. To accomplish the formatting, we use the fdformat program specifying the name of the floppy device (usually /dev/fd0):

```
[me@linuxbox ~]$ sudo fdformat /dev/fd0
Double-sided, 80 tracks, 18 sec/track. Total capacity 1440 kB.
Formatting ... done
Verifying ... done
```

Next, we apply a FAT file system to the diskette with mkfs:

```
[me@linuxbox ~]$ sudo mkfs -t msdos /dev/fd0
```

Notice that we use the "msdos" file system type to get the older (and smaller) style file allocation tables. After a diskette is prepared, it may be mounted like other devices.

## Moving Data Directly To/From Devices

While we usually think of data on our computers as being organized into files, it is also possible to think of the data in "raw" form. If we look at a disk drive, for example, we see that it consists of a large number of "blocks" of data that the operating system sees as directories and files. However, if we could treat a disk drive as simply a large collection of data blocks, we could perform useful tasks, such as cloning devices.

The dd program performs this task. It copies blocks of data from one place to another. It uses a unique syntax (for historical reasons) and is usually used this way:

```
dd if=input_file of=output_file [bs=block_size [count=blocks]]
```

Let’s say we had two USB flash drives of the same size and we wanted to exactly copy the first drive to the second. If we attached both drives to the computer and they are assigned to devices /dev/sdb and /dev/sdc respectively, we could copy everything on the first drive to the second drive with the following:

```
dd if=/dev/sdb of=/dev/sdc
```

Alternately, if only the first device were attached to the computer, we could copy its contents to an ordinary file for later restoration or copying:

```
dd if=/dev/sdb of=flash_drive.img
```

**Warning!** The dd command is very powerful. Though its name derives from “data definition,” it is sometimes called “destroy disk” because users often mistype either the if or of specifications. **Always double check your input and output specifications before pressing enter!**

## Creating CD-ROM Images

Writing a recordable CD-ROM (either a CD-R or CD-RW) consists of two steps; first, constructing an iso image file that is the exact file system image of the CD-ROM and second, writing the image file onto the CD-ROM media.

### Creating An Image Copy Of A CD-ROM

If we want to make an iso image of an existing CD-ROM, we can use dd to read all the data blocks off the CD-ROM and copy them to a local file. Say we had an Ubuntu CD and we wanted to make an iso file that we could later use to make more copies. After inserting the CD and determining its device name (we’ll assume /dev/cdrom), we can make the iso file like so:

```
dd if=/dev/cdrom of=ubuntu.iso
```

This technique works for data DVDs as well, but will not work for audio CDs, as they do not use a file system for storage. For audio CDs, look at the cdrdao command.

### Creating An Image From A Collection Of Files

To create an iso image file containing the contents of a directory, we use the genisoimage program. To do this, we first create a directory containing all the files we wish to include in the image, and then execute the genisoimage command to create the image file. For example, if we had created a directory called ~/cd-rom-files and filled it with files for our CD-ROM, we could create an image file named cd-rom.iso with the following command:

```
genisoimage -o cd-rom.iso -R -J ~/cd-rom-files
```

The “-R” option adds metadata for the Rock Ridge extensions, which allows the use of long filenames and POSIX style file permissions. Likewise, the “-J” option enables the Joliet extensions, which permit long filenames for Windows.

### A Program By Any Other Name...

If you look at on-line tutorials for creating and burning optical media like CD-ROMs and DVDs, you will frequently encounter two programs called mkisofs and cdrecord. These programs were part of a popular package called “cdrtools” authored by Jörg Schilling. In the summer of 2006, Mr. Schilling made a license change to a portion of the cdrtools package which, in the opinion of many in the Linux community, created a license incompatibility with the GNU GPL. As a result, a fork of the cdrtools project was started that now includes replacement programs for cdrecord and mkisofs named wodim and genisoimage, respectively.

## Writing CD-ROM Images

After we have an image file, we can burn it onto our optical media. Most of the commands we will discuss below can be applied to both recordable CD-ROM and DVD media.

### Mounting An ISO Image Directly

There is a trick that we can use to mount an iso image while it is still on our hard disk and treat it as though it were already on optical media. By adding the “-o loop” option to mount (along with the required “-t iso9660” file system type), we can mount the image file as though it were a device and attach it to the file system tree:

```
mkdir /mnt/iso_image
mount -t iso9660 -o loop image.iso /mnt/iso_image
```

In the example above, we created a mount point named /mnt/iso_image and then mounted the image file image.iso at that mount point. After the image is mounted, it can be treated just as though it were a real CD-ROM or DVD. Remember to unmount the image when it is no longer needed.
