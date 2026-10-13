restrictions only. The following example creates a CD image called mydoc.iso using the files and subdirectories located in the mdoc directory and labels the CD image with the name "doc":

```
mkisofs -v -r -T -J -U -V "Greatdocs" -o mydocuments.iso  mydocs
```

# Mounting Disk Images

Once you have created your CD image, you can check to see if it is correct by mounting it as a file system on your Linux system. In effect, to test the CD image, you mount it to a directory and then access it as if it were simply another file system. Mounting a CD image requires the use of a loop device. Specify the loop device with the loop option as shown in the next example. Here the mydoc.iso is mounted to the /mnt/cdrom directory as a file system of type iso9660. Be sure to unmount it when you finish.

```
mount -t iso9660 -o ro,loop=/dev/loop0 mydocuments.iso /mnt/cdrom
```

# Bootable CD-ROMs

If you are creating a bootable CD-ROM, you need to indicate the boot image file to use and the boot catalog. With the -c option, you specify the boot catalog. With the -b option, you specify the boot image. The boot image is a boot disk image, like that used to start up an installation procedure. For example, on the Red Hat CD-ROM, the boot image is isolinux/isolinux.bin, and the boot catalog is isolinux/boot.cat (you can also use images/boot.img and boot.cat). Copy those files to your hard disk. The following example creates a bootable CD-ROM using Red Hat distribution files located on the CD-ROM drive.

```
mkisofs -o rd8-0.iso -b isolinux/isolinux.bin -c isolinux/boot.cat \
-no-emul-boot -boot-load-size 4 -boot-info-table \
-v -r -R -T -J -V "Red8.0"  /mnt/cdrom
```

# cdrecord and dvdrecord

Once mkisofs has created the CD image file, you can use cdrecord or cdwrite to write it to a CD write disc. If you have more than one CD-R/W drive to use, you should specify the CD-R/W drive by indicating its SCSI bus number (recall that even IDE CD-R/RW drives are treated as SCSI devices on Linux). You can use cdrecord with the -scanbus option to find out the SCSI numbers of your rewritable devices. In this example, as shown previously in the -scanbus example, the device number for the rewritable CD-RW drive is 0,0. The dev= option is used to indicate this drive. The final argument for cdrecord is the name of the CD image file. dvdrecord works the same way on DVD-R/RW writers and is in fact an extension of cdrecord.

```
cdrecord dev=0,0 mydocuments.iso
```

If you are creating an audio CD, use the -audio option, as shown here. This option uses the CD-DA audio format:

```
cdrecord dev=0,0 -audio moresongs.iso
```

Similar operations apply to dvdrecord, except that dvdrecord will write to a DVD-R disc on a DVD-R recorder.