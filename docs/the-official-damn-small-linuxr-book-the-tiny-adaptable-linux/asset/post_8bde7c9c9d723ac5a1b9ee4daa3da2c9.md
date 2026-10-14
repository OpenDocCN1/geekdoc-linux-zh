
Other sizes or resolutions will not work. You can use the Gimp MyDSL extension to edit and/or create a boot image file.

- **f2 and f3:** These are the help files displayed when the F2 and F3 function keys are pressed at the initial boot prompt. These are text files and can be edited with any text editor.
- **minirt24.gz:** This is the initial ramdisk used to bootstrap DSL.

> **NOTE**
> 
> The Syslinux version has these files packed into a floppy-sized image. This is called `boot.img`. The unpacking and packing of this image file will be discussed later, in the “Creating the Syslinux ISO Image” section.

## Default Boot Options

The default boot time options are stored in either `isolinux.cfg` or `syslinux.cfg` depending on the CD-ROM master type you are choosing. For your Isolinux-based remaster, the file to edit is located at `master/boot/isolinux/isolinux.cfg`. This is a simple text file and can be easily edited. It is the APPEND line where the boot options are specified.

## The Boot Splash Screen

The boot splash screen contains an image that is shown at boot time. This is the image shown above the boot: prompt. This image is quite difficult to create as it is in the LSS16 format. I have provided utilities in the `chapter11/remaster/gnu` directory on the CD-ROM.

The usual procedure is to copy the image file `logo.16` to a working directory on a machine running the X Windows System. To convert the LSS16 to a format that Gimp can display, use the following:

```
# lss16toppm < logo.16 > logo.ppm
# gimp logo.ppm
```

After editing or creating a new image file, use one of the utilities provided in the `chapter11/remaster/gnu` directory: `giftoppm`, `pngtoppm`, or `bmptoppm`. Then, convert back to LSS16 format. For example, if in Gimp you saved the image as `.bmp`, use

```
# bmptoppm < logo.bmp > logo.ppm
# ppmto lss16 < logo.ppm > logo.16
```

After you have completed all the changes to the base system, you are ready to create a new compressed KNOPPIX/KNOPPIX file.

## The makeimage Script

The makeimage script is on the enclosed CD-ROM in the chapter11/remaster directory. The script is to be run from within your working directory. The following shows the script's contents, with line numbers added:

```
1. #!/bin/sh
2. #
3. # Clean up .bash_history
4. if [ -f source/KNOPPIX/.bash_history ]; then
5. rm source/KNOPPIX/.bash_history
6. fi
7. if [ -f source/KNOPPIX/home/ds1/.bash_history ]; then
8. rm source/KNOPPIX/home/ds1/.bash_history
9. fi
10. #
11. # Clean up any ssh hosts
12. if [ -d source/KNOPPIX/root/.ssh ]; then
13. rm -rf source/KNOPPIX/root/.ssh
14. fi
15. #
16. # Check to see if need .bash_profile
17. if [ ! -f source/KNOPPIX/.bash_profile ]; then
18. cp .bash_profile source/KNOPPIX/.bash_profile
19. fi
20. # Copy over the release info.
21. cp -f release.txt source/KNOPPIX/usr/share/doc/ds1/.
22. #
23. mkisofs -R -U -hide-rr-moved -cache-inodes -no-bak -pad source/KNOPPIX | nice -5 create_compressed_fs -best - 65536 > master/KNOPPIX/KNOPPIX
24. #
25. sync
26. sync
```

The makeimage script does the following:

- Lines 4-9 remove all references from what was recorded while chrooted in.
- Lines 12-14 remove any references to ssh connections that you may have used.
- Lines 17-19 check to see if you need a .bash_profile.
- Line 21 writes the release information using the direct method.
- Line 23 creates the new compressed KNOPPIX/KNOPPIX image from your source/ directory and writes it into the master/ directory.

Depending on your machine's resources, running the makeimage script could take a long time. After a successful build of the new compressed image, you must next combine the boot files, the kernel, initial ramdisk, and the compressed runtime image. This process creates the actual ISO image file in your iso/ directory. The ISO file is ready to be burned onto a CD-R CD-ROM. If you add an optional parameter of cd, the script records the image.

## The makeiso Script

After cleaning up the chrooted environment, the next stage actually creates the ISO image. This stage combines the newly created KNOPPIX image file with the boot image files into a single bootable CD or DVD image.

```
1. #!/bin/sh
2. RELEASE=`cat release.txt`
3. #
4. if [ -f master/KNOPPIX/boot.img ]; then
5.   rm master/KNOPPIX/boot.img
6.   tar -zxvf boot/isolinux.tgz
7. fi
8. #
9. mkisofs -pad -l -r -J -v -V KNOPPIX -no-emul-boot -boot-load-size 4 -boot-info-table -b boot/isolinux/isolinux.bin -c boot/isolinux/boot.cat -hide-rr-moved -o iso/"$RELEASE".iso master
10. #
11. sync
12. sync
13. if [ -n "$1" ]; then
14.   if [ "$1" == "cd" ]; then
15.     cdrecord -v speed=4 dev=0,0,0 -data iso/"$RELEASE".iso
16.   fi
17. fi
18. cd iso
19. md5sum "$RELEASE".iso > "$RELEASE".iso.md5.txt
20. sync
21. md5sum -c "$RELEASE".iso.md5.txt
22. cd ../.
```

The makeiso script can be found on the enclosed CD-ROM in the chapter11/remaster directory. The script is to be run from within your working directory. Note the following:

- Line 2 provides the name of your ISO image file and checksum file.
- Lines 4 through 7 allow for handling both Isolinix and Syslinux versions of DSL. Syslinux uses a boot.img for the boot files, whereas Isolinix uses a directory. These lines provide a mechanism to back up/restore your Isolinix
