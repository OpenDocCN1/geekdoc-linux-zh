
你可以使用 `@foo` 删除 `snapshot@foo` 以及任何比它旧的快照。

```
# zfs destroy -vn mypool/dataset@four
would destroy mypool/dataset@one
would destroy mypool/dataset@two
would destroy mypool/dataset@three
would destroy mypool/dataset@four
```

同样，使用 `@foo%` 删除 `@foo` 以及任何比它更更新的快照：

```
# zfs destroy -vn mypool/dataset@six%
would destroy mypool/dataset@six
would destroy mypool/dataset@seven
would destroy mypool/dataset@eight
would destroy mypool/dataset@nine
would destroy mypool/dataset@ten
```

这比重新输入每个快照要简单得多。

## 快照大屠杀 (Snapshot Slaughter)

有时，你想删除所有快照。使用 `@%` 将它们全部付之一于炬。

```
# zfs destroy -vn mypool/dataset@%
would destroy mypool/dataset@one
would destroy mypool/dataset@two
...
would destroy mypool/dataset@ten
```

现在你可以再次开始积累快照了。

如果你拍摄了递归快照，你可能想删掉整个树。添加 `-r` 可以清除某个数据集及其所有子数据集的快照。在这里，我们已经完成了升级，并且对结果表示满意：

```
# zfs destroy -nvR pgsql/data%
would destroy pgsql/data@beforeupgrade
would destroy pgsql/data/base@beforeupgrade
would destroy pgsql/data/pg_xlog@beforeupgrade
```

但是，你知道的……我们想再多留那些备份。

## 恢复已删除的池 (Recovering Destroyed Pools)

当你意识到“等一下，那个命令是个可怕的错误！”时，没有什么比这更糟糕了！你试图停止，但你知道神经冲动在手指按下回车键之前就已经大脑。

在删除 ZFS 池时可能会发生这种情况。ZFS 的设计者非常清楚这种症状。

`zpool destroy` 命令实际上并没有损坏底层磁盘上的任何数据。相反，它将池标记为已删除。`zpool list` 会跳过标记为已删除的池。如果你没有向已删除池下的磁盘写入数据或物理移除磁盘，你就可以恢复该池。使用 `zpool import` 的 `-d` 参数可以查看已删除的池。

```
# zpool import -D
```

你会得到两种响应，针对可恢复的池和不可恢复的池。

### 可恢复的池 (Recoverable Pools)

这是一个你可以轻松恢复的池。

```
# zpool import -D
pool: db2
id: 555215874600692385
state: ONLINE
action: The pool is
config:
  db2
  gpt/zfs4
  gpt/zfs5
```

此池包含两个条带化磁盘。

在原始池中，三路镜像的条带对已变为双路镜像的条带对。

如果你打算长时间保留这个拆分出来的池，你应该添加更多磁盘以创建适当的镜像。不过，如果你只是从这些驱动器提取备份，则可能不需要再添加一组磁盘。

### 不可恢复的池 (Non-Recoverable Pools)

其他池就不容易了。

```
# zpool import -D
pool: db
id: 131227496263209
state: DESTROYED
action: The pool is missing
config:
  db2                DEGRADED
```

### 恢复时重命名 (Rename at Recovery)

有时你想在恢复时重命名池。也许它与某个运行中的池同名，或者池的功能发生了变化。在导入时重命名池，在旧池名称之后添加新名称。在这里我们导入已删除的 `db2` 池并将其重命名为 `olddb2`。

```
# zpool import -D olddb2
```

其余与重命名导入池相同。

## 克隆机器 (Cloning Machines)

ZFS 是虚拟机非常明智的选择。虽然失去对磁盘的直接访问意味着 ZFS 可以为你处理错误，但快照和复制等功能使得 ZFS 变得有利。

大多数虚拟化系统都会为你克隆系统，有时伪装成你可以部署的模板。但是，如果你将包含 ZFS 池的磁盘镜像复制到新的虚拟机，那么你的虚拟机就是原始机的副本。这意味着某些应该是全局唯一的项不再是唯一的了。这在独立的虚拟机上会产生问题吗？但如果你要在虚拟机之间移动磁盘镜像，你将需要更改每个虚拟机池的 GUID。

`guid` 属性包含池的 GUID。在这里我们获取 `db2` 池的 GUID。

```
# zpool get guid db2
NAME PROPERTY VALUE SOURCE
db2 guid 5552158746006792385 default
```

要生成新的池 GUID，使用 `zpool reguid`。将池名作为参数。

```
# zpool reguid db2
# zpool get guid db2
NAME PROPERTY VALUE SOURCE
db2 guid 76624604609377566669 default
```

现在你可以将一个虚拟机的磁盘镜像连接到另一台虚拟机，而不会让 ZFS 发脾气。

如果由于某种原因 `zdb(8)` 找不到你的 `pool.1234`，给池分配一个新的 GUID 也有帮助。

## 不区分大小写的文件系统

某些客户端（特别是 OS X）期望文件系统是不区分大小写的。你可以通过 `casesensitivity` 属性让 ZFS 数据集不区分大小写。

`casesensitivity` 属性默认是 `sensitive`，即传统的 Unix 风格区分大小写。如果你将其设置为 `mixed`，ZFS 可以支持区分大小写和不区分大小写的请求。将 `casesensitivity` 设置为 `insensitive` 意味着 ZFS 将完全不区分大小写。

你只能在创建数据集时设置此属性。

```
# zfs create -o casesensitivity=mixed samba/share
```

要更改现有数据集的大小写敏感性，创建一个正确设置属性的新数据集，然后将文件复制过去。

## ZFS 深度解析：zdb(8)

为了更好地了解 ZFS 内部正在发生什么，能够窥探幕后情况会有帮助。检查 ZFS 的内部状态可以帮助你理解系统为何以这种方式运行运行。即使你对“香肠是如何制作的”不感兴趣，本节也可能包含一些感兴趣的点。

许多人阅读《FreeBSD 系统的设计与实现》第 2 版，Addison-Wesley Professional, 2014 中的 ZFS 章节来学习 ZFS 的内部数据结构。虽然该书提供了大量信息，但对系统中的实际文件研究这些数据结构的能力会让一切更有意义。

FreeBSD 提供的 ZFS 工具套包含 `zdb(8)`，它是 ZFS 调试器。`zdb(8)` 手页明确指出：“命令的输出通常指的是 ZFS 池的磁盘上结构，并且在本质上是不稳定的。大多数调用的精确输出均未记录，假设用户了解 ZFS 内部原理。”输出基于磁盘上的内容以及 `zdb(8)` 对任何时刻内存中内容的模拟。解释工作很大程度上留给了操作员。如果你真的深入研究 `zdb(8)`，你可能需要手头准备一份《设计与实现》以供参考。

`zdb(8)` 命令有许多标记。其中大多数标记可以指定多次，以增加信息的详细程度。

### 块统计

`zdb(8)` 实用可以检查池中块分配的分类情况。我们将从检查一个虚拟机的极小池开始，然后增加较大的池。使用 `-b` 标记和池名称来获取该池的块统计。

分析块统计需要大量内存，因为 `zdb(8)` 在计算各种统计数据时必须跟踪每一个块。非常大的池可能需要的内存超过宿主机内存，最终内核的 OOM 杀手会为了保护系统而终止 `zdb`。在生产系统上运行此命令时要小心，因为 `zdb(8)` 可能会导致系统停顿。

让我们从虚拟机的小型单磁盘池开始。

```
# zdb -b mypool
traversing all blocks to verify nothing leaked...
925M completed ( 473MB/s) estimated time remaining: Uhr 00min 00sec
No leaks (block matches space maps exactly)
```
