

![](img/a0df85c2e542a8d6c913113908553aa4_407_0.png)

## 图 15-9：双成员集群中共享总线上的被服务设备

假设您想使用磁带驱动器备份 dsk0（位于 member1 私有总线上的磁盘），如图 15-9 所示。该磁带驱动器是一个“被服务磁带”设备，当前由 member2 提供服务。您会希望在 member1（sheridan）上运行备份例程，因为它是唯一可以直接访问该磁盘的成员。

您需要做的第一件事是使用 drdmgr 命令检查当前由谁在为该磁带设备提供服务。

```
# drdmgr -a server -a accessnode tape1

View of Data from member sheridan as of 2001-05-19:23:41:54

Device Name: tape1
Device Type: Served Tape
Device Status: OK
Number of Servers: 2
Server Name: sheridan
Server State: Not Server
Server Name: molari
Server State: Server
Access Member Name: molari
```

从 drdmgr 命令的输出可以看出，sheridan 当前并未为 tape1 提供服务。

如果 sheridan 能够直接访问磁带设备，磁带 I/O 就不必跨集群通信互连传输，这样效率会更高。要更改服务器，可以使用如下 drdmgr 命令：

```
# drdmgr -a server=sheridan tape1
```

结果如图 15-10 所示，并通过以下 drdmgr 命令输出得到验证。

![](img/a0df85c2e542a8d6c913113908553aa4_408_0.png)

## 图 15-10：服务器重新定位后双成员集群中共享总线上的被服务设备

```
# drdmgr -a server -a accessnode tape1

View of Data from member sheridan as of 2001-05-19:23:49:25

                 Device Name: tape1
                 Device Type: Served Tape
                Device Status: Online
           Number of Servers: 2
                 Server Name: sheridan
                 Server State: Server
                 Server Name: molari
                 Server State: Not Server
            Access Member Name: sheridan
```

请注意，您可以同时更改多个设备的服务器。例如，如果 tape1 是磁带自动装载机（tape jukebox）中两个磁带设备之一，您可以同时移动 tape1、换带机（mc0）以及另一个磁带驱动器（tape2），如下所示：

```
# drdmgr -a server=sheridan tape1 tape2 mc0
```

然后您可以使用以下 drdmgr 命令验证结果（此处未显示输出）：

```
# drdmgr -a server -a accessnode tape1 tape2 mc0
```

## 15.2.3 重置统计信息

有时，重置某个成员上设备的统计信息以测试其连接性会很有用——事实上，我们将在下一节中进行这项操作。要为当前登录的成员上的设备重置统计信息，请执行以下命令：

```
[sheridan]
# drdmgr -a statistics=0 dsk5
```

要为另一个成员上的同一设备重置统计信息，您无需登录到该成员，只需使用 `-h` 选项即可。设备统计信息是按成员分别统计的。

```
[sheridan]
# drdmgr -h molari -a statistics=0 dsk5
```

## 15.3 DRD 示例

在本节中，我们将更详细地探讨 drdmgr 命令，并展示一些 DAIO 和被服务设备 I/O 的示例。我们已经讨论了在集群中 DAIO 设备与被服务设备的 I/O 应当如何工作，下面就用几个示例来验证。这里另一个有趣的事情是演示如果在集群内造成路径故障会发生什么。听起来很有趣？有点吓人？好吧，非常吓人？至少我们的集群不在生产环境中，所以我们可以放心试验而不会有被解雇的风险——或者说我们是这么希望的。

### 15.3.1 共享总线上的 DAIO 磁盘示例

让我们看看 DRD 如何响应对字符（/devices/rdisk/*）和块（/devices/disk/*）设备特殊文件的 I/O 请求。我们已在第 13 章讨论了直接 I/O 和文件 I/O，因此这里不再展示示例。在下面的示例中，我们将使用双成员集群，尽管这些示例也可以在更大的集群上完成。

#### 15.3.1.1 字符 I/O

我们将使用 dd(1) 命令对共享总线上的一个空闲设备进行读写。我们当前没有使用 dsk5，磁盘上也没有我们丢不起的数据。如果您选择尝试此练习，我们建议您非常非常确定该设备或分区未被使用。如果没有可用的磁盘或分区可供写入，那就只读取它。

我们创建了两个文件 MyFile.molari 和 MyFile.sheridan，其中反复打印了成员的主机名。每个文件的大小在 5 到 8 MB 之间。

