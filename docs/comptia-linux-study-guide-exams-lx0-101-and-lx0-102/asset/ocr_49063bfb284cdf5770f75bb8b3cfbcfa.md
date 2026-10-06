# Chapter 5 • Booting Linux and Editing Files

#

# Other operating systems

#

title Windows

rootnoverify (hd0,1)
chainloader +1

GRUB does not refer to disks by device filename the Linux does. GRUB numbers drives so that it can access /dev/hda or /dev/sda, GRUB uses (hd0). Similarly, /dev/hdb or /dev/sdb is likely to be (hd1). GRUB distinguishes between PATA, SCSI, and USB drives, so on a SCSI-only system, the first drive is (hd0). On a mixed system, ATA normally receives the lower numbers, although this isn't always the case. GRUB Legacy's drive mappings can be found in the /boot/grub/device map.\ Additionally, GRUB labels partitions on a drive starting at 0 instead of 1 that is used by Linux. GRUB separates partition from drive numbers with a comma, as in (hd0,0) for the first partition on the first disk (Linux's /dev/hda1 or /dev/sda1) or (hd0,4) for the first partition. Floppy drives are referred to as (fd0), or conceivably (fd1) or higher if you have more than one floppy drive. Floppy disks are not partitioned, so they do not receive partitions. GRUB treats USB drives just like hard disks, although it relies on the firmware to access these devices, GRUB won't boot from a USB flash drive you're using an older computer that doesn't support this option.
GRUB defines its root partition as the partition in which GRUB's configuration file (menu.grub.cfg or grub.conf) resides. This file is normal in Linux's /boot/grub/ directory, the GRUB root partition will be the same as Linux's root partition if you do not use a separator /boot or /grub if you split off into its own partition, as is fairly common, GRUB root partition will be the same as Linux's /boot partition. You must keep this difference in mind when referring to the GRUB configuration directory.

# Essential Global GRUB Legacy Options

GRUB's global section precedes its per-image configurations. Typically, you'll find a few options in this global section:

Default OS The default= tells GRUB which OS to boot. Listing 1.s default=0 causes the first OS to be booted (remember, GRUB indexes from 0). If you want to boot the second listed operating system, use default=1, and so on, through all OSs.