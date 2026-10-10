# ## Part 1 Getting Started

The second line of the example (beginning with kernel) identifies the boot image (/boot/vmlinuz-2.6.18-92.el5 in this example) and several options. The rhib option produces the graphical boot screen, while the quiet option prevents details of the boot process from being shown. The options identify the partition as initially being loaded (a Read Only) and the location of the root file system on the partition /dev/VolGroup00/LogVol00. The third line (starting with initrd) identifies the location of the initial RAM disk, which contains the minimum files and directories needed during the boot process.

If you are going to change any of the lines related to the boot process, you would probably change only the second line to add or remove boot options. Here is how you do that:

+   1.  Position the cursor on the kernel line and type e.
+   2.  Either add or remove options after the name of the boot image. You can use a minimal set of bash shell command-line editing features to edit the line. You can even use command completion (type part of a filename and press [Tab] to complete it). Here are a few options you may want to add or delete:
+       *   **Boot to a Shell** — If you forgot your root password or if your boot process hangs, you can boot directly to a shell by adding `init=/bin/sh` to the boot line. (The file system is mounted Read Only, so you can copy files out. You need to remount the file system with Read/Write permission to be able to change files.)
+       *   **Turn off a Service** — If your boot process is hanging on a particular service, you can often turn off that service from the boot prompt. For example, you could add the options `noacpi` (to turn off ACPI power management), `nopcimcta` (to turn off PCM-CIA card slot support), or `nodma` (to turn off DMA, if you are getting disk errors). Add `selinux=0` to temporarily turn off SELinux. Sometimes turning off a service at the boot prompt allows you to fix the problem after the system is up and running.
+       *   **Select a Run Level** — If you want to boot to a particular run level, you can add the word `linux` followed by the number of the run level you want. For example, to have CentOS boot to run level 3 (multuser plus networking mode), add **linux 3** to the end of the boot line. You can also boot to single-user mode (1), multuser mode (2), or X GUI mode (5). Level 3 is a good choice if your GUI is temporarily broken.
+   3.  Press [Enter] to return to the editing screen.
+   4.  Type b to boot the computer with the new options. The next time you boot your computer, the new options will not be saved. To add options so they are saved permanently, see the next section.

# ### Permanently Changing Boot Options

You can change the options that take effect each time you boot your computer by changing the GRUB configuration file. In CentOS, GRUB configuration centers around the /boot/grub/grub.conf file.

The /boot/grub/grub.conf file is created when you install CentOS. Here is an example of a grub.conf file: