
how much storage you will need? If you plan to back up this collection, will you use a tape drive, or will you simply copy the files to another hard drive?

If you are planning an installation for a corporate or enterprise-level environment, you must also consider future expansion or evolution of the system. You will want to craft a flexible system that can evolve with your business and its system needs.

Knowing how software is located on your hard drive for Linux, knowing how Red Hat Linux organizes its file system, or layout of directories on storage media. This knowledge will help you make the most out of hard drive space; and in some instances, such as having to have user directories mounted via NFS or other means, it can help head off data loss, increase security, and accommodate future needs. Create a great system, and you'll be the hero of information services.

To plan the best partitioning scheme, research and know the answers to these questions:

- How much disk space does your system require?
- Do you expect your disk space needs to grow significantly in the future?
- Will the system boot Red Hat Linux, or do you need a dual-boot system?
- How much data will require backup, and what backup system will work best? (See Chapter 11, "Backing Up, Restoring, and Recovery,” for more information on backing up your Red Hat Linux system.)

## CD-ROM Installation jumpstart

To install Red Hat Linux from the CDs included with this book, you must have at least a Pentium-class CPU, 650MB hard drive, and 64MB RAM. You'll need at least 128MB to install using Red Hat's graphical installer. A 10GB hard drive can host the entire Red Hat distribution, leaving a little than 5GB free for other data.

To begin the installation, set your PC's BIOS to boot from CD-ROM. Next, insert the CD-ROM and boot your computer. Press Enter at the first screen and follow through the subsequent dialogs to install.

Remember or write down your system's root password. Also, even if you thoroughly configure a graphical desktop during installation, choose to have Red Hat boot to a text-based login (see the section "Step-by-Step Installation" later on). You can start a graphical session after you finish the install, reboot, and log in. You can set Red Hat boot to a graphical login later (see Chapter 6, "The X Window System," to see how).

If you have a floppy drive, create a boot disk during install (see the "Step-by-Step Installation" section in this chapter). Finally, finish the install, remove the CD-ROM from your computer, and reboot. Then log in and enjoy Red Hat Linux!

## Choosing a Boot Loader

You will need to decide how to boot your Red Hat Linux system. For example

LILO is a small boot loader usually installed in the Master Boot Record (MBR) of an IDE hard drive, the Red Linux partition, or on a floppy disk. This loader (like others) can be used to pass essential kernel arguments to the Linux kernel for use during the boot process. Some arguments might include special disk geometry settings or specifying additional network interfaces. You can use other boot loaders, such as GRUB, to support special operations, such as booting from read-only memory (ROM) or flashed memory chips containing boot-loading code. Some, but not all, PC hardware BIOS booting via a network through Universal Serial (USB) removable media or from a floppy disk.

The GRUB loader works with all BSD Unix variants and many proprietary operating systems. This utility also supports menuing, command lines, installed RAM detection, and disk and remote network booting.

On the other hand, LILO has a much longer Linux history and might be more familiar to long-time Linux users. Both bootloaders offer password protection, but LILO’s password protection must be configured before installation.

> Red Hat's mkbootdisk command can be used to create floppy and CD-ROM boot media while using Linux. To do so, use the Linux kernel release number (returned by using the uname -r command) and a specified device. For example, to create a boot floppy, use the command this:

```bash
# mkbootdisk --device /dev/fdb0 `uname -r`
```

To create a CD-ROM boot image image (which must be burned onto a CDR or CDRW blank), use the command with its -iso option like this:

```bash
# mkbootdisk --iso --device boot_cd.img `uname -r`
```

Red Hat Linux can also be booted from a DOS session using the LOADLIN program, a DOS PATH to the Linux kernel, and the location of Linux kernel, as such

```bash
LOADLIN c:\KERNEL\VMLINUX root=/dev/hda2 ro
```

In this example, the kernel named VMLINUX is loaded, and the second primary partition of the first IDE hard drive is specified at the root partition of the Red Hat Linux system.

## Choosing How to Install Red Hat Linux

> NOTE

If you find LOADLIN fails to boot Linux and complains about a large kernel size, you can either try using bzimage to build a smaller kernel or rebuild a kernel that relies less on builtin features and more on loadable modules. See Chapter 24, “Kernel and Module Management,” for more information.

When choosing a commercial boot loader, weigh its capabilities and options. A good boot loader will support multiple operating systems, the ability to boot different Linux kernels (in order to change the characteristics of a system or easily accommodate new hardware), password protection, custom boot displays, and sane defaults.

If you run into trouble after installing Red Hat Linux, make sure to read the documentation for your boot loader to acquire any information.

Red Hat Linux can be installed in a variety of ways:

- Booting using a floppy
- Using a hard drive
- Booting from CD-ROM
- Booting over a network

## Installing from CD-ROM

To use this method, your computer must support CD-ROM, and the CD-ROM drive must be recognizable by the Linux kernel. Most users install Red Hat using the CD-ROM.

## Booting to an Install from DOS

As previously mentioned, you can use a DOS utility as LOADLIN (or BOOTLIN) to either directly boot an install from the CD-ROM or to load the Red Hat kernel.

See the desutils directory on the first Red Hat CD, and read the README file for an overview of the DOS utilities. The directory contains a DOS batch file that can help boot an install:

```bash
loadlin vmlinuz initrd=initrd.img
```

In this example, the LOADLIN command will boot the Red Hat kernel residing under the desutils directory, and then load the installation software.

## Making an Installation Boot Diskette

Your Red Hat Linux installation can be started using a boot floppy. A boot floppy can be used to boot the Red Hat CD-ROM on older CD-ROM drives. A boot floppy can also be used to start a Red Hat installer over a network when the PC does not have a CD-ROM drive but has a network interface card (NIC). Boot floppies are created from floppy images (.img files). These images are contained in the images directory on the first Red Hat CD-ROM.

Red Hat provides a number of images, as listed in Table 3.1.

TABLE 3.1 Red Hat Linux Boot and Driver Disk Images
| Name | Description |
| :--- | :--- |
| boot.img | Enabling boot using CD-ROM or hard partition |
| bootnet.img | install via FTP, HTTP or NFS |
| pcmcia.img | Boot install using PCMIA hardware (requires the pcmciadd.img) |
| pcmciadd.img | PCMIA driver disk with support for SCSI, network, and other adapters |
| drblock.img | Utility image containing various hardware drivers |
| drnnet.img | Additional network drivers |
| oldcdrom.img | Support image for booting using old CD-ROM drives |
| images/pxeboot | Directory containing a PXE-enabled Linux kernel and RAM-disk images to support network booting |
