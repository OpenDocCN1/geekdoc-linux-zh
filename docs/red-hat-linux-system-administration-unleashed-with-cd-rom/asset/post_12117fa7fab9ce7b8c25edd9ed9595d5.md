
## Kernel Panic

One of the more disconcerting things that can happen on a Linux system is to have the kernel detect something wrong and call a halt to the proceedings. This safety-valve feature is actually a normal part of the kernel communication process.

If the kernel encounters a fatal condition, such as attempting to use a memory address that is no longer available, it issues a “kernel panic.” The kernel will halt operation and printk() will display the error message on the console, then wait for someone to come along, note the message, and reboot the system. For unattended systems, it is sometimes preferable to have the system log the message then reboot itself automatically, if possible. This can be achieved by adding the following line to the appropriate stanza in /etc/lilo.conf:

```
panic=30
```

This instructs the system to attempt to reboot itself thirty seconds after encountering an oops condition.

### Tip

> A LILO trick that is sometimes useful for troubleshooting is to raise the threshold of messages that the kernel printk() displays on the console. The default is to log anything greater than DEBUG level. If you add the debug option to /etc/lilo.conf (or manually boot the system as linux debug at the LILO prompt), it changes the console log level to DEBUG level, which displays all kernel messages on the console.

Some conditions are too severe for the system to be able to continue, such as when the boot process cannot find a Linux filesystem to mount. In this situation, printk() will display a kernel panic on the system console that will prompt you to further investigate the situation. In a worst-case scenario, the system might hang with no explanation. This is the most difficult type of problem to resolve. When severe problems occur, the first thing to look for is a hardware error.

## Hardware Errors

With any Intel or Intel-compatible computer, hardware errors can be caused by a number of conditions, including hardware interrupt conflicts, faulty device drivers, BIOS problems on the system board, or hardware component failure. Diagnosing hardware errors follows a time-honored pattern: Look first for obvious problems and if that leads nowhere, look deeper for more subtle causes.

Start by checking all the obvious things such as internal and external cables, power supplies, power cables, network activity lights, powerbar switches, and UPS switches. A routine but careful examination of the physical environment can often save wasted effort. It's self-defeating to work hard at restoring a hard disk, only to find hours later that the problem was merely a loose connector.

There are two times when hardware problems are most likely to occur:
- When you first build your Red Hat system on an Intel PC, and
- When you add or change hardware.

If your system has been running without problems and no changes have been made, it is possible that an existing hardware component has failed or that a driver has become corrupted.

### Identifying Hardware Errors at Startup

Red Hat 6 provides a considerable amount of help in identifying hardware errors at startup. The startup messages identify hardware devices that have been probed successfully. If you're at the console, you can scroll backwards, using Ctrl-PageUp, to examine messages that have already scrolled by. On successfully probed ports, Red Hat 6 displays an OK message in green on a color monitor.

If it's too late to scroll back the console monitor, Red Hat offers two additional ways to view startup messages. You can replay these messages by typing /bin/dmesg (as shown in the previous chapter), and Red Hat supplies another file, /var/log/boot.log, that can be scanned for additional diagnostic messages:

```
[root@wallace /root]# less /var/log/boot.log

Aug 26 15:20:37 wallace fsck: /dev/hda4: clean, 64978/499712 files, 1061324/1992060 blocks
Aug 26 15:20:37 wallace rc.sysinit: Checking root filesystem succeeded
Aug 26 15:20:37 wallace isapnp: Board 1 has Identity 61 10 00 4b 14 51 00 0c 0e:
CTL0051 Serial No 268454676 [checksum 61]
Aug 26 15:20:37 wallace isapnp: CTL0051/268454676(){Audio}: Ports 0x220 0x330 0x388; IRQ5 DMA1 DMA5 ... Enabled OK
Aug 26 15:20:37 wallace isapnp: CTL0051/268454676[2](Game): Ports 0x200; ... Enabled OK
Aug 26 15:20:37 wallace rc.sysinit: Setting up ISA PNP devices succeeded
```

This file is a variant of /var/log/dmesg and it provides another place to look for information that might help diagnose hardware problems. It supplies information from processes such as isapnp, a program that attempts to set Plug-and-Play devices.

The classic condition to watch for when experiencing a hardware problem is "last change syndrome." The last piece of hardware you changed, or added, is likely to be the culprit. These changes can be subtle, such as substituting a 3Com 905B network card for a 3Com 905 card. Unless your device driver is current enough to support the 905B, the network card will stop working, and a failure to initialize the card will be displayed in the startup messages.

If you have added a second drive and you receive a "Kernel panic: VFS: Unable to mount root fs ..." message during a LILO boot, check the cabling. If you accidentally plugged your primary drive internal cable into the secondary controller, on an EIDE drive, your /dev/hda drive will be seen as /dev/hdc and Linux will not boot. Restoring the cable to its original system-board connector will resolve the problem.

## BIOS Problems

Linux gets deployed on a wide range of Intel-compatible hardware and sometimes a particular system-board BIOS will cause problems. If you're experiencing quirky, intermittent hardware glitches, try switching off any special features in the system BIOS. You might also check with the manufacturer's Web site to see if there's an upgrade to the BIOS. Upgrades have been known to cure certain system board incompatibilities with Linux.

## Plug-and-Play (PnP) Devices

Plug-and-Play is a specification that is designed to allocate four specific resources to drivers and hardware: I/O addresses, IRQs, DMA channels (ISA bus only), and memory regions. Some BIOSes do a good job of detecting and configuring PnP devices and some don't. If the BIOS doesn't adjust the device correctly, the device can be left in a disabled state.

If you're attempting to install an ISA PnP card that is not being detected by Linux, check to see if PnP can be disabled with a DOS utility. A PnP card usually includes a DOS utility diskette that can be used to adjust the card's settings. If the DOS utility has been misplaced or lost, the utility is often available from the manufacturer's Web site. It is often easier to configure a card manually than to get PnP to work when it's being stubborn. In certain cases, however, you might not want to do this. If you have a Linux/Windows dual-boot system, for instance, Windows may be depending on the card's PnP settings or you may not have access to the DOS utilities required to switch off PnP. Some cards are PnP only, offering no option for disabling this feature.

Alternatively, you can attempt to adjust the settings with the Linux isapnp utility. This is discussed in the section "Diagnostic Tools," later in the chapter.

## PCI Devices

Occasionally, newer PCI devices will not be recognized and initialized correctly. If this happens you will see the following kernel message:

```
Warning : Unknown PCI device (8086:7100). Please read include/linux/pci.h
```

This can be caused by your system board chipset PCI-CPU bridge or PCI-ISA bridge. Your first step is to try to find which PCI device is causing the problem. Check /proc/pci for information to see if there are any obvious clues. The following listing shows how to display the contents of /proc/pci:

```
[root@wallace /root]# cat /proc/pci
PCI devices found:
Bus 0, device 7, function 0:
  Host bridge: Intel 82439HX Triton II (rev 1).
    Medium devsel.  Master Capable.  Latency=32.
Bus 0, device 7, function 0:
  ISA bridge: Intel 82371SB PIIX3 ISA (rev 0).
    Medium devsel.  Fast back-to-back capable.  Master Capable.  No bursts.
Bus 0, device 7, function 1:
  IDE interface: Intel 82371SB PIIX3 IDE (rev 0).
    Medium devsel.  Fast back-to-back capable.  Master Capable.  Latency=32.
    I/O at 0xffa0 [0xffa1].
Bus 0, device 17, function 0:
  VGA compatible controller: Matrox Millennium II (rev 0).
    Medium devsel.  Fast back-to-back capable.  IRQ 11. Master Capable.
    Latency=32.
    Prefetchable 32 bit memory at 0xf0000000 [0xfd000008].
    Non-prefetchable 32 bit memory at 0xfffac000 [0xfffac000].
    Non-prefetchable 32 bit memory at 0xfff00000 [0xfff00000].
```
