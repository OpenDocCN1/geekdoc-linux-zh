
## PART 2 | Layered Security and Linux

## Locking Down Boot Hardware

The risks associated with physical access ports fall into two categories. First, there are the physical access ports on a server. As previously noted, a black-hat hacker with access to a CD/DVD drive or USB port can gain administrative access to a system. This applies to servers, workstations, and desktops. But there's more. To enhance physical security on a system, consider the following measures:

- Make sure cases on towers are locked. A black-hat hacker who disconnects a BIOS battery could reset any configured passwords.
- Secure the installation of blade and rack servers with nonstandard tools such as Allen nuts.
- Remove any CD/DVD drives. If you use a CD/DVD to start the installation of an operating system, which should be all that's needed. Other CD/DVD-based Linux software can be installed from mounting their .iso files as virtual CD/DVDs.
- Secure any unused external ports. Black-hat hackers with access to a USB port—or any other boot port—could boot the operating system of their choice.

Similar issues apply to virtual hosts. Of course, it's not possible to physically lock down a virtual server. "Physical security" on a virtual host depends on the permissions applied to associated files. It is easier to install or remove noted virtual components, including CD/DVD drives and USB ports.

Beyond boot hardware, open ports on networking equipment are an open invitation to malicious users.

## Locking Down Boot Loaders

While there are many excellent non-Linux boot loaders, this is a book on securing Linux platforms and applications. To that end, this chapter will cover two boot loaders: the Linux Loader (LILO) and the Grand Unified Bootloader (GRUB). Although LILO is no longer included with many Linux distributions, including Red Hat, it is still used surprisingly on Linux systems.

There are several versions of GRUB in common use. Version 1 (shown as version 0.97) is still the default for Red Hat, Fedora, and SUSE distributions. Upcoming sections in this chapter refer to as "traditional GRUB." Version 2 is the default for the latest Ubuntu releases. In addition, for those who use the TPM chip described earlier in this chapter, there is a trusted version of GRUB known as TrustedGRUB.

> NOTE The terms "bootloader" and "boot loader" are synonymous and used interchangeably. This book will use "boot loader" unless the proper name of a program specifies "bootloader" as one word.

## Hard-Drive Device Files

Various Linux hardware components, have fallen into two categories., are associated with device files. Traditionally, they've fallen into slightly older distribution releases (including Red Hat Enterprise Linux 5), Parallel Attached Technology (PATA) hard drives were classified by their attachment location. For example, the first hard drive to the master connection on the primary controller was assigned the /dev/hda name. Small Computer System Interface (SCSI) and Serial Advanced Technology Attachment (SATA) hard drives aren't installed on the same system; they're named sequentially starting with /dev/sda.

If you have PATA drives and are not sure of their associated device files, run the fdisk -l command as the root user. The output of that command lists all detected devices and configured partitions, with their file names.

With the latest Linux distribution releases, there is no longer a difference in device files. PATA, SATA, and SCSI hard drives are sequential device file names starting with /dev/sda. To reduce confusion, it's normally best to avoid mixing drive types on a single system.

KVM has introduced another hard-drive option known as a virtio block device. It is a paravirtualized device that works in a hardware-virtualized machine. Because paravirtualization is essentially a shortcut, it makes for a faster virtual hard drive. Related hard drives may have device files such as /dev/vda1.

Partitions take the hard-drive device file one step further. The first partition on the first drive on the latest Linux system is given the file name /dev/sda1.

When loading a boot loader, beware. Some options in the boot loader are designed to help the forget administrator reset a root password. Those options make it possible to log in as the administrative user without a password. In this section, you'll learn how to make it more difficult to access the root account in this manner—at least from the LILO and GRUB boot menu. The forget administrator can still reinstall a CD/DVD drive and boot a live CD to recover a root password.

## Back Up the Current Boot Loader

The following sections specify changes to a system's boot loader. If you're trying to learn about boot loader options, be careful. It's best to back up the current boot loader on a system before making any changes. If something goes wrong, you'll be able to use the rescue media available for the distribution to recover the boot loader.

If the system includes a floppy drive, GRUB and LILO can both be set up on that drive. The commands vary depending on your configuration. If it is properly configured, you'll be able to boot the current system from that specially configured floppy drive. While you may also be able to set up the same backup boot loader on a USB drive, not all systems can boot from that.

But not all systems have floppy drives. Alternatively, you could back up key files associated with the current boot loader. If something goes wrong, you could use the rescue mode associated with the local distribution or a live CD to boot the system, access the local drives, and restore the boot loader from backup. Don't forget to use the appropriate command (grub-install or lilo) to write appropriate information to.

## Securing LILO

LILO is rarely available since 2007. Most work from Linux developers on the boot loader now focuses on GRUB.

## CHAPTER 3 | Basic Security: Facilities Through the Boot Process

### /etc/lilo.conf: Sample LILO boot loader.

```markdown
boot=/dev/sda
prompt

install=menu
map=/boot/map
vga=normal

default=Linux
delay=100
image=/mlinuz
password=option1
root=/dev/sda
initrd=/initrd.img
label=Linux
read-only
other=/dev/sdb
password=option2
label=windows
table=/dev/sdb
```

FIGURE 3-1 A Linux loader configuration file.

with a delay. When you see automatically with appropriate directives in the UEFI and/or BIOS menus, this means you have to use a rescue or live CD.

By default, LILO does include the prompt directive, which allows administrators to boot into a system in single-user mode. Also known as runlevel 1, single-user mode automatically boots a system into the root administrative account. The user is not prompted for the root password.

Most LILO configuration files do not include password directives. Those directives can prompt the user for the noted password before booting into the stanza. As you can see in Figure 3-1, the password is shown in clear text.

the root user. The standard is 600 permissions, which is read-write access to the user owner. For more information on discretionary permissions, see Chapter 4.

In this configuration, the image and initrd point to links from the top-level root directory to the actual locations of the Linux kernel and RAM disk files. It's equally valid to point these to the full path to the actual.

> NOTE: if you choose LILO, it should be installed on the MBR of one of the first hard drives on a system. If you configured a different boot loader on the MBR, you can set up LILO on the partition with the /boot directory. If it's the first partition of the first SATA drive, the associated command is lilo /dev/sda.

Other versions of LILO are available; the version created for HP Antarctica 64-bit systems is designed for Extensive Firmware Interface (EFI)-based hardware. However, the last version of LILO for standard PCs and servers was released in 2007.
