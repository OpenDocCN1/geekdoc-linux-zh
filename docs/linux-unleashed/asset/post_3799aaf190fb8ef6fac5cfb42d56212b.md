
while trying to do two things at the same time.) Although many people ignore the rule about using root only when necessary, most of them eventually find out why this rule is important!

## Starting and Stopping the System

There are several ways of booting the Linux operating system, as well as a few ways to safely shut it down. Some were mentioned earlier in this book. Because Linux can be installed in many different ways, there is no single "right" method of booting the operating system, so we must look at both hard-disk–based and floppy-disk–based boot procedures.

### Booting from a Floppy

A boot floppy, as its name implies, is a floppy disk that boots the Linux kernel. A boot floppy has the root partition installed on the floppy itself instead of the hard drive (although both may coexist). Without the root partition, Linux would be unable to find the hard drives for the rest of the operating system.

You can create Linux boot floppies with the setup routine included in most distributions of the operating system. Check the documentation or information files that came with your Linux distribution, if there are any. Alternatively, most Linux setup utilities have a menu-driven interface that prompts you for a boot floppy setup when you rebuild or reconfigure the kernel. You should use this procedure to make a boot floppy, which is also useful for emergencies.

In most cases, a boot floppy is used only in emergencies when your system won’t start up normally. The boot floppy enables you to load Linux and then mount the hard drives that are causing the problem to check for damage. Luckily, this is not required very often. If you haven’t used LILO to choose the partition to boot or set your boot sequence to Linux by default, you may need the boot floppy to start up Linux. In this case, the boot floppy is much like a DOS boot floppy.

You can create a boot floppy from scratch by copying over the kernel image from the hard drive. The kernel image is usually in the file `vmlinuz`, `vmlinux`, `Image`, or `/etc/Image`, depending on the distribution of Linux. The Slackware distribution uses `vmlinuz`, which is a compressed kernel (hence the z in the name). Compressed kernels uncompress themselves as they are loaded into memory at boot time. The `vmlinuz` image expands to `vmlinux`. (Compressed kernels take up less disk space; that’s why they are used.)

After you have identified the kernel, you can set the root device in the kernel image to point to the root partition on either the floppy or hard drive. In this case, we want the floppy. The root partition is set with the `rdev` command, whose format is as follows:

```
rdev kernelName device
```

`kernelName` is the name of the kernel image, and `device` is the name of the Linux root partition. To set a floppy boot device with the file vmlinuz, for the first floppy on the system, the command would be as follows:

```
rdev vmlinuz /dev/fd0
```

You can set other parameters with `rdev` as well if you want to change system defaults during boot. Check the `rdev` man page for the `rdev` help file for complete information.

As a final step in creating the boot floppy, copy the kernel image to the floppy disk. You should use a preformatted disk (format with DOS if necessary) to allow the Linux routines to identify the type of disk and its density. To copy the vmlinuz kernel to the first floppy drive, use this command:

```
cp vmlinuz /dev/fd0
```

The floppy should now be ready to boot the system. You may not be able to boot the system without the floppy if you change the location of the root partition. You can change the root partition back to the hard drive with the `rdev` command after completing the boot floppy, which enables you to boot from either. This can be useful when you have disks for several different boot configurations. You can also create the boot floppy from the Linux setup program.

### Using LILO to Boot

LILO is a program that resides in the boot sector of your hard drive and allows Linux to be booted from the hard disk either after you tell it to or after a default number of seconds has elapsed.

LILO can also be used with other operating systems such as OS/2 and DOS. If you have LILO set to autobot Linux, you must interrupt the process by pressing the Ctrl, Alt, or Shift key when the bootup is started. This displays a boot prompt that enables you to specify another operating system. If LILO is set to allow a given time before it boots into Linux, you can use the Ctrl+Alt+Shift sequence to interrupt the boot process before the timer expires and Linux starts loading. Finally, if LILO is set to not autobot into Linux but to wait for explicit instructions, you must press Enter to boot Linux or type the name of the other operating system.

Some Linux distributions have a configuration file in the directory /etc/lilo that can be edited to provide boot information, while other versions of Linux configure LILO during the installation process. If the latter is the case, you can change the settings with the setup utility. Some versions of Linux use the configuration file /etc/lilo.conf instead of /etc/lilo.

## Shutting Down Linux

You can't just turn off the power switch! This can cause damage to the file system, sometimes irreversibly. Because Linux keeps many files open at once, as well as several processes, they must all be closed down properly before you cycle the power to the unit. There are a few ways to shut the Linux system down, but the formal method is to use the shutdown command. The syntax for shutdown is as follows:

```
shutdown [minutes] [warning]
```

minutes is the number of minutes to wait before shutting the system down and warning is an optional message displayed for all users currently logged in. Some versions of shutdown allow the word now instead of a time, while others require either no argument or the number 0 to shut the system down immediately without waiting. You can have shutdown reboot the system after the shutdown by adding the argument -r (for reboot).

Using shutdown is best if you have other users on your system, because it gives them a warning that they should log out, and it prevents loss of information. It can also be used to automate a shutdown much later (such as at midnight), with messages that appear just before that time warning any users still logged in.

If you can't wait and want to shut the system down immediately, use the halt command or the "three-finger salute" of Ctrl+Alt+Delete. This immediately shuts down all the processes and halts the system as quickly as possible. Then the power can be shut off.

![](img/e8e6b47ac20475e23d48b4c476f5d891_610_0.png)

Some Linux distributions don't support Ctrl+Alt+Delete, and a couple of older distributions use it to halt the system immediately without terminating processes properly. This can cause damage. Check the documentation or man pages for information.

## Mounting File Systems

File systems are not available until they are mounted onto the Linux main file system. Even hard drives must be mounted, because only the root file system is available in the / directory until the rest are mounted. The mount command is used to mount a file system.

During the boot process, the mount command is used from the startup files (such as the /etc/rc file or files under the /etc/rc.d directory) to mount all the file systems maintained in the file /etc/fstab. You can look at the file to see the type of information maintained there. Every file system that is mounted during the boot process has an entry giving its device name, its mount directory (called the mount point), the type of file system it is, and any options that apply.

You can add a new file system from a hard disk, a CD-ROM, a floppy, or any other type of device that provides a file system supported by Linux, using the mount command. The format is as follows:

```
mount filesystem mountpoint
```

filesystem is the name of the device and mountpoint is where in the Linux file system it should be mounted. For example, if you want to mount a SCSI CD-ROM to the file system as /usr/cdrom, issue the following command:

```
mount /dev/cd0 /usr/cdrom
```

The directory /usr/cdrom must be created before the command is given, or the mount command generates an ambiguous error. You should replace /dev/cd0 with the name of your CD-ROM device driver (/dev/cd0 for most non-SCSI CD-ROM drives and /dev/cd0 for SCSI CD-ROM drives). When the file system is mounted properly, changing to /usr/cdrom lets you access all the files on the CD-ROM as if they were part of the normal file system.

If your /etc/fstab file doesn't have any entries in it already, you have to mount the file system with a slightly different syntax:

```
mount -t fstype filesystem mountpoint
```

fstype is the type of file system (such as ISO9660, MSDOS, and so on). The rest of the arguments are the same as the example above. The -t option is used when the file system to be mounted doesn't already have an entry in the /etc/fstab file.
