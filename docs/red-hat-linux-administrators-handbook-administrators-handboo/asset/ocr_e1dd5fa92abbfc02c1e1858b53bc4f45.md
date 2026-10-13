# Creating a boot disk under Linux

If you do not have an MS Windows system and thus want to use another Linux system to create the boot disk, do the following:

+   1. Mount your Red Hat CD-ROM as usual. These instructions assume that you have mounted it on the /mnt/cdrom directory. Change your current directory to the /mnt/cdrom/images directory where the boot image is kept.
+   2. Assuming your floppy drive is /dev/fd0 (the default floppy device) and you are using a 1.44MB (3.5-inch, high-density) floppy disk, run the following command:
+   ```
+   dd if=boot.img of=/dev/fd0 bs=1440K
+   ```

This should create the necessary boot disk. You can also create the supplementary floppy image disk by replacing the if=boot.img argument with if=supp.img in the preceding command. You need only the supplementary image for PCMCIA-based devices, which typically are used only on laptop/notebook computers.

After you create the boot disk, you are ready to install Red Hat Linux from the CD-ROM.

# Installing Red Hat Linux

If you are booting the system from the CD-ROM, insert your Red Hat CD-ROM in the drive and restart or start your intended server computer. In case you are using a boot floppy, insert it in the bootable floppy drive and restart or start the system.

When the system is booted, you see a welcome screen from Red Hat and then this prompt:

boot:

You have three choices.

+   - Press the Enter key to start a normal installation or upgrade.