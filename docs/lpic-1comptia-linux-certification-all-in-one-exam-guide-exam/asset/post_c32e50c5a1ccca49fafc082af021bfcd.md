
## Configuring LILO

The LILO bootloader has been around a very long time. LILO stands for “Linux LOader.” LILO is a very flexible bootloader that can be used to launch just about any operating system from your computer’s hard drive, including Linux, Windows, or DOS.

When LILO is used as the default bootloader, the LILO boot menu is displayed to end users, allowing them to select the operating system kernel they want to boot. A sample LILO boot menu is shown in Figure 6-5.

> **NOTE** Many Linux distributions may present the LILO menu graphically instead of as the text menu shown in Figure 6-5.

Most early Linux distributions used LILO as the default bootloader. Because of this, LILO is probably one of the most widely deployed Linux bootloaders. Therefore, a good Linux administrator needs to know how to work with LILO.

> **NOTE** While LILO used to be very widely used, many current Linux distributions no longer support LILO. Most use the GRUB bootloader instead of LILO.

We’re going to look at the following LILO topics here:

- Installing LILO
- Configuring LILO
- About ELILO

Let’s begin by discussing how to install the LILO bootloader.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_231_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_231_1.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_232_0.png)

## Installing LILO

There are two different ways you can install the LILO bootloader. First, with Linux distributions that still support LILO, you can specify that the LILO bootloader be used for the system being installed. For example, in Figure 6-6, the openSUSE installer provides you with the option of changing the bootloader from the default of GRUB to LILO in the Boot Loader Settings screen.

You can opt to install the LILO bootloader either in the MBR or within the boot partition itself. Either option seems to work just as well. You can also install the LILO bootloader on a Linux system that’s already configured with another bootloader by first installing the LILO package on the system and then entering `lilo` at the shell prompt.

> **NOTE** We'll discuss installing packages later in this book.

This will overwrite the existing bootloader and install the LILO bootloader. However, before you can do this, you need to first configure the LILO configuration file in `/etc`. Let’s discuss how this is done next.

## Configuring LILO

The LILO bootloader is configured using a file in `/etc` named `lilo.conf`. A sample `lilo.conf` file from a SUSE Linux Enterprise Server 10 system is shown here:

```bash
$4: # cat /etc/lilo.conf
menu-scheme = Wb:Kw:Wb:Wb
timeout = 80
lba32
change-rules
reset
read-only
prompt
default = SLES_10_SP3
message = /boot/message
boot = /dev/sda2

image = /boot/vmlinuz-2.6.16.60-0.54.5-emp
###Don't change this comment - YAST2 identifier: Original name: linux##
  label = SLES_10_SP3
  append = "  resume=/dev/sda1 splash=silent showopts"

vga = 0x317
initrd = /boot/initrd-2.6.16.60-0.54.5-smp
root = /dev/sda2

image = /boot/vmlinuz-2.6.16.60-0.54.5-smp
###Don't change this comment - YaST2 identifier: Original name: failsafe###
label = Failsafe
append= "showopts ide=nodma apm=off acpi=off noresume edd=off 3"
vga = 0x317
initrd = /boot/initrd-2.6.16.60-0.54.5-smp
root = /dev/sda2

fs4:~ #
```

The first section contains global options that apply to all other sections in the file. The last two sections contain options specific to each menu item. You can review what each one does in Table 6-1. The options listed in Table 6-1 aren't all-inclusive. There are many more options you can use in your `/etc/lilo.conf` file. We don't have time or space to cover all of them here. For a complete listing, see the man page for `lilo.conf`.

The `lilo.conf` file is just a text file. You can use any Linux text editor to modify it. After modifying the file and exiting your editor, you must remember to run `lilo` from the shell prompt. If you don't, your changes to the configuration file won't be applied. This is shown here:

```bash
fs4:~ # lilo
Added SL55_10_SP3 *
Added Failsafe
fs4:~ #
```

Notice that the output from the `lilo` command indicates that the two images were added. You may have noticed that the `lilo` command we just used here to update our configuration is the same command that is used to install LILO. It is exactly the same command. In effect, every time you make a change to the LILO configuration file, you have to reinstall LILO with the `lilo` command. We should point out here that you can use the `-b` option with the `lilo` command to specify where the bootloader should be installed. If you specify a device, such as `/dev/sda`, then the bootloader will be installed in that device's MBR. If you specify a partition, such as `/dev/sda1`, then it will be installed in that partition and a pointer will be placed in the MBR.

Before shifting gears and talking about the GRUB bootloader, we need to first review a variation of LILO called ELILO. Let's do that next.

### About ELILO

ELILO works in pretty much the same manner as LILO. However, it's designed to run on computer hardware that isn't compatible with the standard version of LILO. For instance, it can boot a Linux kernel on the IA-64 (IPF) and IA-32 (x86) EFI-based hardware platforms. ELILO is also backward compatible with standard Intel x86 hardware. However, only a limited number of Linux distributions use it at this point.

Enough with LILO! It's time now to start working with GRUB!

| Section | Option | Description |
| :--- | :--- | :--- |
| Global Options | menu-scheme | Describes the colors used in the LILO boot menu. The syntax is: **text_color**:**highlight_color**:**border_color**:**title_color** Two characters are used for each value. The first character is the foreground color, while the second is the background color. See the lilo.conf man page for a listing of all the colors and their associated characters that can be used with this option. |
| | timeout | Sets the timeout period in tenths of seconds before the default menu item is automatically run. For example, if this option is set to **80**, it gives the user eight seconds to select a menu item. |
| | lba32 | Tells LILO to ignore the hard drive’s physical geometry and use logical block addressing. This allows LILO to work with disks that have more than 1023 cylinders (which all modern hard drives do). |
| | change-rules | Defines boot-time changes to partition type numbers. |
| | reset | Specifies that all default change-rules are removed. |
| | read-only | Specifies that the root (/) file system be mounted read-only at first. After checking the integrity of the file system, the kernel will usually remount the file system in read-write mode. |
| | prompt | Specifies that the boot: prompt be displayed. |
| | default | Specifies the default image that will be loaded if the user doesn’t make a selection. |
| | message | Specifies the location of the image file that LILO will display on boot. |
| | boot | Specifies the device that contains the boot sector. For example, to configure LILO to use the first partition on the first hard drive, you would set this option to /dev/sda2. |
| Image Options | image | Specifies the path to the boot image of a Linux kernel. |
| | label | Specifies a name for the image. |
| | append | Appends the specified options to the parameters that are passed to the kernel by LILO. This is usually only used if the system uses hardware that the kernel is having a difficult time auto-detecting. |
| | vga | Specifies the VGA text mode that should be used while the system is booting. |
| | initrd | Specifies the initial ramdisk image to be loaded with the kernel. Usually, this is set to /boot/initrd or /boot/initrd-version if you’re booting a Linux kernel. |
| | root | Specifies the device that should be mounted as root. For example, if you want to configure the second partition on the first hard drive to be the partition that should be mounted as the root partition, you would set this parameter to /dev/sda2. |

**Table 6-1** /etc/lilo.conf Configuration Options
