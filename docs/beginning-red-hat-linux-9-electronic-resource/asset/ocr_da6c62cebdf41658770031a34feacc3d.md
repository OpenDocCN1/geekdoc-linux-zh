```
(parted) rm 4
(parted) resize 2 101.975 5773.359
```

9. Now that we have learned to resize partitions, we can try and restore things to their original state (at the start of this example). We delete the newly created partition using the rm command, specifying the partition number of the partition we wish to remove. Finally, we resize Partition 2 to its original size:

```
(parted) print
Disk geometry for /dev/hda: 0.000-6149.882 megabytes
Disk label type: msdos
Minor Start End Type File system Flags
1 0.031 101.975 primary ext3 boot
2 101.975 5773.359 primary ext3
3 5773.359 6149.882 primary linux-swap
(parted) quit
```

10. The print command confirms our latest attempt to resize the partition. Once we are done experimenting, we exit the parted program using the quit command.

# Adding a New Hard Disk

Regardless of the hard disk real estate that we start out with, it is very likely that most of us will run out of disk space before the end of the lifecycle of our machines. This is when we will most likely get a disk upgrade by purchasing an additional hard disk or replace the current disk with one that has more storage capacity.

When we first installed Red Hat Linux 9 on the system, we did not have to bother about explicitly setting up our hard disk – the installer took care of this behind the scenes. But if we need to add a disk ourselves, there are a few manual steps that we need to perform.

# Detecting the Hard Disk

After hooking up the new hard disk to the system, and before going any further, it is necessary to ensure that the disk has been recognized by the operating system. Usually, Red Hat’s kudzu configuration tool will allow us to configure our new hardware when it is detected during the bootup process.

To ensure that the new disk has been recognized, we need to examine the kernel startup messages – these messages can be viewed using the dmesg command. We need to look for detection messages corresponding to our new hard disk. Here is a typical dmesg line, which indicates that the new hard disk has been detected:

```
$ dmesg | grep -i maxtor
hdb: Maxtor 90651U2, ATA DISK drive
```