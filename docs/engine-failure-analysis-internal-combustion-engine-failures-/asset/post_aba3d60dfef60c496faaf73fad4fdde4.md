
Defines a specific boot procedure to be used for two or more *boot images* (versions of the Linux kernel that are designed to be loaded by LILO). If more than one Per-image section is present, you can choose which one you want to use by default. You do so by typing a label at the LILO prompt. If you have configured your system to run Microsoft Windows 98 as well as Linux, press Tab at the LILO prompt to see what to type to start Windows.

The Global section contains options that govern all the Per-image sections. This section must begin with a boot entry that specifies the location of the master boot record (MBR). The following illustrates a Global section in /etc/lilo.conf:

```
## Global section
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
default=linux
```

This example is supplied for illustration only; the various commands must correspond to the partitions, directories, and boot images present on your system. The following table, Global Options, explains the entries that you can place in this section.

## GLOBAL OPTIONS

| Use This Entry | To Do This |
| :--- | :--- |
| backup=fname | Copy the original boot sector to the specified backup filename. |
| boot=device | Specify the name of the device that contains the boot sector. |
| compact | Attempt to merge sector read requests, which can shorten load time when booting from a floppy. |
| default=name | Use the specified image name as the default boot image. |
| delay=time | Set the delay time (in seconds) before booting from the first image. |
| force-backup=filename | Copy the original boot sector to the specified backup filename. Overwrites the old backup copy. |
| ignore-table | Ignore corrupt partition tables. |
| install=filename | Install the specified filename as the new boot sector. |
| linear | Generate linear sector addresses instead of sector/head/cylinder addresses. |
| lock | Enable automatic recording of boot command lines as the defaults for the following boots. |
| map=filename | Specify the location of the map file. |
| message=filename | Specify a filename containing a message that is displayed before the boot prompt. |
| nowarn | Disable warnings about possible future dangers. |
| optional | Apply the per-image option optional to all images. |
| password=password | Apply the per-image option password to all images. |
| prompt | Forces manual initiation of the boot process unless timeout is set. |
| restricted | Apply the per-image option restricted to all images. |
| serial=port, bps, [parity] [bits] | Enable control from a serial line. You must specify the serial port, and you can optionally specify the bits per second (bps), parity (n for no parity, e for even parity, or o for odd parity), and the number of bits per character (7 or 8). |
| timeout=seconds | Specify a timeout for keyboard input. If no input is received, the boot process begins using the default settings. |
| verbose=level | Control the amount of progress reporting with a level from 1 (low reporting) to 5 (high reporting). |

### Per-Image Options

Each Per-image section defines a specific boot procedure that can be initiated by typing its label (see label in the following table).

The following illustrates a Per-image section for booting Linux:

```
image=/boot/vmlinuz-2.2.12-20
label=linux
initrd=/boot/initrd-2.2.12-20.img
read-only
root=/dev/hda1
```

A Linux Per-image section must begin with an image entry. This entry specifies where the Linux boot image can be found.

This Per-image section illustrates a Windows 98 boot alternative:

```
other=/dev/hda1
label=windows
loader=/boot/chain.b
table=/dev/hda
```

A Windows, DOS, or OS/2 section must begin with another entry that specifies where the alternative operating system can be found.

The options for Linux and other operating systems differ. The following tables explain the options available for each.

#### PER-IMAGE OPTIONS FOR LINUX

| Use This Entry | To Do This |
| :--- | :--- |
| alias=name | Specify a second name for this image. |
| append=string | Pass the specified string to the kernel. |
| image=path name | Specify the path name to the file or device containing a boot image of the Linux kernel. If you are configuring a device, you must also specify the range. |
| label=name | Display this name to identify the image. |
| literal=string | Pass the specified string to the kernel and remove all other options. |
| lock | Enable automatic recording of boot commands as the default for the next boot. |
| optional | Omit the image if it is not available at map creation time. |
| password=password | Require entry of the specified password to boot the image. |
| ramdisk=size | Specify the size of the optional RAM disk. |
| range=start end | Specify the start and end sectors of the image; required only if the image option points to a device rather than a filename. |
| read-only | Mount the filesystem in read-only mode. |
| read-write | Mount the filesystem in read-write mode. |
| restricted | Require a password only if boot parameters are specified on the command line. |
| root=device | Mount the specified device as root. |
| vga=mode | Select the VGA mode to be used during booting. Available options are:<br>**normal**: Select normal 80x25 text mode.<br>**extended**: Select 80x50 text mode.<br>**ask**: Ask for user input at boot time. |

#### PER-IMAGE OPTIONS FOR OPERATING SYSTEMS OTHER THAN LINUX

| Use This Entry | To Do This |
| :--- | :--- |
| alias=name | Specify a second name for this image. |
| label=name | Display this name to identify the image. |
| loader=loader | Specify the loader to be used. |
| lock | Enable automatic recording of boot commands as the default for the next boot. |
| optional | Omit the image if it is not available at map creation time. |
| other=path name | Specify the path name to an alternative operating system. |
| password=password | Require entry of the specified password to boot the image. |
| restricted | Require a password only if boot parameters are specified on the command line. |
| table=device | Specify the device that contains the partition table. |

## Configuring Init Processes

After the boot process begins, a script called init starts automatically. This script begins by reading the default startup configuration file, called `/etc/inittab`. An important configuration option in this file concerns the default run level. A run level is an overall configuration that determines whether the Linux system is connected to the network and whether the X Window System starts automatically. When the default run level has been determined, init turns the system over to a system utility called getty. This utility opens up terminal connections and displays the login prompt. Then getty turns the system over to yet another utility, called login, which accepts the user's login name and password. In addition to getty and login, init launches the X server, as long as the default run level is the one that starts X automatically.

Typically, Linux distributions come with pre-configured init, getty, and login utilities, so you needn't worry about them. Most Linux installation utilities enable you to select the default run level. However, you may wish to change the default run level later, so it's wise to learn how your Linux distribution defines the various run levels, as explained in the next section.

## Understanding Run Levels

In the file /etc/inittab, you will find a section containing a line such as the following:

```
id:5:initdefault:
```

This statement specifies the default run level setting by means of a number (5 in this example). The following table, Run Levels, explains what these numbers stand for. For example, if you replace 5 with 3, Linux will start in console mode. Run levels 0, 1, 2, 3, and 6 are reasonably well standardized among Linux distributions. However, some distributions use 4 to start X automatically, while others use 5. Consult your Linux system's documentation, or the comments in /etc/inittab, to determine which run level starts X in the distribution that you are using.

> **WARNING**: Do not make any changes to /etc/inittab other than changing the run level number! If you do, your system may not start. Also, be aware that you shouldn't choose run level 0 or 6 as the default run level: You don't want your system to halt or reboot the minute you start it.

### RUN LEVELS

| Run Level | Description |
| :--- | :--- |
| 0 | Halts the system. |
| 1 | Single user mode (useful for troubleshooting). |
| 2 | Multi-user system (console mode) without Network Filesystem (NFS) support. |
| 3 | Full multi-user console mode (text-only). |
| 4 | Starts X Window System automatically or unused. |
| 5 | Starts X Window System automatically or unused. |
| 6 | Reboots. |
