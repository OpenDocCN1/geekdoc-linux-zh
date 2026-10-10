
![](img/1ea833f5a3e3c1547e3dd2891f52804a_451_0.png)

Click in the Password field (as shown in Figure 17.2) and type in a password to protect your system from remote access.

When you have finished entering your password, click the OK button. Your Mac OS Desktop is now ready for viewing. At a remote computer (such as another Power Mac running Linux), use the `vncviewer` command, along with a default display number (always 0 for Windows or Mac OS) to connect to the desktop, like this:

```bash
$ vncviewer titanium:0

VNC server supports protocol version 3.3 (viewer 3.3)
Password:
```

![](img/1ea833f5a3e3c1547e3dd2891f52804a_451_1.png)

VNC authentication succeeded
Desktop name *titanium*
Connected to VNC server, using protocol version 3.3
VNC server default format:
16 bits per pixel.
Most significant byte first in each pixel.
True colour: max red 31 green 31 blue 31, shift red 10 green 5 blue 0
Using default colormap which is TrueColor. Pixel format:
16 bits per pixel.
Most significant byte first in each pixel.
True colour: max red 31 green 31 blue 31, shift red 10 green 5 blue 0

After you press Enter, you will see a desktop, such as that shown in Figure 17.3.

## Stopping a Linux VNC Session

Stopping the VNC software on systems such as Windows or Mac OS is as simple as using the server's menu. However, under Linux, you must kill the VNC server's process. One quick way to do this is by using the `killall` command, which “kills” processes by name. For example, to stop a running `Xvnc` server, you can use the `killall` command, like this:

```bash
$ killall Xvnc
```

![](img/1ea833f5a3e3c1547e3dd2891f52804a_452_0.png)

You may also find process ID and log files for the session under your `~/.vnc` directory in your home directory. The VNC software will also create temporary files under the `/tmp` directory. Another, and perhaps more graceful, way to kill a running session is to use the `vncserver` command's `-kill` option, followed by the current display number.

# Using MOL

The Mac-on-Linux emulator is an X11 client that uses your system's Mac OS ROM (*Read-only Memory*) file to run Mac OS in a window on your Desktop. This software package, the product of a project headed by Samuel Rydh and numerous PPC Linux hackers, runs natively, and is amazingly fast!

Download and then install (as root) the binary version of `mol` using the `rpm` command, like this:

```bash
# rpm -ivh mol*rpm
mol
########################################
```

If you use Mac OS 8.6 or newer, use the `strip_nwrom` command to create a file named `rom.nw` under the `/usr/lib/mol/rom` directory. You can get this file from your existing System Folder, or from your Mac OS System restore CD-ROM. Use the command, like this:

```bash
# mount -t hsfs /dev/cdrom /mnt
# /usr/bin/strip_nwrom "/mnt/System Folder/Mac OS ROM" /usr/lib/mol/rom/rom.nw
```

In this example, the restore CD-ROM has been mounted under the `/mnt` directory. Your next task is to edit the file `/etc/molrc`. In particular, you will need to edit the section that lists your available Mac OS partition. You can find this information (as root) by using the `pdisk` command, like this:

```bash
# pdisk -l
```

```text
Partition map (with 512 byte blocks) on '/dev/hda*'
#       type name            length      base        (size )
1:      Apple_partition map 'Apple'               63 @ 1
2:      Apple_Driver43* 'Macintosh'           54 @ 64
3:      Apple_Driver43* 'Macintosh'           74 @ 118
4:      Apple_Driver_ATA* 'Macintosh'         54 @ 192
5:      Apple_Driver_ATA* 'Macintosh'         74 @ 246
6:      Apple_FWDriver 'Macintosh'            200 @ 320
7:      Apple_Driver_IOKit 'Macintosh'        512 @ 520
8:      Apple_Patches 'Patch Partition'       512 @ 1032
9:      Apple_HFS 'Macintosh HD'              12400855 @ 1544   ( 5.9G)
10:     Apple_HFS '/boot'                     65536 @ 12402399 ( 32.0M)
11:     Linux_PPC '/'                         12400854 @ 12467935 ( 5.9G)
12:     Linux_PPC 'Swap'                      646087 @ 24968789 (315.5M)
13:     Linux_PPC '/d2'                       14495644 @ 25514876 ( 6.9G)
14:     Apple_Free 'Extra'                    24 @ 40010520
```

In this example, you can see that `/dev/hda9` is the resident Mac OS partition. Look in the file `/etc/molrc` for the section:

```bash
####################
# HFS volumes
####################

# blkdev:      device  flags
#
#  Device can for instance be /dev/hda, /dev/hda6 or /dev/ada4.
#  The following flags are supported:
#
#     -rw/-ro       read-write / read-only [default]
#     -force        export non-HFS partitions (be careful!)
#     -cd           CD

blkdev:           /dev/hda          -ro
blkdev:           /dev/hda9         -ro
```

Edit this file to point to your Mac OS partition. You should also thoroughly read, examine, and make changes to `/etc/molrc` in order to configure `mol` for your system. Once you have configured `mol` to your tastes, start the emulator from the command line of an X terminal window, like this:

```bash
$ mol &
```

After you press Enter, you will see a window, as shown in Figure 17.4 (this depends on how you have configured the emulator's display via settings in `/etc/molrc`).

> Intel-based Linux users can turn to another emulator named Executor. This emulator is commercial software provided by Ardi 2000, and may be found at http://www.ardi.com/.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_454_0.png)

![](img/1ea833f5a3e3c1547e3dd2891f52804a_455_0.png)

*Figure 17.4 The Mac-on-Linux emulator provides a way to run Mac OS apps while using Linux.*

## BSD on the Mac

The Berkeley Software Distribution, or BSD UNIX, is a variant of the commercial UNIX tree. Following a series of lawsuits in the mid-1990s, the free portions (totally rewritten and copyright-free portions) of this operating system were released to the world as 4.4BSD-Lite. Following this release, developers started working on various ports of this version of UNIX to run on Intel-based PCs.

### Types

After nearly 10 years, and nearly 30 years after the birth of UNIX, there are now three main variants of BSD available royalty and license-free, which include FreeBSD, NetBSD, and the ultra-secure OpenBSD.

One version that is available for use on Apple Power Macs is from http://www.openbsd.org. You can download a current development version, or *snapshots*, from ftp://ftp.openbsd.org/pub/OpenBSD/snapshots/powerpc/. This version has been in development since 1996, and is actively supported and constantly revised. According to the OpenBSD project, the current version supports the Power Mac G4, Power Mac Dual G4, Power Mac G4 Cube, iMac Rev A, B, C, DV, and DV+, along with the FireWire PowerBook G3, and PowerBook (Titanium) G4. Support for additional machines may be available by the time you read this.

### Features

OpenBSD is one of the premiere operating systems available for any computer. OpenBSD is considered one of the most secure operating systems available when installed and properly configured. Reliability and scalability (the ability to respond to increased resource demands) are key features of all BSD variants.

### Installation

One of the great features about OpenBSD is that it can be installed quickly and easily. Its main distribution consists of 12 compressed archives comprising less than 70MB. A full installation only uses 150MB of hard drive space. Despite this small size, there are many additional programs available for OpenBSD. Unlike LinuxPPC 2000, Yellow Dog Linux, and SuSE PPC Linux, the precompiled binary OpenBSD software is distributed in archives known as *packages*. It is manipulated by the `pkg_add`, `pkg_create`, `pkg_delete`, and `pkg_info` commands.

OpenBSD may be installed as the sole operating system, or may be used in a dual-boot configuration. There are three basic ways to boot to an install: use a supplied CD-ROM boot image; boot via a network (FTP, HTTP); and boot by loading the bootloader from an HFS partition. After booting, you will be asked to partition your drive and then to create BSD *disklabels*, or entries in BSD’s *disktable*, a database of partitions and their (nearly 20) characteristics, such as size and drive geometry.

Like PPC Linux, booting BSD requires interaction with Open Firmware. With OpenBSD, booting will most likely be done from the Open Firmware prompt.

### Resources

- [http://www.uk.research.att.com/vnc/index.html](http://www.uk.research.att.com/vnc/index.html). Home page for the remarkable free virtual network computing software from AT&T.
- [http://www.maconlinux.com/](http://www.maconlinux.com/). The MOL home page, with links to the latest version of the Mac-on-Linux emulator.
- [http://www.openbsd.org/powerpc.html](http://www.openbsd.org/powerpc.html). Information about Apple NewWorld Power Macs that can run OpenBSD.
