# Chapter 8

# Storage

# Enabling swapping

Raw partitions or logical values, rather than structured filesystems, are normally used for swap space. Instead of using a filesystem to keep track of the swap area's contents, the kernel maintains its own simplified mapping from memory blocks to swap space blocks.

On some systems, it's also possible to swap a file in a filesystem partition. Over older kernels this configuration can be slower than a dedicated partition, but it's still very handy in a pinch. In any event, logical volume managers eliminate most of the regions you might want to use a swap file rather than a swap volume.

See page 1129 for information about splitting areas.

The swap space you have, the virtual memory processes can also allocate. The best virtual memory performance is achieved when the swap area is split among several devices. Of course, the best option of all is not to swap; consider adding RAM if you find yourself needing to optimize swap performance.

On Linux, swap areas must be initialized with mkswap, which takes the device name of the swap volume as an argument.

You can manually enable swapping to a particular device with swap or -a device on Solaris. However, you will generally want to have this function performed automatically at boot time. Except on AIX, you can list swap areas in the regular filesystem catalog (stab or vstab) by giving them a filesystem type of swap. AIX has a separate file that lists the system's swap areas, /etc/swapspaces.

To review the system's current swapping configuration, run swap -s on Linux systems, swap -s on Solaris, or swapinfo on HP-UX.

![](bbox=[0.186, 0.596, 0.228, 0.632])

On AIX, you can use the mkps command to create a logical volume swapping, adding it to the /etc/swapspaces file, and start using it. This is the command called by the SMIT interface.

# 8.10 ZFS: ALL YOUR STORAGE PROBLEMS SOLVED

ZFS was introduced in 2005 as a component of OpenSolaris and it quickly made its way to Solaris 10 and to various BSD-distributions. In 2008, it became usable as a root filesystem, and it has the front-line filesystem of choice for Solaris ever since.

Although ZFS is usually referred to as a filesystem, it is in fact a comprehensive approach to storage management that handles the functions of a logical volume manager and a RAID controller. it redefines many common aspects of storage administration to make them simpler, easier, and more consistent. Although the current version of ZFS has a few limitations, most fall into the "not yet implemented" category rather than the "can't do for architectural reasons" category.

The advantages of ZFS's integrated approach are clear. If you're not familiar with ZFS, we predict that you'll enjoy working with it. There is little doubt that