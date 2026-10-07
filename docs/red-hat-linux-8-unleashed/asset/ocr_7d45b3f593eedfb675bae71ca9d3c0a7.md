# Partitioning Before and During Installation

NOTE

It is possible to create a dual-boot configuration, which allows the choice of booting Red Hat Linux and another operating system, such as Windows XP. To configure your system for dual-booting, you must first install Windows and then install Linux. Note that many Windows system-restore CD-ROMs will wipe out all data on your hard drive, including Linux. During installation of Red Hat Linux, you can install the GRUB Linux bootloader in the primary drive's Master Boot Record, or MBR. When properly configured, GRUB allows your system to reboot to Windows or Linux. See Chapter 24 for information on GRUB.

CAUTION

Before you partitioning your drive or installing Red Hat Linux, get your safety nets in order. First, back up all critical data Any changes to your system's hard drive or operating system your existing data at risk. To prevent the loss of time and resources that inevitably follow data loss, do backups before you make any changes to your system. Create a bootdisk when you install Red Hat Linux, so you'll be able to at least boot Linux if something goes wrong. See Chapter 11, "Backing Up, Restoring, and Recovery," for information on backups on Linux.

# Choosing a Partitioning Scheme

Like deployment and installation of Linux, partitioning your hard drive to accept Red Hat Linux requires some foresight, especially if the target computer is going to be used other than as a home PC on which to learn.

If Linux is to be the only resident operating system, the Red Hat Linux installer can be used to automatically create and use a partition scheme according to the type of install-select during the install. If you plan to have a dual-boot system in which you can boot Linux or another operating system, you'll need to manually partition your hard drive before and possibly during the install.

The simplest and most basic scheme for a Linux system requires a Linux native root partition and a swap partition. On a single-drive system with 10GB storage and 128MB RAM, the scheme might look like this:

| Hard Drive Partition | Mount Point | Size |
| --- | --- | --- |
| /dev/hda1 | / | 9.74GB |
| /dev/hda2 | swap | 256MB |

On a system running Windows, the scheme might look like this:

| Hard Drive Partition | Mount Point | Size |
| --- | --- | --- |
| /dev/hda1 | /mnt/dos | 2GB |
| /dev/hda2 | / | 7.74GB |
| /dev/hda3 | swap | 256MB |