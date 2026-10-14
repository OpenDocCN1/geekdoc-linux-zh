To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

# Extracting a File into a Device

Although creating a tar file is easy, it is not what tar is about. What’s more important is that you can extract directly into a device. The device (typically a tape drive) won’t have a file system, so it cannot be mounted or accessed in the same way that you access your disks. However, it will store the data as if it were a file. So, if you tar into a tape or floppy, the entire tape or floppy is taken to be one large tar file. (Multiple tar files can be put in a tape; I’ll talk about that in a little bit.) In the case of a floppy, you won’t be able to mount it because it won’t have a file system where you can store files. (Remember that we discussed mounting in Chapter 7, “Working with Disks.”)

# Taring into a device

Taring into a device is the same as taring into a file. The only difference is that the destination of the archive is the path to the device representing your backup hardware. The basic devices that you’ll want to work with are floppies and tape drives.

# Floppy Devices

To create a tar file on a floppy, you use the /dev/fd x device, where x is the number of your floppy drive. Typically, this will be 0 if you’ve got only one floppy, or 0 or 1 if you’ve got two floppies:

```
tar cvf /dev/fd0 /etc /home/alberto/nsmail
```

This command will tar /etc and /home/alberto/nsmail into the