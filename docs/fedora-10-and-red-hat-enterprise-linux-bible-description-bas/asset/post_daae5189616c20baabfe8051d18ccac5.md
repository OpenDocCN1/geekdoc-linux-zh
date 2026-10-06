
## Chapter 2: Installing Fedora

When you install Fedora or RHEL, information needed to boot your computer (with one or more operating systems) is automatically set up and ready to go. Simply restart your computer. When you see the boot message, press the Enter key (quickly before it times out) and the GRUB screen appears (it says GRUB at the top and lists bootable partitions below). Then you can do one of the following:

- Default — If you do nothing, the default operating system will boot automatically after a few seconds.
- Select an operating system — Use the up and down arrows to select any of the operating systems shown on the screen. Then press Enter to boot that operating system.
- Edit the boot process — If you want to change any of the options used during the boot process, use the arrows to select the operating system you want and press e to select. Follow the next procedure to change your options temporarily.

When you want to change your boot options so they take effect every time you boot your computer, see the section on permanently changing boot options. Changing those options involves editing the /boot/grub/grub.conf file.

### Temporarily change boot options

From the GRUB boot screen, you can select to change or add boot options for the current session. First, quickly before GRUB times out and boots the default system, press any key. From the GRUB selection screen that appears, select the operating system you want (using the arrow keys) and type e (as described earlier). You will see a graphical screen that contains information like shown in Figure 2-3, but with your Linux kernel and options listed.

There are three lines in the example of the GRUB editing screen that identify the boot process for the operating system you chose. The first line (beginning with root) shows that the entry for the GRUB boot loader is the first partition of the hard disk (hd0,0). GRUB represents the hard disk as hd, regardless of whether it is a SCSI, IDE, or other type of disk. You just count the drive number and partition number, starting from zero.

The second line in the example (beginning with kernel) (/boot/vmlinuz-2.6.25.1-fc9 in this example) and several options. The rhgb option produces the Red Hat graphical screen, while the quiet option prevents details of the boot process from being shown. The options identify the partition as initially being loaded ro (read-only) and the location of the root file system on a partition with the LABEL=/1. The third line (starting with initrd) identifies the location of the initial RAM disk, which contains the minimum files and directories needed during the boot process.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_123_0.png)

**Figure 2-3:** Edit the boot entry from your Fedora system from the GRUB menu.

If you are going to change any of the lines related to the boot process, you would probably change only the second line to add or remove boot options. Here is how you do:

1. Position the cursor on the kernel line and type e.
2. Either add or remove options after the name of the boot image. You can use a minimal set of bash command-line editing features to edit the line. You can use command completion (type part of a filename and press Tab to complete it). Here are a few options you may want to add or delete:
    - **Boot to a shell** — If you forgot your root password or if boot process hangs, you can go directly to a shell by adding init=/bin/sh to the boot line (The file system is mounted read-only, so you can copy files out. You may need to mount the file system with read/write permission to change files).
    - **Turn off a service** — If your boot process is hanging on a particular service, you can often turn off that service from the boot prompt. For example, you could add the options noacpi (to turn off ACPI power management), nopcmia (to turn off PCMCIA card slot support), or nodma (to turn off DMA), if you are getting disk errors. Add selinux=0 to temporarily turn off SELinux. Sometimes turning off a service at the boot prompt allows you to fix the problem after the system is up and running.
    - **Select a run level** — If you want to boot to a particular run level, you can add the word linux, followed by the number of the run level you want. For example, to have Fedora boot to level 3 (multuser networking mode), add linux 3 to the end of the boot line. You can also boot to single-user mode (1), multi-user mode (2), or X GUI (5). Level 3 is a good choice if your GUI is temporarily broken.
3. **Press Enter** to return to the editing screen.
4. **Type b** to boot the computer with the new options. The next time you boot your computer, the new options will not be saved. To add options they are saved permanently, see the next section.

## Permanently changing boot options

You can change the options that effect each time you boot your computer by changing the GRUB configuration file. In Fedora, GRUB configuration centers around the /boot/grub/grub.conf file.

The /boot/grub/grub.conf file is created when you install Fedora. Here is an example of a grub.conf file:

```
# grub generated by anaconda
# Note that you do not have to rerun grub after making
# changes to this file
# NOTICE: You have a /boot partition. This means that
    all kernel and initrd paths are relative to /boot/, eg.
    root (hd0,0)
    kernel /vmlinuz-version root=/dev/sda7
    initrd /initrd-version.img
#boot=/dev/sda
default=0
timeout=5
splashimage=(hd0,0)/boot/grub/splash.xpm
hiddenmenu=0
title Fedora (2.6.27-0.382.rc8.git4.co10.1686)
root (hd0,0)
kernel /vmlinuz-2.6.27-0.382.rc8.git4.co10.i686 root=UUID=866237bb-d845-4117-a1b2-2e86df056f15 rhgb quiet
initrd /initrd-2.6.27-0.382.rc8.git4.co10.1686
title Windows XP
rootrollover (hd1,0)
chainloader +1
```

The default=0 line indicates that the first partition in this list (in this case Fedora) is the one that is booted by default. The line timeout=5 causes GRUB to pause for 5 seconds booting the default partition. (Because of the hiddenmenu option, you won't even see the GRUB screen if you don't press Enter before 5 seconds.)

> NOTE: GRUB indexes partitions using the following notation: (hd0, 0). The first number represents the disk, and the second is the partition on that disk. So, (hd0, 1) is the second partition (1) on the first disk (0). That would equate to /dev/sda2 in Linux.

The splashimage line loads the second partition on the first disk (hd0,0) for the boot partition (in this case /dev/sda, which is the /boot partition). GRUB loads splash.xpm.gz as the image on the splash screen (/boot/grub/splash.xpm.gz). The splash screen appears as the background of the boot screen.

> NOTE: You can replace the splash screen with any image, provided that it meets certain specifications. Using GIMP or other image editor, save the size to 640x480 pixels, 14 colors, and xpm format. Next, use gzip to compress the file. Then copy that file to the /boot/grub directory. The last step is to edit the grub.conf file to have the splashimage value point to the new file.

The two bootable partitions in this example are Fedora and Windows XP. The title lines for each of those partitions are followed by the name that appear on the screen to represent each partition.

For the Fedora system, the root line indicates the location of the boot partition on the first disk. So, the bootable kernel and the initrd ram boot image loaded. GRUB looks in the root of hd0,0 (which is represented by /dev/sda and is eventually mounted as /boot). Other options on the kernel line set the partition as read-only initially (ro) and set the root file system to LABEL=1.

For the Windows XP partition, the rootverifier indicates that GRUB should not try to mount the partition. Since Windows XP is the first partition of the second disk (hd1,0 or /dev/sdb1). Instead of mounting the partition and passing options to the new operating system, the chainloader +1 indicates to handle the booting of the operating system to another boot loader. The +1 indicates that the first section of the partition is used as the boot loader.

> NOTE: Microsoft operating systems require that you use the chainloader to boot them from GRUB.

If you make any changes to the /boot/grub.conf file, you do not need to load those changes. Changes are automatically picked up by GRUB when you reboot your computer. If you are accustomed to using LILO boot loader, this may confuse you at first, as LILO requires you to rerun the lilo command for the sake effect.

### Adding a new GRUB boot image

You may have different boot images for kernels that include different features. These days, as you get updated kernels for Fedora or RHEL, you simply install an RPM containing the new
