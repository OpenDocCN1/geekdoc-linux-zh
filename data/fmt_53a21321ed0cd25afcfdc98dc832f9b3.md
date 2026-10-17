
```text
# fstyp -v /dev/vx/dsk/homevol | more
ufs
magic 11954  format dynamic  time Sat Mar  6 18:15:59 1999
sblkno 16  cgblkno 24  iblkno 32  dblkno 800
sbsize 2048  cgsize 8192  cgoffset 32  cgmask 0xfffffe00
ncg 167  size 8378368  blocks 8247421
bsize 8192  shift 13  mask 0xffffe000
fsize 1024  shift 10  mask 0xfffffc00
frag 8  shift 3  fsbtodb 1
minfree 1%  maxbpg 2048  opttime 1
maxcontig 32  rotdelay 0  rps 120
csaddr 800  cssize 3072  shift 9  mask 0xfffffe00
ntrak 32  ncsect 64  spc 2048  ncycg 8182
cpg 49  bpg 6272  fpg 50176  ipg 6144
nindir 2048  inopb 64  nspf 2
nbfree 176719  ndir 10241  ntrfree 956753  nffree 21495
cgrotor 152  mod 0  ronly 0  logbno 0
fs_reclaim is not set
file system state is valid, fsclean is 0
blocks available in each rotational position
cylinder number 0:
    position 0:   0   4   8  12  16  20  24  28  32  36  40  44
                  48  52  56  60  64  68  72  76  80  84  88  92
                  96 100 104 108 112 116 120 124
    position 2:   1   5   9  13  17  21  25  29  33  37  41  45
                  49  53  57  61  65  69  73  77  81  85  89  93
                  97 101 105 109 113 117 121 125
    position 4:   2   6  10  14  18  22  26  30  34  38  42  46
                  50  54  58  62  66  70  74  78  82  86  90  94
                  98 102 106 110 114 118 122 126
    position 6:   3   7  11  15  19  23  27  31  35  39  43  47
                  51  55  59  63  67  71  75  79  83  87  91  95
                  99 103 107 111 115 119 123 127

cs[1].cs_(nbfree,ndir,nifree,nffree):
        (23,26,5708,102) (142,26,5724,244) (87,20,5725,132) (390,69,5737,80)
        (72,87,5815,148) (3,57,761,110) (267,87,584,4) (0,66,5434,4)
        (217,46,5066,94) (53,87,5789,70) (0,87,5750,68)
        .
        .
        .
cylinders in last group 48
blocks in last group 6144

cg 0:
magic 90255  tell 6000  time Sat Feb 27 22:53:11 1999
ncg 0  ncyl 49  niblk 4096  ndblk 60176
nbfree 23  ndir 26  nifree 5708  nffree 102
rotor 1224  irotor 144  frotor 1224
frsum 7  3  1  1  0  9
sum of frsum: 102
used: 0-143, 145-436
free: 1244-1295, 1304-1311, 1328-1343, 4054-4055, 4126-4127, 4446-4447, 4455,
4637-4638,
```

# 14.3 UFS 实现

UFS 是作为一个可加载文件系统模块实现的，其中包含 `vfs` 和 `vnode` 对象的实例。UFS `vnode` 接口实现文件操作，UFS `vfs` 接口实现文件系统管理。

UFS 文件系统的实现可分为五个主要部分：

- `vfs` 对象的一个实例，以及用于挂载和卸载文件系统、收集文件系统统计信息的方法
- 用于文件操作的 `vnode` 方法的实现
- 使用标准目录名查找缓存的目录实现
- 用于将文件映射到存储设备上磁盘块的块映射算法
- 一个 inode 缓存，用于在 `vnode` 不再被引用后将其保留在内存中

图14.6显示了 UFS 文件系统各组件之间的关系。UFS 实现了用于文件访问的 `vnode` 接口和用于文件系统管理的 `vfs` 接口。UFS 与以下部分交互：用于持久存储的设备驱动程序、用于存储和检索元数据的块缓冲区缓存、用于缓存路径名的目录名查找缓存，以及用于缓存文件数据的虚拟内存系统。

在下面的段落中，我们讨论 UFS 文件系统内部各个部分的实现。

![](img/220ae4af07df2fe8e5be69d27f885d1b_632_0.png)

图14.6 *UFS 文件系统*

## 14.3.1 文件到磁盘块的映射

基于磁盘的文件系统的核心是块映射算法，这些算法实现了磁盘上的文件系统格式。这些算法将 UFS 文件和偏移对映射到底层存储上的磁盘地址。对于 UFS，两个主要函数—`bmap_read()` 和 `bmap_write()`—实现磁盘上的格式。这些函数被调用来完成以下工作：

- `bmap_read()` 查询文件系统，确定文件块所在的物理磁盘扇区；也就是说，它请求查找包含所需块磁盘地址的直接/间接块。
- `bmap_write()` 在为文件扩展或分配块时分配新的磁盘块。

`bmap_read()` 函数用于读取和写入时定位磁盘块；它接受 `inode` 和偏移量作为输入参数，并接受磁盘地址和长度的指针作为输出参数。

```c
int
bmap_read(struct inode *ip, u_offset_t off, daddr_t *dap, int *lenp);
```

头文件 `<fs/ufs_inode.h>`

`bmap_read()` 函数同时用于文件读取和写入。在这两种情况下，文件系统都使用 `bmap_read()` 算法来定位正在读取或写入的文件的物理块。`bmap_read()` 函数搜索 `inode` 的直接、间接和双重间接块，以定位映射到所提供偏移量的磁盘块的磁盘地址。该函数还从偏移量向前搜索，寻找继续映射 `inode` 连续部分的磁盘块，并通过长度指针参数返回连续段的长度。该长度和文件系统块聚集参数在文件系统内部用作聚集连续块的边界，以便一次从磁盘读取文件更大的部分，从而提高性能。

```c
int
bmap_write(struct inode *ip, u_offset_t off, int size,
        int alloc_only, struct cred *cr);
```

头文件 `<fs/ufs_inode.h>`

`bmap_write()` 函数在文件被扩展或具有空洞的文件首次写入块时，在文件系统中分配文件空间。`bmap_write()` 使用转子算法（在第585页的“UFS 块分配”中讨论）搜索空闲块列表，并更新被扩展文件的 `inode` 中的本地、直接和间接块。

### 14.3.1.1 读写 UFS 块

文件系统读取调用 `bmap_read()` 来定位被读取文件的底层物理块。然后 UFS 调用设备驱动程序的策略例程。

包含文件系统的设备通过调用 `bdev_strategy()` 启动读操作的时间。

扩展文件的文件系统写操作首先调用 `bmap_write()` 分配新块，然后调用 `bmap_read()` 获取写入的块位置。UFS 通过 `bdev_strategy()` 与设备驱动程序的策略例程协作，以启动文件写入。

## 14.3.1.2 缓冲块元数据
