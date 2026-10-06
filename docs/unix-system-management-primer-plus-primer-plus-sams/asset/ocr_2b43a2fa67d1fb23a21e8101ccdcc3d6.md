# Chapter 11 • PERFORMANCE TUNING AND CAPACITY PLANNING

and becomes a bottleneck for the entire area. Disk geometry should be ideal as well as the stripes line up efficiently without wasting space.

The second factor that affects performance is the interface size. Calculating the correct size is a complicated task, involving disk geometry, I/O request sizes, and access patterns. For sequential access patterns, performance is best when the size of an I/O request is the same as the interface size. Successive requests hit different disks, but most operating systems buffer related I/O requests and issue them at the same time, allowing the striped disks to operate in parallel.

Random access patterns call for large interface sizes. These patterns typically signal small I/O requests, and large sizes eliminate the risk of crossing a chunky boundary Crossing this boundary sends the request to the next disk in the array, adding to latency and reducing the overall performance of the array.

The last factor to consider is the disk-controller relationship. With multiple disks acting as a single device and serving requests at the same time, it is ideal for a single controller hosting all of those disks to be overloaded with I/O requests and data transfers. Ideally, your system should have a one-to-one disk-to-controller relationship, but this can be quite an expensive option. An alternative strategy is to alternate disks across two or more controllers, so that consecutive requests go to different controllers.

![](bbox=[0.098, 0.483, 0.168, 0.513])

# ##RAID 0+1: Mirrored Stripes
RAID-0 by itself offers an incredible increase in performance, but does not provide redundancy. If one disk fails in a RAID-0 array, the entire array fails. You can, however, mirror the drives in a RAID-0 configuration, creating what is called RAID 0+1. In this configuration, any single disk can fail without affecting the performance or integrity of the array. RAID 0+1 is seen as the "Holy Grail" of performance and redundancy, but it comes at a price—twice the number of disks is required to provide the mirroring component.

```
# /dev/rdsk/c0t1d03
newfs construct a new file system /dev/rdsk/c0t1d03:(y/n)
/dev/rdsk/c0t1d03: 4198032 sectors in 81 cylinders of 19 tracks, 248 sectors
2050.0MB in 41 groups (22 c/g, 50.62MB/g, 8256 i/q)
super-block backups (for fsck -u 0#) at:
32, 103952, 208782, 317192, 415712, 519632, 623552, 727472, 831392, 935392,
1039232, 1143152, 1247072, 1358992, 1459412, 1558832, 1662752, 1766672,
```