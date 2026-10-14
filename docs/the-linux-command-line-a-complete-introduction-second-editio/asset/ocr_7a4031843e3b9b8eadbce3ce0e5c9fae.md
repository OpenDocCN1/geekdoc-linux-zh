Likewise, the -J option enables the Joliet extensions, which permit long filenames for Windows.

# A PROGRAM BY ANY OTHER NAME . . .

If you look at online tutorials for creating and burning optical media like CD-ROMs and DVDs, you will frequently encounter two programs called mkisofs and cdrecord. These programs were part of a popular package called cdrtools authored by Jörg Schilling. In the summer of 2006, Mr. Schilling made a license change to a portion of the cdrtools package, which, in the opinion of many in the Linux community, created a license incompatibility with the GNU GPL. As a result, a fork of the cdrtools project was started that now includes replacement programs for cdrecord and mkisofs named wodim and genisoimage, respectively.

# Writing CD-ROM Images

After we have an image file, we can burn it onto our optical media. Most of the commands we will discuss in the sections that follow can be applied to both recordable CD-ROM and DVD media.

# Mounting an ISO Image Directly

There is a trick that we can use to mount an ISO image while it is still on our hard disk and treat it as though it were already on optical media. By adding the -o loop option to mount (along with the required -t iso9660 file system type), we can mount the image file as though it were a device and attach it to the file system tree.

```
mkdir /mnt/iso_image
mount -t iso9660 -o loop image.iso /mnt/iso_image
```

In this example, we created a mount point named /mnt/iso_image and then mounted the image file image.iso at that mount point. After the