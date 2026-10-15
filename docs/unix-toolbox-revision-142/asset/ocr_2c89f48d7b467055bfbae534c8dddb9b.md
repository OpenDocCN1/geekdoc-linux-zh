# 3.9 Mount an image

# Linux loop-back

```
# mount -t iso9660 -o loop file.iso /mnt          # Mount a CD image
# mount -t ext3 -o loop file.img /mnt             # Mount an image with ext3 fs
```

# FreeBSD

With memory device (do # kldload md.ko if necessary):

```
# mdconfig -a -t vnode -f file.iso -u 0
# mount -t cd9660 /dev/md0 /mnt
# umount /mnt; mdconfig -d -u 0                     # Cleanup the md device
```

Or with virtual node:

```
# vnconfig /dev/vn0c file.iso; mount -t cd9660 /dev/vn0c /mnt
# umount /mnt; vnconfig -u /dev/vn0c               # Cleanup the vn device
```

# Solaris and FreeBSD

with loop-back file interface or lofi:

```
# lofiadm -a file.iso
# mount -F hsfs -o ro /dev/lofi/1 /mnt
# umount /mnt; lofiadm -d /dev/lofi/1               # Cleanup the lofi device
```

# 3.10 Create and burn an ISO image

This will copy the cd or DVD sector for sector. Without conv=notrunc, the image will be smaller if there is less content on the cd. See below and the dd examples (page 41).

```
# dd if=/dev/hdc of=/tmp/mycd.iso bs=2048 conv=notrunc
```

Use mkisofs to create a CD/DVD image from files in a directory. To overcome the file names restrictions: -r enables the Rock Ridge extensions common to UNIX systems, -J enables Joliet extensions used by Microsoft systems. -L allows ISO9660 filenames to begin with a period.

```
# mkisofs -J -L -r -V TITLE -o imagefile.iso /path/to/dir
```

On FreeBSD, mkisofs is found in the ports in sysutils/cdtools.

# Burn a CD/DVD ISO image

# FreeBSD

FreeBSD does not enable DMA on ATAPI drives by default. DMA is enabled with the sysctl command and the arguments below, or with /boot/loader.conf with the following entries:

```
hw.ata.ata_dma="1"
hw.ata.atapi_dma="1"
```

Use burncd with an ATAPI device (burncd is part of the base system) and cdrecord (in sysutils/cdtools) with a SCSI drive.

```
# burncd -f /dev/acd0 data imagefile.iso fixate      # For ATAPI drive
# cdrecord -scanbus                                   # To find the burner device (like 1,0,0)
# cdrecord dev=1,0,0 imagefile.iso
```

# Linux

Also use cdrecord with Linux as described above. Additionally it is possible to use the native ATAPI interface which is found with:

```
# cdrecord dev=ATAPI -scanbus
```

And burn the CD/DVD as above.