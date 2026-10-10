```
Vendor: YAMJUA Model: GPM424S Rev: 1.0f  
Type: CD-ROM ANSI SCSI revision: 02  
Detected scsi CD-ROM sr0 at scsi0, channel 0, id 1, lun 0  
sr0: scsi3-mmc drive: 24x/16x writer cd/w xa/form2 cdda tray  
Uniform CDROM driver Revision: 2.56
```

This information will come in handy later. The important data to remember are the channel, id, and lun numbers (used with the `cdrecord` command, discussed in the next section), and that the drive is recognized as `sr0` (which corresponds to the `/dev/scd0` device).

# # Command-Line Utilities

To mount, read, create, and write CD-ROM images, you'll need several Linux utilities: `mkisofs` to create an ISO image on your hard drive to hold the CD's contents, `mount` to mount an existing CD-ROM as an ISO image, `dd` to copy a CD's contents, `mke2fs` to format blank hard drive image files, and `cdrecord` to write selected files or write an ISO image to your CDR or CDWR drive. Note that before you begin, you might need up to 1.4GB of free hard drive space!

For example, one way to make a quick copy of a data CD-ROM (such as a bootable Linux CD) is to first use the `dd` command to copy the CD:

```
# dd if=/dev/scd0 of=cimage
```

You can then write the image with the `cdrecord` command, specifying your CDR or CDWR drive like this:

```
# cdrecord -v speed=2 dev=0,1,0 -data cimage
```

This will copy the file `cimage` onto your blank CDR or CDWR disk in the SCSI drive with an ID of 1 on bus 0. If your CDR or CDWR drive is fast enough, you can use a faster speed= setting. If you downloaded an ISO image of a CD-ROM, you can mount the image locally (and access its files and directory structure) like this:

```
# mount -t iso9660 -o loop=/dev/loop1 cimage /mnt/cdrom
```

This command will mount the CD-ROM's image file under the `/mnt/cdrom` directory as if it were an inserted CD-ROM. You can then copy the files from `/mnt/cdrom` to a new directory, such as `/mnt/cdrom_new`, to change the files or fix any problems. You can then create a new ISO image from the new directory by using the `mkisofs` command and specifying the new `/mnt/cdrom_new` directory like this:

```
# mkisofs -r -o new_cimage /mnt/cdrom_new
```