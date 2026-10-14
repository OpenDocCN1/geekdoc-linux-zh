# The Cluster Logical Storage Manager (CLSM)

The Cluster Logical Storage Manager subsystem is a cluster-aware version of the Logical Storage Manager (which is a port of the VERITAS Volume Manager by Veritas Software Corporation). The CLSM allows you to use the Logical Storage Manager (LSM) in a cluster.

# 14.1    Introduction to the Logical Storage Manager

What follows is a brief introduction to the Logical Storage Manager. For more in-depth information, see the Tru64 UNIX Logical Storage Manager Guide as well as the Tru64 UNIX File System Administration Handbook by Steve Hancock.

LSM is essentially RAID implemented in software. What is RAID? See Figure 14-1.

LSM manages a pool of physical storage and allows you to divide that pool in a variety of ways to create virtual devices that are presented to the operating system as logical volumes. These logical volumes can be accessed via both block and character device special files located in the /dev/vol and /dev/rvol subdirectories respectively.

The CLSM subsystem sits atop the I/O Mapper and the Device Request Dispatcher (DRD) and below the file systems layer as illustrated in Figure 14-2.

¹ LSM is based on version 2.3 of the Veritas Volume Manager. Additional development is also done by Compaq to enhance the product (e.g., TruCluster support).