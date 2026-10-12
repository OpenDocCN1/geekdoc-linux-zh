
这是`Netcat`的一个比较新奇的用法，但当你没有其他工具来测试两台机器之间的网络速度时，它非常有用。为了这一点，你将不得不使用`netcat-tradical`方法。现在，在服务器机器上，你需要执行以下命令：

在客户端机器上，执行下一个命令并在`10`秒后按`Ctrl+C`即可使其工作：

```
$ yes | nc traditional -v -n 192.168.2.4 2222
```

使用`bc`，你可以发现网络速度约为每秒`1,048,067`字节，这对于`10 Mbps`的无线网络来说是绝对完美的。

## 15 使用 Netcat 传输目录

你已经学习了如何使用`Netcat`传输文件。现在，你将学习如何借助`tar`命令传输目录。服务器部分如下所示：

客户端部分应该使用：

```
$ nc localhost 1234 | tar -xvf -
```

## 16 使用 Crypt 加密 Netcat 连接

以明文传输数据是不妥的，并且可能会导致问题。如果你感到不安，可以使用`Crypt`，它是`True`加密的轻量级版本。在`Ubuntu`系统上，你可以安装：

```
$ sudo apt install crypt
```

现在，你已经准备好加密`Netcat`了。服务器部分看起来如下：

```
$ crypt -passphrase -l -p 12345
```

客户端部分应该运行以下命令：

```
$ crypt -passphrase localhost 12345
```

## 使用 Dropbox 传输目录

## 17 使用 tcpdump 和 Wireshark 捕获网络数据

如果连接失败且你无法找到实际问题所在，使用`tcpdump`。`Wireshark`是一个图形化工具，可以帮你检查数据。命令是：

```
$ tcpdump -i any -c 100 port 1234
```

如果你无法用`tcpdump`解决问题，请用`tcpdump`捕获数据并用`Wireshark`处理。

## 防火墙和路由器问题

在尝试将服务器与路由器配时，`Netcat`可能会出现异常行为。困难在于，当源和目的不在同一子网时，路由器或防火墙可能会启用或阻止连接。结果是机器无法通过入站转发监听指定的端口。如果你在参数后收到错误的错误，连接将自动终止。如果你想确保数据加密，请使用...

## 18 使用 tcpdump 捕获网络数据

## 切换到 btrfs 文件系统

由于`btrfs`存储数据的方式，它最佳用处之一是使用类似的技术将一系列硬盘放入`/dev/RAID0`。例如，在终端中执行：

`btrfs`拥有某些使其它成为系统非常完美的特性。某些发行版一直渴望将`btrfs`作为默认文件系统，过去几年，它在桌面发行版中被广泛使用并运行良好，即使在`LVM`内部。某些发行版创建了可以回滚的快照。尽管有一个新的竞争者，`Fedora`一直非常渴望将`btrfs`作为默认文件系统，它...

## 资源

- `Gparted` <http://gparted.org>

- `btrfs-tools`

## 别忘了，你可以随时检查 btrfs 分区和硬盘

- `01 寻找正确的工具`：第一步是安装相应的设置工具。虽然内核支持，但并非每个发行版都默认包含这些包。在`Debian`和`Ubuntu`发行版中，通过以下命令安装：

- `02 格式化分区`：现在你可以在系统上设置你的`btrfs`分区了。启动并导航到想要格式化的设备。要么格式化现有分区，要么创建一个较小的`btrfs`分区。

- `03 进入终端`：现在你可以在终端执行此操作来读取磁盘。打开并使用`fdisk -l`如果你需要确定系统上的分区和硬盘。这就是创建你的`btrfs`分区的方法：

- `04 创建 RAID`：`btrfs`的最佳用处之一（由于其存储数据的方式）是使用类似的技术将一系列硬盘放入`/dev/RAID0`。例如，在终端中执行：

- `05 提取你的系统文件`：以防你忘记它们，你可以随时检查`btrfs`分区和硬盘的详情。这对于数组中的硬盘同样有效，这正是`RAID`所需要的。

- `06 创建分区`：我们已经创建了硬盘、`RAID`和子卷，但你也可以使用之前的方法创建`btrfs`分区。通过执行终端并使用某些操作将分区转换为`btrfs`。

## 技巧 | 妙招 | 黑科技 | 应用

![](img/6e6bbc2d7ddad215386a38abf7a3b0b7_51_0.png)

### 09 权限

磁盘、分区和子卷的创建方式意味着你必须使用`root`账户访问它们才能正常使用。我们可以通过以下命令为它们赋予普通权限：

> “如果你正在进行硬件`RAID`，让元数据保持冗余可能会很有用”

```bash
$ sudo chown 777 btrfs/
```

`RAID 0`

`RAID 1`

`A1 A2`

`A3 A4`

`A5 A6`

`A7 A8`

`A9 A10`

### 10 关于 RAID

你可以创建不同类型的`RAID`组——默认是`RAID 0`，但它也支持`RAID 1 (10+1)`和`RAID 6`。选择哪种`RAID`取决于个人偏好以及你投入维护系统投入的精力。

### 11 RAID 1

`RAID 1`将数据在驱动器间进行复制以实现冗余，可以使用修改后的创建`btrfs`块或选择设备的命令在`btrfs`上创建。`-d`选项允许定义数据的存储位置。

### 13 RAID 10

`RAID 10`的基础镜像和条带化适用于大型数据仓库和冗余。我们可以同时使用`-m`和`-d`选项来指定哪些元数据数据需要进行适当冗余：

#### 12 非冗余元数据

如果你正在进行硬件`RAID`，元数据的冗余可能是没有必要的——否则，如果元数据不冗余，你可能会丢失数据。在这种情况下，请使用带有`'single'`模式的单硬盘或`RAID 0`。

#### 14 查看不同选项

`-m`和`-d`选项允许你实现一些花哨的操作。你可以使用`-d /single/dev/sdb/dev/`创建一个简单的`RAID 10`（`Just a Bunch (of Drives)`）。你也可以在数据冗余的同时让元数据不冗余，例如使用`-m raid0 -d raid1 /dev/sdd /dev/sdd`。还有许多方法可以根据你的需要进行。

```bash
$ btrfs -m raid1 -d raid1 /dev/sdb /dev/sdc
```

```bash
$ btrfs -m raid0 -d raid1 /dev/sdb /dev/sdc
```

Linux 技巧、妙招、黑科技 & 应用

## 技巧 | 妙招 | 黑科技 | 应用

![](img/6e6bbc2d7ddad215386a38abf7a3b0b7_52_0.png)

```bash
robz@ubuntu:~# sudo btrfs volume snapshot btrfs/subvolume btrfs/snapshot-1
create snapshot of btrfs/subvolumes in 'btrfs/snapshot-1'
robz@ubuntu:~# sudo btrfs volume list btrfs/volume1
[password for root]: 
ID 257 gen in level 5 pathvolume:
ID 258 gen in level 5 pathvolume1
robz@ubuntu:~# sudo btrfs volume set-default 258 btrfs/
[password for root]: 
robz@ubuntu:~#
```

### 15 RAID 5 和 6

`RAID 5`和`6`是极佳的选择，通过在多个驱动器上混合使用条带化和镜像，使得高达`75%`的空间可用于存储，同时仍能无硬盘故障的影响。在相同冗余下（理论上），它提供了比标准更多的功能；`RAID 6`则增加了冗余，但将五块驱动器的效率降低到其满容量的`60%`。

`btrfs`支持的功能仍存在`Bug`，即使在理想情况下`RAID 5`可能会很麻烦。关于`RAID 5`和`6`位的更多详细信息，请参阅文档`https://btrfs.wiki.kernel.org/index/RAID056`。

将其存放在原始子卷的不同位置以避免混淆：

```bash
$ btrfs subvolume snapshot btrfs/subvolume btrfs/snapshot-1
$ btrfs subvolume set-default 258 btrfs/
```

然后卸载并重新挂载子卷以生效更改。

### 16 创建快照

`btrfs`写入数据的方式意味着旧的修改方法只要有空闲空间就存在——这意味着你可以“回滚”到某个点。然而，你可以创建更持久的子卷快照。

### 18 包含备份快照

单个快照可以单独挂载，你也可以用旧版本替换新版本。如果你需要列出每个子卷的快照，可以在终端中执行：
