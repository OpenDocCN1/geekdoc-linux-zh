LI [...] This is caused by geometry mismatch or by moving /etc/lilo/boot.b without running the installer.

LIL [...] This is typically caused by media failure or geometry mismatch.

The geometry means the number of sectors/heads/cylinders used in the hard drive configuration of your BIOS. Hope this helps!

It is a very good idea to have a handbook for Linux or at least a UNIX handbook. Handbooks for Windows are useless, handbooks for Linux are great! "Red Hat Lilo Unleashed is a very good handbook but I am sure there are many other good ones.

With a LILO error like above, you can boot your machine using a Linux or DOS boot floppy. There seems to be several general possibilities to correct such a LILO error, depending on what is wrong:

+   1. If LILO gets corrupted, you can remove and re-install it. You can remove LILO by running under Linux:

```
lilo -u /dev/hda
```

or, under DOS:

```
DISK/MBR
```

which rewrites the hard drive master boot record (MBR), in which LILO resides, and replaces it with "clean" DOS stuff. You will lose access to Linux, but you can boot it from the floppy and re-install LILO on top of the DOS MBR. To re-install LILO simply re-run the command lilo (as root).

+   2. Specify the option

linear

in your /etc/lilo.conf file. This is particularly useful for large drives (>8 GB). See man lilo.conf for details. The option "linear" is safe--it should not affect a properly working system, so you can specify this option is any case.

+   3. Look into your BIOS setup and figure out how your hard drive geometry does not match your hard drive. From under Linux, you can display the hard drive geometry using (example, for the first IDE drive:

```
hdparm -g /dev/hda
```

+   4. Put LILO on another partition (different hard drive) and make this partition bootable from fdisk (if your system supports booting from another drive).

+   5. Maybe you prefer to use "loadlin" instead of "lilo". Under DOS, locate your CDROM and see the program /dosutils/loadlin.exe . It boots Linux from DOS.