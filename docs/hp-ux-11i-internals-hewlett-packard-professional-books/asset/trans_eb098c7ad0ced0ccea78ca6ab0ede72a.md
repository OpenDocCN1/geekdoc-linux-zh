

# LVM：内核视角

在图 11-6 中，我们可以看到内核中 LVM 伪驱动程序的组织概况。如前所述，应用程序线程通过引用文件系统路径名来请求打开文件。虚拟文件系统将其解析为内核文件系统表中的一个特定 vnode。vnode 包含文件所在文件系统的设备号。基于 LVM 的文件系统的设备号会通过内核的设备切换表将所有 I/O 请求定向到 LVM 伪驱动程序。一旦驱动程序接收到 I/O 请求，它必须将该请求通过多个层次传递。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_338_0.png)

**图 11-6** LVM 伪驱动程序架构

**策略层：** 该层接收针对特定文件系统块的块 I/O 事务的初始请求。内核通过传递一个 buf 结构体来促进此请求，该结构体包含逻辑卷号 (b_dev)、定义事务的请求标志 (v_flags)、逻辑卷内的块号 (b_blkno)、请求的字节计数 (b_bcount) 以及各种选项 (b_options)。策略层必须验证请求，检查所请求卷的可用性以及其大小与卷块大小的匹配情况。

**镜像一致性层：** 如果配置了逻辑卷镜像，则该层必须协调镜像写入。卷可以被配置为将镜像写请求缓存到 MWC（镜像写缓存）中。卷组被划分为逻辑轨组 (LTG)，缓存的写请求首先在内核内存中的 MWC 缓存记录（每个 LTG 一个）中注册，并写入卷组中某个物理卷上的 mwc_entry。最初，每个卷组有 32 个 LTG，但在 11.1 版本中，这一数字增加到了 126 个。

缓存的数据不包含用户数据，但它确实注册了更新磁盘数据的意图。当写入已完成到所有镜像副本后，缓存记录被清除。在系统崩溃并重启的情况下，物理卷上的缓存记录可用于识别哪些 LVG（逻辑卷组）可能处于不同步状态。如果不使用 MWC，则必须重新同步镜像上的所有逻辑区段。

**调度层：** 该层充分利用基于内核的卷组配置信息副本。实际的镜像位置和数量被转换成一个或多个物理请求。策略层接受来自前一层级的 buf 指针，并引导其通过 LVM。

逻辑卷可以被配置为遵循几种调度策略之一。如果请求针对磁盘上的保留区域（用于配置和管理卷的实际元数据结构），则可能是 LVM_RESERVED。正常的读和写请求可能是 LVM_SEQUENTIAL 或 LVM_PARALLEL。这会影响用于镜像读和写请求的方法。最后，请求可能被标记为 LVM_STRIPE，用于并行条带化操作。

**物理层：** 这个最后一层是“橡胶与路面接触”的地方。LVM 驱动程序将请求及其相关的 buf 结构体传递给负责映射物理卷的实际物理设备驱动程序。

## 工作队列：保持请求在轨道上

由于 LVM 伪驱动程序是一种内核资源，因此在任何时间点，它通常都会在处理各种层级的多个请求。除了为多个线程提供服务外，缓冲区还可能在等待访问物理设备或在 LVM 驱动程序内部传输到下一层时排队。

在图 11-7 中，我们可以看到请求可能会出现在许多队列中。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_339_0.png)

**图 11-7** 工作队列

它们可以分为四个不同的类别。

- **全局队列：** `pf_wait_Q` 包含所有可能由于电源故障而无法完成的请求。此队列上的请求正在等待终止和清理。
- **每卷组队列：** `vg_cache_wait_queue` 持有等待其卷组 MWC 中空闲条目的请求。`vg_cache_write` 队列提供了一个可供 MWC 更新到磁盘的物理卷链接列表。当 LVM 驱动程序需要将其卷组中的 MWC 数据存储到物理磁盘时，它会选择此队列头部的卷。
- **每物理卷队列：** 为特定物理卷调度的所有请求都链接到 `pv_read_Q`。`pv_cache_wait` 持有等待其 MWC 数据写入物理磁盘的请求。

LVM 系统支持一种称为物理卷链接（`pv links`）的功能。该功能允许在一个总线和备用总线之间自动切换；也就是说，当总线控制器发生故障时，如果系统有可用的备用路径，I/O 将切换到该路径。`pv_wait_Q` 持有等待 `pv links` 切换生效的请求。

目前，`pv links` 支持活动/备用模式的操作。这指的是同一时间只能有一个接口是活动的。如果它失效，备用被动接口将被激活。未来，这可能得到增强，以允许活动/活动配置，其中两个接口都可以用来共享负载并提高整体吞吐量，同时提供真正的热备用功能。

- **每逻辑卷队列：** `work_Q` 实际上是卷所有未完成请求的每逻辑卷数组。数组条目是各个请求当前链接到的其他队列。由于此主队列了解卷的所有当前未完成请求，内核策略层利用此信息尽可能地对 I/O 请求进行序列化。

`lv_read_Q` 是等待传递给伪驱动程序中 MWC 层的请求的暂存区。

接下来，让我们考虑存储在内核中以支持 LVM 子系统操作的数据结构。

## 内核驻留数据结构

当卷组被激活（在启动时或通过 `vgchange -a y` 命令）时，其元数据会被复制到内核驻留结构。图 11-8 展示了这些结构的概况。这些结构的起点是内核 `vol1grp[]` 数组。由于单个 `vol1grp` 结构是内核中最大的结构之一，其数量受内核可调整参数 `maxvgs` 限制，默认为 10。注意：如果您正在创建新的卷、组目录和 `vgoup` 文件，传递给 `mkcmd` 命令的卷组号（次号参数的前两位数字）不应超过此可调整值。卷组的编号用作内核驻留 `vol1grp[]` 数组的索引。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_341_0.png)

**图 11-8** 内核驻留配置结构

让我们从检查 volgrp 结构（列表 11.10）开始。

### 列表 11.10 q4> fields struct volgrp

```text
We start with lock pointers and counters
 4 0 4 0 *        vg_lock.interlock
 4 0 4 0 u_int    vg_lock.delay
 8 0 4 0 int      vg_lock.read_count
12 0 1 0 char     vg_lock.want_write
13 0 1 0 char     vg_lock.want_upgrade
14 0 1 0 char     vg_lock.waiting
15 0 1 0 char     vg_lock.no_swap
Next a pointer to the lvol array (sized to 256), the number of
logical volumes, a lock, a pointer to the pvol array and its
size, the major number for the volume group pseudo-device file
(0x40, acts as a sanity check), the volume group identifier, a
count of the open volumes
16 0 4 0 *        lvols
20 0 4 0 u_int    num_lvol
24 0 4 0 *        vg_pvollistLock.lvc_lock
28 0 4 0 *        pvols
32 0 4 0 u_int    size_pvol
36 0 4 0 u_int    num_pvol
40 0 4 0 int      major_num
44 0 4 0 u_int    vg_id.id1
48 0 4 0 u_int    vg_id.id2
52 0 2 0 u_short  vg_extshift
54 0 2 0 u_short  vg_opencount
56 0 4 0 u_int    vg_flags

VG_LOST_QUORUM run quorum is lost
VG_ACTIVATED volume group is activated
VG_NOLOCKOPS disallow lvol opens
VG_READONLY volume group activated read-only

60 0 4 0 *        vg_intlock.lvc_slock
Total number of requests processed in the strategy layer and
the current pending requests
64 0 4 0 int      vg_totalcount
68 0 4 0 int      vg_requestcount
72 0 4 0 *        vg_ca_intlock.lvc_slock

Byte offset 80 through 539 holds a variety of MWC information structures. This section is examined later in this chapter.

Pointers and offsets to various related structures
540 0 4 0 *        vg_vgda
544 0 4 0 u_int    vg_LvEntry_off
548 0 4 0 u_int    vg_PvEntry_off
552 0 4 0 u_int    vg_PvEntry_len
556 0 4 0 u_int    vg_VGtrail_off

byte offset 560 through 1087 contains volume group status area data.

Configured limits for the volume group, logical volumes,
physical volumes, physical extents, extent size, data area
length, status area length, mirror cache size, the volume
group number (a quick sanity check for available physical
volumes, data area and status area block sizes, cluster
locking ID, and configuration mode (used in conjunction with
service guard configuration)
1088 0 2 0 u_short  vg_maxlvs
1090 0 2 0 u_short  vg_maxpvs
1092 0 2 0 u_short  vg_maxpxss
1100 0 4 0 u_int     vg_pxsize
1104 0 4 0 u_int     vg_vgda_len
1108 0 4 0 u_int     vg_ssa_len
1112 0 4 0 u_int     vg_mwc_len
1116 0 4 0 u_int     vg_num
1118 0 4 0 u_int     vg_npv_avail
1120 0 4 0 u_int     vg_npv_newavail
```

