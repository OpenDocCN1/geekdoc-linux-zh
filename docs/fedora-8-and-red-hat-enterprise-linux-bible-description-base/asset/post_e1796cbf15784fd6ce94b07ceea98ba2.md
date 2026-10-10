
# Configuring modules

In a perfect world, after installing and booting Linux, all of your hardware should be detected and available for access. While Fedora and Red Hat Enterprise Linux systems are rapidly moving closer to that world, there are times when you must take special steps to get your computer hardware working.

Fedora and RHEL systems come with tools for configuring the drivers that stand between the programs you run (such as Web players and Web browsers) and the hardware they use (such as CD-ROM drives and network cards). The intention is to have only the most critical drivers your system needs built into the kernel; these are called resident drivers. Other drivers that are added dynamically as needed are referred to as loadable modules. The trend is to keep the basic kernel as lean as possible, so that each running system has only a few resident drivers and it can dynamically add what it needs.

The following is a list of actions kudzu takes when a device is added:

- **Sound card** — Runs the sndconfig command to configure and test the sound card.
- **Mouse** — Runs the mouseconfig command to configure and test the mouse.
- **Modem** — Links the new modem device to /dev/modem.
- **CD-ROM** — Links the CD-ROM device to /dev/cdrom.
- **Scanner** — Links the new scanner device to /dev/scanner.
- **Keyboard** — Runs the kbdconfig command to reconfigure the keyboard. Also, if you are using a serial console, it makes sure /etc/inittab and /etc/security/tty are configured to be used by a serial console.

The following is a list of actions kudzu takes when a device is removed:

- **Network** — Removes the alias for the Ethernet interface (eth0, eth1, and so on).
- **SCSI** — Removes the alias for the SCSI host adapter (scsi hostadapter).
- **Modem** — Removes the link to /dev/modem.
- **CD-ROM** — Removes the link to /dev/cdrom.
- **Scanner** — Removes the link to /dev/scanner.

To run kudzu, either reboot (during the reboot, kudzu is run automatically) or simply run the kudzu command (as root user from a shell). For any hardware that has been added or removed since the last time kudzu was run, you are asked if you want to configure it, not configure it, or do nothing.

> **NOTE:** Removable devices, such as digital cameras, USB flash drives, and Webcams, are detected and configured on-the-fly using the hald daemon. The hald daemon relies on the Udev device management facility to dynamically create devices and mount points (if needed) when those types of devices are connected. See Chapter 8 for descriptions of how CDs and digital cameras are detected.

### Listing loaded modules

To see which modules are currently loaded into the running kernel on your computer, you can use the `lsmod` command. Here's an example:

```bash
# lsmod
Module                  Size  Used by
snd_seq_oss            38912  0
snd_seq_midi_event      9344  1 snd_seq_oss
snd_seq                67728  4 snd_seq_oss,snd_seq_midi_event
snd_seq_device           8328  2 snd_seq_oss,snd_seq
.
.
.
autofs                 16512  0
ne2k_pci               9056  0
8390                  13568  1 ne2k_pci
ohci1394               41860  0
ieee1394               284464  1 ohci1394
floppy                 65712  0
sg                     36120  0
scsi_mod               124600  1 sg
parport_pc             39724  0
parport                47336  1 parport_pc
ext3                  128424  2
jbd                    86040  1 ext3
```

This output shows a variety of modules that have been loaded on a Linux system. The modules loaded on this system include several to support the ALSA sound system, including some that provide OSS compatibility (`snd_seq_oss`).

To find information about any of the loaded modules, you can use the `modinfo` command. For example, you could type the following:

```bash
# modinfo snd-seq-oss
filename:       /lib/modules/2.6.23.1-31.fc8/kernel/sound/core/seq/oss/snd-seq-oss.ko
alias:          sound-service-7-1
alias:          sound-service-7-8
license:        GPL
Description:    OSS-compatible sequencer module
author:         Takashi Iwai <tiwai@suse.de>
version:        B37509B8403309A4C7CE5D7
depends:        snd,snd-seq,snd-seq-midi-event,snd-seq-device
vermagic:       2.6.23-0.61.git5.fc8 SMP mod_unload 686 4KSTACKS
parm:           maxqlen:maximum queue length (int)
parm:           seq_oss_debug:debug option (int)
```

This output tells you the location of the module (filename), the author, and description, among other information. The output describes `snd-seq-oss` as an OSS-compatible sequencer module.

You can use the `-d` option to list just the description, the `-a` option to see the author of the module or `-n` to see the object file representing the module. The author information often has the e-mail address of the driver's creator, so you can contact the author if you have problems or questions about it.

### Loading modules

You can load any module that has been compiled and installed (to the /lib/modules directory) into your running kernel using the modprobe command. The most common reasons for loading a module are that you want to use a feature temporarily (such as loading a module to support a special file system on a floppy you want to access) or to identify a module that will be used by a particular piece of hardware that could not be autodetected.

Here is an example of the modprobe command being used to load the parport module. The parport module provides the core functions to share parallel ports with multiple devices.

```bash
# modprobe parport
```

After parport is loaded you can load the parport_pc module to define the PC-style ports available through the interface. The parport_pc module lets you optionally define the addresses and IRQ numbers associated with each device sharing the parallel port. For example:

```bash
# modprobe parport_pc io=0x3bc irq=auto
```

In the previous example, a device is identified as having an address of 0x3bc. The IRQ for the device is autodetected.

The modprobe command loads modules temporarily. At the next system reboot, the modules you enter disappear. To permanently add the module to your system, add the modprobe command line to one of the start-up scripts that are run at boot time.

> **NOTE:** An alternative to using modprobe is the insmod command. The advantage of using modprobe, however, is that insmod will only load the module you request, while modprobe will try to load other modules that the one you requested is dependent on.

### Removing modules

You can remove a module from a running kernel using the rmmod command. For example, to remove the module parport_pc from the current kernel, type the following:

```bash
# rmmod parport_pc
```

If the module is not currently busy, the parport_pc module is removed from the running kernel. (Instead of rmmod, you can use modprobe -r to remove the module, plus related modules.)

> **NOTE:** There are times when a piece of hardware is improperly detected and a module is loaded that is either the wrong module or is simply a broken module. In that case, you can consider adding the name of the offending driver to the `/etc/modprobe.d/blacklist` file, to prevent that module from being loaded. After that, you can consider loading the proper module manually or by adding a `modprobe` command to load the module you want from a system startup file.

## Managing File Systems and Disk Space

File systems in Linux are organized in a hierarchy, beginning from root ( `/` ) and continuing downward in a structure of directories and subdirectories. As an administrator of a Fedora or RHEL system, it is your duty to make sure that all the disk drives that represent your file system are available to the users of the computer. It is also your job to make sure there is enough disk space in the right places in the file system for users to store what they need.

File systems are organized differently in Linux than they are in Microsoft Windows operating systems. Instead of drive letters (for example, A:, B:, C:) for each local disk, network file system, CD-ROM, or other type of storage medium, everything fits neatly into the directory structure. For hard drive partitions, it is up to an administrator to create a mount point in the file system and then connect the disk to that point in the file system. For removable media (such as CD, DVD, USB flash drives, or digital cameras), mount points are automatically created and connected (in the `/media` directory) when those items are connected or loaded.

> **CROSS-REFERENCE:** Chapter 2 provides instructions for using Disk Druid to configure disk partitions. Chapter 4 describes how the Linux file system is organized.

The organization of your file system begins when you install Linux. Part of the installation process is to divide your hard disk (or disks) into partitions. Those partitions can then be assigned to:

- A part of the Linux file system,
- Swap space for Linux, or
- Other file system types (perhaps containing other bootable operating systems)

For our purposes, I want to focus on partitions that are used for the Linux file system. To see what partitions are currently set up on your hard disk, use the `fdisk` command as follows:

```bash
# fdisk -l
Disk /dev/sda:  40.0 GB, 40020664320 bytes
255 heads, 63 sectors/track, 4825 cylinders
Units = cylinders of 16063 * 512 bytes = 825280 bytes
```

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| /dev/sda1 | * | 1 | 13 | 104 | b | Win95 FAT32 |
| /dev/sda2 | | 84 | 89 | 48195 | 83 | Linux |
| /dev/sda3 | | 90 | 522 | 3478072+ | 83 | Linux |
