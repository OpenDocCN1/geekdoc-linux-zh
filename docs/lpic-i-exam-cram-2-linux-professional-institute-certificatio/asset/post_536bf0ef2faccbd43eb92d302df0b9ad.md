
boot-time options from the LILO or boot prompt, and answering them correctly demands having seen this change happen when you press Ctrl+X. So remember, **LILO:** and **boot:** are the same for our purposes.

Entering options at boot time is necessary to troubleshoot or correct a problem that causes the machine to be unable to boot as configured. For example, if you have a system that, right after bootup, has a problem with the GUI, the system might hang for a long time and then become unusable, requiring a reboot. Typically, this system will have the default runlevel in the /etc/inittab set to 5 and will experience the same problem every reboot until fixed. To fix this, the system should be rebooted and at the **LILO:** or **boot:** prompt, you should enter **linux 1** to boot it into single user mode or **linux 3** to boot it into text mode. Here’s the syntax:

```bash
LILO: linux 1
```

Or

```bash
Boot: linux 3
```

If your system won’t boot into runlevel 5 (the X GUI login screen), you should specify the runlevel as shown and then run the X configuration tools again.

Important LILO boot options include

- **root=/dev/hda1**—Sets the root device and is good for rescue
- **mem=#**—Sets the RAM amount to access older machines
- **maxcpus=#**—Is good for troubleshooting bad CPUs

## Troubleshooting LILO

Another issue that causes some confusion is how LILO records the kernel location on disk for use in the MBR code, rather than the /directory/filename information. Only 512 bytes of space is available into which to cram all those options and parameters.

Therefore, if you move the files in the /boot directory or the directory itself, or upgrade the files (even with the same name), it’s not the same location on disk and LILO throws an error.

Always, always rerun LILO after

- Updating kernel or other /boot files
- Changing the disk size
- Changing the partition size
- Moving the /boot directory

If you encounter errors, examine the /etc/lilo.conf file for mistakes. The /sbin/lilo command does some syntax and file-presence checking, but it can miss something.

Always rerun the /sbin/lilo command after you've made any changes to the /etc/lilo.conf file, and particularly after you've updated or created a new kernel, even if you name it the same name as the existing one.

![](img/49f4f38f3aec011238fa50f89e643db3_66_0.png)

> Overwriting your only existing kernel file with a new untested one is a quick way to stop all productive work and gain some troubleshooting experience. Watch for questions about this on the exam.

# LILO Command Options

LPI likes to test the LILO command options, probably because you'll end up using them fairly often and troubleshooting is a very important part of the job for many sysadmins.

These options are used for troubleshooting with the /sbin/lilo command in the following format:

```bash
lilo -options
```

- **-b**—Sets the boot device (such as /dev/hdb).
- **-c**—Specifies a configuration file other than the default /etc/lilo.conf.
- **-D**—Boots a particular kernel (lilo -D label, where label is the corresponding name of a kernel's image label).
- **-L**—Makes the system use linear or 24-bit addresses when accessing the disks.
- **-l**—Makes the system use 32-bit or LBA32 addressing, allowing access to all disks that are larger than 1,024 cylinders.
- **-q**—Queries the /boot/map file for the names and locations of the kernels that can be booted. It can be combined with the -v verbose option to give more detailed information.
- **-r**—If followed by a discrete command sequence, that sequence is run at the next boot.
- **-s**—A copy of the MBR or first sector is saved when LILo is rerun. The saved contents are put in /boot/boot.NNNN, where NNNN depends on IDE or SCSI for its naming.
- **-t**—Tests the configuration only; doesn't write it to the MBR or first sector. Essentially, this is a dry run.
- **-T**—This is arguably the most useful option for LILo; its keyword values can be used to bring back information about the disk and video, among others.
  - **-T help**—This shows help for the -T options, including
  - **-T geom**—Lists the drive geometry (cylinders, heads, and sectors) for all attached drives
  - **-T video**—Shows the graphic modes that LILo can use, which is important for laptops, specialty displays, and LCD monitors
- **-u**—Followed by the device name (/dev/hda), this option copies the saved boot sector (/boot/boot.NNNN) back to the MBR or first sector. If a device name is not specified, it takes the first bootable device.

![](img/49f4f38f3aec011238fa50f89e643db3_67_0.png)

> LILo is a favorite topic for the first exam, with all sorts of options being tested. Be aware of how to run a command at the next boot, how to back up the MBR, and how to restore it from a boot disk.

# LILo Error Codes

When a system boots, that occurs in two stages. The first stage loader is a single sector that is read from the BIOS or MBR. The system lets you know it's in the first stage by displaying the letter L on the screen, leading eventually to the word LILo. When the first stage is done, it prints the letter I to the screen and transfers control to the second stage loader.

The second stage loader is called from the first, and it can contain multiple sectors and more information. When the second stage loader receives control, it prints the second L in LILo to the screen, announcing that it's starting its process. When it has concluded its process, it prints the O in LILo to the screen, and then any parameters or labels desired can be entered.

If an error occurs, LILo prints a hexadecimal code for the error and attempts the process again. Some important error codes that you might see are shown here:

- **01**—Invalid disk command
- **0A**—Bad sector flag
- **0B**—Bad track flag
- **20**—Controller failure
- **40**—Seek failure (BIOS)
- **40**—Cylinder>1023 (LILO)
- **99**—Invalid second stage index sector (LILO)
- **9A**—No second stage loader signature (LILO)
- **AA**—Drive not ready

# Grand Unified Boot Loader

Grand Unified Boot Loader (GRUB) is newer than LILO and offers some updated features, such as being able to edit the GRUB menu on-the-fly, rather than having to reparse a file and rewrite the MBR as LILO must.

# GRUB’s Configuration Files

The GRUB configuration file is *boot/grub/menu.lst*. This file contains several items, including some that are similar to LILO’s configuration file.

Listing 1.2 shows a sample grub.conf file.

```
Listing 1.2  A GRUB Configuration File
# Sample boot menu configuration file
# By default, boot the first entry, if only one entry, it's # the default
default 0
# Boot automatically after 30 secs, remember seconds, not # deci-seconds like LILO!
timeout 30
# Fallback to the second entry.  If there isn't one, it will # just fail.
fallback 1
# To boot Linux
title Linux
kernel (hd0,0)/vmlinuz root=/dev/hda1
# To boot Windows
title Windows
root (hd0,1)
makeactive
chainloader+1
```

## How GRUB Treats Disks

GRUB isn't able to tell the difference between IDE and SCSI disks; it just reads the BIOS entries and goes on from there. To make things more predictable, it detects and uses IDE disks before SCSI disks.

The numbering of disks and partitions is a little different from other boot loaders. The following is a representation of the first hard disk and the first partition on that disk:

```
(hd0,0)
```

GRUB numbers its disks from 0, with 0–3 usually being the IDE disks. The partitions are numbered similarly, with 0–3 being the primary partitions and 4 always being the first logical partition on the disk.

The following is the designator for the first floppy on the systems:

```
(fd0)
```

![](img/49f4f38f3aec011238fa50f89e643db3_69_0.png)

Multiple partitions aren't possible on a floppy, so no partition designator is necessary.

## Setting Up GRUB

Installation consists of running the *grub-install* script with parameters or running *grub* and setting up the boot loader while in GRUB.

Here's an example of installing to the first hard disk:

```bash
grub-install /dev/hda
```

This simply installs the boot loader into the MBR of the first hard disk.

Here's an example of installing to a /boot directory:

```bash
grub-install -root-directory=/boot /dev/hda
```

This is necessary for a system that uses a small /boot partition to hold the boot files and to avoid the 1024-cylinder problem.

## Another GRUB Install Option

You don't have to use the *grub-install* script—you can set up GRUB from the *grub>* prompt. In other words, you might be using a different boot loader and decide to install GRUB without knowing some details, such as the location of the GRUB stage loaders.
