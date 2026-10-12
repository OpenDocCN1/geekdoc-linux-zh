

## 重置日期和时间

Fedora 安装程序在安装过程中会询问你默认的时区设置，以及你的计算机硬件时钟是否设置为格林威治标准时间（GMT）——更准确地说，这被称为 UTC，即协调世界时。

Linux 提供系统日期和时间；而你的计算机硬件提供基于硬件时钟的时间。在许多情况下，这两种时间可能会出现偏差。Linux 系统时间基于自 1970 年 1 月 1 日以来经过的秒数。你的计算机硬件时间取决于安装在 PC 主板上的时钟芯片类型，而许多主板芯片组都以容易出现漂移而闻名。

保持准确的时间不仅对单个工作站很重要，在网络安全环境中也至关重要。备份、计划停机以及其他全网络操作需要精确协调。

Fedora 提供了几个你可以在命令行或 X 会话期间使用的日期和时间工具，包括：

- `date`——用于从命令行显示、设置或调整系统日期和时间
- `hwclock`——一个根命令，用于显示、设置、调整以及同步硬件时钟和系统时钟
- `system-config-date`——Red Hat 的图形化日期、时间和网络时间配置工具

### 使用 date 命令

使用 date 命令来显示或设置你的 Linux 系统时间。此命令要求你使用特定的数字序列来表示期望的日期和时间。要查看你的 Linux 系统当前认为的日期和时间，请像这样使用 date 命令：

```bash
# date
Wed Jan 10 14:17:01 EDT 2005
```

要调整系统时间（例如，设置为 2005 年 1 月 23 日 上午 8 点），请使用包含月、日、时、分和年的命令行，如下所示：

```bash
# date 012308002005
Tue Jan 23 08:00:00 EST 2005
```

### 使用 hwclock 命令

使用 hwclock 命令来显示或设置你的 Linux 系统时间，显示或设置你的 PC 硬件时钟，或者同步系统时间和硬件时间。要查看你的硬件日期和时间，请使用 hwclock 及其 --show 选项，如下所示：

```bash
# hwclock --show
Wed 10 Sep 2003 02:17:53 PM EDT  -0.193809 seconds
```

使用 hwclock 及其 --set 和 --date 选项来手动设置硬件时钟，如下所示：

```bash
# hwclock --set --date "09/23/03 08:00:00"
# hwclock --show
Tue 23 Sep 2003 08:00:08 AM EDT -0.151718 seconds
```

在这些示例中，硬件时钟已通过 hwclock 设置，然后再次使用该命令以验证新的硬件日期和时间。你还可以使用 hwclock 通过硬件时钟的值来设置 Linux 系统日期和时间。

例如，要从 PC 的硬件时钟设置系统时间，请使用 --hctosys 选项，如下所示：

```bash
# hwclock --hctosys
```

要使用系统时间设置你的硬件时钟，请使用 --systohc 选项，如下所示：

```bash
# hwclock --systohc
```

### 使用 system-config-date 客户端

Fedora 的图形化 X 工具 system-config-date 可用于设置你的系统日期和时间。通过单击桌面菜单中的“系统设置”>“日期和时间”菜单项，或者在 X11 终端窗口中像这样从命令行启动客户端：

```bash
$ system-config-date &
```

按下 Enter 键后，你将需要输入 root 密码。输入 root 密码并单击“确定”按钮。然后你会看到一个窗口，如图 4.9 所示。

![](img/774d40fd20903495c5cd00e2efad3f33_140_0.png)

**图 4.9** 使用 Fedora 的 system-config-date 客户端来设置系统日期和时间。

使用日历和时间字段设置日期和时间。你还可以通过在网络时间协议（Network Time Protocol）字段中输入远程时间服务器主机名，让你的工作站通过网络获取更新的日期和时间信息。这需要正确配置并运行 ntpd 时间守护进程。

> **注意**
> 关于使用 ntpd 守护进程的 HTML 文档位于 /usr/share/doc/ntp*/ntpd.htm（如果系统安装了 ntpd）。

单击“时区”选项卡来更改或验证系统的时区。当前系统时区由 /etc 目录下名为 localtime 的文件指定，该文件是 /usr/share/zoneinfo 目录下相关时区数据库文件的副本。例如，

```bash
$ ls -l /etc/localtime
-rw-r--r-- 1 root root 1267 Apr 1 16:39 /etc/localtime

$ ls -l /usr/share/zoneinfo/America/New_York
-rw-r--r--   5 root      root        1267 Mar 13 18:00 /usr/share/zoneinfo/America/New_York
```

如果你使用 `system-config-date` 进行有时区更改，此文件将会改变。

## 管理 PCMCIA

移动 Linux 用户利用笔记本 PCMCIA 插槽添加 70 针、信用卡大小的设备，以支持以太网局域网连接、无线操作、火线设备、Compact Flash 硬盘、外部存储设备、串行端口和调制解调器。Linux 内核和大卫·汉兹（David Hinds）的 Card Services 软件支持许多不同类型的 PCMCIA 卡和 PCMCIA 卡座中的 Compact Flash 外形规格卡。

电力通过卡槽直接提供给 PCMCIA 设备和适配器，尽管一些外部硬件可能需要额外的电源。PCMCIA 支持在启动时根据 `/etc/sysconfig/pcmcia` 文件和 `/etc/rc.d/init.d/pcmcia` 启动脚本进行启用和配置。`/etc/sysconfig/pcmcia` 文件可能看起来像这样：

```ini
PCMCIA=yes
PCIC=yenta_socket
PCIC_OPTS=
CORE_OPTS=
```

以前的 Red Hat Linux 发行版和 PCMCIA 在此文件中使用了特定的控制器信息。然而，对于较新的 Linux 内核，支持是由内核模块或直接的 Linux 内核支持提供的。

### 使用 PCMCIA

PCMCIA Card Services 软件通过插入卡片时发出的一个或多个高音或低音哔声提供诊断信息。一高一低两个哔声表示卡片已被识别，但配置失败。单个哔声表示卡片仅被识别。两个高音哔声表示卡片已被识别并配置。

例如，如果你使用 Compact Flash 存储设备并在 Fedora 运行期间将其插入笔记本，你应该听到两个高音哔声。然后你可以使用 `dmesg` 命令检查已分配给该卡片的设备：

```bash
$ dmesg
...
hde: SunDisk SDCFB-8, ATA DISK drive
ide2 at 0x100-0x107,0x10e on irq 3
ide-floppy driver 0.99.newide
hde: 15680 sectors (8 MB) w/1KiB Cache, CHS=245/2/32
hde: hde1
...
```

这里没有显示所有输出（而且你的输出可能不同），但这个示例表明该卡片已被识别并配置为 `/dev/hde` 设备（包含一个分区，`/dev/hde1`）。然后你可以像使用其他存储介质一样使用此设备（有关使用 Linux 硬盘的更多信息，请参阅第 37 章“管理文件系统”）。

其他设备也可以以类似的方式被识别和配置。例如，如果你有一张以太网和调制解调器组合的 PCMCIA 卡并将其插入笔记本，你应该听到两组高音哔声（表示网络接口和调制解调器的成功识别和配置）。Linux 内核将报告接口和设备信息：

```bash
$ dmesg
...
eth0: NE2000 (DL10019 rev 05): io 0x300, irq 3, hw_addr 00:E0:98:06:84:C5
ttyS04 at port 0x0af8 (irq = 3) is a 16450
...
```

在这里，网络接口被识别为 eth0（请参阅第 17 章“网络连接”了解如何连接到网络）。调制解调器被配置为使用 `/dev/ttyS04`。

同样，解决 PCMCIA 卡的问题可能很困难，特别是随着 802.11b/g 无线网卡在流行程度和类型上的激增。解决此类问题可能需要下载、构建和安装新的驱动程序。

然而，幸运的是，几乎所有串行、调制解调和 Compact Flash 存储卡都容易被识别和配置。许多以太网卡也得到了支持。要检查许多卡片的当前支持状态，请阅读 SUPPORTED.CARDS 文件。如果你安装了 pcmcia-cs RPM 包，你会在 `/usr/share/doc/kernel-pcmcia-cs-3.X.XX/` 目录下（其中 X.XX 是包的版本）找到一份副本。

> **注意**
> 如果在配置和使用 PCMCIA 卡时遇到问题，请浏览 Linux PCMCIA 主页：http://pcmcia-cs.sourceforge.net/。单击 SUPPORTED.CARDS 链接，查看你的卡片是否受到支持。单击已知问题链接，查看其他拥有相同卡片的用户是否遇到问题，或者该卡片是否未得到完全支持。如果 PCMCIA 内核驱动程序有新版本可用，并且你的卡片驱动程序已发生变更（或开发了新的驱动程序），请下载并安装较新的软件。请参阅第 38 章了解有关安装新 PCMCIA 模块的信息，或遵循 PCMCIA 软件中包含的说明。

### 控制 PCMCIA 服务

虽然在使用 Red Hat 时可以在运行状态下插入或移除 PCMCIA 卡，但使用这些卡时要小心。例如，不要在与远程计算机连接时移除网络卡。不要拔出 Compact Flash 卡或其他存储介质卡（例如

