
`top`为监控CPU利用率提供了一个非常好的起点。如果它没有提供你所需的所有信息，你可能想尝试`vmstat`工具。首先，你可能需要使用`yum -y install sysstat`安装此包。通过`vmstat`，你可以获得服务器上发生情况的详尽的视图。CPU部分特别值得关注，因为它包含了CPU使用率最重要的参数。

- `cs`上文切换的次数
- `us`CPU处于用户空间的时间百分比
- `sy`CPU处于内核空间的时间百分比
- `id`CPU空闲百分比

`vmstat`有两种运行方式。可能最实用的方式是采样模式。在这种模式下，`vmstat`每隔几秒进行一次采样。你必须指定时间间隔来运行`vmstat`。运行`vmstat`的另一种方式是使用`-s`选项。在这种模式下，会显示自系统启动以来的统计数据。运行`vmstat`总是有利。在这种模式下，它会显示关于处理器、内存、交换分区的信息。除了CPU相关的选项外，`vmstat`还会显示关于交换分区、I/O和系统的信息。这些选项将在本文后续介绍。

# 分析内存占用

`top`为监控CPU利用率提供了一个非常好的起点。如果它没有提供你所需的所有信息，你可能想尝试`vmstat`工具。首先，你可能需要使用`yum -y install sysstat`安装此包。通过`vmstat`，你可以获得服务器上发生情况的详尽的视图。CPU部分特别值得关注，因为它包含了CPU使用率最重要的参数。

分析内存使用 427

```
915056 used memory
168988 active memory
598880 inactive memory
101872 free memory
541564 buffer memory
59084 swap cache
2064376 total swap
0 used swap
2064376 free swap
142311 non-nice user cpu ticks
251 nice user cpu ticks
30673 system cpu ticks
1332644 idle cpu ticks
242566 IO-wait cpu ticks
371 IRQ cpu ticks
1175 softirq cpu ticks
0 stolen cpu ticks
21556610 pages paged in
56830 pages paged out
0 pages swapped in
0 pages swapped out
2390762 interrupts
695020 CPU context switches
1347791046 boot time
6233 forks
```

## 内核内存

在分析内存使用时，你还应该考虑内核本身使用的内存。这被称为slab内存。你可以在`/proc/meminfo`文件中查看当前使用的slab数量。列表17.9提供了该文件内容的示例，它提供了关于内存使用的的详细信息。

列表17.9：`/proc/meminfo`文件提供了关于内存使用的详细信息

```
[root@hnml-01 ~] cat /proc/meminfo
MemTotal: 1016928 kB
MemFree: 99568 kB
Buffers: 541568 kB
Cached: 59092 kB
SwapCached: 0 kB
```

- Active: 171172 kB
- Inactive: 598808 kB
- Active(anon): 69128 kB
- Inactive(anon): 103728 kB
- Active(file): 102044 kB
- Inactive(file): 495080 kB
- Unevictable: 0 kB
- Mlocked: 0 kB
- SwapTotal: 2064376 kB
- SwapFree: 2064376 kB
- Dirty: 36 kB
- Writeback: 0 kB
- AnonPages: 169292 kB
- Mapped: 37268 kB
- Shmem: 3492 kB
- Slab: 90420 kB
- SReclaimable: 32420 kB
- SUnreclaim: 58000 kB
- KernelStack: 2440 kB
- PageTables: 27636 kB
- NFS_Unstable: 0 kB
- Bounce: 0 kB
- WritebackTmp: 0 kB
- CommitLimit: 2572840 kB
- Committed_AS: 668328 kB
- VallocTotal: 3435973836 kB
- VallocUsed: 2723452 kB
- VallocChunk: 3435948140 kB
- HardwareCorrupted: 0 kB
- AnonHugePages: 38912 kB
- HugePages_Total: 0
- HugePages_Free: 0
- HugePages_Rsvd: 0
- HugePages_Surp: 0
- Hugepagesize: 2048 kB
- DirectMap4k: 8192 kB
- DirectMap2M: 1040384 kB

在列表17.9中，你可以看到Linux内核使用的内存相对较小。如果你需要更多关于内核如何使用这些内存的详细信息，你可能想要使用`slabtop`工具。该工具提供了关于内核不同部分（称为对象）以及它们具体在做什么的信息。对于普通的性能分析目的，SIZE和NAME列是最感兴趣的。其他列主要供程序员和内核开发者感兴趣，本章将不会讨论这些内容。列表17.10显示了`slabtop`提供的信息类型示例。

## 分析内存使用

列表17.10：`slabtop`工具提供了关于内核内存使用的信息

```
[root@]# slabtop
Active / Total Objects (% used) : 1069357 / 1105539 (96.7%)
Active / Total Slabs (% used) : 19402 / 19408 (100.0%)
Active / Total Caches (% used) : 110 / 190 (57.9%)
Active / Total Size (% used) : 71203.9K / 77888.23K (91.4%)
Minimum / Maximum Object : 0.02k / 0.07k / 4096.0k

| OBJECT USE SIZE SLABS OBJ/SLAB CACHE SIZE NAME |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 480672 | 480640 | 0.02k | 3338 | 144 | | avtab_node |
| 334096 | 333932 | 0.03k | 2983 | 112 | | size-s2 |
| 147075 | 146347 | 0.01k | 3975 | 37 | | buffer_head |
| 17914 | 10951 | 0.06k | 338 | 53 | | selinux_inode_security |
| 15880 | 10140 | 0.19k | 794 | 20 | | dentry_ |
| 15694 | 13577 | 0.06k | 266 | 59 | | size-664 |
| 14630 | 14418 | 0.14k | 413 | 19 | | vm_area_struct |
| 11151 | 11127 | 0.09k | 413 | 27 | | sysfs_dir_cache |
| 8239 | 9768 | 0.05k | 107 | 77 | | anon_vm |
| 6440 | 6276 | 0.04k | 70 | 92 | | anon_vm |
| 6356 | 4632 | 0.72k | 155 | 7 | | radix_tree_node |
| 6138 | 6138 | 0.10k | 1023 | 62 | | inode_cache |
| 5560 | 5486 | 0.19k | 118 | 20 | | filp |
| 4505 | 4399 | 0.07k | 85 | 53 | | Aci- |
| 4444 | 2577 | 0.15k | 1006 | 111 | | ext4_inode_cache |
| 4110 | 3596 | 0.12k | 137 | 30 | | size-128 |
```
