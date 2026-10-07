In this example, the first non-SCSI disk has three partitions and the second disk has two. Your system's output will probably be different, of course. If you don't see any partition information, either the hard disk controller is not recognized properly or the disk drives themselves are not accessible. These problems have a number of potential causes, including the obvious:

+   Check the cables inside the computer. The hard disk cable should run from the adapter card to each drive's connector. Make sure the cables are connected in the proper manner (the red strip on the cable is at pin 1 on the connector).

+   Check that the power connector is attached to each disk drive. Without power, your drive won't spin up, and Linux can't touch it.

+   Check the partition table to make sure you created a Linux partition properly.

After that, if the drive is not working properly with Linux but works okay when you boot DOS, it is probably a kernel driver for the hard disk that is at fault. Some IDE drives, for example, are not as well-behaved (not conforming to the IDE standards) as others, and your IDE kernel driver might not be able to talk to your drives. Try using a different kernel image and see whether the problem solves itself. If you are using a SCSI kernel and adapter and the drives are not recognized, use the utilities that came with the SCSI adapter card to force a check of the hard drives. They may have a SCSI ID set incorrectly.

# # Device Conflicts

One of the most common problems is when hardware is not recognized properly. This can happen to a CD-ROM, a network card, and even a hard disk. This is usually caused by a conflict in the IRQ (interrupt), DMA (Direct Memory Address), or I/O address settings. When two devices have the same settings on any one of the three characteristics, Linux and the BIOS may not be able to communicate with the device properly.

A symptom of this problem may be Linux hanging when it tries to find a specific device, as explained on the boot messages. When Linux boots up, it generates verbose messages on the console that explain what it is doing. If you see a message that it is trying to connect to the network card, for example, and it never gets past that point, chances are that the network card has a conflict with another device. (Totally failed cards are very rare and don't usually stop the boot process because Linux ignores devices it can't access. The problem with a working card with conflicting settings is that Linux is getting messages from two devices that don't act the same.)

To check for conflicts, you should run a diagnostic utility under DOS, such as MSD or Norton Info. These can show you the current IRQ, DMA, and I/O addresses and pinpoint any conflicts. They can also be used for finding available settings.