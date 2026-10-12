```
# cd /
# umount /mnt/image
```

There are simpler ways of doing this (for example, booting with your boot floppy, logging in as root and typing lilo) but solving this problem with a rescue disk is good practice for a more serious emergency session. In this simple example, we mounted the Linux filesystem on /mnt/image, then chroot’d to /mnt/image to make that directory our root directory. It also launched a bash shell. From there, simply executing the /sbin/lilo command rewrote LILO into the MBR.

This technique can also be used to fix another common problem: building a new kernel but forgetting to run /sbin/lilo to write the new boot information to the MBR. This condition will often prevent you from booting Linux at all, necessitating a rescue operation to restore use of the system.

# Rewriting Configuration Files

Simple misconfigurations of configuration files are easily repaired in rescue mode. Let’s say we inadvertently make a typo while editing /etc/fstab and can’t get back into the system. We meant to write /dev/hda4 in the first line as our key partition to mount, but our keyboard bounced and we entered /dev/hda44 without noticing, and now Linux won’t boot.

Return to rescue mode, mount /dev/hda4 as before, edit the /etc/fstab file, save it, and reboot, with relief:

```
# mount -t ext2 /dev/hda4 /mnt/image
# pico -w /mnt/image/etc/fstab
# umount /mnt/image
```

# Repairing a Partition

While Linux is booting, fsck will attempt to fix any partitions that don’t come up clean during an integrity check. This often happens after an abrupt shutdown where power is removed from the system before the shutdown procedure finishes, as can occur during a power outage or an inadvertent shutdown by accidentally turning off the computer.

The rescue disk set can be used to manually run e2fsck to check and attempt to repair disk damage.

```
# e2fsck -f /dev/hda4
e2fsck 1.14, 9-Jan-1999 for EXT2 FS 0.5b, 95/08/09
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
```