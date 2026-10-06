
## Take Advantage of extent-Based Volume Managers

The proliferation of extent-based volume managers—also known as logical volume managers—is eliminating the problem of partitioning altogether. Rather than associating a fixed-size partition with a Unix disk device, extent-based volume managers treat pools of space from which they can allocate arbitrarily sized chunks extents to logical devices (see Figure 11.3). Extent-based volume managers can dynamically resize disk devices and expand file system capacity. These managers can also take space from other disks, which means file systems created on one disk are not limited to the size of that one disk.

### FIGURE 11.3
A high-level view of a physical disk with three extents allocated to different logical disks. 1GB of free space is available for the creation of new extents.

![](img/894492738e879267320b8d6f9a044180_331_0.png)

Veritas Volume Manager is the most widely known extent-based volume manager, and it’s especially popular for Solaris systems. IBM’s LVM (the standard disk management software on AIX) and Linux VM are just as effective.

## Use Quotas to Limit User Space Consumption

The file system quota is one of the most time-tested methods of disk space preservation. Quotas place limits on the number of blocks and inodes that can be allocated to a particular user or group within the Unix system, and they can minimize excessive usage by any one user.

BSD style quotas are the most common type and are available on many Unix file systems, including UFS, ext2fs, and Berkeley FFS. These quotas apply to entire file systems, not just files or directories. BSD quotas also support soft and hard limits; can exceed soft limits for a certain period of time (the grace period), but they can never exceed an hard limit. When the hard limit is reached or the soft limit grace period expires, the system can allocate no more blocks or inodes (depending on which type of quota has been exceeded).

The quota command displays the current status of quotas for a user, as:

```bash
bash$ quota
Disk quotas for user jeff (uid 1000):
Filesystem blocks quota limit grace files quota limit grace
/home 281455 514288 1048576 11325 0
```

If the soft limit has been exceeded, a grace period reflects how much time the user has to reduce usage using the soft limit.

Other file systems have more granular quota mechanisms. For example, AFS (the Andrew File System) introduces the concept of volume, which is a directory tree that can be mounted anywhere within the AFS namespace. You can assign each volume a size quota; if you want to limit the size of a certain directory, you can mount a volume in its place and assign a quota to that volume. The fs lg command shows the quota status for an AFS directory's corresponding

```bash
bash pwd
/afs/umich.edu/user/jh/jhorwitz
bash fs lg -
```

| Volume Name | Quota | Used | Partition |
| :--- | :--- | :--- | :--- |
| user.jhorwitz | 100000 | 83410 83% | 65% |

## Gauging Memory Performance and Capacity

Memory is needed to run everything from the smallest Unix utility to the largest instance of an Oracle database. Running out of memory incurs an enormous penalty in performance when the system begins to swap, monitoring of its performance and usage is critical.

## Virtual Memory Implementations

Unix virtual memory is a complicated subsystem that system administrators frequently misunderstand, which is unfortunate because it is such an important part of the operating system. Virtual memory makes possible the transparent sharing of code and data between processes, the allocation of more memory than physically present on a system, and even plays a part file system performance on some operating systems by providing caching functionality. Virtual memory implementations differ widely among the many flavors of Unix, but the following four concepts are always present:

- Real memory
- Paging
- Swap space
- Swapping

## Real Memory

Real memory is a system's actual physical memory, known as RAM. Real memory is the fastest and most efficient way to store temporary data, so applications should be given as much of it possible. RAM comes in many forms today: SIMMs, DIMMs, Rambus, DDR, and even custom memory boards such as the mezzanine boards used in Sun Netra tl 105 servers. Error correction (usually ECC) is also available on most forms of RAM, though it comes at a pre-

## Use Error Correction in Server Hardware

Always install RAM with error correction in server hardware. The cost is higher, but it significantly reduces the risk that a failing memory module will crash your system.

## Swap Space

Swap space is an area of disk dedicated to the temporary storage of memory, usually invoked by paging and swapping process. Some operating systems such as Linux do not require swap space; others, for example, Solaris running an Oracle database, often recommend swap spaces two to four times the size of the real memory on the system. Only experience can expose the true needs of a system.

## Solaris Uses Swap for More Than One Function

Solaris uses swap space as a crash dump when the operating system panics, so the kernel image can be debugged. The kernel writes the dump at the end of the swap partition to prevent overwriting at the next reboot, so administrators maintain twice as much swap space as real memory on a Solaris server.

## Paging

Paging is the process of transferring data from disk to memory and vice versa. The process is called paging because Unix memory is divided into evenly sized pages; page sizes are 4KB and 8KB. When an executable program runs, it is "paging" from one disk one page at a time. Likewise, when pages of memory remain idle for a certain period of time, they may be paged out to swap space to make the idle RAM available to other programs that need it.

Many file system operations are tied to the virtual memory subsystem (pmap in particular), so significant file system activity can result in significant paging activity. If your system is paging constantly but not low on real memory, you may want to check file system I/O operations using `vmstat` or `ostat`.

## Swapping

Paging is often confused with swapping, but they are far from the same thing. While paging transfers idle parts of a process memory footprint to disk, swapping transfers entire processes to disk when there is not enough real memory to satisfy new allocations. Swapping activity is usually an indication of a low memory condition.

## Displaying Swap Statistics

Each operating system has a different method for displaying swap space statistics. Using Solaris as an example, `swap -l` lists the swap devices that are configured on the system and the size of each, and `swap -s` displays the usage statistics for each swap device.

```bash
bash$ usr/sbin/swap -1
swapfile dev swaplo blocks free
/dev/dsk/c0t0ds1 32,1 16 2101536 1956640
bash$ /usr/sbin/swap -s
total: 316952k bytes allocated + 17824k reserved = 334776k used, 1045936k
available
```

Other operating systems have different ways of displaying this information, as summarized in Table 11.3.

### TABLE 11.3 Commands for Display Swap Statistics on Different Unix Operating Systems

| Operating System | Swap Statistics Commands |
| :--- | :--- |
| OpenBSD | swapctl -1 |
| | swapctl -s |
| Red Hat Linux | swapon -s |
| Solaris | swap -1 |
| | swap -s |

## Using vmstat to Monitor Memory Usage

The Solaris version of vmstat can report detailed virtual memory statistics. The important fields are as follows:

| | |
| :--- | :--- |
| swap | Available swap space (in kilobytes) |
| free | Available real memory (in kilobytes) |
| pi | Page-in operations |
| po | Page-out operations |
| sr | Scan rate |

The swap and free fields are self-explanatory, but the others bear some explanation. An abnormally high number of page-in operations may be alarming, but in most cases it is normal. Remember that during paging in, data is being read into memory; paging in can also be indicative of file system activity. In most cases, you can ignore this column.

The free list also plays a part in paging. Unix operating systems typically reserve a small amount of physical memory, called the free list, so there is always memory available for new processes. When the free list hits a low-water mark (called lotsfree on Solaris), the operating system scans for idle pages. The system can page out those pages to reclaim some of that memory. Paging out is normal behavior for most Unix systems, but excessive page-outs can have a
