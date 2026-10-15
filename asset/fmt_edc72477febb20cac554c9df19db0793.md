
## 图 19.12 使用基于 Web 的 CUPS 管理界面来配置和管理打印。

本节提供了一个简短示例，展示如何使用 CUPS 的基于 Web 的接口创建 Linux 打印机条目。使用 CUPS 接口创建打印机和设备队列类型，例如本地、远程、串行端口或 Internet；然后输入设备的统一资源标识符 URI，例如 `lpd://192.168.2.35/1p`，它表示远程 UNIX 打印服务器的 IP 地址以及服务器上远程打印队列的名称。你还需要指定打印机的型号或制造商及其驱动程序。打印机页面链接允许你打印测试页、停止打印服务、管理本地打印队列、修改打印机条目或添加另一台打印机。

在管理页面中，点击“添加打印机”按钮，然后在名称字段中输入打印机名称，例如 `lp`，在位置字段中输入打印机的物理位置，并在描述字段中填写有关打印机的简短注释，例如其类型。图 9.13 展示了一个 Brother 多功能打印机的示例条目。

![](img/34e72348d53ca54c2a1d9c871316691b_467_0.png)

图 19.13 使用 CUPS 创建新的打印机队列。

点击“继续”按钮。然后，你可以在设备页面中选择打印机访问类型，本地、远程、串行端口或 Internet，如图 19.14 所示。例如，若要配置向本地打印机打印，请选择“并行端口 #1”；若是远程打印机，请选择“LPD/LPR 主机或打印机”条目。做出选择后，点击“继续”进入连接选项屏幕，如图 19.15 所示。

![](img/34e72348d53ca54c2a1d9c871316691b_467_1.png)

图 19.14 选择打印机的连接方式。

![](img/34e72348d53ca54c2a1d9c871316691b_468_0.png)

图 19.15 根据打印机连接情况输入适当的连接详细信息，如示例所示。

再次点击“继续”，并根据图 19.16 中所示对话框的要求选择打印机制造商。

![](img/34e72348d53ca54c2a1d9c871316691b_469_0.png)

图 19.16 创建新队列时选择打印机制造商。

点击“继续”后，接着选择驱动程序。创建打印机后，你可以使用如图 19.17 所示的打印机页面来打印测试页、停止打印服务、管理本地打印队列、修改打印机条目或添加另一台打印机。

![](img/34e72348d53ca54c2a1d9c871316691b_469_1.png)

图 19.17 使用 CUPS 打印机页面轻松管理打印机。

CUPS 提供许多其他功能，在安装、配置并运行后，为 Fedora 提供透明的传统 UNIX 打印支持。

> 注意
>
> 要了解有关 CUPS 的更多信息并获取该系统的简要概述，请访问 [http://www.cups.org/](http://www.cups.org/)。

### 控制台打印控制

旧版本的 Red Hat Linux 使用了 4.3BSD 行式打印机假脱机系统及其配套的基于文本的打印实用程序。这些实用程序的新版本，名称相同，包含在你的 Fedora DVD 中，但它们是 CUPS 包的一部分。这些命令支持在后台启动打印作业，作为后台进程、打印多个文档、指定本地和网络打印机、控制打印机以及管理等待在打印机假脱机队列中的文档。

### 使用基本打印命令

配置好打印机后，你可以使用任何支持打印的图形客户端从桌面进行打印。如果你不使用桌面，而是更喜欢使用或通过基于文本的界面访问你的 Fedora 系统，你也可以在命令行中输入若干打印命令。用于从命令行打印和控制打印的主要 CUPS 命令如下：

- ► `lp`—行式打印机假脱机命令；用于使用特定打印机打印文档
- ► `lpr`—行式打印机队列显示命令；用于查看等待打印的现有文档列表
- ► `lpstat`—显示服务器和打印机状态信息
- ► `lprm`—行式打印机队列管理命令；用于从打印机队列中移除打印作业
- ► `lpc`—行式打印机控制程序；由 root 操作员用于管理打印假脱机、lp 守护程序和打印机活动

这些命令提供了 CUPS 所提供功能的一个子集，但可以从命令行用于启动和控制打印机及打印队列。

你使用 `lp` 命令配合指定的打印机和文件名来打印文件，文档或图像。例如，要用名为 `lp` 的打印机打印文件 `mydoc.txt`，请使用 `lp` 命令、其 `-d` 命令行选项以及打印机名称，如下所示：

```bash
# lp -d lp mydoc.txt
```

### 管理打印作业

你还可以从命令行打印多个文档。例如，若要同时向 `lp` 打印机打印一组文件，请像这样使用 `lpr`：

```bash
# lp -d lp *.txt
```

这种方法利用 shell 的通配符功能，将当前目录中所有以 `.txt` 结尾的文件提供给 `lpr` 命令进行打印。使用 `lpq` 命令查看打印机的队列，如下所示：

```bash
# lpq
lp is ready and printing
Rank   Owner   Job   File(s)         Total Size
active root     7     classes.conf     3072 bytes
```

`lpq` 命令报告作业、所有者、作业号、正在打印的文件以及作业大小。作业号，本例中为 7，由 CUPS 用于跟踪正在打印或等待打印的文档。每个作业都有唯一的作业号。若要停止本例中的打印作业，请在 `lprm` 命令后跟作业号，如下所示：

```bash
# lprm 7
```

`lprm` 命令将假脱机文件从打印机队列中移除并终止该作业。打印作业的所有者，如普通用户，只能移除他们拥有的假脱机作业。作为 root 操作员，你可以终止任何作业。

只有 root 操作员才能使用 `lpc` 命令来管理打印机和队列，因为该命令主要用于打印机和队列控制。作为普通用户，你无法使用它来重新排列打印作业的顺序，但你可以获取任何系统打印机状态的显示。在命令行上像这样启动 `lpc`：

```bash
# /usr/sbin/lpc
```

`lpc` 命令内置了帮助，但仅包含五个命令：`exit`、`help`、`quit`、`status` 和 `?`。`status` 命令显示指定打印机或所有打印机的状态：

```bash
# lpc
lpc> ?
Commands may be abbreviated. Commands are:

exit help quit status ?
lpc> status
lp:
    printer is on device 'parallel' speed -1
    queuing is enabled
    printing is enabled
    no entries
    daemon present

netlp:
    printer is on device 'parallel' speed -1
    queuing is enabled
    printing is enabled
    no entries
    daemon present
lpc> quit
```

上述示例会话显示了两台打印机，`lp` 和 `netlp` 的状态报告。另一个有用的命令是 `lpstat`，你使用其 `-t` 选项时如下所示：

```bash
# lpstat -t
scheduler is running
system default destination: lp
device for lp: parallel:/dev/lp0
device for net1p: parallel:/dev/lp0
lp accepting requests since Jan 01 00:00
net1p accepting requests since Jan 01 00:00
printer lp is idle. enabled since Jan 01 00:00
printer net1p is idle. enabled since Jan 01 00:00
```

此命令列出了本地系统上打印队列的所有状态信息。

### 避免打印机支持问题

排查打印机问题可能会令人沮丧，尤其是当你发现新打印机无法在 Linux 上正常工作的时候。首先，请记住今天市场上几乎所有的打印机都能与 Linux 配合使用。然而，某些厂商在支持 Linux 方面的记录更好。如果你想查看评分表，请访问 http://www.linuxprinting.org/vendors.html。

### 一体化，打印/传真/扫描 设备

有问题的打印机，或者可能与 Fedora 不兼容的打印设备，包括将扫描、传真和打印服务结合在一起的多功能，或一体化 打印机。你应研究任何计划购买的设备，并避免任何不愿意提供驱动程序或开发信息以支持 Linux 的厂商。

在 Linux 对多功能打印机的支持领域，惠普对 HP OfficeJet Linux 驱动程序项目的支持是一颗闪耀的明星，地址为 http://hpgoj.sourceforge.net/。许多型号支持打印和扫描，传真支持正在开发中。
