
There are additional arguments, such as `mkfr` (for controlling the video clock) and `pil`, which are not documented (except in the Linux kernel source). The Linux kernel recognizes many different arguments. Different video drivers (such as Matrox) can recognize more than 40!

If you click on the BootX Options button, you see a dialog box, as shown in Figure 4.2. Use this dialog box to enable cache on G3 PowerPC Macs, force the use of SCSI, force video settings, or select a RAMdisk image (only required during a Linux install—which may be discarded afterwards). When finished, click OK or Cancel to return to the main dialog box. Use Cmd+s to save your BootX preferences at any time.

When you turn on your Power Mac, BootX appears shortly after the initial Mac OS dialog box. You have about 10 seconds to choose either the Mac OS or Linux.

### Configuring Yaboot

Yaboot, like BootX, is a bootloader for PPC Linux. This is the preferred bootloader to use with NewWorld Power Macs, and is relatively easy to configure. You will need to know the partition number of your root Linux partition, along with any desired kernel arguments. This loader, also by Ben Herrenschmidt, attempts to boot Linux using Apple’s Open Firmware. If Yaboot is properly configured, it does not require the use of the Open Firmware prompt (accessed by holding down the Opt+Cmd+o+f keys at startup).

The basic approach to using this bootloader is to create a small, separate Mac OS HFS volume to hold a pseudo-System Folder, Finder, Yaboot, a PPC Linux kernel, and Yaboot’s configuration file named `yaboot.conf` (see Figure 4.3).

![](img/1ea833f5a3e3c1547e3dd2891f52804a_92_0.png)

![](img/1ea833f5a3e3c1547e3dd2891f52804a_93_0.png)

Figure 4.3 *The pseudo-System Folder on a Mac OS HFS boot volume contains everything you need to boot Linux.*

Another boot method you may want to explore is Ethan Benson's ybin. This utility, used in conjunction with Yaboot, offers some additional flexibility, and automatically configures an Apple Open Firmware boot script according to Yaboot's configuration file. For details, browse to http://www.alsaka.net/–erbenson/ybin/.

### Configuring LILO

SuSE PPC Linux includes a special version of the LILO (*Linux Loader*) for use with PPC Linux. This version obeys much of the syntax used in the version for Intel-based PCs, and works at the boot prompt nearly the same way. LILO was originally designed for Intel-based PC hardware. As a bootloader and boot utility, LILO is typically installed in the MBR (*Master Boot Record*) or in the root Linux partition on an IDE drive to support booting to Linux or other operating systems. A configuration file named *lilo.conf*, located under the /etc directory, contains directions and a roadmap for LILO's install and operation.

Under SuSE's PPC Linux, LILO is used to create files under the /boot directory that contain directions and a roadmap for booting either Mac OS or Linux. The /etc/lilo.conf contains a picture of your system, which is familiar to Intel Linux users. For example:

```
# partition of the HFS volume holding the pseudo System Folder
boot=/dev/hda10
# how long to wait before booting the default
timeout=100

# the default OS to boot (according to label=)
default=linux
# the kernel to boot Linux
image=/boot/vmlinux
label=linux
# insert any required/desired kernel arguments
append=""
# the root Linux partition
root=/dev/hda11
# boot to an installation (e.g., type "install" at LILO prompt)
image=/boot/vmlinux
label=install
append="ramdisk_size=10000"
root=/dev/fd0
inirld=/boot/initdisk.gz
# boot MacOS (e.g., type "macos" at LILO boot prompt)
other=/dev/hda9
label=macos
```

In this example, the standard HFS volume containing yaboot and a pseudo-System Folder is located on /dev/hda10. The primary Mac OS partition is /dev/hda9. The root Linux directory is installed in /dev/hda11. After typing in your /etc/lilo.conf, you should then run LILO at the Linux command line (as root) like this:

```
# lilo
```

LILO will then create the necessary files under the /boot directory.

Using LILO may or may not work on your system. Due to the way SuSE PPC Linux is configured, LILO can generally be used, and is a part of the booting solution. However, other PPC Linux distributions, such as LinuxPPC 2000 Q4, offer a more simplified booting operation using Yaboot.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_94_0.png)

You will find Power Mac-specific information regarding LILO under your SuSE PPC Linux /usr/share/doc/packages/lilo directory. LILO is not used with other PPC distributions.

## Understanding Open Firmware

The Open Firmware prompt is basically a command-line interface to a FORTH-like interpreter. The FORTH language, originally designed in 1970 by astronomer Chuck Moore for control of telescopes, is popular because it is a compact, portable, and extensible language that is ideal for ROM-based solutions. FORTH has been used in many different types of embedded devices, including many commercial arcade games.

Apple implemented its NewWorld Power Mac boot language, named Open Firmware, to allow equipment flexibility and boot-time configuration. It is not necessary to learn how to program in FORTH (which is stack-oriented and uses postfix notation) in order to boot Linux on your Power Mac. However, you will benefit by knowing how to access the prompt, and understanding a few Open Firmware keywords.

SuSE PPC Linux uses a script that contains Open Firmware language to help configure and boot Linux. Part of this script, named os-chooser (which resides in the pseudo System Folder named suseboot) contains:

```
* get-key-map* " keyboard* open-dev $call-method
dup 20 dump
5 + C@ 08 = if
* Booting MacOS ..." cr " boot hd:9,\\tbxi\ eval
else
* Booting Yaboot ..." cr " boot hd:10,\\yaboot* eval
```

In this example, Linux is started by loading Yaboot from /dev/hda10, a standard HFS boot volume created during the Linux install. Yaboot then boots Linux. Open Firmware’s role in booting Linux is to start Yaboot, which contains directions to boot Linux or Mac OS.

You can boot your Power Mac directly to the Open Firmware prompt by holding down the Cmd+Option+o+o keys after turning on your machine. The screen will clear, and you will be at the Open Firmware prompt.

Open Firmware contains default settings that correspond to your particular Power Mac. You should exercise caution in modifying existing settings unless you know what you are doing. If you run into trouble, use the reset-all command to reset settings back to default. Use the printenv command to see a list of current settings.

Changes are typically made to Open Firmware environment settings in order to define or create boot variables, such as the definition of a Linux or Mac OS partition, and to create commands to boot Linux or the Mac, perhaps using the boot keyword (which exits Open Firmware). Problems can occur in booting Mac OS if the Open Firmware variable boot-device is incorrectly configured.

Hopefully, as PPC Linux matures, more user-friendly boot configuration interfaces will be created. For now, follow the directions included with your SuSE PPC, LinuxPPC 2000, or Yellow Dog Linux manuals when working with Open Firmware.

## Troubleshooting

Problems most often occur in attempting to boot Linux due to incorrect bootloader configuration. Other problems include using an incorrect kernel, inappropriate kernel arguments, a kernel that has been compiled without support for the correct type of hard drive, or specifying the wrong type of video hardware.

Problems that involve incorrect Yaboot configurations can be avoided by writing down a partition map of your system, making sure to note partitioning numbers during installation, or by using a partition editor to acquire partition information.

One helpful utility is the `pdisk` command, a counterpart to the Intel-based `fdisk` command. You can use `pdisk` while running Linux to quickly get a snapshot of your system by using the `-l`, or list, option like this:

```
$ pdisk -l
```

```
Partition map (with 512 byte blocks) on '/dev/hda'

#:	type name			length	base		(size )
1:	Apple_partition_map 'Apple				63 @ 1
2:	Apple_Driver43* 'Macintosh		54 @ 64
3:	Apple_Driver43* 'Macintosh		74 @ 118
4:	Apple_Driver_ATA*' 'Macintosh		54 @ 192
5:	Apple_Driver_ATA* 'Macintosh		74 @ 246
6:	Apple_FWDriver* 'Macintosh		200 @ 320
7:	Apple_Driver_10Kit ' 'Macintosh	512 @ 520
8:	Apple_Patches 'Patch Partition'	512 @ 1032
9:	Apple_HFS* 'Macintosh HD	12400855 @ 1544	( 5.9G)
10:	Apple_HFS	'/'boot			65536 @ 12402399	( 32.0M)
11:	Linux_PPC	'/'				12400854 @ 12467935	( 5.9G)
12:	Linux_PPC	'/'swap			646087 @ 24868789	( 315.5M)
13:	Linux_PPC	'/'d2				14495644 @ 25514876	( 6.9G)
14:	Apple_Free	'Extra				24 @ 40010520

Device block size=512, Number of Blocks=40010543 (19.1G)
```
