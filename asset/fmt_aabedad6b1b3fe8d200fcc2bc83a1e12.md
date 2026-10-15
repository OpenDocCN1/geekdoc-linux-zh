
表 A-8 列出的参数与 Solaris 中的进程和调度器子系统有关。更多信息请参阅第286页的“内核进程表”。

### 表 A-8 进程与分发器（调度器）参数

| 参数 | 默认值 | 类别 | 描述/备注 |
| :--- | :--- | :--- | :--- |
| reserved_procs | 5 | 限制 | 系统进程保留的进程槽位数量。 |
| maxpid | 30,000 | 限制 | PID 的最大值，以及系统随时存在的最大进程数。 |
| max_nprocs | (10 + 16 * max-users) | 限制 | 系统存在的最大进程数。如果设置的值大于 maxpid，则将设置为 maxpid。 |
| maxuprc | max_nprocs - reserved_pro | 限制 | 非 root 用户可以创建的最大进程数。 |
| noexec_user_stack | 0 | 开关 | 如果设置为 1，栈页将映射为不可执行 (noexec)，提供防止缓冲区溢出的保护。64 位 Solaris 7 默认将栈页映射为不可执行。 |
| rechoose_interval | 3 | 可调 | 线程到处理器的亲和时钟计数。分发器尝试将线程放置在上次运行的处理器上以获得最佳缓存命中，取决于 rechoose_interval。 |
| hires_tick | 0 | 可调 | 默认 0 每秒产生 100 次中断（ms 间隔）。设置此值每秒产生 1000 次。 |

## A.7 STREAMS 参数

表 A-9 列出了内核 STREAMS 的可调参数。本书未涵盖这些。

### 表 A-9 STREAMS 参数

| 参数 | 默认值 | 类别 | 描述/备注 |
| :--- | :--- | :--- | :--- |
| nstrpush | 9 | 限制 | 推入 STREAM 的模块数量。 |
| strmsgs | 65536 | 限制 | STREAMS 数据消息的最大大小（字节）。 |
| strctls | 1024 | 限制 | STREAMS 控制消息的最大大小（字节）。 |
| sadcnt | 16 | 限制 | STREAMS 管理 (sad) 设备数量。 |
| nautopush | 32 | 限制 | autopush 结构数量。 |

## 内核虚拟地址映射

在本录中，我们说明了构成 Solaris 7 地址空间的特定段信息。内核空间由系统对象 `kas` 指向，驱动程序管理内核空间内的段。`img/a86367b95bf21add85c994ac951c666_0.png`

### 内核空间与段

可以使用 `as` 查看内核空间。`as` 宏将显示内核空间和段列表。

```
adb -k physmem b91akas$as
10423320 (mutex) owner/waiters
0
10423328 flagsbits
0
10423330 seglast
3000ebf8 0 300002f8
10423350 lock (rwlock) size
2052c000 104230e0 nwh
0
10423368 segs size
10346786 hirevel
0 0
10423386 unusedobjectdir
0 0
10423390 sizedir nwpage
0 0
```

然后可以使用 `seglist` 宏打印内核内存段列表。

```
1034678$seglist
ktextseg: base as
mtextseg: 10000000 4a0000 10423320
mtextseg+0x18: next prev ops
1041fd60 0 segkmem_ops
seg+0x30: data
0
kvalloc: base size as
kvalloc: 104a0000 e200000 10423320
kvalloc+0x18: next prev ops
104233a0 1034678 segkmem_ops
kvalloc+0x30: data
0
kvseg32: base size as
kvseg32: 78000000 400000 10423320
kvseg32+0x18: next prev ops
300002af88 1041fd60 segkmem_ops
kvseg32+0x30: data
0
```

## 内核虚拟地址映射

接下来的图展示了 Solaris 7 地址空间如下：

- 图 B.2 Solaris 7 sun4u 64 位内核空间
- 图 B.3 Solaris 7 sun4u 32 位内核空间
- 图 B.4 Solaris 7 sun4d 32 位内核空间
- 图 B.5 Solaris 7 sun4m 32 位内核空间
- 图 B.6 Solaris 7 x86 32 位内核空间

### 内核虚拟地址映射

| 0xFFFFFF.FFFFFF | Open Prom 页表 |  |
| :--- | :--- | :--- |
| 0xFFFFFFFC.00000000 | 64 位内核堆 segkmemm | (8 GB) |
| 0x00000302.00000000 | | |
| 0x00000300.00000000 | 文件系统缓存 segmap | (256 MB) |
| 0x000002A7.50000000 | 可分页内核内存 segkp | (512 MB) |
| 0x000002A1.00000000 | | |
| 0x00000000.FFFFFFFF | Open Boot Prom | |
| 0x00000000.F0000000 | 内核调试器 | |
| 0x00000000.7C000000 | 32 位内核堆 segkmem32 | |
| 0x00000000.78002000 | Panic 消息缓冲区 | |
| 0x00000000.78000000 | 大 TSB | (512 KB 页面) |

# 内核虚拟地址映射

| 地址 | 描述 | 大小 |
|---|---|---|
| 0xFFFFFFFF | Open Boot Prom | |
| 0xF0000000 | 内核调试器 | |
| 0xEDD00000 | 内核堆内存 segkmem | (2 Gbytes) |
| 0x60000000 | 文件系统缓存 segmap | (256 Mbytes) |
| 0x50000000 | 可分页内核内存 segkp | (512 Mbytes) |
| 0x30000000 | 大型 TSB | (512-Kbyte 页面) |
| 0x10800000 | sun4u HAT 结构小型 TSB & Map Biks | (4 Mbytes) (1 x 4-Mbyte 页) |
| 0x10400000 | 内核数据段 | (4 Mbytes) (1 x 4-Mbyte 页) |
| 0x10000000 | 内核文本段 中陷表 | |
| 0x0 | 无效 | |

图 B.3 Solaris 7 sun4u 32位内核内核地址空间

| 地址 | 描述 |
|---|---|
| 0xFFFFFFFF | 无效 |
| 0xFFFF0000 | 监器 |
| 0xFFFD0000 | 内核堆内存 segkmem (251 Mbytes) |
| 0xF0200000 | 文件系统缓存 segmap (32 Mbytes) |
| 0xF0080000 | 可分页内核内存 segkp |
| 0xEE080000 | sun4d HAT 结构 内核数据段 / 内核文本段 |
| 0xE0040000 | 中陷表 (4 Kbytes) |
| 0xE0000000 | 进程地址空间 |
| 0x0 | |

图 B.4 Solaris 7 sun4d 32位内核内核地址空间

| 地址 | 描述 | 大小 |
|---|---|---|
| 0xFFFFFFFFFF | 无效 | |
| 0xFF000000 | 监器 | |
| 0xFFD00000 | | |
| 0xFE400000 | 可分页内核内存 segkp | (38 Mbytes) |
| 0xFEBE00000 | 调试器 | |
| 0xFBD00000 | | |
| 0xF5903000 | 内核堆内存 segkmem | (100 Mbytes) |
| 0xF5901000 | 恐慌消息缓冲区 | |
| | 文件系统缓存 segmap | (16 Mbytes) |
| | sun4m HAT 结构 内核数据段 / 内核文本段 / 中陷表 (4 Kbytes) |
| 0xF0040000 | | |
| 0xF0000000 | 进程地址空间 | |
| 0x0 | | |

图 B.5 Solaris 7 sun4m 32位内核内核地址空间

图 B.6 Solaris 7 x86 32位内核内核地址空间

# 一个示例 PROFS 工具
