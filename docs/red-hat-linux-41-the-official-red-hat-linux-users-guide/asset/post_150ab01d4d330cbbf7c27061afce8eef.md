
from Windows NT").

## EB164

The EB164, like all of the Alpha Evaluation Boards built by Digital, contains the Evaluation Board Debug Monitor and so this is available to load Milo (Section E.5.2 Loading from the Debug Monitor). Quite often (although not always), boards whose design is derived from these include the Debug Monitor also. Usually, these boards include the Windows NT ARC firmware (Section E.5.1 booting from Windows NT ARC firmware). The SRM console is also available (Section E.5.5 Loading Milo from the SRM Console). A flash management utility, runnable from Milo, is available so that once Milo is running, it can be blown into flash (Section E.7 running the flash management utility). This system supports Milo environment variables.

These systems have several boot images in flash controlled by jumpers. The two jumper bank is J1 and is located at the bottom of the board on the left (if the Alpha chip is at the top). You select between the boot options (and Milo when it has been put into flash) using a combination of jumpers and a boot option which is saved in the NVRAM of the TOY clock.

Jumper SP-11 of J1 in means boot the image described by the boot option. Jumper SP-11 of J1 out means boot the Evaluation Board Debug Monitor.

Blowing an image into flash via the Evaluation Board Debug Monitor is exactly the same procedure as for the AlphaPC64 (Section E.5.6 AlphaPC64).

## XL266

The XL266 is one of a family of systems that are known as Avanti. It has a riser card containing the Alpha chip and cache which plugs into the main board at right angles. This board can replace the equivalent Pentium board.

Some of these systems ship with the SRM console but others, notably the XL266, ship with only the Windows NT ARC firmware (Section E.5.1 booting from Windows NT ARC firmware).

Here is my list of compatible systems:

- AlphaStation 400 (Avanti),
- AlphaStation 250,
- AlphaStation 200 (Mustang),
- XL. There are two flavours, XL266 and XL233 with the only difference being in processor speed and cache size.

Note: The system that I use to develop and test Milo is an XL266 and so this is the only one that I can guarantee will work. However, technically, all of the above systems are equivalent; they have the same support chipsets and the same interrupt handling mechanisms.

## Platform2000

This is a 233MHz 21066 based system.

## E.6 Milo’s User Interface

Once you have correctly installed/loaded/run Milo, you will see the MILO (for MIniLOader) prompt displayed on your screen. There is a very simple interface that you must use in order to boot a particular Linux kernel image. Typing “help” is a good idea as it gives a useful summary of the commands.

### E.6.1 The "help" Command

Probably the most useful command that Milo has:

```text
MILO> help
MILO command summary:

ls [-t fs] [dev:[dir]]
    - List files in directory on device
boot [-t fs] [dev:file] [boot string]
    - Boot Linux from the specified device and file
run [-t fs] dev:file
    - Run the standalone program dev:file
show
    - Display all known devices and file systems
set VAR VALUE
    - Set the variable VAR to the specified VALUE
unset VAR
    - Delete the specified variable
reset
    - Delete all variables
print
    - Display current variable settings
help [var]
    - Print this help text
```

Devices are specified as: fd0, hda1, hda2, sdal…
Use the '-t *filesystem-name*' option if you want to use anything but the default *filesystem* ('ext2').
Use the 'show' command to show known devices and *filesystems*.
Type 'help *var*' for a list of variables.

**Note** that the *bootopt* command only appears on AlphaPC64 (and similar) systems. Refer to the board's documentation to find out just what it means.

**Devices** Until you use a command that needs to *make use* of a device, no device initialisation will take place. The first *show, ls, boot* or *run* commands all cause the devices within Linux to be initialised. Devices are named in the same way (exactly) that Linux itself will name them. So, the first IDE disk will be called 'hda' and its first partition will be 'hda1'. Use the *show* command to show what devices are available.

**File Systems** Milo supports three *file systems, MS DOS, EXT2* and *ISO9660*. So long as a device is available to it, Milo can *list, boot* or *run* an image stored on one of these *file systems*. Milo's default *file system* is *EXT2* and so you have to tell Milo that the *file system* is something other than that. All of the commands that use *filenames* allow you to pass the *file system* using the *-t [filesystem]* option. So, if you wanted to list the contents of a SCSI CD ROM, you might type the following:

*MILO> ls -t iso9660 scd0:*

**Variables** Milo contains some settable variables that help the *boot* process. If you are loading via the Windows NT ARC firmware, then Milo makes use of the *boot* option environment variables set up by that firmware. For some systems, Milo (for example, the AlphaPC64) maintains its own set of environment variables that do not change from *boot* to *boot*. These variables are:

```text
MILO> help var
Variables that MILO cares about:
MEMORY_SIZE  - System memory size in megabytes
BOOT_DEV     - Specifies the default boot device
BOOT_FILE    - Specifies the default boot file
BOOT_STRING  - Specifies the boot string to pass to the kernel
SCSI0_HOSTID - Specifies the host id of the n-th SCSI controller
AUTOBOOT     - If set, MILO attempts to boot on powerup
              and enters command loop only on failure.
AUTOBOOT_TIMEOUT - Seconds to wait before auto-booting on powerup.
```

### E.6.2 Booting Linux

The boot command boots a linux kernel from a device. You will need to have a linux kernel image on an EXT2 formatted disk (SCSI, IDE or floppy) or an ISO9660 formatted CD available to Milo. The image can be gzip'd and in this case Milo will recognise that it is gzip'd by the .gz suffix.

You should note that the version of Milo does not usually have to match the version of the Linux kernel that you are loading. You boot Linux using the following command syntax:

```text
MILO> boot [-t file-system] device-name:file-name [boot-option(s)]
```

Where device-name is the name of the device that you wish to use and file-name is the name of the file containing the Linux kernel. All arguments supplied after the file name are passed directly to the Linux kernel.

If you are installing Red Hat, then you will need to specify a root device and so on. So you would use:

```text
MILO> boot fd0:vmlinux.gz root=/dev/fd0 load_ramdisk=1
```

Milo will automatically contain the block devices that you configure into your vmlinux. I have tested the floppy driver, the IDE driver and the NCR SCSI driver, these work fine. Also, it is important to set the host id of the SCSI controller to a reasonable value. By default, MILO will initialize it to the highest possible value (7) which should normally work just fine.

However, if you wish, you can explicitly set the host id of the $n$-th SCSI controller in the system by setting environment variable SCSIn_HOSTID to the appropriate value. For example, to set the hostid of the first SCSI controller to 7, you can issue the following command at the MILO prompt:

```text
setenv SCSIO_HOSTID 7
```

### E.6.3 Rebooting Linux

You may want to reboot a running Linux system using the **shutdown -r now** command. In this case, the Linux kernel returns control to Milo (via the HALT CallPAL entrypoint). Milo leaves a compressed copy of itself in memory for just this reason and detects that the system is being rebooted from information held in the HWRPB (Hardware Restart Parameter Block). In this case it starts to boot reusing exactly the same command that was used to boot the Linux kernel the last time. There is a 30 second timeout that allows you to interrupt this process and boot whatever kernel you wish in whatever way you wish.

### E.6.4 The “bootopt” command

For flash based systems such as the AlphaPC64, EB164 and the EB66+, there are a number of possible boot options and these are changed using the **bootopt** command. This has one argument, a decimal number which is the type of the image to be booted the next time the system is power cycled or reset:

- 0: Boot the Evaluation Board Debug Monitor.
- 1: Boot the Windows NT ARC firmware.

In order to tell the boot code to boot the Milo firmware from flash then you need a boot option that means boot the N$^{th}$ image. For this, you need to 128 plus N, so if Milo is the third image, you would use the command:

```text
MILO> bootopt 131
```

**Note:** Be very careful with this command. A good rule is never to set bootopt to 0 (the Evaluation Board Debug Monitor), but instead use the system's jumpers to achieve the same thing.
