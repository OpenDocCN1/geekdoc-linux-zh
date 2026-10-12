
![](img/9479df2d00f5e62b87366b125224950f_146_0.png)

FIGURE 4-11. A RAID10 configuration

The advantage of a RAID10 volume is that you can achieve the administrative and performance advantages of a RAID0 volume coupled with the fault-tolerance of a RAID1 volume. The downside is that RAID10 volumes are the most expensive, since half of the usable space is lost to the mirror.

For database operations, RAID10 is the most preferable, as you will see later in this chapter.

## RAID2

RAID2 is a parallel access RAID level where an error correction scheme called Hamming Code is used to correct errors. With RAID2, since all disk drives are used for all I/O operations, it can provide high throughput at the speed of one disk drive. RAID2 is shown in Figure 4-12.

While RAID2 can provide for a great deal of throughput, it takes three disk drives to provide the fault tolerance.

## RAID3

RAID3 is a parallel access fault-tolerant method, similar to RAID2. The difference is that RAID3 only requires one disk drive for fault-tolerance. This is due to the fact that RAID3 uses a bit-wise parity rather than error correcting code. RAID3 is shown in Figure 4-13.

![](img/9479df2d00f5e62b87366b125224950f_146_1.png)

FIGURE 4-12. A RAID2 configuration

![](img/9479df2d00f5e62b87366b125224950f_147_0.png)

FIGURE 4-13. A RAID3 configuration

RAID3 can achieve a high transfer rate, but as with RAID2, only one I/O can be processed at a time. For small random I/Os, this can be a liability. RAID2 and RAID3 are both good for large sequential transfers, such as streaming video feeds.

## RAID4

RAID4 is known as *drive parity*, or *data guarding* (not to be confused with Oracle Data Guard). In RAID4, one of the drives in the volume is used for data parity, as shown in Figure 4-14. If any one of the disks fails, the other disks continue running by reconstructing the missing data from the parity drive. The space available in a RAID4 volume incurs the loss of one disk drive's worth of space.

Unlike RAID2 and RAID3, RAID4 uses an independent access technique where multiple disk drives can be accessed simultaneously. This is good for random I/Os since they can be accessed in parallel. Thus the number of I/Os per second can reach the sum of the individual disk drive limits.

![](img/9479df2d00f5e62b87366b125224950f_147_1.png)

FIGURE 4-14. A RAID4 configuration

When you write to a RAID4 volume, extra I/Os are incurred in order to keep the parity up-to-date. In fact, since the parity must be kept up-to-date whenever data is added, the following process occurs:

- 1. Both the old data and old parity stripes are read.
- 2. An XOR is performed on old data and old parity.
- 3. The value and XOR are taken with new data to get the new parity.
- 4. Both the new data and new parity drives are written out.

Thus, for a single RAID4 write, four physical I/Os are incurred. For a RAID4 read, no additional I/O overhead is incurred.

The greatest disadvantage in RAID4 is the dedicated parity disk. Since the parity drive is involved in every write operation, only one write to the volume can be performed at a time. Other writes will begin to queue up under heavy write activity, and reads which depend on those writes will also begin to queue. Add this to the expense of the additional physical operations for each logical write, and you quickly build to a huge performance bottleneck on one disk.

## RAID5

RAID5 is also known as distributed data guarding. RAID5 is similar to RAID4 except that the parity is not isolated to one disk drive. Rather, the parity is distributed across all the disk drives in the system, as shown in Figure 4-15.

As with RAID4, there is a penalty associated with RAID5 writes. For each write to disk, two reads take place, a calculation of the parity is done, and then two writes are done. Although a read generates only one I/O, a write generates four I/Os. This is done to maintain the parity.

![](img/9479df2d00f5e62b87366b125224950f_148_0.png)

FIGURE 4-15. A RAID5 configuration

RAID5 will not suffer from the same write contention to a single disk as RAID4 does. Since the parity is distributed among all drives in the volume, more than one write operation can be in progress at a time. Potentially, there can be half as many writes occurring as there are disks in the volume.

RAID4 and RAID5 are both very economical, since you only lose one disk drive’s worth of space in order to provide fault-tolerance; however, they pay the price in terms of performance.

## Parity Overview

RAID3, RAID4, and RAID5 use a parity in order to maintain fault-tolerance. A parity is a binary method where the sum of the individual pieces add up to either an even or an odd value. The bits are added up using binary arithmetic and either a 0 or a 1 is added as a parity bit. The value of this parity bit depends on what is needed to maintain the proper parity of the sum of all of the bits.

## Parity Example

Let’s look at an example using three different bits and one parity bit. For our example, we will select even parity, thus the sum of all of the bits must add up to an even number. Taking the following three values:

```
A=1
B=0
C=1
```

These values add up to 2, thus the sum of A+B+C+Parity will equal an even number (2) if the value of the parity bit is 0. In another example, let’s take the following values:

```
A=0
B=1
C=1
```

In order for the sum of these values A+B+C+Parity to equal an even number (2), the value of the parity bit must be 1. In this manner, parity is created on every disk drive in the RAID controller—byte by byte, bit by bit.

## Creating Parity

In order to create a RAID3, RAID4, or RAID5 volume, each data stripe must be read off of each disk drive and the parity calculated. This is sometimes known as data scrubbing. If you have created one of these RAID volumes, you may have noticed it taking a long time to create. This is why. Every disk in the volume must be read, parity created, and the parity must be written out. This can be quite time-consuming, depending on the size of the disk drives and the number of disk drives in the array.

## Maintaining Parity

Once the volume has been created, it is unnecessary to recalculate the parity each time. Since the parity has already been calculated, it is possible to modify the parity based on the changes made by the insertion or modification of data. For example, if a data bit does not change, the parity bit does not need to change. If the data bit changes, then so must the parity bit. This is done using a bitwise exclusive "OR" operation (or XOR) on both the data and the parity bits.

Thus, to modify parity data, the following steps should be performed:

- 1. Read the data and parity stripes.
- 2. XOR the old data and parity.
- 3. Calculate a new parity using an XOR operation and new data.
- 4. Write out both new data and new parity.

Thus, for a parity write, four physical I/Os and two XORs are incurred. Not only are the additional I/Os important due to disk drive limitations, but their order is as well. Since there are two I/Os, two calculations, and two additional I/Os, the latency is, at minimum, twice the latency of a non-parity I/O (assuming infinitely fast parity calculation). This is important considering how sensitive Oracle is to I/O latency.

## RAID Performance Overview

Now that you have seen the different RAID levels, let's look at how they perform. From this section until the end of the chapter, we will only look at the commonest RAID levels: RAID0, RAID1, RAID10, and RAID5. Although you may encounter other RAID levels, it is rare.

First, let's review a few facts.

- **Individual I/O operations occur at the speed of one disk drive** No matter how many disk drives are in the RAID volume, the I/O is going to one of them, thus you cannot exceed that speed. It is the fact that multiple I/O operations can occur at the same time on different disks that gives us better performance in a RAID system.
- **If you do exceed the physical performance limitations of the disk drive, queuing will occur and latencies will increase.**
- **The optimal performance rate for random I/Os is 128 IOPS (in these examples)** Exceeding this rate may cause increased latencies. Additional drives will allow for additional concurrency and more performance. If one drive can do 128 IOPS, a ten-drive RAID volume can do 1280 IOPS.
- **Almost all I/O operations are random in nature** Even if you are doing a sequential table scan, if someone else is accessing the same disk, the I/Os will become random.

Now let's look at the performance of some of the common RAID levels.
