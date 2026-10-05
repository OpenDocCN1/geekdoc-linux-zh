

## 第 13 章

## 驱动程序与内核

通过在自定义规则目录中创建一个同名文件，可以忽略或覆盖默认规则文件。

udev 的主配置文件是 `/etc/udev/udev.conf`；然而，默认行为是合理的。某些发行版的 `udev.conf` 文件仅包含注释，但其中一个启用了错误日志的文件除外。

遗憾的是，由于发行版之间和开发者之间的政治斗争，不同发行版之间几乎很少有协同效应。默认规则目录中的许多文件名在不同发行版之间是相同的，但文件内容存在显著差异。

规则文件按照 `mn-description.rules` 的模式命名，其中 `mn` 通常是一个两位数字。文件按字典顺序处理，因此数字较小的文件先被处理。规则目录中的文件会被合并，然后由 udev 守护进程 `udev` 对它们进行解析。`.rules` 后缀是强制性的；没有该后缀的文件将被忽略。

规则的形式如下：

```
match_clause, [match_clause, ...] assignment_clause [,assignment_clause ... ]
```

匹配子（match-clauses）定义了规则应用的情况。每个匹配子由一个键、一个操作符和一个值组成。例如，上述的 `ATTR(size=="174271")` 子句被视为规则的一个潜在组件；它选择所有 `size` 属性为 1,974,271 的设备。

大多数键指向属性（udev 从 `/sys` 文件系统获取这些属性），但某些键指向依赖于上下文的属性，例如正在处理的操作（如设备添加或删除）。所有匹配子必须全部匹配，规则才能被激活。

表 13.8 显示了 udev 识别的匹配键。

### 表 13.8 Udev 匹配键

| 匹配键 | 功能 |
| --- | --- |
| ACTION | 匹配事件，例如 add（添加）或 remove（删除） |
| DEVPATH | 匹配特定的设备路径 |
| KERNEL* | 匹配内核对设备的命名 |
| SUBSYSTEM* | 匹配特定的子系统 |
| DRIVER* | 匹配设备使用的驱动程序 |
| ATTR(filename)* | 匹配设备的 sysfs 值；文件名是 sysfs 树中的叶节点，对应于特定属性 |
| ENV[key] | 匹配环境变量的值 |
| TEST[mask] | 测试命令；如果返回码为 0 则匹配 |
| PROGRAM | 运行外部命令；如果返回符合条件则匹配 |
| RESULT | 匹配通过 PROGRAM 调用的最后输出 |
| a. | 也可用复数形式。它通过搜索设备路径来匹配值。 |

## 构建规则和持久性名称

对于匹配规则，赋值子句（assignment_clauses）指定了 udev 处理该事件时应该采取的操作。它们的格式与匹配子句相似。

最重要的赋值键是 `NAME`，它指示 udev 应该为设备命名。可选的 `SYMLINK` 赋值键通过在 `/dev` 中指定的路径为设备创建符号链接。

让我们用一个示例将这些组件结合：一个 USB 驱动器。假设我们想让驱动器的设备名称在插入和弹出时保持持久，并且希望设备自动挂载和卸载。

首先，插入闪存盘并检查内核是如何识别它的。有几种方法可以实现。通过运行 `lsusb` 命令，我们可以检查 USB 总线：

```
ubuntu$ lsusb
Bus 001 Device 007: ID: 1307:0163 Transcend, Inc. USB Flash Drive
Bus 001 Device 001: ID: 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID: 1d6b:0001 Linux Foundation 1.1 root hub
```

或者，我们可以检查提交到 `/var/log/messages` 的日志记录。在我们的案例中，连接遵循了详尽的审计追踪：

```
Aug 19:50:03 ubuntu kernel: [4269.25554] scsi 8:0:0: Direct-Access
Ut163 USB2FlashStorage 0.00 POQ: 0 ANSI: 2
Aug 19:50:03 ubuntu kernel: [4269.299226] sd [1974271 512-
byte hardware sectors: (1.01 GB/963 MiB)
Aug 19:50:03 ubuntu kernel: [4269.30749] sd 8:0:0: [1974271 512-
byte hardware sectors: (1.01 GB/963 MiB)
Aug 19:50:03 ubuntu kernel: [4269.307182] sdb: db1
Aug 19:50:03 ubuntu kernel: [4269.427785] sd 8:0:0: Attached SCSI
removable disk
Aug 19:50:03 ubuntu kernel: [4269.428405] sd 8:0:0: Attached scsi generic-generation type 0
```

上面的日志显示该设备被识别为，这为我们从 `/sys` 中识别设备提供了一种简单的方法。我们现在可以使用一些该设备的特征规则片段来检查 `/sys` 文件系统，这些片段可以用于 udev 规则。

```
ubuntu$ udevadm info -a -p /block/sdb1
looking at device '/devices/pci:pci0000:00/0000.11:0.0/usb1/1.0/1-1/1:1/host/target30:0:0:0:0:0/block/sdb1'
KERNEL="sdb1"
SUBSYSTEM="block"
DRIVER=""
ATTR(partition)="63"
SIZE="1974208"
ATTR(stat)="71 792 1857 808 0 0 0
0 512 808*"
```

![](img/579efec8c67772f31ecf34844bbb71a2_489_0.png)

（此处省略重复的 udevadm 输出，内容与原文一致）

