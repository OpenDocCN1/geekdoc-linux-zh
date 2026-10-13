# Creating the Boot Disks

If you are installing Red Hat using the DVD-ROM included with this book, or you are using a set of CD-ROM discs to install Linux, and if your computer is fairly new, it most likely has the ability to boot from your CD-ROM. This book's DVD-ROM operates as a bootable CD-ROM. In this case, you can just use your CD-ROM or this book's DVD-ROM as your installation disk and skip this section. (You may need to configure your BIOS to boot from your CD-ROM.) If you cannot boot from your CD-ROM or DVD-ROM, you will have to create floppy install disks as described here.

Note If you are installing from the Red Hat DVD-ROM included with this book, you will need a DVD-ROM drive on your computer to read the DVD-ROM disc. The DVD-ROM included with this book has been configured to be bootable, functioning like a boot CD-ROM. If your system supports bootable CD-ROMs, then it will boot from this DVD-ROM, letting you install your Red Hat system from the DVD-ROM directly.

On Windows, to use the rawritewin program to create a floppy install disk, first insert the CD-ROM into your CD-ROM drive (if you are installing from the DVD-ROM disc included with this book, you would use your DVD-ROM drive instead). Change to your CD-ROM drive. Once you have changed to the CD-ROM drive, you then need to change to the \dosutils directory. The rawritewin command is in the dosutils\rawritewin directory. Just double-click it to start it. It is very easy to create a boot disk with rawritewin. Just run it from Windows and use its interface to select the floppy disk image bootdsk.img, with support disks pcmiadd.img, and drvnet.img. The image file you want for a CD-ROM or DVD-ROM installation is the boot.iso file, also located on your CD-ROM in the images/ directory. Be sure that your floppy drive is correctly listed. The default will be A:. Then place a blank floppy in your floppy drive and click Write.

For rawrite, which you have to use on MS-DOS, at your DOS prompt, change to your CD-ROM drive, using whatever the letter for that drive may be. For example, if your CD-ROM drive is the E drive, just type e: and press ENTER. Once you have changed to the CD-ROM drive, you then need to change to the \images directory. On the DVD-ROM included with this book, the install disk image is bootdsk.img with support disks for network and notebooks, drvnet.img and pcmiadd.img. The rawrite command has to be run at a DOS prompt. Enter the full path for the rawrite command, including the CD-ROM or DVD-ROM drive letter, such as e:\dosutils\rawrite. The rawrite command first prompts you for the name of the disk image file you want to copy. Enter the full name of the install image file. The command then asks you to enter the letter of the floppy drive where you put your floppy disk. On many systems, this is the A drive.

```
E:\> cd images
E:\col\launch\floppy > e:\dosutils\rawrite
Enter source file name: bootdsk.img
Enter destination drive (A or B) and press ENTER: a
```

Press ENTER to confirm that you have a blank floppy disk in the drive. rawrite will then copy the image file to your floppy disk, creating your install disk. When it finishes, remove your disk from the floppy drive. This is the disk that the installation procedure (described later) refers to as the install diskette. If you need to create a network support disk, use drvnet.img. For PCMCIA support, use pcmiadd.img.

To create floppy disks on a Linux or Unix system, you use the dd command and specify the boot image file to use along with the name of the floppy device and the size of the floppy disk. You will first need to mount the CD-ROM, then change to its mount directory. On most Linux systems, the first floppy disk drive is at /dev/fd0 and its size is usually 1440 for a 1.4 floppy disk. With the if option, you specify the image file to use, the of option indicates the floppy device name, and the bs option specifies the block size.

```
dd if=images/bootdsk.img of=/dev/fd0 bs=1440
```

If your system contains very old CD-ROM drives, SCSI adapters, or network cards, you will likely have to create a driver disk. Your Red Hat CD-ROM/DVD-ROM provides a floppy disk image called /images/drvnet.img that contains drivers for many uncommon devices, particularly those not using the PCI bus. If you have devices supported by theses drivers, you should create a driver disk using drvnet.img and