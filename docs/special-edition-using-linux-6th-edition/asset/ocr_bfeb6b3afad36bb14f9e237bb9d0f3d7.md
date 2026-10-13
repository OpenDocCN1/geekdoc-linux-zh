If you had another distribution of Linux installed and the LILO boot loader was loaded to the MBR, that copy is seen first. OpenLinux installs by default to the OpenLinux partition. So the stale copy of LILO is looking for a kernel that no longer exists. Boot using the CD-ROM or boot floppy, and at the LILO prompt enter

```
boot root=/dev/hda
```

When in OpenLinux, use the `dd if=/boot/virgin.mbr of=/dev/hda bs=512 count=1` described in the previous text and your reboots should find OpenLinux again.

*I rebuilt my kernel, replaced the old one with the new one of the same name, but then forgot to run LILO before rebooting. Now the system won't reboot.*

You'll need to boot from either the install floppy or the CD-ROM and do the following:

+   1. When you get the LILO boot prompt, press the Shift and then Tab keys in succession. Enter the following (substituting the correct location of your root drive for `/dev/hda1`):
+   
+      ```
+      boot root=/dev/hda1
+      ```
+   2. Ensure your `/etc/lilo.conf` is correct and run LILO.
+   3. Reboot so you can boot into your new kernel.

*I want to see the kernel messages during bootup, but I get a Caldera screen instead that obscures the messages. How can I get rid of it?*

Change the `vga = 274` line to `vga = normal` and remove the `debug=2` from the `append =` line. Also comment out the `message =` above the boot stanza. Then rerun LILO. On your next bootup, you should see all the kernel boot-time messages.

*I want to boot into `single user mode | runlevel 3 | ... |` instead of runlevel 5. How can I do this?*

When you see the LILO boot prompt, press the Shift key then the Tab key. Type in the kernel name, a space, and the runlevel you want (single, 1, 2, 3, or 4). See the next chapter for more information.

*When I boot, I get stage1, but I never get stage2.*

The stage1 prints just before GRUB goes looking for the file. The GRUB that is booting cannot find the stage1 file. If you created a boot disk during install, use that to boot into the system and run the GRUB command line to reinstall GRUB. If you didn't create a boot disk, you can use the CD-ROM to boot, changing the command line by editing it and specifying the root disk and partition.