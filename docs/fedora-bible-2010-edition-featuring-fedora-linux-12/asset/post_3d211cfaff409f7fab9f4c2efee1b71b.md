
## Using PolicyKit for assigning administrative privilege

PolicyKit provides a system for graphical applications to run privileged operations without granting full root access to the applications. Since starting with Fedora 8, PolicyKit has grown to manage more applications so that only certain operations run as root. This is in contrast to the normal applications on the System → Administration menu, where you enter the root password and the entire application runs with root privileges.

For example, the Clock applet appears on the GNOME desktop showing the current time and date. If you place this applet on your desktop and then right-click on it, you can choose to Adjust Date & Time. If you do so, you will see a PolicyKit Authenticate dialog like the one shown in Figure 9-4.

![](img/c78bdcb5b7842a0d73dcc98921f872a2_387_0.png)

If you think about this, it makes perfect sense. There is no real security issue with letting users know the date and time. So, the Clock applet should run with plain old user privileges. Changing the system time, however, should be protected, as this could cause quite a bit of disruption to a Linux system that runs various tasks at specified times.

Fedora 12 ships with the 1.0 release of PolicyKit. With time, more and more applications will take the approach of running with user privileges except for a small set of protected operations. This helps security by reducing the amount of privileges granted to applications.

See `http://hal.freedesktop.org/docs/polkit/` for more on PolicyKit.

## Administering Your Linux System

Your Linux system administrator duties don't end after you have installed Fedora. Your ongoing job as a Linux system administrator includes the following tasks:

- **Configuring hardware** — Often when you add hardware to your Fedora computer, that hardware will be automatically detected and configured by tools such as HAL. In those cases where the hardware was not properly set up, you can use commands such as `lspci`, `modprobe`, `insmod`, and `rmmod` to configure the right modules to get the hardware working.
- **Managing file systems and disk space** — You must keep track of the disk space being consumed, especially if your Fedora system is shared by multiple users. At some point, you may need to add a hard disk or track down what is eating up your disk space. (You can use commands such as `find`, `du`, and `df` to do this.)
- **Monitoring system performance** — You may have a run-away process on your system or you may just be experiencing slow performance. Tools that come with Fedora can help you determine how much of your CPU and memory are being consumed.

The aforementioned administrative tasks are described in the rest of this chapter. Other chapters cover other administrative topics, such as managing user accounts (Chapter 10), automating system tasks (Chapter 11), performing system backups and restores (Chapter 12), and securing your system (Chapter 13). Tasks related to network and server administration are covered in Chapters 14 through 25. Ways of getting updates to your Linux software (using the Add/Remove Software window and yum command) are described in Chapter 5.

### Configuring Hardware

For many hardware items that you attach to your computer, Linux will simply detect them and configure them. During system boot time, the kernel will probe and identify your IDE drives, SCSI drives, PCI cards, and other hardware. After Linux desktop is running, USB devices that you plug in (such as pen drives or digital cameras) will be detected and any file systems they contain will be automatically mounted.

The following sections describe how to add and reconfigure hardware in Linux. This includes sections on checking your hardware, using HAL (for detecting and configuring hardware) and commands for working with loadable modules when hardware isn’t being detected and configured properly.

#### Checking your hardware

Sometimes the fact that Fedora can’t properly detect and configure your hardware may make it impossible for you to install Linux. In those cases, I suggest you try to determine what hardware you have before you install. See Chapter 2 for information on checking your hardware before installing Fedora (you can try the bootable Fedora live CD that comes with this book to test your hardware).

## Managing hardware with the DeviceKit

In prior releases of Fedora, a program called kudzu ran at boot time and checked your hardware against a saved configuration. Kudzu allowed you to reconfigure your hardware when it detected new devices.

Starting with Fedora 9, kudzu was replaced by another system called HAL, short for Hardware Abstraction Layer. HAL maintains a list of devices on your system, and provides a programming API for applications to access. A background process, hald, looks for changes to your installed hardware.

Then, starting with Fedora 11, HAL has been deprecated in favor of a newer replacement called DeviceKit. (We detect a pattern here.) In Fedora 12, two main systems have been migrated to the DeviceKit framework: power management and disks.

To see a list of disks managed by the DeviceKit, run a command like the following:

```bash
# devkit-disks --enumerate
```

You can then get information on a single device by running a command like the following:

```bash
# devkit-disks --show-info /dev/sda1
```

Note that you enter the Linux device file, not the name of the device as known by DeviceKit—`/org/freedesktop/DeviceKit/devices/sda1` in this case.

> **NOTE:** Removable devices, such as digital cameras, USB flash drives, and Webcams are detected and configured on-the-fly using the hald daemon. The hald daemon relies on the Udev device management facility to dynamically create devices and mount points (if needed) when those types of devices are connected. See Chapter 7 for descriptions of how CDs and digital cameras are detected.

## Configuring modules

In a perfect world, after installing and booting Linux, all of your hardware should be detected and available for access. While Fedora systems are rapidly moving closer to that world, there are times when you must take special steps to get your computer hardware working.

Fedora systems come with tools for configuring the drivers that stand between the programs you run (such as CD players and Web browsers) and the hardware they use (such as CD-ROM drives and network cards). The intention is to have only the most critical drivers your system needs built into the kernel; these are called *resident drivers*. Other drivers that are added dynamically as needed are referred to as *loadable modules*. The trend is to keep the basic kernel as lean as possible, so that each running system has only a few resident drivers and it can dynamically add what it needs.

## Listing loaded modules

To see which modules are currently loaded into the running kernel on your computer, you can use the `lsmod` command. Here’s an example:

```bash
# lsmod
Module            Size  Used by
vfat              9520   0
fat               45968  1 vfat
fuse              59860   2
nfsd              230824  1
lockd             66772  1 nfsd
nf_conntrack_ipv4 2684   1 nfsd
.
.
.
nf_conntrack_ipv6 18784  1
ip6table_filter     3360  1
ip6_tables          11684  1 ip6table_filter
ipv6             264816  36 ip6t_REJECT,nf_conntrack_ipv6
.
.
.
usb_storage        49048  0
i915             203884  3
```

This output shows a variety of modules that have been loaded on a Linux system. The modules loaded on this system include several to support various types of file storage, including fuse, a module that provides a file system in user space.

To find information about any of the loaded modules, you can use the `modinfo` command. For example, you could type the following:

```bash
# modinfo fuse
filename:  	/lib/modules/2.6.31.1-56.fc12.i686.PAE/kernel/fs/fuse/fuse.ko
alias: 	char-major-10-229
license: 	GPL
description: 	Filesystem in Userspace
author:	Miklos Szeredi <miklos@ZZZZZZZ>
srcversion:	A8C366D3D1129A5A809809
vermagic:	2.6.31.1-56.fc12.i686.PAE SMP mod_unload 686
```

This output tells you the location of the module (filename), the author, and description, among other information. The output describes the fuse module. You can use the `-d` option to list just the description, the `-a` option to see the author of the module, or `-fn` to see the object file representing the module. The author information often has the e-mail address of the driver’s creator (obscured here so as not to show someone’s real e-mail address) so you can contact the author if you have problems or questions about it.
