
## Troubleshooting LILO

LILO writes a new boot sector onto your hard drive when you run `lilo`, not when the system boots. Therefore, it must be rerun to update that boot sector whenever `/etc/lilo.conf` changes. If you forget to do this, the system will not boot. To fix this, you can boot with the install/rescue floppy, mount the root directory on `/mnt` and rerun LILO using the command `lilo -r /mnt`. An alternative is to boot from an install/rescue floppy, mount the root directory on `/mnt`, run the command `chroot /mnt` to make the system treat `/mnt` as the root directory, and then run LILO normally.

| Error | Description |
| :--- | :--- |
| LIL | The second-stage boot loader runs but can't function properly. This frequently indicates a geometry mismatch or a problem with the hard disk. |
| LIL? | LILO has loaded the second-stage boot loader into the wrong address. This is usually caused by moving `/boot/boot.b` without re-running `lilo`. |
| LIL\ | LILO has detected a damaged descriptor table, `/boot/map`. This can be caused by disk geometry mismatch or by moving the descriptor file without re-running `lilo`. |
| LILO | The program has loaded and run correctly. Subsequent problems are likely related to the kernel or other Linux startup files. |

**Note** Hard disks are composed of one or more *platters*, each of which has associated with it one or two *heads*. These heads move across several different *tracks*, forming *virtual cylinders* across the stacked platters. Each *cylinder* is broken up into multiple *sectors*, each of which holds 512 bytes on most hard disks. Early hard disks could be defined by the number of *cylinders*, *heads*, and *sectors* they used; hence the term *CHS geometry* or *disk geometry*. The x86 BIOS and the standard x86 partitioning table use this method of describing a disk. The trouble is that all modern hard disks lie about their CHS geometries. Furthermore, the lies told by the disks sometimes cause problems, so BIOSes and OSes frequently change these lies to other lies. With so much fabrication occurring, the situation sometimes collapses in chaos when two different software components believe different things about the disk’s geometry. This can be the source of some LILO problems, if LILO uses one CHS geometry setting and another tool uses another setting.

## Making the System Boot a New Kernel

Once you get a kernel that has everything that you need, you might want it to be booted by default. After compiling and thoroughly testing a new kernel, edit the configuration file for the boot loader to change the default.

### LILO

To change the default boot kernel from `linux` to `linux_new`, edit the `/etc/lilo.conf` file to change the `default=linux` line to `default=linux_new`. If you don't see a `default` line, simply add one. Not long ago, LILO simply took the first listed kernel image as the default image, so older `lilo.conf` files won't have the `default` parameter. Don't forget to rerun `/sbin/lilo` after you make any changes to the `/etc/lilo.conf` file.

Here is a sample `/etc/lilo.conf` file:

```
boot=/dev/hda
map=/boot/map
root=/dev/hda1
install=/boot/boot.b
prompt
timeout=50
message=/boot/message
linear
default=linux
image=/boot/vmlinuz-2.4.7-10
    label=linux
    read-only
image=/boot/vmlinuz-2.4.7-10-new
    label=linux_new
    read-only
```

### GRUB

GRUB uses a number from 0 to one less than the number of configured kernel images to denote which image is to be the default. To change the default boot kernel from `linux` to `linux_new` using GRUB, edit the `/boot/grub/grub.conf` file to change the `default=0` to the appropriate number (remember to start counting the stanzas at zero). Alternately, you can add any new stanzas above the existing ones, the first stanza being the default.

Here is a sample `/boot/grub/grub.conf` file:

```
# NOTICE:  You have a /boot partition. This means that
#
#           all kernel paths are relative to /boot/
default=0
timeout=30
splashimage=(hd0,0)/grub/splash.xpm.gz

title Red Hat Linux (2.4.7-3-jul2001)
    root (hd0,0)
    kernel /vmlinuz-2.4.7-3-jul2001 ro root=/dev/hda3
    initrd /initrd-2.4.7-3-jul2001.img

title Red Hat Linux (2.4.7-3)
    root (hd0,0)
    kernel /vmlinuz-2.4.7-3 ro root=/dev/hda3
    initrd /initrd-2.4.7-3.img
```

## Hardware Not Detected at Boot

For a variety of reasons, hardware might not be detected at boot. Sometimes passing the appropriate information as an option to the boot loader will fix the problem.

### LILO

If hardware in your system isn't recognized at boot, it may be possible to get Linux to see it using an `append` line in `/etc/lilo.conf`. Say you have more than one network interface card (NIC) in your computer but Linux doesn't detect this on boot. Assuming that the problem is not that you are running a modularizing kernel and the correct module doesn't exist, you can try appending the hardware data about the card. The `append` statement will look something like the following, except that the parameters will be replaced by values reflecting your hardware:

```
append="aha152x=0x140,12,7,0,0  sb=240,5,1,5,300"
```

### GRUB

GRUB handles things slightly differently. Instead of adding an `append` line, you actually append the information to the end of the kernel line in the `grub.conf` file. For example:

```
title Red Hat Linux (2.4.7-3-jul2001)
    root (hd0,0)
    kernel /vmlinuz-2.4.7-3-jul2001 ro root=/dev/hda3
    initrd /initrd-2.4.7-3-jul2001.img
```

would become:

```
title Red Hat Linux (2.4.7-3-jul2001)
    root (hd0,0)
    kernel /vmlinuz-2.4.7-3-jul2001 ro root=/dev/hda3 aha152x=0x140,12,7,0,0 sb=240,5,1,5,300
    initrd /initrd-2.4.7-3-jul2001.img
```

Notice that the kernel line is continued without a new line.

## Dual-booting with Another OS Like Windows

It is very easy to set up a system to dual-boot Linux and another operating system using two separate disks.

### LILO

LILO is quite happy to boot multiple operating systems. Sometimes, because Windows likes to be on the first disk, you should switch the disks around, making the Windows disk `/dev/hda` and the Linux disk `/dev/hdb`. Remember to have a rescue disk or CD-ROM around when you're doing this, since LILO won't know where things are anymore. Boot into rescue mode and mount the Linux disk. Edit the `/etc/lilo.conf` file to include the Windows partition. Assuming that Windows is on the first disk (`/dev/hda`), Linux is on the second disk (`/dev/hdb`), and the partition containing `/boot` is correctly included below the 1024-cylinder mark of the disk it is on, your `lilo.conf` file should look like the following.

```
boot = /dev/hda
map = /boot/map
install = /boot/boot.b
prompt
timeout = 50
default = linux

image = /boot/vmlinuz-2.4.18-3
    label = linux
    read-only
    root=/dev/hdb1
other = /dev/hda1
    label = msdos
```

Run `lilo` to write out LILO's new configuration, sync the disks since you are in rescue mode, and reboot.

### GRUB

Assuming the same setup as above, the `grub.conf` file would include the following stanzas:

```
title linux
    root (hd1,0)
    kernel /boot/vmlinuz-2.4.18-3 ro root=/dev/hdb3
    initrd /boot/initrd-2.4.18-3.img
title win2000
    rootnoverify(hd0,0)
    chainloader +1
```

## Can't Remove Boot Loader from the Master Boot Record

It's possible that you'll install Linux on a computer and then discover that you need to recycle the computer for use with Windows, DOS, or some other OS. Many new Linux administrators have problems with this, though, because after they've removed Linux, the boot loader hangs on like an albatross around the computer's neck. Fortunately, there are ways to deal with this problem. If your system still has Linux installed using LILO and you want to remove LILO from the MBR, you log in as root and use the LILO uninstall command as follows:

```
# lilo -u
```

If you use GRUB or have for some reason deleted Linux from your system and installed some version of Microsoft Windows, you can use the Windows `FDISK` command to rewrite the Master Boot Record and then reboot:

```
C:\> FDISK /MBR
```

## Kernel Won't Load or Loads Only Partially

There are two possibilities here. Either the kernel image has become corrupted in some way or LILO is being passed an incorrect parameter. You see this if someone adds an incorrect `append` line in `/etc/lilo.conf`.

Often this is an incorrect `mem` line. The `mem` option isn't usually needed but occasionally you'll run across a system for which LILO doesn't recognize the correct amount of memory. If you need to help LILO recognize a large amount of memory, such as 256MB, add the line `mem=256M` to the `/etc/lilo.conf` file and then run `lilo`. If you incorrectly add `mem=2256M` or some other too-large number, your kernel will not fully load. If you incorrectly add `mem=256m` using the lowercase `m`, that will also inhibit the kernel's ability to fully load.

When LILO is run, it catches some of the errors in the `/etc/lilo.conf` file. If you specify a kernel image that doesn't exist, the `lilo` program will generate an error message. If you've specified a boot device that doesn't exist, you will see a message like this:

```
Fatal: open /dev/hdb: Device not configured
```

## Login Problems

Because gaining access to your systems is so important, you must be able to diagnose and repair login problems. Knowing the login process step by step is the key to this ability. Once you've been doing Linux system administration for a while, these problems will be easy for you to fix.

## Lost Password

One of the most frustrating problems occurs when you have a system and no one seems to remember the root password. With luck this won't happen often. Sometimes, though, the root password is needed and not known and needs to be reset.
