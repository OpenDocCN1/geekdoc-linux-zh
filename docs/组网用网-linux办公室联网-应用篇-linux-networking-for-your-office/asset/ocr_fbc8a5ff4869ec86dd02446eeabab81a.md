# FIGURE 5.1

Partition Magic lets you click on a partition to resize it, move it, or copy it.

# CAUTION

Even if you use a utility like FIPS or Partition Magic, it's wise to back up your system before proceeding because dynamic partition modifications are inherently dangerous.

The details of how to use these partition resizing utilities vary substantially, so you should check the documentation of the package you intend to use to learn how to do it.

If you're installing Linux as the only OS on a system, you can use the Linux fdisk program during installation to set up the partitions. In fact, you might need to use fdisk even if you use a partition resizer. I'll describe this process later, but in case you can set up your partitions before starting the installation, I'll describe Linux's partition requirements here.

A minimal Linux installation typically takes somewhere between 100MB and 500MB, depending on the distribution and what you consider "minimal." To be truly useful, I recommend 1GB or more be devoted to Linux, and if you want to use Linux as a heavy-duty server, you might need quite a few gigabytes of space. Fortunately, the prices of multi-gigabyte hard disks are falling rapidly, so disk space shouldn't be an issue unless you're on a shoestring budget.

For a person who's unfamiliar with Linux, I generally recommend creating only two or three partitions for Linux. One partition, typically 20MB–120MB in size, is the swap partition.