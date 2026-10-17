
| delgroup | hdparm | isattr | | swapon | who |
| deluser | head | lmod | readlink | switch_root | whoami |
| depmod | hexdump | itmac | reldate | | xargs |
| devm | hostid | | izop | realpath | sysctl | yes |
| df | hostname | | izcopcat | reforme | syslog | zcat |
| dhcprelay | httpd | | makemime | rence | | zcip |
| * | hush | | set | | | |

# 第 13 章

![](img/55fba0370caa0078213ac3714cffd0ec_204_0.png)

其中共享库存放的位置总共占了 14 MB。那么问题是，你是否在其他地方需要这些共享库？

编译选项（Build Options）也是你可以选择交叉编译器前缀的地方，请注意它已经为你设置好了。

在安装选项（Installation Options）下，你可以选择符号链接创建的方式。它们可以是软链接、硬链接或脚本“封装器（wrappers）”。由于指向相同数据的硬链接共享同一个节点，对于节点数量有限的系统，这是一个非常有用的选项。软链接是默认选项，也是最好的选择。

安装前缀（Installation Prefix）是错误的。它标识了你安装 BusyBox 的文件系统根目录。在案例中，你可以在这里指定，也可以在 `make install` 步骤通过添加 `CONFIG_PREFIX=/home/target_fs` 来指定。有趣的是，在 BusyBox 的早期版本中，如果不指定位置，它会默认到 BusyBox 树内的一个目录。现在已经不起作用了。

# BusyBox 与 Linux 初始化

![](img/55fba0370caa0078213ac3714cffd0ec_205_0.png)

图 1.2

BusyBox menuconfig 顶部菜单。

## 应用程序 (Applets)

300 多个 BusyBox 应用程序分为几个类别。这些类别与 BusyBox 的目录树紧密对应。在许多情况下，BusyBox 版本省略了一些晦涩的选项。你可以将这些视为“精简版（lite）”。尽管如此，这些选项对于你的嵌入式系统已经足够了。在某些情况下，你可以选择你需要的命令。例如，Coreutils 类别并滚动到 `ls`。这样做的原因是为了减小代码体积。如果每个选项都能节省一些空间将会很好。浏览类别以了解情况。你会发现有很多不需要的东西，比如 `vi` 编辑器。你真的需要 `tar` 吗？查看 Shell 类别。默认 shell 是 `ash`，它声称是 BusyBox 发行版中最完整且正确的 shell。两个 shell `hush` 和 `msh` 功能较少，以换更小的内存。

## 编译与安装

BusyBox 使用标准的 `make` 和 `make install` 命令来编译和安装包。

# 第 13 章

标识你正在安装 BusyBox 的文件系统。在我们的案例中，你可以在这里指定，也可以在 `make install` 步骤通过添加 `CONFIG_PREFIX=/home/target_fs` 来指定。有趣的是，在早期 BusyBox 版本中，如果不指定位置，它会默认到 BusyBox 树内。现在不再有效。

### 硬链接 vs 软链接

在第 3 章，我们简要讨论了链接的概念。这个练习的目的是：硬链接是相同数据的替代名称或别名，它们指向磁盘上的相同数据块。在引用计数变为零之前，该数据不会被删除。相比之下，软链接或符号链接指向的数据，而是一个*名称*，而该名称可能不存在。

现在执行此操作：

```bash
ln ls lslink
ls -l
```

```bash
ln -s ls ls
ls -l
```

```bash
stat ls
stat ls
```

```bash
rm -f ls
ls -l
```

```bash
rm -f lslink
ls -l
```

你注意到了什么？特别是，`ls` 和 `lslink` 共享同一个索引（inode）。但 `ls` 具有不同的索引。

```bash
stat ls
stat lslink
```

```bash
rm -f ls
ls -l
```

```bash
rm -f lslink
ls -l
```

```bash
stat ls
stat lslink
```

```bash
rm -f ls
ls -l
```

当你从 BusyBox 执行 `ls` 时，结果如下。

`ls` 项被高亮，显示它指向的文件不存在。`ls` 的引用计数现在为 1。最后，将 `ls` 重命名为 `ls`：

```bash
mv ls ls
ls -l
```

```bash
stat ls
stat ls
```

```bash
rm -f ls
ls -l
```

```bash
rm -f lslink
ls -l
```

```bash
stat ls
stat lslink
```

```bash
rm -f ls
ls -l
```

`ls` 项被高亮，显示它指向的文件不存在。`ls` 的引用计数现在为 1。最后，将 `ls` 重命名为 `ls`：

```bash
mv ls ls
ls -l
```

```bash
stat ls
stat ls
```

```bash
rm -f ls
ls -l
```

```bash
rm -f lslink
ls -l
```

```bash
stat ls
stat lslink
```

```bash
rm -f ls
ls -l
```

`ls` 项被高亮，显示它指向的文件不存在。`ls` 的引用计数现在为 1。最后，将 `ls` 重命名为 `ls`：

```bash
mv ls ls
ls -l
```

# BusyBox 与 Linux 初始化

我们的恒温器现在是一个相当实用的网络设备，但它没有本地显示。如果你的 Mini2440 有 LCD，我们现在可以解决这个问题。首先是简单的历史。

多年前，Unix 以及随后的 Linux 系统典型的“控制台（console）”设备是通过串口连接到计算机的哑终端。这是一个经典的字符设备。当像数字设备公司（DEC）的 VT100 这样的视频终端变得“智能”时，提供了移动光标、更改颜色和选择性删除屏幕部分的方法。随后，PC 将位图“帧缓冲区（framebuffer）”设备的概念引入了计算机本身。

这些发展避免地在 Linux 驱动模型中引入了额外的复杂性。在串口视频终端时代，每个制造商最初都发明了自己的协议来处理光标控制等问题。因此，为了可移植性，这些互不兼容的协议必须被“抽象”成统一的形式。

# 第13章

“控制台设备驱动程序”的作用正是这样做——为那些需要不仅仅是输出字符流的应用程序提供一个统一的接口。

VT100 协议已成为终端控制的事实标准，这就是典型的控制台驱动程序向其暴露的 API。

同样，帧缓冲区（framebuffer）设备具有各种形状和大小，具有多种颜色深度，以及将位和字节映射到屏幕像素的各种方法。帧缓冲区的作用是暴露统一的 API，允许应用程序（实际上还有像控制台这样的驱动程序）以一致的方式管理这些差异。

LCD 面板的驱动是一个帧缓冲区驱动程序。主号为 29 的帧缓冲区设备。遗憾的是，帧缓冲区 API 的文档并不是非常详尽。不过没关系，因为我们反正不会直接使用它。

相反，我们将使用一个连接到设备号 40 的控制台驱动程序。该驱动程序正确地附加到 S3C2410 LCD 帧缓冲区驱动程序，任何写入它的内容最终都会显示在屏幕上。

### ANSI 终端转义序列

事实上，有一种用于控制控制台设备的标准协议。它基于 DEC 最初为其 VT100 系列视频终端开发的协议。该标准有许多常用名称，其中大多数包含 ANSI（美国国家标准协会）的缩写。

终端控制命令以转义字符 27 或 0x1b 开始，通常缩写为 `<ESC>`。通常后面紧跟着一个 "[" 字符以及一个或多个定义控制动作的字符。字符串 `<ESC>[` 被称为控制序列起始符（CSI）。

用于终端控制的完整 ANSI 标准非常详尽，我必须找到一个真正具有可读性的版本。作为参考，由欧洲计算机制造商协会（ECMA）编写的版本包含在光盘 `ECMA-048.pdf` 中。要查找其他版本，可以在 Google 上搜索“ansi terminal escape.” 之类的内容。

幸运的是，对于我们的目的，转义序列需要我们做的并不多。我们想要做的主要事情是移动光标，为我们的恒温器创建一个用户友好的显示界面。设置光标的方法是：

```
<ESC><row>:<col>H
```
