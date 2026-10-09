
amd64/EM64T hardware includes only one CPU type, HAMMER, as that architecture has only one CPU family. While a kernel configuration can include multiple CPU types, they must be of similar architectures; a kernel can run on 486 and Pentium CPUs, but you can't have a single kernel run on both Intel-compatible and ARM processors.

- **ident** Every kernel has a single `ident` line, giving a name for the kernel. That's how the `GENERIC` kernel gets its name; it's an arbitrary text string.
- **makeoptions** This string gives instructions to the kernel-building software. The most common option is `DEBUG=-9`, which tells the compiler to build a debugging kernel. Debugging kernels help developers troubleshoot system problems.
- **options** These are kernel functions that don't require particular hardware. This includes filesystems, networking protocols, and in-kernel debuggers.
- **devices** Also known as *device drivers*, these provide the kernel with instructions on how to speak to certain devices. If you want your system to support a piece of hardware, the kernel must include the device driver for that hardware. Some device entries, called *pseudodevices*, aren't tied to particular hardware, but instead support whole categories of hardware—such as Ethernet, random number generators, or memory disks. You might wonder what differentiates a pseudodevice from an option. The answer is that pseudodevices appear to the system as devices in at least some ways, while options have no device-like features. For example, the loopback pseudodevice is a network interface that connects to only the local machine. While no hardware exists for it, software can connect to the loopback interface and send network traffic to other software on the same machine.

Here's another snippet of a configuration file—the part that covers ATA controllers:

```
# ATA controllers
    device              ahci      # AHCI-compatible SATA controllers
    device      ata       # Legacy ATA/SATA controllers
    device      mvs       # Marvell 88SX50XX/88SX60XX/88SX70XX/SoC SATA
    device      sis       # SiliconImage SiI3124/SiI3132/SiI3531 SATA
```

Each of these devices is a different type of ATA controller. Compare these entries to a couple of our ATA entries in /var/run/dmesg.boot:

```
atapci0: <Intel PIIX4 UDMA33 controller> port 0xf10-0xf17,0x3f6,0x170
-0x177,0x3f6,0xc160-0xc16f at device 1.1 on pci0
ata0: <ATA channel> at channel 0 on atapci0
ata1: <ATA channel> at channel 1 on atapci0
ada0 at ata0 bus 0 scbus0 target 0 lun 0
cd0 at ata1 bus 0 scbus1 target 0 lun 0
```

The kernel configuration has an ATA bus, device ata. It’s a “legacy” ATA bus, whatever the word “legacy” means today. The dmesg snippet here starts with the atapci device, the controller where ATA meets PCI. We then have two ATA buses, ata0 and ata1. Disk ada0 is on ata0, while CD drive cd0 is on ata1.

Without device ata in the kernel configuration, the kernel would not recognize the ATA bus. Even if the system figured out that the system has a DVD drive, the kernel wouldn’t know the route to get information to and from it. Your kernel configuration must include all the intermediary devices for the drivers that rely on them. On the other hand, if your system doesn’t have ATA RAID drives, floppy drives, or tape drives, you can remove those device drivers from your kernel.

If this host had an AHCI, MVS, or SIIS controller, those device names would show up in dmesg instead of ata.

## Configuration Files

Fortunately, you don’t normally create a kernel configuration file from scratch; instead, you build on an existing one. Start with the GENERIC kernel for your hardware architecture. It can be found in /sys/<arch>/conf— for example, the i386 kernel configuration files are in /sys/i386/conf, the amd64 kernel configuration files are in /sys/amd64/conf, and so on. This directory contains several files, of which the most important are DEFAULTS, GENERIC, GENERIC.bints, MINIMAL, and NOTES:

- **DEFAULTS** This is a list of options and devices that are enabled by default for a given architecture. That doesn't mean that you can compile and run *DEFAULTS*, but it is a starting point should you want to build a kernel by adding devices. Using *GENERIC* is easier, though.
- **GENERIC** This is the configuration for the standard kernel. It contains all the settings needed to get standard hardware of that architecture up and running; this is the kernel configuration used by the installer.
- **GENERIC.hints** This is the hints file that is later installed as /boot/device.hints. This file provides configuration information for older hardware.
- **MINIMAL** This configuration excludes anything that can be loaded from a module.
- **NOTES** This is an all-inclusive kernel configuration for that hardware platform. Every platform-specific feature is included in *NOTES*. Find platform-independent kernel features in /usr/src/sys/conf/NOTES.

Many architectures also have architecture-specific configurations, needed only for that hardware. The i386 architecture includes the PAE kernel configuration, which lets you use more than 4GB of RAM on a 32-bit system. The arm architecture includes dozens of configurations, one for each of the many different platforms FreeBSD supports.

Sometimes, you'll find a kernel configuration that does exactly what you want. I want the smallest possible kernel. The *MINIMAL* kernel looks like a good place to start. Let's build it.

## Building a Kernel

A base install of FreeBSD, combined with the operating system source code, includes all the infrastructure you need to easily build a kernel. All you need to do is tell the system which kernel configuration to build through the KERNCONF variable. You can set KERNCONF in /etc/src.conf (or /etc/make.conf, if you're really old-school).

```
KERNCONF=MINIMAL
```

If you're experimenting with building and running different kernels, though, it's best to set the configuration file on the command line when you build the kernel. Build the kernel with the make buildkernel command.

```
# cd /usr/src
# make KERNCONF=MINIMAL buildkernel
```

The build process first runs config(8) to find syntactical configuration errors. If config(8) detects a problem, it reports the error and stops. Some errors are blatantly obvious—for example, you might have accidentally deleted support for the Unix File System (UFS) but included support for booting off of UFS. One requires the other, and config(8) will tell you exactly what's wrong. Other messages are strange and obscure; those that may take the longest to figure out are like this:

```
MINIMAL: unknown option "NET6"
```

NET6 is the IPv6 option, isn't it? No, that's I NET6. Apparently some doofus examined the config file in a text editor and accidentally deleted a letter. The error is perfectly self-explanatory—once you're familiar with all the supported kernel options. Read these errors carefully!

Once config(8) validates the configuration, the kernel build process takes a few minutes on a modern machine. A successful build ends with a message like this.

```
>>> Kernel build for MINIMAL completed on Tue Sep 12 14:27:08 EDT 2017
```

After building the kernel, install it. Running make installkernel moves your current kernel to /boot/kernel.old and installs the new kernel in /boot/kernel. Installing a kernel is much faster than building it.

## TRUSTING THE KERNEL

Eventually, you’ll get to where you trust your kernel configuration and want to build and install it in a single command. The `make kernel` command builds and installs the kernel. Truly intense sysadmins run `make kernel && reboot`.

Once the install completes, reboot your server and watch the boot messages. If everything worked, you’ll get something like the following, showing exactly what kernel is running and when it was built.

```
Copyright (c) 1992-2018 The FreeBSD Project.
Copyright (c) 1979, 1980, 1983, 1984, 1985, 1986, 1989, 1991, 1992, 1993, 1994
The Regents of the University of California.  All rights reserved.
FreeBSD storn 12.0-CURRENT FreeBSD 12.0-CURRENT #0 r323136: Sat Sep 2
21:46:53 EDT 2018     root@storm:/usr/obj/usr/src/sys/MINIMAL     amd64
--snip--
```

The catch is, the `MINIMAL` kernel doesn’t boot all hardware. It doesn’t boot *most* hardware. And of the hardware `MINIMAL` can boot, it won’t boot most FreeBSD installations on that hardware.

`MINIMAL` leaves everything that can be a module in a module. Disk partitioning methods, both GPT and MBR, can be modules. You must load either `geom_part_gpt.ko` or `geom_part_mbr.ko` via `loader.conf` to boot `MINIMAL`. Filesystems are modules too, so you have to load those. In short, you have to load every stupid module required by the hardware and your installation decisions. `MINIMAL` is a good reference of what all kernels need, and a decent place to start designing your own kernel, but insufficient for production.

## Booting an Alternate Kernel

So, what to do if your new kernel doesn’t work, or if it works badly? Perhaps you forgot a device driver or accidentally cut out the `INET` option and can’t access the internet. Sometimes it’ll hang up so early in
