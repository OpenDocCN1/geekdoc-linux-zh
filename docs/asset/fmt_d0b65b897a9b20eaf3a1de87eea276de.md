
如果计时器到期且系统没有等待写入磁盘的事务，ZFS 将不会写入任何数据。ZFS 不会为了有一个事务组而写入一个空事务。然而，它仍然会增加事务组的计数。

将事务组超时时间设置为五秒以下会遇到 I/O 调度器和写入节流的限制。对大多数人来说，五秒是最小合理值。

## txg 大小

增长得足够大的 `txg` 会在超时之前提交到磁盘。FreeBSD 在启动时会根据主机的内存量和可调优的 `vfs.zfs.dirty_data_max_percent` 自动调整事务组的最大尺寸。默认值为 10%，最高可达 4 GB，并由 `vfs.zfs.dirty_data_max_max` 控制。一旦事务组使用了系统 10% 的内存内存，它就会被写入磁盘。

你可以在系统启动后使用 `sysctl vfs.zfs.dirty_data_max` 更改事务组的最大尺寸。该值的单位是字节，将你所需的 GB 数值乘以 `$1024^3` 即可获得适当的 `sysctl` 值。

棘手的问题是：你是否应该更改事务组的大小？你的系统将 RAM 的 10% 写入磁盘需要多久？发生的频率是多少？大多数主机的 RAM 内存远大于其 I/O 吞吐量。尝试在五秒内写入十分分之一的内存将是一场灾难。Lucas 的测试主机在单个池中有几块硬盘并拥有 32 GB 内存。向磁盘写入 3.2 GB 数据需要 20 秒。如果该主机在标准的五秒超时时间内生成了 3.2 GB 的磁盘活动，机器将迅速陷入不可用的状态。

如果你的系统是一个高性能磁盘阵列，具有极大的吞吐量目标和经济规模的内存，你可能会发现增加最大值是有用的。

在“写入周期”期间，大多数从磁盘的读取会被挂起。这允许写入尽快完成。写入完成后，读取恢复。这种交替工作负载通常可以提高性能。通过对工作负载的了解，你可以决定是频繁地刷新大组还是频繁地刷新小组。在同一个池内大量拷贝数据时，Jude 将 `txg` 大小增加到 24 GB 并将超时延长到 30 秒，性能提高了 25%。

## txg 持续时间和内容

如果你正在调整事务组的大小和周期，使用以下脚本测量它们的大小和耗时是合理的：

```dtrace
#!/usr/bin/dtrace -s
txg-syncing
((dsl_pool_t*)arg0)->dp_spa->spa_name == $1/
{
  start = timestamp;
}
txtg-synced
/start && ((dsl_pool_t*)arg0)->dp_spa->spa_name == $1/
{
  this->d = timestamp - start;
  printf("%4dMB of %dMB synced in %d.%0d seconds",
  d_total / 1024 / 1024,
  d_max / 1024 / 1024, this->d / 1000000000,
  this->d / 1000000000 % 100);
}
```

运行脚本并传入池名称。Lucas 创建了一些可以同时测量这两者的 `dtrace` 脚本。

```dtrace
dtrace -s 'duration' matched 2 probes

CPU ID:NAME
1::txg-synced synced 0.11 seconds
2::txg-synced synced 0.24 seconds
4::txg-synced synced 0.22 seconds
2::txg-synced synced 0.31 seconds
```

## 写入节流

你可能会听到的一个术语是写入节流（`write throttle`）。当程序向内存提供数据而 ZFS 可以将其写入磁盘时，写入节流就会发挥作用。随着系统 RAM 越来越满，ZFS 开始在每个写入请求中插入微小的延迟。程序会等待写入请求的响应，这种延迟迫使它们慢下来。目标是确定磁盘可以承受的负载，并让程序以恰好该速度运行。

FreeBSD 10 及更高版本中的写入节流算法运行得流畅得多。你可以通过 I/O 调度器对其进行调优，将在下文中讨论。

## I/O 调度

并非所有硬件都是平等的。Jude 的顶配笔记本电脑的 I/O 容量远低于他的内容分发网络服务器。FreeBSD 的默认设置相当通用。虽然在笔记本电脑上你并不需要对它们进行调优，但如果你有几十个或上百个具有特定工作负载的磁盘，你可以通过调优调度来调整性能。I/O 调度允许你调整延迟和吞吐量。

吞吐量是指可以从存储设备读取和写入的数据量。当你说 SATA-3 可以以 6.0 GB/s 的速度传输数据时，你说的的就是吞吐量。

延迟是系统处理这些请求所需的时间。复杂的存储系统（带有光纤通道总线和建筑多个部分的多个机架）在数据穿过系统时可能会产生延迟。当你通过同时复制太多文件导致硬盘过载时，你的笔记本电脑更容易出现存储延迟。

虽然硬盘通常的营销描述是它们每秒可以执行多少次 I/O 操作（IOPS），但这个术语的意义并不如你想象的那样。能够执行 250 IOPS 经过仔细挑选的数据，并不能说明硬盘处理你数据的能力。

将硬盘想象成汽车。有些针对容量进行了优化，另一些针对里程进行了优化。一辆巨大的双挂牵引车可以运输的货物远比特斯拉 Roadster 多，而后者在红灯起步时并不敏捷。我们大多数人会在周末使用大卡车将一个百人的呼叫中心搬到城市另一端，但在阑尾破裂前把孩子送到医院时会倾向于不同的优化方案。

与汽车不同，你可以在某种程度上控制大多数硬盘的优化。（某些特殊存储设备是专门为某些优化而设计的。）这就是为什么你可以向笔记本电脑的硬盘中倾倒大量数据并导致系统无响应——你只是用吞吐量换了延迟。

ZFS I/O 调度旨在平滑延迟。这可能会降低吞吐量，但会让整体体验更具一致性。通常，通过更改调度，你是在尝试在不引入过多延迟的情况下提高性能。

ZFS 调度是围绕 I/O 队列构建的。

## 测量延迟和吞吐量

你如何知道某个更改是否正向影响了系统性能？通过测量来。Adam Leventhal 为 illumos 编写了一个延迟和吞吐量的 DTrace 脚本，但这里有一个针对 FreeBSD 修改后的的版本。

```c
#pragma D option quiet
inline uint32_t BIO_READ = 1;
inline uint32_t BIO_WRITE = 2;
this uint64_t delta;
BEGIN
{
 start = timestamp;
io::=start / args[0] /
{
 ts[args[0]] = timestamp;
}
 io::=done /args[0] & ts(args[0])/
this->delta = (timestamp - ts(args[0])) / 1000;
this->name = (args[0]-bio_cmd & BIO_READ | BIO_WRITE) == BIO_READ ?
"read" : "write"
@q[this->name] = quantize(this->delta);
@a[this->name] = avg(this->delta);
@v[this->name] = stddev(this->delta);
@if[this->name] = count();
@b[this->name] = sum(args[0]->bio_bcount);
ts(args[0]) = 0;
}
END
{
normalize(@q);i, (timestamp - start) / 1000000000);
normalize(@b, (timestamp - start) / 1000000000 * 1024);
printf("%-30s %11s %11s %11s\n", "", "avg latency", "stddev", "iops")
printf("%-30s %9us %9us %bu/s %8uk/s\n", @a, @v, @i, @b);
```

在系统承受正常负载时多次运行脚本，以获得延迟和吞吐量的准确基准。

`dtrace -s rw.d -c 'sleep 30'`

`sleep` 命令告诉脚本花费多长时间收集数据。`rw.d` 脚本监控这几秒钟内的吞吐量和延迟，然后打印读取和写入两张图表。最后你将得到如下所示报告：

| avg latency | stddev | iops | throughput |

| :--- | :--- | :--- | :--- |

| write | 1362us | 8378us | 68/s | 4620k/s |

| read | 6943us | 5839us | 2/s | 46k/s |

通而言之，性能调优的目标是在提高你关心的数字的同时，不让其他数字变得太大。尝试调整每类型允许的最大读取和写入次数，在每次运行之间增加 20–100%。确保不要将这些值调得太高以至于你的 VDEVs 超过了每个 VDEV 的限制——或者，尝试调整最小值。

`stddev`（标准差）列特别值得注意。你可能获得了卓越的吞吐量，但发现延迟波动很大。如果你的某些读取和写入需要五秒才能完成，巨大的吞吐量还可以吗？只有你知道。
