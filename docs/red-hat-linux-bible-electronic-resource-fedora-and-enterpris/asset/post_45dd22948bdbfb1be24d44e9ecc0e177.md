
3. Change to the dosutils directory (cd \dosutils).

4. Run the rawrite command as follows:

```
C:> rawrite
Enter disk image source file name: D:\images\bootdisk.img
Enter target diskette drive: a:
Please insert a formatted diskette into drive A: and press -Enter- :
```

5. Press Enter. The image is written to the disk. Remove the disk and mark it.

## Using GRUB or LILO boot loaders

A boot loader lets you choose when and how to boot the bootable operating systems installed on your computer's hard disks. GRUB is the only boot loader that comes with the Fedora Core distribution of Red Hat Linux. Earlier versions of Red Hat Linux and the current Red Hat Enterprise Linux also include the LILO boot loader. The following sections describe both GRUB and LILO boot loaders.

### Booting your computer with GRUB

With multiple operating systems installed and several partitions set up, how does your computer know which operating system to start? To select and manage which partition is booted and how it is booted, you need a boot loader. The boot loader that is installed by default with Red Hat Linux is called the GRand Unified Boot loader (GRUB).

GRUB is a GNU software package (www.gnu.org/software/grub) that replaced the LILO boot loader by default in Red Hat Linux 7.2. GRUB offers the following features:

- Support for multiple executable formats.
- Support for Multiboot operating systems (such as Red Hat Linux, FreeBSD, NetBSD, OpenBSD, and other Linux systems).
- Support for non-Multiboot operating systems (such as Windows 95, Windows 98, Windows NT, Windows ME, Windows XP, and OS/2) via a chain-loading function. Chain-loading is the act of loading another boot loader (presumably one that is specific to the proprietary operating system) from GRUB to start the selected operating system.
- Support for multiple file system types.
- Support for automatic decompression of boot images.
- Support for downloading boot images from a network.

For more information on how GRUB works, type `man grub` or `info grub`. The `info` command contains more details about GRUB.

### Booting with GRUB

When you install Red Hat Linux, information needed to boot your computer (with one or more operating systems) is automatically set up and ready to go. Simply restart your computer. When you see the GRUB boot screen (it says GRUB at the top and lists bootable partitions below it), do one of the following:

- **Default:** If you do nothing, the default operating system will boot automatically after a few seconds.
- **Select an operating system:** Use the up and down arrow keys to select any of the operating systems shown on the screen. Then press Enter to boot that operating system.
- **Edit the boot process:** If you want to change any of the options used during the boot process, use the arrow keys to select the operating system you want and type **e** to select it. Follow the next procedure to change your boot options temporarily.

If you want to change your boot options so that they take effect every time you boot your computer, see the section on permanently changing boot options. Changing those options involves editing the `/boot/grub/grub.conf` file.

#### Temporarily changing boot options

From the GRUB boot screen, you can select to change or add boot options for the current boot session. First, select the operating system you want (using the arrow keys) and type **e** (as described earlier). You will see a graphical screen that contains information like the following:

```
GRUB  version  0.93  (639K  lower  /  128768K  upper  memory)

root  (hd0,0)
kernel  /boot/vmlinuz-2.4.22-1  ro  root=LABEL=/  hdc=ide-scsi
initrd  /boot/initrd-2.4.22-1.img
```

```
Use the ↑ and ↓ keys to select which entry is highlighted.
Press 'b' to boot, 'e' to edit the selected command in the
boot sequence, 'c' for a command-line, 'o' to open a new line
after ('O' for before) the selected line, 'd' to remove the
selected line, or escape to go back to the main menu.
```

There are three lines in the example of the GRUB editing screen that identify the boot process for the operating system you chose. The first line (beginning with `root`) shows that the entry for the GRUB boot loader is on the first partition of the first hard disk (hd0,0). GRUB represents the hard disk as hd, regardless of whether it is a SCSI, IDE, or other type of disk. You just count the drive number and partition number, starting from zero.

The second line of the example (beginning with `kernel`) identifies the boot image (`/boot/vmlinuz-2.4.22-1`) and several options. The options identify the partition as initially being loaded ro (read-only) and the location of the root file system on a partition with the label LABEL=/. The third line (starting with initrd) identifies the location of the initial RAM disk, which contains the minimum files and directories needed during the boot process. If you are going to change any of the lines related to the boot process, you would probably change only the second line to add or remove boot options. Here is how you do that:

1. Position the cursor on the kernel line and type e.
2. Either add or remove options after the name of the boot image. You can use a minimal set of bash shell command-line editing features to edit the line. You can even use command completion (type part of a filename and press Tab to complete it). Here are a few options you may want to add or delete:
   - **Boot to a shell:** If you forgot your root password or if your boot process hangs, you can boot directly to a shell by adding `init=/bin/sh` to the boot line. (The file system is mounted read-only, so you can copy files out. You need to remount the file system with read/write permission to be able to change files.)
   - **Select a run level:** If you want to boot to a particular run level, you can add the word `linux`, followed by the number of the run level you want. For example, to have Red Hat Linux boot to run level 3 (multiuser plus networking mode), add `linux 3` to the end of the boot line. You can also boot to single-user mode (1), multi-user mode (2), or X GUI mode (5). Level 3 is a good choice if your GUI is temporarily broken.
3. Press Enter to return to the editing screen.
4. Type b to boot the computer with the new options. The next time you boot your computer, the new options will not be saved. To add options so they are saved permanently, see the next section.

### Permanently changing boot options

You can change the options that take effect each time you boot your computer by changing the GRUB configuration file. In Red Hat Linux, GRUB configuration centers around the `/boot/grub/grub.conf` file.

The `/boot/grub/grub.conf` file is created when you install Red Hat Linux. Here is an example of a grub.conf file.

```
# grub.conf generated by anaconda
#
# Note that you do not have to rerun grub after making
# changes to this file
# NOTICE: You have a /boot partition. This means that
# all kernel and initrd paths are relative to /boot/, eg.
# root (hd0,0)
# kernel /vmlinuz-version ro root=/dev/hda3
# initrd /initrd-version.img
#boot=/dev/hda

default=0
timeout=10
splashimage=(hd0,4)/grub/splash.xpm.gz
title Red Hat Linux (2.4.22-1)
 root (hd0,4)
 kernel /vmlinuz-2.4.22-1 ro root=LABEL=/ 
 initrd /initrd-2.4.22-1.img
title Windows XP
 rootnoverify (hd0,0)
 chainloader +1
```

The `default=0` line indicates that the first partition in this list (in this case Red Hat Linux) will be the one that is booted by default. The line `timeout=10` causes GRUB to pause for ten seconds before booting the default partition. (That's how much time you have to press e if you want to edit the boot line, or to press arrow keys to select a different operating system to boot.)

The `splashimage` line looks in the fifth partition on the first disk (hd0,4) for the boot partition (in this case /dev/hda5, which is the /boot partition). GRUB loads `splash.xpm.gz` as the image on the splash screen (/boot/grub/splash.xpm.gz). The splash screen appears as the background of the boot screen.

> **NOTE:** GRUB indicates disk partitions using the following notation: (hd0, 0). The first number represents the disk, and the second is the partition on that disk. So, (hd0, 1) is the second partition (1) on the first disk (0).

The two bootable partitions in this example are Red Hat Linux and Windows XP. The `title` lines for each of those partitions are followed by the name that appears on the boot screen to represent each partition.

For the Red Hat Linux system, the `root` line indicates the location of the boot partition as the second partition on the first disk. So, to find the bootable kernel (vmlinuz-2.4.22-1) and the initrd initial RAM disk boot image that is loaded (initrd-2.4.22-1.img), GRUB looks in the root of hd0,4 (which is represented by /dev/hda5 and is eventually mounted as /boot). Other options on the `kernel` line set the partition as read-only initially (ro) and set the root file system to /dev/hda6.

For the Windows XP partition, the `rootnoverify` line indicates that GRUB should not try to mount the partition. In this case, Windows ME is on the first partition of the first hard disk (hd0,0) or /dev/hda1. Instead of mounting the partition and passing options to the new operating system, the `chainloader +1` indicates to hand control the booting of the operating system to another boot loader. The +1 indicates that the first sector of the partition is used as the boot loader.

> **NOTE:** Microsoft operating systems require that you use the chainloader to boot them from GRUB.
