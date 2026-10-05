# Manually Installing or Reconfiguring LILO

If you don't install LILO during SuSE Linux install, you can install LILO in two basic steps (as root):

+   1. Configure /etc/lilo.conf.

+   2. Run /sbin/lilo to install LILO and make it active.

This discussion describes modifying an existing lilo.conf file. Before making any changes, do yourself a favor and create a backup of the file in the same directory or on a separate disk. Several files are important to LILO and are created during an initial install:

+   * /sbin/lilo—A map installer, see man lilo for more information.

+   * /boot/boot.b—A boot loader.

+   * /boot/map—A boot map that contains the location of the kernel.

+   * /etc/lilo.conf—LILO's configuration file.

# Configuring LILO

Under Linux, your hard drives are abstracted to (that is, referred to or referenced as) /dev directory. If you have one or more IDE drives, your first hard drive is referred to as /dev/hda and your second hard drive is /dev/hdb (hard drive “a” and hard drive “b”). SCSI drives are referred to as /dev/sda and /dev/sdb (scsi drive “a” and scsi drive “b”). When you installed Linux, you most likely partitioned your hard drive (at least to create a swap drive). The first partition on your drive will be /dev/hda1 or /dev/sda1, your second partition will be /dev/hda2 or /dev/sda2, and so on.

Before configuring LILO, you should know which partitions have operating on them. You should also know where to install LILO. In almost all cases, you will want to put LILO on the MBR. You shouldn't do this, however, if you run OS/2, BootMagic, or similar products because they use the MBR. If you are using these types of software packages, LILO should be installed on the superblock of the root Linux partition.

You can look to see what partitions you currently using (or are mounted from within Linux) by running the df command (/bin/df):

```
df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda1 1973472 1161391 710070 62% /
/dev/hda3 4036649 2443 3825361 0% /home
```