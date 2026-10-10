specify a specific device instead of a UUID. If you find you get further along in the boot process that way, then you can use the `blkid` command to see the UUID that's assigned to a particular device:

```
$ sudo blkid -s UUID /dev/sda2
/dev/sda2: UUID="528c6527-24bf-4201-b98b-c175f7b66a0f"
```

Once you know what the UUID should be, you can then edit your GRUB configuration file (and /etc/fstab) so that it references the proper UUID.

# The Root Partition Is Corrupt or Failed

The other main reason why a kernel may not be able to mount the root file system is that it is corrupt or the disk itself has completely failed. When a file system gets mounted, if errors are detected on the file system, it will automatically start a repair process; however, in many cases the corruption is significant enough that the boot process will drop you to a basic shell so you can manually attempt to repair the file system. If your boot process gets to this state, go to the Repair Corrupted File Systems section of Chapter 4 for details on how to correct the errors. If you fear that your disk has completely failed, check out Chapter 10, which talks about how to diagnose hardware issues.

# Can't Mount Secondary File Systems

Many servers have multiple file systems that might get mounted automatically as the system boots. These file systems are defined in the /etc/fstab file and might look somewhat like the following:

```
# /etc/fstab: static file system information.
# <file system>       <mount point>  <type> <options>  <dump>  <pass>
proc                  /proc        ext3  defaults        0    0
/dev/sda1             /            ext3  defaults        0    0
/dev/sda2             swap         swap  defaults        0    0
/dev/sda3             /var         ext3  defaults        0    0
/dev/sdb1             /home        ext3  defaults        0    0
```