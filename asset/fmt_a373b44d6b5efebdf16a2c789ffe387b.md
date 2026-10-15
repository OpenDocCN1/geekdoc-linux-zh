
active bwagner@linuxbox1+396 396 (stdin) 511 17:43:21

`lpq` 支持的命令行选项非常少。重要的选项总结在表 9.5 中。

## 表 9.5. 一些 lpq 命令行选项

| lpq 选项 | 目的 |
|---|---|
| + [seconds] | 使用 + 选项获取打印机队列状态的实时报告。你指定的时间（以秒为）是报告间隔的时间。例如，命令 `lpq +5000` 将每隔 5000 秒打印一次打印机队列状态。 |
| -1 | 使用 -1 选项强制 `lpq` 以长格式打印输出（这更详细且易于阅读）。 |
| -P [printer] | 使用 -P 选项获取特定打印机的 lp 报告。例如，`lpq -PMondo` 将获取打印机 Mondo 的状态报告。 |

## 关于支持的打印机

要确定支持的打印机，请检查 `/etccap`。以下是一些示例输出：

```
cat /etccap
```

遗憾的是，并不是所有的打印机名称都是完全な。因此，你经常看到缩写。表 9.6 总结了一些缩写及其指向的打印机。

### 表 9.6. /etccap 中的打印机名称

| 名称 | 打印机 |
|---|---|
| bj10e | Canon BubbleJet |
| deskjet | Hewlett-Packard DeskJet |
| epson | Epson dot-matrix |
| ibmpro | IBM ProPrinter (contact |
| laserjet | Hewlett-Packard LaserJet |
| lbp8 | Canon LBP-8 |
| ljetplus | Hewlett-Packard LaserJet Plus |
| okil 82 | Okidata MicroLine |
| paintjet | Hewlett Packard PaintJet |
| sparc | Sparc |

## 处理应用程序

![](img/b0bfb2d724c393178bf462832858a65d_148_0.png)

## 本章内容

- 解压缩文件
- 安装软件

这种事情发生在每个人身上。早晚，你难免会陷入“下载成瘾”。当你发现 UNIX 有数千个免费程序可用时，这种状态通常就会出现。（北卡罗莱纳山大学的 Sunsite 足够让你忙碌几十年。Sunsite 的地址为 http://sunsite.unc.edu。）

问题是，一旦你下载了所有好东西，你就需要知道如何解压它们、安装并运行它们。这正是本章的核心内容。

## 在开始之前：这真的是你的菜吗？

当你偶然发现一个 UNIX 软件存档时，你会对那里提供的免费程序之多感到震惊。然而，在实际下载任何内容之前，你必须先确定几点：

- 软件是否能在你的 UNIX 变体上运行
- 软件是二进制形式还是源码形式
- 你是否拥有运行它所需的工具

## 软件兼容性问题

你可以通过以下三种方法判断可下载软件是否与你的机器兼容：

- 检查它所在的目录
- 检查文件名中的线索
- 检查 README 文件

例如，大多数软件存档会将站点拆分，使得 Solaris 的资源与 Linux 的资源存储在不同的目录中。这里是 Sunsite 一个目录的示例列表：

```
ftp> 1s
200 PORT command successful.
150 Opening mode data connection for file list.
lost+found
X11
packages
academic
multimedia
sun-info
gnu
docs
micro
electronic-publications
languages
archives
UNC-info
talk-radio
patches
solaris
Linux
226 bytes received in 0.05 seconds (3.40 Kbytes/sec)
```

注意那 `solaris` 和 `Linux` 目录了吗？通过为每个操作系统创建单独目录，许多系统让你的软件选择工作变得更容易。Netscape 就是这么做的。查看他们的 Communicator 4.5 目录：

| drwxr-xr-x 2 888 999 4096 Aug 24 22:50 |
| drwxr-xr-x 5 888 999 50 Jul 15 03:22 .. |
| -rw-r--r-- 1 888 999 16379 Jul 14 21:04 README.txt |
| drwxr-xr-x 2 888 999 116 Aug 24 22:50 aix4 |
| drwxr-xr-x 2 888 999 116 Aug 24 22:50 freebsd |
| drwxr-xr-x 2 888 999 114 Aug 24 22:50 hpu10 |
| drwxr-xr-x 2 888 999 114 Aug 22 22:50 hpux10_pro |
| drwxr-xr-x 2 888 999 113 Aug 22 22:50 hpux9 |
| drwxr-xr-x 2 888 999 113 Aug 22 22:50 irix62 |
| drwxr-xr-x 2 888 999 113 Aug 22 22:50 irix62_pro |
| drwxr-xr-x 2 888 999 117 Aug 22 22:50 linux12 |
| drwxr-xr-x 2 888 999 117 Aug 22 22:50 linux20 |
| drwxr-xr-x 2 888 999 117 Aug 22 22:50 linux20_pro |
| drwxr-xr-x 2 888 999 117 Aug 22 22:50 linux2glibc2 |
| drwxr-xr-x 2 888 999 117 Aug 22 22:50 mklinux |
| drwxr-xr-x 2 888 999 110 Aug 22 22:50 ncr40 |
| drwxr-xr-x 2 888 999 111 Aug 22 22:50 sinix54 |
| drwxr-xr-x 2 888 999 117 Aug 22 22:50 sunos54 |
| drwxr-xr-x 2 888 999 115 Aug 22 22:50 sunos54_x86 |
| drwxr-xr-x 2 888 999 119 Aug 22 22:50 sunos5551 |
| drwxr-xr-x 2 888 999 119 Aug 22 22:50 sunos551_pro |

几乎每个 UNIX 变体都有对应的目录，甚至还有同一种变体的多个版本（如 Linux）。

```
total 22596
drwx---- 2 101 10 2048 Jul 7 1995 .
drwxr-xr-x 6 12873 2048 Oct 25 1995 .
-rw-r--r-- 1 101 10 93696 Jul 7 1995 Mosaic-alpha
-rw-r--r-- 1 101 10 11131 Jul 7 1995 Mosaic-dec
-rw-r--r-- 1 101 10 85335 Jul 7 1995 Mosaic-hp
-rw-r--r-- 1 101 10 79775 Jul 7 1995 Mosaic-ibm
-rw-r--r-- 1 101 10 15718 Jul 7 1995 Mosaic-indy
-rw-r--r-- 1 101 10 903973 Jul 7 1995 Mosaic-linux
-rw-r--r-- 1 101 10 64843 Jul 7 1995 Mosaic-sgl
-rw-r--r-- 1 101 10 170807 Jul 7 1995 Mosaic-solaris-23
-rw-r--r-- 1 101 10 809343 Jul 7 1995 Mosaic-solaris-24
-rw-r--r-- 1 101 10 142723 Jul 7 1995 Mosaic-sun
-rw-r--r-- 1 101 10 144271 Jul 7 1995 Mosaic-sun-1
-rw-r--r-- 1 101 10 18355 Jul 7 1995 README
-rw-r--r-- 1 101 10 845 Jul 7 1995 README.solaris
```

在这种情况下，文件名本身就指示了软件兼容的 UNIX 变体。这是发现下载哪个文件的另一种方法：检查文件名。

在少数情况下，你可能需要下载并阅读 `README` 文件，因为目录名或文件名都没有反映兼容性。

## 第二部分 基础知识

### 二进制还是源码？

UNIX 软件有两种格式：

- 二进制 `Binary`
- 源码 `Source`

两者之间存在巨大差异——这种差异会影响你是否可以运行某个软件包。
