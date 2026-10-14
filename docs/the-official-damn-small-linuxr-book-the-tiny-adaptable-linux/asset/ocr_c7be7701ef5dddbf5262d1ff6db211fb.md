With Frugal Lilo, you don't need to worry about other operating systems being installed, or who will own the MBR. Frugal Lilo does have more prompts to eliminate or reduce the need to be editing the Lilo configuration file for you after installation changes.

> NOTE
> Before installing Frugal Lilo, it is best to have booted from the DSL CD-ROM and have learned the additional boot options that may be required or desired for your particular machine or purpose.

Use the following steps to do a CompactFlash Lilo install:

+   1. Select menu option 5 from the DSL Install Options screen (refer to Figure 8-1). You see the following disclaimer and prompt for the target partition:
+   
+       DSL Compressed Image Install/Upgrade.
+   
+       No responsibility for data loss or hardware damage!
+   
+       A linux partition large enough to hold the image file must be created prior to installation.
+   
+       This version uses Lilo Boot Loader in the specified partition. You must therefore make that partition the active/boot one.
+   
+       For Grub Boot Loader version, use frugal_grub.sh
+   
+       Enter the target partition to hold DSL image & Lilo (EXAMPLE: hda1):
+   
+   Again, if you do not have a Linux partition, the script exits with an error.

+   2. Type the device name of the target partition. For example, if you are using the first IDE hard drive on your computer (hda), with the first partition (hda1) assigned to swap and the second partition (hda2) assigned as a Linux file system, you could type hda2 and press Enter.
+   
+   As with Frugal Grub, you are prompted with the source location, as follows:
+   
+   Install from:
+   [L]iveCD or Frugal Install
+   [P]endrive
+   Local [I]so File
+   Fetching latest iso from [W]eb160
+   From Poormans via [B]ootfloppy
+   Choose (l/p/i/w/b):