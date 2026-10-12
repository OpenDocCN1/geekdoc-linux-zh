
## 纯 Linux 系统示例

对于第一个示例，让我们从一个仅运行 Linux 且只有一个可能内核的系统开始。对每个示例，我们将使用图 5.2 中所示的硬盘布局。硬盘总共有五个分区。前两个是主分区，另外三个是包含在单个扩展分区内的逻辑分区。

### 图 5.2
为 Linux 准备的示例硬盘布局。

| 项目 | 设备 |
|---|---|
| 分区表 | /dev/hda |
| 分区 1 | /dev/hda1 |
| 分区 2 | /dev/hda2 |
| 扩展分区 | /dev/hda3 |
| 扩展分区表 | |
| 分区 3 | /dev/hda5 |
| 扩展分区表 | |
| 分区 4 | /dev/hda6 |
| 扩展分区表 | |
| 分区 5 | /dev/hda7 |

该系统按经典 Linux 风格设置，如下所述：

- 根分区是设备 `/dev/hda1` 上的分区 1。
- `/usr` 分区位于分区 2，`/dev/hda2`。
- 分区 3 包含交换分区 `/dev/hda5`。
- `/home` 位于分区 4，`/dev/hda6`。
- `/var` 位于分区 5，`/dev/hda7`。

第一个需要回答的问题是安装 LILO 的位置。鉴于刚刚描述的设置，我们有四个选择。这四个选择对应于 Linux 文件系统分区。唯一不能安装 LILO 的分区是位于 `/dev/hda5` 的 Linux 交换分区。其他任何分区都可用于安装 LILO。这可能与你过去的做法相悖，并且受制于一些注意事项，但它仍然是一个真实的陈述。话虽如此，通常将 LILO 安装在两个位置之一。其中之一是包含 Linux 根分区的分区的引导扇区，在我们的示例中为 `/dev/hda1`。该引导序列如图 5.3 所示，其中加载 DOS MBR，搜索活动分区（`/dev/hda1`），然后该处的引导扇区将 Linux 内核加载到内存中并执行它。

### 图 5.3
DOS MBR 引导序列。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_148_0.png)

该设置有一些优点，也有缺点。一个优点是，如果机器将来被重新分配运行另一个操作系统，摆脱 LILO 所需的唯一操作就是重新分区硬盘。另一方面，使用此方法也有一些缺点。首先是系统必须使用 Windows 或 DOS 安装才能将 DOS MBR 写入硬盘。或者，你可以使用带 /MBR 开关的 DOS FDISK 命令创建主引导记录。另一个小缺点是，你必须使安装 LILO 的分区处于活动状态，以便 DOS MBR 能够找到它。

另一个选项是将 LILO 安装在主引导记录中，替换 DOS MBR。这导致如图 5.4 所示的引导序列。由于这是一个纯 Linux 系统，这可能是更自然的设置，但缺点是如果将来从该系统上移除 Linux，你需要有一种方法来替换 MBR 上的 LILO。它不需要先用 DOS 或 Windows 准备磁盘，并且 LILO 不使用活动标志来确定要引导哪个分区。

### 图 5.4
LILO MBR 引导序列。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_148_1.png)

那么如何确定 LILO 应该安装在哪里？如果你使用 Red Hat 安装介质安装所有系统，你将得到两个选择：

- 主引导记录
- 第一个 Linux 分区

如果你的系统仅为 Linux 且引导盘从未用 DOS 或 Windows 分区，你应该选择主引导记录。这是因为主引导记录中目前没有加载引导加载程序来将控制权传递给 LILO。如果你的系统最初包含 DOS 或 Windows，或你的系统将为双启动，你可以任选其一。请记住，如果你选择第一个 Linux 分区，你必须将其标记为活动，以便主引导记录中的加载程序可以找到它。一旦你做出选择，安装程序会为你构建合适的 lilo.conf 文件并运行

/sbin/lilo，即映射安装程序。自然地，系统安装后你也可以手动完成，通过编辑 lilo.conf 文件并在命令行运行 /sbin/lilo。

> **注意**
> 
> 学习如何操作 lilo.conf 文件并使用映射安装程序 /sbin/lilo 强烈推荐。LILO 提供了大量可供选择的配置选项。Red Hat 安装程序仅构建最基本的配置文件。本章后面 “LILO 技巧和窍门” 部分描述了一些更有趣的可用选项。

以下列表显示了在 Linux 根分区上安装 LILO 所需的 lilo.conf 文件。

```
#
# General section
#
boot = /dev/hda1
install = /boot/boot.b
verbose = 2
prompt

# After 5 seconds, boot the default image
timeout = 50

#
# Boot my Linux 2.2.5 kernel
#

image = /boot/vmlinuz-2.2.5
    label = linux
    root = /dev/hda1
    read-only
    initrd = /boot/initrd.gz
```

前述文件中主要关注的行是 boot = /dev/hda1。该行告诉 LILO 将自身安装到何处。通过按以下文件列表所示更改此行，LILO 将改为加载到主引导记录中。

```
#
# General section
#
boot = /dev/hda
install = /boot/boot.b
verbose = 2
prompt

# After 5 seconds, boot the default image
timeout = 50

#
# Boot my Linux 2.2.5 kernel
#

image = /boot/vmlinuz-2.2.5
    label = linux
    root = /dev/hda1
    read-only
    initrd = /boot/initrd.gz
```

## 双操作系统系统

一个稍微复杂一些的示例涉及引导其他操作系统。例如，如果你有一个系统希望在 Windows 和 Linux 之间双启动，LILO 也能实现这一点。回到我们定义的分区，假设这次 Windows 安装在第一个分区。我们将按如下方式设置：

- Windows—位于第一个分区，/dev/hda1
- Linux 根—位于第二个分区，/dev/hda2

剩余分区用于其他 Linux 文件系统。在这种情况下，我们将把 LILO 安装在主引导记录中，即使这意味着如果我们决定卸载它，就必须重新处理重建主引导记录。请考虑以下 lilo.conf 文件：

```
#
# General section
#
boot = /dev/hda
install = /boot/boot.b
verbose = 2
prompt

# After 5 seconds, boot the default image
timeout = 50

#
# Boot my Linux 2.2.5 kernel
#
image = /boot/vmlinuz-2.2.5
label = linux
root = /dev/hda2
read-only
initrd = /boot/initrd.gz

#
# Boot Windows on the first partition
#
other = /dev/hda1
label = windows
table = /dev/hda
```

在此文件中，我们引入了关键字 other，用于指定包含其他操作系统的分区。我们还看到了 table 关键字的首次使用，它指定了此操作系统的分区表信息所在位置。在这种情况下的引导序列如图 5.5 所示。

### 图 5.5
以 LILO 作为 MBR 的双启动。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_151_0.png)

## /etc/lilo.conf 文件

要完全理解这些示例，你必须了解 LILO 配置文件 /etc/lilo.conf 的语法，因此让我们查看每个可用关键字及其含义。LILO 配置文件有两个部分。第一个是全局关键字部分。在此处指定关键字不是必需的，但通常这样做是为了避免不必要的重复。表 5.1 显示了全局部分的关键字及其含义。

### 表 5.1 LILO 全局部分关键字

| 关键字语法 | 描述 |
|---|---|
| backup=filename | 当运行 lilo 时，正在写入的引导扇区的备份会被复制到指定文件中。 |
| boot=boot_dev | 将 lilo 将写入引导加载程序代码的分区命名。 |

