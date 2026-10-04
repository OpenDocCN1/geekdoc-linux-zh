![](bbox=[0.22, 0.1, 0.78, 0.45])

# Figure 7.1 Partitioning a 320 Mb hard disk.

Here, the first partition has been set aside for DOS use as the C: drive, the second partition will be used as swap space under Linux and the third partition will be used to hold the Linux root filesystem. Each separate filesystem under Linux will have its own disk partition.

Sometimes you will want to use more than four partitions on a hard drive, especially if it is a rather large drive. In this case, one of the four primary disk partitions can be used as an extended partition. The extended partition is then used like a container to hold a set of logical disk partitions (up to 23 of them under DOS).

In addition to considering extended and logical disk partitions, for really large disk drives, a new problem pops into the frame. Due to a design oversight (the designers couldn’t imagine hard drives becoming available that would be big enough to break their design limits...) you cannot generally boot a PC from a disk partition that uses disk cylinder numbers greater than 1023 (unless you have a modern motherboard whose BIOS supports large drives). For Linux, this means that its root filesystem must lie entirely in a partition under the 1024 cylinder boundary. Linux can hold data and programs in partitions above the boundary; you just can’t boot Linux from these partitions. For an IDE disk, the 1024 cylinder limit comes at 504 Mb.

Suppose, then, that you have a 720 Mb IDE disk and you want to partition it to give a 150 Mb DOS C: drive, a 200 Mb DOS D: drive (probably to use as a compressed drive), a 16 Mb Linux swap partition and then the rest of the disk (354 Mb) for Linux filesystem space. Figure 7.2 shows one possible disk partitioning arrangement which takes all the constraints into account.

Notice that the Linux space has been split into two parts, so that the partition holding the root filesystem can fit below the 504 Mb boundary. This leaves the problem of where in the Linux directory tree the other Linux filesystem/partition can usefully be mounted. One obvious division, and the one shown here, is to split the Linux space into a system partition and a user partition. All of the Linux in-