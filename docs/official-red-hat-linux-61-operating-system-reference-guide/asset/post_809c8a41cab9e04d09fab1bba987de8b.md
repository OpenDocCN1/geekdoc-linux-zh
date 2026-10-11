
issues, some philosophical, some technical. On the philosophical side, above a certain size, it seemed that the additional space provided by a larger drive created more clutter. On the technical side, some file systems were never designed to support larger drives. Or the file systems *could* support larger drives, but the overhead imposed by the file system became excessive.

The solution to this problem was to divide disks into **partitions**. Each partition can be accessed as if it were a separate disk. This is done through the addition of a **partition table**.

## Please Note

While the diagrams in this chapter show the partition table as being separate from the actual disk drive, this is not entirely accurate. In reality, the partition table is stored at the very start of the disk, before any file system or user data. But for clarity, we'll keep it separate in our diagrams.

## Figure B-5 Disk Drive with Partition Table

![](img/eda1471ab4ce718c791c97a85559a478_300_0.png)

As Figure B-5, Disk Drive with Partition Table shows, the partition table is divided into four sections. Each section can hold the information necessary to define a single partition, meaning that the partition table can define no more than four partitions. Each partition table entry contains several important characteristics of the partition:

- The points on the disk where the partition starts and ends;
- Whether the partition is "active";
- The partition's type.

Let's take a closer look at each of these characteristics. The starting and ending points actually define the partition's size and location on the disk. The "active" flag is used by some operating systems' boot loaders. In other words, the operating system in the partition that is marked "active" will be booted.

The partition's type can be a bit confusing. The type is a number that identifies the partition's anticipated usage. If that statement sounds a bit vague, that's because the meaning of the partition type is a bit vague. Some operating systems use the partition type to denote a specific filesystem type, to flag the partition as being associated with a particular operating system, to indicate that the partition contains a bootable operating system, or some combination of the three.

Table B-1, Partition Types contains a listing of some popular (and obscure) partition types, along with their numeric values.

**Table B-1 Partition Types**

| Partition Type | Value | Partition Type | Value |
| :--- | :--- | :--- | :--- |
| Empty | 00 | Novell Netware 386 | 65 |
| DOS 12-bit FAT | 01 | PIC/IX | 75 |
| XENIX root | 02 | Old MINIX | 80 |
| XENIX usr | 03 | Linux/MINUX | 81 |
| DOS 16-bit <=32M | 04 | Linux swap | 82 |
| Extended | 05 | Linux native | 83 |
| DOS 16-bit >=32 | 06 | Linux extended | 85 |
| OS/2 HPFS | 07 | Amoeba | 93 |
| AIX | 08 | Amoeba BBT | 94 |
| AIX bootable | 09 | BSD/386 | a5 |
| OS/2 Boot Manager | 0a | OpenBSD | a6 |
| Win95 FAT32 | 0b | NEXTSTEP | a7 |
| Win95 FAT32 (LBA) | 0c | BSDI fs | b7 |
| Win95 FAT16 (LBA) | 0e | BSDI swap | b8 |
| Win95 Extended (LBA) | 0f | Svr4ix | c7 |
| Venix 80286 | 40 | CP/M | db |
| Novell? | 51 | DOS access | e1 |
| Micropart | 52 | DOS R/O | e3 |
| GNU HURD | 63 | DOS secondary | f2 |
| Novell Network 286 | 64 | BBT | ff |

Now you might be wondering how all this additional complexity is normally used. See Figure B-6, *Disk Drive With Single Partition* for an example.

## Figure B-6 Disk Drive With Single Partition

![](img/eda1471ab4ce718c791c97a85559a478_302_0.png)

That’s right -- in many cases there is but a single partition spanning the entire disk, essentially duplicating the pre-partitioned days of yore. The partition table has only one entry used, and it points to the start of the partition.

We’ve labeled this partition as being of type "DOS," although as you can see from Table B-1, *Partition Types*, that’s a bit simplistic, but adequate for the purposes of this discussion. This is a typical partition layout for most newly purchased computers with some version of Windows pre-installed.

## B.1.3 Partitions within Partitions — An Overview of Extended Partitions

Of course, in time it became obvious that four partitions would not be enough. As disk drives continued to grow, it became more and more likely that a person could configure four reasonably-sized partitions and still have disk space left over. There needed to be some way of creating more partitions.

Enter the extended partition. As you may have noticed in Table B-1, Partition Types, there is an “Extended” partition type; it is this partition type that is at the heart of extended partitions. Here’s how it works.

When a partition is created and its type is set to “Extended,” an extended partition table is created. In essence, the extended partition is like a disk drive in its own right -- it has a partition table that points to one or more partitions (now called logical partitions, as opposed to the four primary partitions) contained entirely within the extended partition itself. Figure B-7, Disk Drive With Extended Partition shows a disk drive with one primary partition, and one extended partition containing two logical partitions (along with some unpartitioned free space).

## Figure B-7 Disk Drive With Extended Partition

![](img/eda1471ab4ce718c791c97a85559a478_304_0.png)

As this figure implies, there is a difference between primary and logical partitions -- there can only be four primary partitions, but there is no fixed limit to the number of logical partitions that can exist. (However, in reality it is probably not a good idea to try to define and use more than 12 logical partitions on a single disk drive.)

Now that we’ve discussed partitions in general, let’s see how to use this knowledge to get Red Hat Linux installed.

## B.1.4 Making Room For Red Hat Linux

There are three possible scenarios you may face when attempting to repartition your hard disk:

- Unpartitioned free space is available.
- An unused partition is available.
- Free space in an actively used partition is available.

Let’s look at each scenario in order.

> **Please Note**
>
> Please keep in mind that the following illustrations are simplified in the interest of clarity, and do not reflect the exact partition layout that you will encounter when actually installing Red Hat Linux.

### Using Unpartitioned Free Space

In this situation, the partitions already defined do not span the entire hard disk, leaving unallocated space that is not part of any defined partition. Figure B-8, *Disk Drive with Unpartitioned Free Space* shows what this might look like.

![](img/eda1471ab4ce718c791c97a85559a478_305_0.png)

If you think about it, an unused hard disk also falls into this category; the only difference is that *all* the space is not part of any defined partition.

In any case, you can simply create the necessary partitions from the unused space. Unfortunately, this scenario, although very simple, is not very likely (unless you've just purchased a new disk just for Red Hat Linux). Let's move on to a slightly more common situation.

### Using Space From An Unused Partition

In this case, maybe you have one or more partitions that you just don't use any longer. Perhaps you've dabbled with another operating system in the past, and the partition(s) you've dedicated to it never seem to be used anymore. Figure B-9, Disk Drive With an Unused Partition illustrates such a situation.

## Figure B-9 Disk Drive With an Unused Partition

![](img/eda1471ab4ce718c791c97a85559a478_306_0.png)

If you find yourself in this situation, you can use the space allocated to the unused partition. You'll first need to delete the partition, and then create the appropriate Linux partition(s) in its place. You can either delete the partition using DOS fdisk, or you'll be given the opportunity to do so during a custom-class installation.
