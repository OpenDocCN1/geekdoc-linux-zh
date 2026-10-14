To reverse the process and repack the initial ramdisk and related files back into the boot.img file, perform the following:

+   1. Change directory out of mroot, unmount, and compress the initial ramdisk:
+      # cd ..
+      # umount mroot/
+      # gzip -9 minirt24
+   2. Move the compressed ramdisk back into the boot mount point:
+      # mv minirt24.gz boot/
+      mv: Overwrite "boot/minirt24.gz"? y
+   3. Unmount the boot mount point and remove the work directories:
+      # umount boot
+      # rmdir boot/ mroot/

# Building the DSL Qemu Embedded Version

Virtualization is currently very popular. DSL has incorporated many features to make running DSL in a sandbox standalone virtual environment very easy. The creation of the zip image is also very easy, using your mkqemu automated script from within your working directory.

# The makeqemu Script

The makeqemu script is on the CD-ROM in the chapter11/ remaster directory. This script, as the others, is to be run from within the base of your working directory. The following shows the contents of the makeqemu script:

+   1. #!/bin/bash
+   2. RELEASE=`cat release.txt`
+   3. rm iso/"$RELEASE"-embedded.zip
+   4. cd qemu
+   5. pwd
+   6. cp ../master/KNOPPIX/KNOPPIX knoppix/.
+   7. ../gnu/zip -r ../iso/"$RELEASE"-embedded.zip .
+   8. cd ../iso
+   9. md5sum "$RELEASE"-embedded.zip > "$RELEASE"-embedded.zip.md5.txt
+   10. sync
+   11. md5sum -c "$RELEASE"-embedded.zip.md5.txt
+   12. cd ../..

Note the following about the makeqemu script:

+   - Line 2 names your distribution file.
+   - Line 3 removes any preexisting copy of your distribution file.
+   - Line 6 copies the compressed runtime image file into the qemu/ directory.