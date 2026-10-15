
如你所见，你可以在 `C` 代码中尽可能多次调用 `tracepoint()`。第一个参数是跟踪名称，其余是参数列表。

`BabelTrace` 是一个帮助你处理跟踪字段的工具，遵循通用规则。它允许使用通用跟踪格式 (`CFT`) 查看跟踪，适用于将跟踪转换为其他格式。你已经安装了它，可以使用 `Trace Compass` (https://tracecompass.org/) 查看 `LTTng` 跟踪，这是一个图形化应用程序。你也可以通过 http://trace.org/ctf 了解更多关于 `CTF` 格式的信息。`babeltrace` 包在执行 `traceMc` 之前最后要做的一件事是在跟踪会话后启用 `libtrace.h` 中定义的事件：

- `lttng create`
- `lttng enable-user`
- `lttng start`
- `./traceMc`
- `lttng stop`
- `lttng destroy`

在执行 `traceMc` 时运行以下命令将显示 `libtrace.h` 中定义的所有可用字段。为了从这里获取输出，`traceMc` 必须运行——这就是调用 `sleep()` 的原因（见下文）。由于 `traceMc` 使用递归函数，它有 515 行，但在跟踪单个会话时你会得到的更少。

## C 代码分析

输出如下：

- `babeltrace/libftrace_tracing-session-2016015-193031`
`[26:285711(777777777)] libftraceng_field`
`(cpu_id=0, input_field_id=0)`
`[26:285711(00004200002831)] libftraceng_field`
`(cpu_id=0, input_field_id=1)`
- `babeltrace/libftrace_tracing-session-2016015-193031ve.`

`5121 50934`
`ascii` 事件将显示跟踪的数量
`babeltrace/libftrace_tracing-session-2016015-193031 awk '{print $1}' | sort -c -rn`（可以看到输出，左侧），你可以理解 `traceMc` 需要优化！如果你想跟踪应用程序，你需要安装一个额外的包：

- `pip install lttng`
- `lttng-analyze`
- `LTTng-UST Python agent`
- `sudo apt install lttng`

跟踪 Python 代码超本教程的范围，你可以在 http://lttng.org/docs/doc-python-application 了解更多信息。

> 这里是使用 `babeltrace` 的 `traceMc` 输出，显示 `traceMc.c` 中存在严重的性能问题。

![](img/97fdf078658cf34e6c480f18f12014d_118_0.png)

## Hacking

### Grub: 从 USB 启动 ISO

避免满袋 DVD 的一种简单方法是将它们全部复制到一个 U 盘上，并带有一个方便的菜单选择启动哪一个。

光盘上几乎所有的发行（distro）ISO 文件都是所谓的混合文件（hybrid files）。这意味着它们不仅可以复制到 U 盘中，而且可以像 DVD 一样启动。好消息是，大多数发行版都支持这一点，而且从 ISO 启动的选项很少有记录。这种方法的主要缺点（至少对于难以让 USB 正常工作的新手来说）是不同的发行版需要不同的处理方式。随着持有几十 GB 容量的 U 盘和小型硬盘越来越难以寻找，这是一种既节省空间又节省口袋的方法。在同一个 盘上放置多个 ISO 并不理想。使用 Grub 启动 DVD，它具有允许从 ISO 文件启动的功能。

在接下来的几页中，我们将展示如何这样做：首先设置 U 盘，以及你从自己的发行版驱动器无法获得的选项。我们还将展示如何处理协作程度较低的发行版。

#### 设置 U 盘

首先，我们需要格式化 U 盘。我们假设 U 盘设置为单分区，尽管你可以使用多分区布局中的第一个分区。你不能使用格式化为 NTFS 的 U 盘。如果你使用 ext 或 ext4，那么文件系统的选择非常重要，只要它与 Grub 兼容即可。

我们将使用 FAT32（在闪盘上使用日志型的 ext3 或 ext4 没有意义）。使用任何适合你驱动器的格式，这意味着我们可以从 Windows 计算机下载并提取 ISO 镜像。无论你给文件系统起什么标签，我们都使用 `MULTIBOT`，因为它在稍后很重要。

# Grub

## EFI 启动

在此实例中，我们创建了一个使用旧版 MBR 方法的闪盘。虽然现在大多数计算机都使用 UEFI，但它们仍然具有从 MBR 启动的兼容模式。因此，这让我们坚持使用旧的便携方案，但如果你需要使用 UEFI 启动你的 U 盘，可以使用 `grub-install` 命令指定 UEFI 目标，如下所示：

```bash
$ sudo grub-install --target=x86_64 --boot-directory=/media/MULTBOOT/
```

这是一个 64 位的目标，因为 UEFI 在 64 位硬件上是完全支持的。如果你想在 32 位设备上使用 U 盘，很抱歉（不支持）MBR 启动方法。

![](img/97fdf078658cf34e6c480f18f1f2014d_120_0.png)

在这些示例中，usb 设备位于 `/dev/sdb`（电脑有多个硬盘），文件系统挂载在 `/media/sda1`，请根据实际情况修改路径。如果首先要在盘上安装 Grub 以使其可启动：

```bash
$ mkdir -p /media/MULTBOOT/boot
$ sudo grub-install --target=i386-pc --boot-directory=/media/MULTBOOT/boot
```

注意：`boot-directory` 选项将包含 Grub 文件，但你提供的设备名称是整个 U 盘，而不是分区。我们通过以下命令创建配置：

```bash
$ grub-mkconfig -o /media/MULTBOOT/boot/grub/grub.cfg
```

这将创建一个启动硬盘上发行版的配置，因此请编辑 `grub.cfg` 以添加符合你行内容的条目：

```
### END /dev/sdb/grub.cfg
```

## 添加发行版

这为我们提供了一个没有菜单条目的可启动介质。如果我们从这个 U 盘启动，将会进入 Grub shell 界面。所以，让我们添加一个常规的（抱歉，但是）Ubuntu 条目，以便从 ISO 文件启动（也很简单，这能让事情变得简单）。只需将条目添加到文件末尾即可：

```
set isofile=/ubuntu/ubuntu-16.04-amd64.iso
loopback loop isofile
linux (isofile)/casper/vmlinuz-16.04-generic isofile=ubuntu-16.04-amd64 quiet splash
initrd (isofile)/casper/init.rd
```

![](img/97fdf078658cf34e6c480f18f1f2014d_120_1.png)

Ubuntu 16.04 -

在驱动器上创建目录并拷贝 ISO 文件。然后使用 U 盘并从 U 盘重启。你应该能看到一个 Grub 菜单，其中有一个 Ubuntu 条目，然后你可以打开并从安装启动。

## 特殊选项

第一行创建一个用于存储 ISO 文件的变量。我们使用变量是因为当我们要向驱动器添加菜单时，只需要更改一个地方。第二行告诉 Grub 挂载回环设备（将文件挂载为类似于块设备）。然后我们有两个条目。你可能会奇怪我们如何知道要在菜单条目中添加什么。通过原始启动菜单并查看 ISO 来了解需要添加什么。后者，在 Ubuntu 的情况下，是将 `isofile` 变量设置为我们需要挂载的 ISO 文件的路径。要查看原始启动菜单，我们需要这样做：

```bash
$ sudo mount --loop /path/to/iso/somewhere
```
