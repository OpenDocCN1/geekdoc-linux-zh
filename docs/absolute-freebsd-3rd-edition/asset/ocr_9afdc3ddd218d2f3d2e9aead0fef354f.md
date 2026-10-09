The installer asks me whether I’m sure. This layout should keep Bert from complaining that log files have overflowed his system, so I’m content. Select **Finish** to partition the disk and have the install proceed.

# ## ZFS Installs

If I choose ZFS, I’ll get the ZFS configuration screen shown in Figure 3-15.

![](bbox=[0.12, 0.29, 0.89, 0.64])

The default option is Install, which will give you an error because you haven’t selected a ZFS virtual device type yet. You’ll need to start with Pool Type/Disks. Before we get there, though, let’s look at the other choices.

The default name of a FreeBSD root ZFS pool is *zroot*. There’s no real reason to change this, unless you want your system to look different than any other ZFS system out there or your organization has standards for naming pools.

The Force 4K Sectors option is important for reasons we’ll discuss in Chapter 10. Unless you know for absolutely certain that your disks have