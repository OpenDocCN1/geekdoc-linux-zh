**5** Low-level format the disk by typing **fdformat /dev/fd0** and then pressing **Enter**. The utility displays its progress as it performs its operation. When the format is complete, your screen should look similar to Figure 8-5.

![](bbox=[0.24, 0.17, 0.77, 0.46])

**Figure 8-5: Results of fdformat command**

+   * Make the floppy disk bootable by typing **dd if=/boot/vmlinuz-2.2.5-15 of=/dev/fd0** and then pressing **Enter**.

Note: If you are not using Linux Red Hat Version 6, the kernel image (in this case, vmlinuz-2.2.5-15) will differ. Use the one you located in Step 1.

Note: After you create a bootable disk, you can use it to start the system. Place the bootable disk in drive A, and turn on the system. Linux then boots from the floppy disk instead of the hard drive.

You can also use the dd command to make a back-up copy of a floppy disk. You can copy the entire contents of a floppy to a single file on your hard drive. You can then copy the file onto a second floppy disk, thus making a back-up copy of the original disk. In the next exercise, you make a back-up copy of the bootable floppy disk you created in the previous exercise. You need a second blank disk, which has already been formatted.