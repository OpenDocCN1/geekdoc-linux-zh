

### 13.9.5 调整预读和写回线程

CFS 客户端对文件的顺序访问由预读和写回线程处理。默认情况下，CFS 读取以 64KB 为增量进行远程读取，即从 CFS 服务器读取，因此如果 CFS 检测到多次顺序读取，它会使用预读线程提前读取下一块数据，以期该数据也会被请求。

但是，如果你使用的是 TruCluster Server 版本 5.1A，则 CFS 将使用直接访问缓存读取（参见第 13.8 节），因此读取将直接从存储设备进行，从而绕过 CFS 服务器并可能减少集群互连流量。此外，使用直接访问缓存读取时，I/O 通常可以更大（首选 I/O 传输大小为 128KB）。请注意，即使使用直接访问缓存读取，预读线程仍然会被使用。

写回线程用于在后台写入缓存中的脏页。它尝试从缓存中找到其他连续的脏页，将页面合并为更大的 I/O 传输到文件系统。

这些线程是内核空闲任务的一部分，可以通过使用以下 ps(1) 命令并通过管道传递给 grep(1) 命令来查看。

```
```sh
# ps -elm | grep cfsiod
```
```

默认情况下，每个集群成员上存在 32 个预读和写回线程。这可以通过将之前的命令字符串通过管道传递给 wc(1) 命令来轻松验证。

```
```sh
# ps -elm | grep cfsiod | wc -l
       32
```
```

如果你的 CFS 客户端一次顺序访问超过 32 个大文件，你可能需要增加这个数字以提高性能。判断是否需要更多预读/写回线程的一个基本检查是检查等待线程的状态：

```
```sh
# ps -emo states,wchan | grep cfsiod
S   cfsiod_
S   cfsiod_

S   cfsiod_
S   cfsiod_
S   cfsiod_
```
```

如果大多数等待线程处于“S”状态（即线程已休眠约 20 秒以下）并且等待线程的计数波动很大，你可能需要增加预读和写回线程的数量。

cfs 子系统中的 cfs_async_biod_threads 属性可用于动态修改预读和写回线程的数量。cfs_async_biod_threads 的取值范围为 0 到 128。要修改 cfs_async_biod_threads，可以使用 sysconfig 命令，如以下示例所示。

检查 cfs_async_biod_threads 属性的初始值。

```
# sysconfig -q cfs cfs_async_biod_threads
cfs:
cfs_async_biod_threads = 32
```

重新配置 cfs_async_biod_threads 属性，将其设置为 100。

```
# sysconfig -r cfs cfs_async_biod_threads=100
cfs_async_biod_threads: reconfigured
```

验证重新配置是否成功。

```
# sysconfig -q cfs cfs_async_biod_threads
cfs:
cfs_async_biod_threads = 100
```

你也可以看到线程已被创建。

```
# ps -elm | grep cfsiod_ | wc -l
100
```

# NOTE:

此练习是在相对空闲的集群成员上执行的，因此我们能够说明线程数量等于 cfs 子系统中的 cfs_async_biod_threads 属性值。可能你会看到比实际配置更少的线程数，当运行以下命令时：

```
# ps -elm | grep cfsiod_ | wc -l
```

这很可能表明线程当前正在运行。我们搜索的 "cfsiod_" 字符串实际上来自 WCHAN，它是线程正在等待的事件的地址（或部分名称）。换句话说，如果线程未处于等待状态，其 WCHAN 将不是 "cfsiod_"。

根据 TruCluster Cluster Administration Guide 第 9 章，预读和写回线程在未使用时消耗的资源很少，因此增加线程数量可能不会损害你的性能。但是，如果你计划增加线程数量，请以适度的增量进行，并在提高到最大值之前评估其对系统的效果。由于该属性可以动态修改，如果你注意到任何不利影响，可以在无需重新启动系统的情况下降低该值。

一旦你找到了适合你配置的属性值，你需要使用 sysconfigdb 或 dxkerneltuner 命令将其放入系统的 /etc/sysconfigtab 文件中。

## 13.10 CFS 事件

CFS 事件定义在 /usr/share/evm/templates/clu/cfs.evt 模板文件中。以下是已注册的 CFS 事件：

```
# evmwatch -A -i -E "[name *.cfs]" -t "@[priority] @name"
[200] sys.unix.clu.cfs.advs.served
[200] sys.unix.clu.cfs.fs.served
[200] sys.unix.clu.cfs.advs.not_served
[200] sys.unix.clu.cfs.fs.not_served
[300] sys.unix.clu.cfs.advs.no_server
[300] sys.unix.clu.cfs.fs.no_server
```

## 13.11 参考文献

- The TruCluster Server Technical Overview Guide.
- The TruCluster Server Cluster Administration Guide.
- The Tru64 UNIX System and Configuration Guide.
- The Tru64 UNIX File System Administration Handbook, by Steven M. Hancock, Digital Press (ISBN: 1-55558-227-3)
- Reference pages (noted within the text).

