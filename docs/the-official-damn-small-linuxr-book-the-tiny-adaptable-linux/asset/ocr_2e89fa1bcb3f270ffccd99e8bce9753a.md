directory. The Syslinux boot.img is the standard DSL floppy image and therefore does not need to be included in the backup/restore process.

+   - Line 9 is the actual ISO creation. This combines the files in the master/ directory into an ISO image file in the iso/ directory.
+   - Lines 13 through 17 check if the script was started with cd as an option. The script defaults with the CD-ROM burner at device location 0,0,0. Using this option writes the new ISO image to a CD-R.
+   - Line 19 creates an md5sum checksum file for network transport and verification.
+   - Line 21 verifies the consistency of the checksum.

# Creating the Syslinux ISO Image

Many older computers cannot boot Isolinux-based CD-ROMs. These older computers are limited to an initial boot image that is the actual size of a floppy disk. The older Syslinux boot loader uses just such a mechanism.

# The makesys Script

The makesys script can be found on the enclosed CD-ROM in the chapter11/remaster directory. The script is to be run from within your working directory to create a Syslinux bootable ISO image. The following shows the contents of that script:

```
```sh
#!/bin/sh
RELEASE=`cat release.txt`
#
if [ -d master/boot ]; then
  tar -czvf boot.isolinux.tgz master/boot/
  rm -rf master/boot
fi
cp boot.img master/KNOPPIX/.
mkisofs -pad -l -r -J -b KNOPPIX/boot.img -c KNOPPIX/boot.cat -hide-rr-moved -o iso/"$RELEASE"-syslinux.iso master
sync
sync
if [ -n "$1" ]; then
if [ "$1" == "cd" ]; then
  cdrecord -v speed=4 dev=0,0,0 -data iso/"$RELEASE"-syslinux.iso
fi
fi
cd iso
md5sum "$RELEASE"-syslinux.iso > "$RELEASE"-syslinux.iso.md5.txt
sync
md5sum -c "$RELEASE"-syslinux.iso.md5.txt
cd ../.
```
```