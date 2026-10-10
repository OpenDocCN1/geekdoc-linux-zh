# FreeBSD Complains "Device Not Configured" While Trying to Mount a CD-ROM Drive

This problem can be caused by a few things, as follows:

+   - The CD-ROM drive might be empty; simply insert a CD and try again.

+   - The second possibility is that an ATAPI CD-ROM drive is configured as the slave drive on the secondary controller and there is no master drive on the controller. You will need to reconfigure your CD-ROM drive as the master if this is the case (you usually can do this reconfiguration from jumpers on the back of the CD-ROM).

+   - If you have a SCSI CD-ROM drive, the drive might not be getting enough time to answer the bus reset request when the kernel is started. If this is the case, find the options SCSI_DELAY line in the kernel configuration file and increase the time. (The time is given in milliseconds. By default, it is set to 15000, or 15 seconds. You might start by doubling it to a value of 30000.) You will then need to rebuild the kernel (see Chapter 16).

# Programs Crash with Signal 11 Errors

This problem is somewhat like an illegal operation error in Windows. It basically means that a program tried to access memory that was not allocated to it. This could be the result of a bug in the program or, if it is occurring with utilities included with FreeBSD, a bug in FreeBSD itself.

A third potential cause of this problem is flaky hardware. If the problem occurs at random points while compiling software, you can almost sure that flaky hardware is the culprit. Common hardware causes for such problems include defective RAM, a CPU that is over-heating (Is your CPU fan running? Are you overclocking?), defective cache memory, or a flaky power supply.

# Strange Error Messages Occur When Running top, ps, and Other System Utilities

This type of error is almost always caused by your world and your kernel being out of sync. Often, the problem stems from using make world to build the system from source and then failing to build a new kernel. The reverse could also be true: You built a new kernel with sources that you downloaded but did not do a make world first.

Because it is much quicker to rebuild the kernel than to rebuild the world, the simplest solution is to try making a new kernel and rebooting first (see Chapter 16 for detailed information on rebuilding the kernel).

If rebuilding the kernel doesn't fix the problem, try rebuilding the world. (See Chapter 17, "Keeping Up to Date with FreeBSD," for details on doing a make world.)