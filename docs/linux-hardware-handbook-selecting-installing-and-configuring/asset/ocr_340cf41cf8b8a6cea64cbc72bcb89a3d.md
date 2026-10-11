Before you post, you should search for similar problems on Deja News
(http://www.deja.com/usenet/). This site archives Usenet News postings, and enables you to
search through both recent and older postings for keywords.

# ## Installing Linux

Installing Linux on a computer that already contains Windows entails providing Linux with
disk space. One way to achieve this goal is to purchase a second hard disk. You can then
devote one disk to Windows and another to Linux. If you don’t want to purchase a new hard
disk, though, you must re-allocate disk space used by Windows so that Linux can use that
space. The easiest way to do this is to remove Windows entirely. If you want to keep Windows
as well as Linux, however, you must find a way to shrink the Windows installation so that you
can install Linux.

> **NOTE**
> 
> Some Linux distributions can install themselves in a Windows partition, thus obviating
> the need to repartition the hard disk. I recommend you not use this option, however.
> Linux’s disk performance suffers when it’s installed in this way, and it’s generally not
> as reliable as an installation to a dedicated Linux partition. With the ready availability
> of tools to repartition, as I describe shortly, there’s very little reason to install Linux to
> a Windows partition.

# ## Removing Windows

If you want to devote the computer entirely to Linux, you can remove Windows from the
machine. The simplest way to do this is to use whatever partitioning tools your Linux distribu-
tion provides during installation. For instance, Figure 21.2 shows the partitioning tool from the
Corel Linux 1.0 installation. To remove the FAT-32 partition on which Windows resides, you
click its name (*`/dev/hda1`*) and then click Delete. You can then select the entire hard disk
(*`/dev/hda`*) and click Add to create new Linux partitions.

Precisely how you perform these actions varies from one Linux distribution to another, so the
details of the preceding description might not apply to your distribution. The basic principles
are the same, though.

Some distributions include options that cause the distribution to automatically take over the
entire hard disk. This feature can be convenient if you want to quickly install Linux with what-
ever default partitioning scheme the distribution favors. But if you want finer control, you
should select the customized partitioning options.