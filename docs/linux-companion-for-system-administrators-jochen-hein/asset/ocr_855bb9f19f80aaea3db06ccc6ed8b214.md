# 3.2.2 The loadin boot loader

loadlin and loadinX by Hans Lermen are programs that run under MS-DOS and allow you to start LINUX from MS-DOS. loadinX² is a preprocessor for loadin which carries out a conversion of the command line parameters. Together with the UMSDS file system, loadin allows you to 'nose around' in LINUX without the need to repartition the hard disk. Particularly for LINUX newcomers, this possibility represents a simpler safer alternative to lilo. loadin is also useful when, for example, a soundcard must be initialized by means of a special program under DOS before it can be used LINUX.

To be able to use loadlin, LINUX must be installed, via a distribution. The step that follows in many distributions, namely installation of lilo into the boot sector, is skipped. Creation of a boot diskette, instead, must be carried out to LINUX to be initially booted from the floppy disk. The kernel /mlinuz is then copied to the DOS partition. If the DOS partition has not yet mounted by the installation routine, this can be done manually by means of, for example, mount -t mdsos /dev/hdal /mnt.

The loadlin program is passed the DOS name of the kernel image to be started as the parameter, for example root=/vmlinuz. The second argument, for example root=/dev/hda2, contains the partition to be used as root file system. The only further specification needed is whether the root partition is to be read-only (ro) or read/write (rw). A typical command would be:

```
C:> c:\linux\loadlin c:\linux\vmlinuz root=/dev/hdb2 rw
```

If UMSDS is used as the file system, care should be taken to employ the loadinX preprocessor instead of loadlin. When using loadinX, only the drive to be used, for example the primary DOS partition C: or one of the drives A: or B;, is passed as an argument in the root= parameter. A command line using of loadinX could look like the following:

```
C:> c:\linux\loadinX c:\linux\vmlinuz root=c:
```

It should be noted that using UMSDS, write-protected mounting of the file system (ro/read-only) is not possible. There are no special boot parameters to be used exclusively with loadlin.

Even DOS 6.2 does not distinguish between upper and lower case in commands; the upper case X in loadinX is only meant to emphasize the different program names.