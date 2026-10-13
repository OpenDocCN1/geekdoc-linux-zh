system from the CD-ROM first, then from the hard disk, and finally from the A floppy drive. Such an option allows you to keep the setting as is, because you simply need to remove any CD-ROM from the CD-ROM drive to boot from the hard disk.

# Creating a boot disk under MS Windows 9x/2000

You can create the boot disk under MS Windows 9x/2000 operating systems as follows:

+   1. Assuming your CD-ROM drive is called D and you have the Red Hat CD-ROM mounted in the drive, run the following command from an MS-DOS shell window:
+      `d:/dosutils/rawrite`
+   2. The rawrite utility will display the following prompt:
+      `Enter disk image source file name:`
+      `Please insert a formatted diskette into drive A: and press the enter key`
+   3. Enter `\images\boot.img` as the image source file. Now rawrite displays the following prompt:
+      `Enter target diskette drive:`
+   4. Enter the appropriate drive letters. For example, if your floppy disk is in the A drive, enter `a:` as the target drive.
+   5. Put a blank, formatted floppy disk in the floppy drive and press Enter to continue.
+   6. The rawrite utility will write the boot.img image to the disk, and you are done.

![](bbox=[0.1, 0.85, 0.18, 0.95])

Tip
If you need to use a PCMCIA-based CD-ROM to install Red Hat Linux, you also need to create a supplementary floppy disk using the technique just described. Enter only `\images\supp.img` as the image source filename in step 3.