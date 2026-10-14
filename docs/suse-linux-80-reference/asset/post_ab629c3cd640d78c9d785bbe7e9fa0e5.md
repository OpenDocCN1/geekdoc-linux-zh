
- To set up an Internet or FTP server: 700 MB minimum.

How should the disk be divided up? A simple question which requires a not-so-simple answer.

> **Tip**
>
> It is a very good idea, especially for novices, to follow the strategy suggested by YaST: if needed, place a small partition at the beginning of the hard disk for `/boot` (about 10 MB, for large drives, a 1-cylinder partition is enough), a partition for swap (128–256 MB), all the rest for `/`.

If you want to partition something, but also as little as possible, then the following simple rules apply.

- Up to 500 MB: swap partition and root (`/`)
- 500 MB to 4 GB: small boot partition for the kernel and LILO at the very beginning of the hard disk (`/boot`, approximately 8–16 MB or 1 cylinder), a swap partition, and the rest for the root partition `/`.
- More than 4 GB: boot (`/boot`), swap, root (250 MB), home (`/home` with approximately 20 MB per user) and the rest for applications (`/usr`), possibly a further partition for `/opt` and for `/var`.

> **Note**
>
> If you plan to start Linux directly from the hard disk, you will need a Linux partition below the “1024-cylinder limit” as a boot partition (read more on this in *LILO Locations* on page 94). This does not concern you if you are starting Linux from DOS/Windows with loadlin.

Bear in mind that some programs (mostly commercial programs) install their data in `/opt`. If you are installing a number of these, either create a separate partition for `/opt` or enlarge the dimensions of the root partition accordingly. KDE and GNOME are also stored in `/opt`.

## Partitioning for Experts

In Section *Partitioning Tips* on the page before, details are given as to how to partition your system. This section should provide more detailed information for tailoring a system that best suits your needs. This section is mainly of interest for those who want an optimized system as far as security and performance are concerned and who are prepared to reinstall the complete system where necessary.

## Special Installation Procedures

It is absolutely essential that you have extensive knowledge of the functions of a UNIX file system. You should be familiar with the topics mount point, primary, extended, and logical partitions.

It should be mentioned here that there is no golden rule for all, but many rules for each situation. However, you will find concrete figures in this section to help you.

First, you need to gather the following information:

- What is the purpose of the machine (file server, compute server, stand-alone machine)?
- How many people are going to work with this machine (simultaneous logins)?
- How many hard disks are installed? How big are they and what kind (EIDE, SCSI, or even RAID controllers)?

### Size of Swap Partition

Quite often you will read: “Swap should be at least as large as physical RAM”. This is a relic of times when 8 MB was regarded as a lot of RAM memory. Applications that need considerable memory have shifted these values up. Generally, 64 MB of virtual swap should be sufficient. Do not be stingy. If you compile a kernel in X and want to have a look at the manual pages using Netscape and have an emacs running, you will already take up all 64 MB. To be safe, opt for at least 128 MB of virtual memory. One thing you should never do is not assign swap space at all. Even on a machine with 256 MB RAM, there should be a swap partition. The reasons for that are outlined in Section Processing Speed and Size of Main Memory on page 55.

If you want to run extensive simulations with a memory requirement of several gigabytes, read Section Using as a Compute Server on page 53 (Example: compute server).

### Implementation of the Computer

#### Computer Used as Stand-Alone Machine

The most common use for a Linux machine is as a stand-alone computer. To make decisions as easy as possible for you, we provide you with some concrete figures you can use at home or at your company. Table 3.1 on the following page is an overview of size requirements for different Linux systems.

| installation | required disk space |
|---|---|
| minimum | 180 MB to 400 MB |
| small | 400 MB to 800 MB |
| medium | 800 MB to 4 GB |
| large | 4 GB to 8 GB |

*Table 3.1: Examples of Disk Space Requirements for Different Installations*

##### Example: stand-alone machine (small)

You have a 500 MB spare hard disk to hold Linux: use a 64 MB swap partition and the rest for / (root partition).

##### Example: stand-alone machine (average)

You have 1.2 GB available for Linux. A small boot partition /boot (5–10 MB or 1 cylinder), 128 MB for Swap, 800 MB for /, and the rest for a separate /home partition.

##### Example: stand-alone machine (deluxe)

If you have more than 1.2 GB available, there is no standard way to partition. Read Section *Optimizations* on the next page.

#### Using as a File Server

Here, hard disk performance is *really* crucial. You should use SCSI devices if possible. Keep in mind the performance of the disk and the controller. A file server is used to save data centrally. This data might be home directories, a database, or other archives. The advantage of this is that administration of the data is simple.

If the file server will serve a huge net (20 users and more), optimizing hard disk access is essential. Suppose you want to provide a file server for 25 users (their home directories). If the average user requires 100–150 MB for personal space, a 4 GB disk mounted under /home will probably do.

If there are fifty such users, you will need an 8 GB disk. In this case, it would be better to split home into two 4-GB disks, as now they would then share the load (and access time).

> **Tip**
>
> The web browser cache should absolutely be stored locally on the user’s hard disk.

#### Using as a Compute Server

A compute server is generally a powerful machine that carries out extensive calculations over the net. Normally, such a machine is equipped with extensive main memory (512 MB RAM or greater). The only point where fast disks are needed is for the swap space. If you have a number of hard disks, you can spread swap partitions across them.

#### Optimizations

The disks are normally the limiting factor. To avoid this bottleneck, there are three possibilities that should be used together:

- separate the load onto multiple disks
- use an optimized file system (e.g., reiserfs)
- equip your file server with enough memory (at least 256 MB)

##### Using Multiple Disks in Parallel

This needs some further discussion. The total amount of time needed for transferring data can be separated into five factors:

- time elapsed until the request reaches the controller
- time elapsed until this request is sent to the disk
- time elapsed until the hard disk manages to set its head
- time elapsed until the media has turned to the right sector
- time elapsed for transferring data

The first factor depends on the network connection and has to be regulated elsewhere. We do not cover this here. The second factor can be ignored, because it depends on the controller. The third factor is the vital part. The time is counted in milliseconds. Relative to the access time of main memory (measured in nanoseconds), this is a factor of one million. The fourth factor depends on the disk rotation speed. The fifth factor depends on the rotation speed, the number of heads, and the actual position of the data (inside or outside).

For optimized performance, consider factor three. Here, the SCSI feature “disconnect” comes into play. Look at what happens:

The controller sends the command (in this case to the hard disk) “Go to track x, sector y” to the device. Now the disk motor has to start. If this is an intelligent disk (if it supports disconnect) and the driver itself is also able to disconnect, the controller sends a disconnect and the disk separates itself from the SCSI bus. Now other SCSI devices can do work. After a time (depending on the strategy or load on the SCSI bus), a connection to the disk is reestablished. Normally, the device has now reached the requested track.

On a multitasking, multiuser system like Linux, there are lots of optimizations that can be done here. Look at an output of the command `df` (see Output 1).

| Filesystem | Size | Used | Avail | Use% | Mounted on |
|---|---:|---:|---:|---:|---|
| /dev/sda5 | 1.8G | 1.6G | 201M | 89% | / |
| /dev/sda1 | 23M | 3.9M | 17M | 18% | /boot |
| /dev/sdb1 | 2.9G | 2.1G | 677M | 76% | /usr |
| /dev/sdc1 | 1.9G | 958M | 941M | 51% | /usr/lib |
| shmfs | 185M | 0 | 184M | 0% | /dev/shm |

*Output 1: Example of df Command Output*

How does this parallelizing benefit us? Suppose we enter in `/usr/src`:

```shell
root@earth:/usr/src/ > tar xzf package.tgz -C /usr/lib
```

Here, package.tgz will be untarred into /usr/lib/package. To do so, the shell launches tar and gzip (located in /bin, so on /dev/sda) then package.tgz in /usr/src is read (on /dev/sdb). Last, the extracted data is written to /usr/lib (on /dev/sdc). Using parallelizing, positioning as well as read and write of the disks’ internal buffers can be activated at the same time.

This is only one example. There are many more. If this example were a frequent processing requirement and if there are many disks (with these speeds), as a rule of thumb, /usr and /usr/lib should physically be placed on different disks. Here /usr/lib should have approximately seventy percent of the capacity of /usr. /, due to its access, should be placed on the disk containing /usr/lib.

From a certain number of SCSI disks onwards (4–5), consider buying a RAID controller. Thus, operations on the disks are not merely semiparallel but parallel. Fault tolerance is one of its famous by-products.
