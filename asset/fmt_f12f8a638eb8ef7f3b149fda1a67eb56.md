
## 15.3 DRD 示例

在本节中，我们将更详细地探讨 `drdmgr` 命令，并展示一些 DAIO 和被服务设备 I/O 的示例。我们已经讨论了在集群中 DAIO 设备与被服务设备的 I/O 应当如何工作，下面就用几个示例来验证。这里另一个有趣的事情是演示如果在集群内造成路径故障会发生什么。听起来很有趣？有点吓人？好吧，非常吓人？至少我们的集群不在生产环境中，所以我们可以放心试验而不会有被解雇的风险——或者说我们是这么希望的。

### 15.3.1 共享总线上的 DAIO 磁盘示例

让我们看看 DRD 如何响应对字符（`/devices/rdisk/*`）和块（`/devices/disk/*`）设备特殊文件的 I/O 请求。我们已在第 13 章讨论了直接 I/O 和文件 I/O，因此这里不再展示示例。在下面的示例中，我们将使用双成员集群，尽管这些示例也可以在更大的集群上完成。

#### 15.3.1.1 字符 I/O

我们将使用 `dd(1)` 命令对共享总线上的一个空闲设备进行读写。我们当前没有使用 `dsk5`，磁盘上也没有我们丢不起的数据。如果您选择尝试此练习，我们建议您非常非常确定该设备或分区未被使用。如果没有可用的磁盘或分区可供写入，那就只读取它。

我们创建了两个文件 `MyFile.molari` 和 `MyFile.sheridan`，其中反复打印了成员的主机名。每个文件的大小在 5 到 8 MB 之间。

```
[molari]
# ddrmgr dak5

    View of Data from member molari as of 2001-07-19:16:39:53

                    Device Name: dak5
                    Device Type: Direct Access IO Disk
                    Device Status: OK
              Number of Servers: 2
                    Server Name: molari
                   Server State: Server
                    Server Name: sheridan
                   Server State: Server
             Access Member Name: molari
              Open Partition Mask: 0
      Statistics for Client Member: molari
             Number of Read Operations: 0
            Number of Write Operations: 0
                  Number of Bytes Read: 0
               Number of Bytes Written: 0
```

```
[molari]
# ddrmgr -h sheridan dak5

    View of Data from member sheridan as of 2001-07-19:16:39:47

                    Device Name: dak5
                    Device Type: Direct Access IO Disk
                    Device Status: OK
              Number of Servers: 2
                    Server Name: molari
                   Server State: Server
                    Server Name: sheridan
                   Server State: Server
             Access Member Name: sheridan
              Open Partition Mask: 0
      Statistics for Client Member: sheridan
             Number of Read Operations: 0
            Number of Write Operations: 15822
                  Number of Bytes Read: 0
               Number of Bytes Written: 8912310
```

请注意，第二个 `ddrmgr` 命令使用了 `"-h"` 开关，从 member `molari` 获取 member `sheridan` 的统计信息。设备是一个 DAIO 设备，每个 member 都是一个服务器。另请注意，每个 member 的访问 member 名称就是其自身。

由于 `sheridan` 的统计信息不为零，我们将在开始之前将其设为零。

```
[molari]
# ddrmgr -a statistics=0 -h sheridan dak5
```

```
[molari]
# drmgr -a statistics -h sheridan dak5

View of Data from member sheridan as of 2001-07-19:16:46:55

Device Name: dak5
Statistics for Client Member: sheridan
Number of Read Operations: 0
Number of Write Operations: 0
Number of Bytes Read: 0
Number of Bytes Written: 0
```

让我们使用字符设备特殊文件将每个 member 的 `"MyFile"` 写入 `dak5` 的 `"h"` 分区。我们将从 `molari` 开始写入，并在写入完成后再从 `sheridan` 开始写入。

```
[molari]
# dd if=MyFile.molari of=/dev/rdisk/dak5h
11718+1 records in
11718+1 records out
```

```
[molari]
# drmgr -a statistics dak5

View of Data from member molari as of 2001-07-19:16:55:19

Device Name: dak5
Statistics for Client Member: molari
Number of Read Operations: 0
Number of Write Operations: 11719
Number of Bytes Read: 0
Number of Bytes Written: 6000000
```

```
[molari]
# drmgr -a statistics -h sheridan dak5

View of Data from member sheridan as of 2001-07-19:16:55:25

Device Name: dak5
Statistics for Client Member: sheridan
Number of Read Operations: 0
Number of Write Operations: 0
Number of Bytes Read: 0
Number of Bytes Written: 0
```

请注意，`sheridan` 上的统计信息仍然为零。

```
[sheridan]
$ dd if=/myfile.sheridan of=/dev/rdisk/dsk5h
15625+0 records in
15625+0 records out
```

```
[sheridan]
$ drdmgr -a statistics dsk5

View of Data from member sheridan as of 2001-07-19:17:00:01

Device Name: dsk5
Statistics for Client Member: sheridan
Number of Read Operations: 0
Number of Write Operations: 15625
Number of Bytes Read: 0
Number of Bytes Written: 8000000
```

```
[sheridan]
$ drdmgr -a statistics -h molari dsk5

View of Data from member molari as of 2001-07-19:17:00:09

Device Name: dsk5
Statistics for Client Member: molari
Number of Read Operations: 0
Number of Write Operations: 11719
Number of Bytes Read: 0
Number of Bytes Written: 6000000
```

由于设备支持 DAIO 且每个 member 都有物理访问权限，因此每个 member 都能够独立地写入设备，而无需通过集群互连传递数据。

#### 15.3.1.2 Block I/O

执行块 I/O（即从块设备特殊文件读取和写入）是在发送到 DRD 之前由集群文件系统（CFS）层处理的。由于 CFS 以客户端/服务器方式实现，即使设备支持 DAIO 并且位于可被执行 I/O 的 member 直接访问的共享总线上，DRD 也不会在那些是 CFS 客户端的 member 上参与（除非调用直接 I/O 或直接访问缓存读取 [参见第 13 章]）。块设备特殊文件位于 `/devices` 目录层次结构中，因此由 `cluster_root` 域的 CFS 服务器提供服务。

因此，让我们演示在集群中如何执行块 I/O。我们将再次使用 `dd` 命令，但这次我们将使用 `dsk5` 的块设备特殊文件。

我们需要做的第一件事是找出哪个 member 是 `cluster_root` 域的 CFS 服务器。为此我们将使用 `cfsmgr(8)` 命令。

```
# cfsmgr -d cluster_root
域或文件系统名称 = cluster_root
服务器名称 = sheridan
服务器状态 : OK
```

节点 `sheridan` 是 CFS 服务器。

让我们在执行任何 I/O 之前先重置两个成员的统计信息。
