# # First Installation Steps: The Hard Way

+   1. Make installation floppies.
+   2. Boot an installation mini-Linux from the floppies in order to get access to the CD-ROM.

# # Continuing the Installation

+   1. Prepare the Linux file systems. (If you didn’t edit the disk partition table earlier, you will at this stage.)
+   2. Install a basic production Linux from the CD-ROM.
+   3. Boot Linux from the hard drive.
+   4. (Optional) Install more packages from CD-ROM.

# # Basic Parts of an Installation Kit

Here are the basic parts of an installable distribution:

+   ➤ The README and FAQ files. These will usually be located in the top-level directory of your CD-ROM and be readable once the hard disk has been mounted under Linux. (Depending on how the CD-ROM was generated, they may even be visible under DOS/Windows.) To become aware of important updates or changes, it is a good idea to read these files as soon as you have access to them.

+   ➤ A number of boot-disk images (often in a subdirectory). If your CD-ROM is not bootable, one of these is the file that you will write to a floppy to create the boot disk. You’ll select one of the above boot-disk images, depending on the type of hardware that you have in your system.

![](bbox=[0.06, 0.93, 0.19, 1.0])

# **NOTE**

> The issue here is that some hardware drivers conflict with each other in strange ways, and instead of attempting to debug hardware problems on your system, it’s easier to use a boot floppy image with only the drivers you need enabled. (This will have the nice side effect of making your kernel smaller.)

+   ➤ A root-disk image (or perhaps two). If your CD-ROM is not bootable, you will write one of these to a floppy to create the