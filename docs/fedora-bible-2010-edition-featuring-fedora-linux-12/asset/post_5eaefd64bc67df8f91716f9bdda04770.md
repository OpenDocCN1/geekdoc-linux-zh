
normally be the case. (The boot loader must not be installed in the master boot record of the whole disk or the disk will become unbootable.)

5. **Reboot and Alt key** — When Fedora installation is completed, reboot as instructed. Hold the Alt key as the machine reboots. When you see the Boot Camp menu, select Windows and the computer will boot to Fedora. Just use the default boot entry for Fedora because trying to change GRUB boot labels will probably cause the computer to lock up. (By the way, if your DVD gets stuck in the drive, hold down the mouse button when you reboot and the DVD will eject.)

Remember that installing Fedora on an Intel-based Mac is still considered to be experimental. The less you stray from the defaults (partitioning, boot loaders, and so on), the better chance of getting a workable Fedora system running on your Mac.

If you run into problems, I recommend you refer to the Fedora Project's Fedora On MacIntel page (http://fedoraproject.org/wiki/FedoraOnMacIntel). There are also resources available from other Linux projects to get Linux to boot on Intel Mac architecture.

## Using the GRUB boot loader

A boot loader lets you choose when and how to boot the bootable operating systems installed on your computer's hard disks. GRUB is the only boot loader offered for you to configure during Fedora installation. (The LILO boot loader included with earlier versions of Fedora is no longer included as of Fedora Core 5.) The following sections describe the GRUB boot loader.

With multiple operating systems installed and several partitions set up, how does your computer know which operating system to start? To select and manage which partition is booted and how it is booted, you need a boot loader. The boot loader that is installed by default with Fedora is called the GRAnd Unified Boot loader (GRUB).

GRUB is a GNU software package (http://www.gnu.org/software/grub) that replaced LILO as the only boot loader available in Fedora. GRUB offers the following features:

- Support for multiple executable formats.
- Support for multiboot operating systems (such as Fedora, FreeBSD, NetBSD, OpenBSD, and other Linux systems).
- Support for non-multiboot operating systems (such as Windows 95, Windows 98, Windows NT, Windows XP, Windows Vista and OS/2) via a chain-loading function. Chain-loading is the act of loading another boot loader (presumably one that is specific to the proprietary operating system) from GRUB to start the selected operating system.
- Support for multiple file system types.
- Support for automatic decompression of boot images.
- Support for downloading boot images from a network.

For more on how GRUB works, type `man grub` or `info grub`. The `info` command contains more details about GRUB. Or, see the GRUB Wiki: `http://grub.enbug.org`.

When you install Fedora, information needed to boot your computer (with one or more operating systems) is automatically set up and ready to go. Simply restart your computer. When you see the boot message, press the Enter key (quickly before it times out) and the GRUB boot screen appears (it says GRUB at the top and lists bootable partitions below it). Then you can do one of the following:

- **Default** — If you do nothing, the default operating system will boot automatically after a few seconds.
- **Select an operating system** — Use the up and down arrow keys to select any of the operating systems shown on the screen. Then press Enter to boot that operating system.
- **Edit the boot process** — If you want to change any of the options used during the boot process, use the arrow keys to select the operating system you want and type `e` to select it. Follow the next procedure to change your boot options temporarily.

If you want to change your boot options so that they take effect every time you boot your computer, see the section on permanently changing boot options. Changing those options involves editing the `/boot/grub/grub.conf` file.

### Temporarily changing boot options

From the GRUB boot screen, you can select to change or add boot options for the current boot session. First, quickly press any key before GRUB times out and boots the default system.

From the GRUB selection screen that appears, select the operating system you want (using the arrow keys) and type `e` (as described earlier). You will see a graphical screen that contains textual information including GRUB’s root (the `/boot` partition), the kernel, and the initial RAM disk (initrd), which contains the minimum files and directories needed during the boot process.

If you are going to change any of the lines related to the boot process, you would probably change only the second line to add or remove boot options. Here is how you do that:

1. Position the cursor on the `kernel` line and type `e`.
2. Either add or remove options after the name of the boot image. You can use a minimal set of bash shell command-line editing features to edit the line. You can even use command completion (type part of a filename and press Tab to complete it). Here are a few options you may want to add or delete:
   - **Boot to a shell** — If you forgot your root password or if your boot process hangs, you can boot directly to a shell by adding `init=/bin/sh` to the boot line. (The file system is mounted read-only, so you can copy files out. You need to remount the file system with read/write permission to be able to change files.)
   - **Turn off a service** — If your boot process is hanging on a particular service, you can often turn off that service from the boot prompt. For example, you could add the options `noapci` (to turn off ACPI power management), `nopcmcia` (to turn off PCMCIA card slot support), or `nodma` (to turn off DMA, if you are getting disk errors). Add `selinux=0` to temporarily turn off SELinux. Sometimes turning off a service at the boot prompt allows you to fix the problem after the system is up and running.
   - **Select a run level** — If you want to boot to a particular run level, add the number of the run level you want to the end of the kernel line. For example, to have Fedora boot to run level 3 (multiuser plus networking mode), add `3` to the end of the kernel line. You can also boot to single-user mode (`1`), multi-user mode (`2`), or X GUI mode (`5`). Level 3 is a good choice if your GUI is temporarily broken.
3. Press Enter to return to the editing screen.
4. Type `b` to boot the computer with the new options. The next time you boot your computer, the new options will not be saved. To add options so they are saved permanently, see the next section.

### Permanently changing boot options

You can change the options that take effect each time you boot your computer by changing the GRUB configuration file. In Fedora, GRUB configuration centers around the `/boot/grub/grub.conf` file.

The `/boot/grub/grub.conf` file is created when you install Fedora. Here is an example of a `grub.conf` file:

```
# grub.conf generated by anaconda
#
# Note that you do not have to rerun grub after making
# changes to this file
# NOTICE: You have a /boot partition. This means that
# all kernel and initrd paths are relative to /boot/, eg.
# root (hd0,0)
# kernel /vmlinuz-version ro root=/dev/sda7
# initrd /initrd-version.img
#boot=/dev/sda
default=0
timeout=5
splashimage=(hd0,0) / grub/splash.xpm.gz
hiddenmenu
title Fedora (2.6.31.5-127.fc12.i686)
root (hd0,0)
kernel /vmlinuz-2.6.31.5-127.fc12.i686 ro root=UUID=866237bb-d845-4117-alb2-e286d0f56f15 rhgb quiet
initrd /initrd-2.6.31.5-127.fc12.i686.img
title Windows XP
rootnoverify (hd1,0)
chainloader +1
```

The `default=0` line indicates that the first partition in this list (in this case Fedora) will be the one that is booted by default. The line `timeout=5` causes GRUB to pause for 5 seconds before booting the default partition. The default timeout is zero seconds, but since we list more than one operating system, I changed the setting to allow a few seconds to get the chance to choose which operating system to boot. (Because of the `hiddenmenu` option, you won’t even see the GRUB boot screen if you don’t press Enter before 5 seconds.)

> **NOTE:** GRUB indicates disk partitions using the following notation: `(hd0, 0)`. The first number represents the disk, and the second is the partition on that disk. So, `(hd0, 1)` is the second partition (`1`) on the first disk (`0`). That would equate to `/dev/sda2` in Linux.

The `splashimage` line looks in the second partition on the first disk `(hd0, 0)` for the boot partition (in this case `/dev/sda1`, which is the `/boot` partition). GRUB loads `splash.xpm.gz` as the image on the splash screen (`/boot/grub/splash.xpm.gz`). The splash screen appears as the background of the boot screen.

> **NOTE:** You can replace the splash screen with any image you like, provided that it meets certain specifications. Using GIMP or other image editor, save the image to 640x480 pixels, 14 colors, and xpm format. Next, use gzip to compress the file. Then copy that file to the `/boot/grub` directory. The last step is to edit the `grub.conf` file to have the `splashimage` value point to the new file.

The two bootable partitions in this example are Fedora and Windows XP. The `title` lines for each of those partitions are followed by the name that appears on the boot screen to represent each partition.

For the Fedora system, the `root` line indicates the location of the boot partition as the second partition on the first disk. So, to find the bootable kernel and the `initrd` initial RAM disk boot image that is loaded, GRUB looks in the root of `hd0, 0` (which is mounted by `/dev/sda1` and is eventually mounted as `/boot`). Other options on the kernel line set the partition as read-only initially (`ro`) and set the root file system using a UUID label.

For the Windows XP partition, the `rootnoverify` line indicates that GRUB should not try to mount the partition. In this case, Windows XP is on the first partition of the second hard disk (`hd1,0`) or `/dev/sdb1`. Instead of mounting the partition, loading an operating system, and passing options to the new operating system, the `chainloader +1` indicates to hand control the booting of the operating system to another boot loader. The `+1` indicates that the first sector of the partition is used as the boot loader.
