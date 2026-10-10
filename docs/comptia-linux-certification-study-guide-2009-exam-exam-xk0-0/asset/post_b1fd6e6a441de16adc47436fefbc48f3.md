
![](img/95b3ebd6248b36778ccf73988aaab2f2_57_0.png)

## Figure 2.28 Rescue System.

![](img/95b3ebd6248b36778ccf73988aaab2f2_57_1.png)

## Figure 2.29 `parted` help command.

5. At the prompt enter: **parted**.
6. To get help, type **help**.

# DISK TYPES

In the “Laying Out the Filesystem” section, we discussed various disk drive components required during the installation of the Linux operating system. For example, we reviewed primary and extended partitioning and the different types of filesystems (for example, ext3, ext2, and ReiserFS). For this section, two new disk types will be introduced. The first new type added is the LVM. It is used to create logical volumes. The second new type is the RAID. This type is used to improve performance and/or fault tolerance of the disk subsystem. This brings the total number of disk types to three, as shown in Figure 2.30. The LVM-based and partition-based implementations can be configured on top of RAID or non-RAID systems. The Linux system can also support a hybrid system using all the displayed combinations.

# Logical Volume Manager

LVM-based installations offer a unique approach for creating virtual partitions (also known as *logical volumes*). The partition-based approach presented, after implementation, is hard to change. The LVM approach offers greater control of the disk drive environment because you can create virtual partitions that can group physical partitions or disk drives together as one. The command-line tools for LVM are as follows:

- **pvcreate** is a command-line tool for preparing physical volumes for use in LVM.

![](img/95b3ebd6248b36778ccf73988aaab2f2_58_0.png)

- **vgcreate** is a command-line tool for creating and naming volume groups.
- **lvcreate** is a command-line tool for creating and naming logical volumes used by filesystems.

# EXERCISE 2.5: Using Rescue System to execute pvcreate

In this exercise, we will use the **Rescue System** to execute the `pvcreate` command and review the help features.

Complete the following:

1. From a Linux bootable Installation Source Media, boot the target machine.
2. This will start the openSUSE Installer. Select **Rescue System**.
3. The system will display “Rescue login:” Enter **root**.
4. No password is required. This can produce a security concern if no physical security is implemented for the target system. The system will display the “Rescue:~#” prompt.
5. At the prompt enter: `pvcreate --help`.

# Redundant Array of Independent Disk

RAID is a form of technology available to Linux systems that uses your disk subsystem to provide enhanced read/write performance, protection against data lost due to disk failures, or both. It can be implemented using hardware specific RAID controllers (known as *Hardware RAID*) or RAID functionality embedded within the operating system (known as *Software RAID*). Regardless of whether you use hardware- or software-based RAID, your disk subsystem must include two or more hard disks that will be grouped together into an array to form a virtual hard disk. The advantages and disadvantages are presented below:

- Hardware-based RAID performs faster than the software-based RAID implementation. This is because Software RAID requires more CPU time and has additional memory requirements than Hardware RAID.
- Software-based RAID is operating system dependent and hardware-based RAID is vendor independent.
- Hardware-based RAID is more expensive than software-based RAID. Hardware-based RAID requires you to purchase additional hardware components (for example, RAID controllers).

# 48 CHAPTER 2: Installing Linux

To implement RAID technology, you must first have an understanding of three basic RAID concepts. The three concepts are as follows: striping, mirroring, and parity. Striping joins the hard disk drives together to form one large disk drive. For example, three 300MB drives joined together in a striping array will form a single 900MB drive. Striping evenly writes data across all the disks contained in the array. In addition, striping will evenly read data from all disks contained in the array. This increases your overall disk subsystem performance. The downside to striping is that it does not provide any fault tolerance support.

Mirroring joins the hard disk drives together, however; it does not form one large disk drive. Mirroring forms one disk drive whose size is determined based upon the size of the smallest drive. Mirror writes the same data to both the drives. This approach provides you with a level of redundancy in the event one drive crashes. The disadvantage of mirroring is the impact of having to record the same data twice across two different drives. This reduces the disk subsystem performance. Parity stores information in the disk array subsystem that can be used to rebuild files or lost data in the event one of the disks in the disk subsystem array fails. Unlike striping and mirroring, parity requires a minimum of three disks inside the disk array subsystem.

# RAID Levels

To implement striping, mirroring, and parity concepts within your environment, RAID levels are used to describe the different approaches used throughout the industry. The common RAID approaches are presented in Table 2.2. Each RAID level offers advantages and disadvantages, and the best level depends on your requirements. Generally, the partitions should be stored on different drives to get the performance and fault tolerance you want. Do you need a greater performance? Do you need a fault tolerance? If you need both, then RAID 5 is the best solution. In addition to the common levels of RAID, RAID levels can be concatenated (also known as nested). This means that the common RAID level numbers are combined with other common RAID levels, sometimes with a "+" in between. For example, RAID 10 (or RAID 1 + 0) consists of a RAID level 1 disk array subsystem, each of which is one of the “*drives*” of a level 0 disk array subsystem.

During the installation stage, you can elect to configure Hardware RAID or Software RAID subsystems. Hardware RAID installation and configuration are performed in accordance with vendor provided procedures. For Software RAID installation and configuration, the openSUSE expert partitioner tool can be used, as shown in Figure 2.31. The expert partitioner tool allows you to create, edit, and delete Software RAID partitions.

# Table 2.2 RAID Levels

| RAID Level | Striping | Mirroring | Parity | Description |
|---|---|---|---|---|
| 0 | ✓ |  |  | Strips data across two or more hard disk drives within a disk array subsystem. It does not provide data fault tolerance. |
| 1 |  | ✓ |  | Mirrors data across two or more hard disk drives within a disk array subsystem. It does provide data fault tolerance. |
| 2 | ✓ |  | ECC | Provides bit-level striping across five or more hard disk drives within a disk array subsystem. An additional dedicated hard disk drive is used for *Hamming Code* (a form of error correction code) to calculate redundant bits. This level requires a minimum of six disks. |
| 3 | ✓ |  | ✓ | Provides byte-level striping data across two or more hard disk drives within a disk array subsystem. An additional dedicated hard disk drive is used for parity. This level requires a minimum of three disks. |
| 4 | ✓ |  | ✓ | Provides block-level striping data across two or more hard disk drives within a disk array subsystem. An additional dedicated hard disk drive is used for parity. This level requires a minimum of three disks. |
| 5 | ✓ |  | ✓ | Strips data across three or more hard disk drives within a disk array subsystem. A technique known as *distributed parity* is used to also strip the parity bit across each of the disk drives. |
| 6 | ✓ |  | ✓ | Strips data across four or more hard disk drives within a disk array subsystem. A technique known as *dual distributed parity* is used to also strip the parity bits across two disk drives. |
| **Nested RAID Levels** |  |  |  |  |
| 0+1 | ✓ | ✓ |  | This is a striped array set in a mirrored disk array subsystem. A minimum of four disks is required. The number of disks must be even. |
| 1+0 | ✓ | ✓ |  | This is a mirrored array set in a striped disk array subsystem. A minimum of four disks is required. The number of disks must be even. |
| 5+0 | ✓ |  | ✓ | Data is striped between two or more distributed parity RAID disk subsystems. |
| 5+1 | (✓) | ✓ | ✓ | Data is mirrored between two or more distributed parity RAID disk subsystems. The (✓) indicates that the striping is performed as a part of the RAID 5 level. |
