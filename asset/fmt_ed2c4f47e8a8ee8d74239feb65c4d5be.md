
> `system-config-printer` 实用程序是 `gnome-cups-manager` 的替代品，后者曾是 Ubuntu 的默认打印机配置工具。此新实用程序实际上最初是为 Fedora 开发的，已被 Ubuntu 采用。

## 管理打印服务

定义打印机后，你可以使用命令行查看和控制打印作业，或如果为 root，则控制系统上所有打印作业和打印机。表 8.1 包含 Ubuntu 中包含的部分 CUPS 及相关打印命令和驱动程序列表。

### TABLE 8.1 Print-Related Commands and Drivers

| Name | Description |
|------|-------------|
| a2ps | 将文本文件格式化为 PostScript 打印 |
| accept | 控制 CUPS 打印作业目标 |
| cancel | 取消 CUPS 打印作业 |
| disable | 控制 CUPS 打印机 |
| dvi[lj, ij4l, lj2p, ij4] | 将 TeX DVI 文件转换为特定 PCL 格式 |
| enable | 控制 CUPS 打印机 |
| enscript | 将文本文件转换为 PostScript |
| escputil | Epson Stylus 喷墨打印机实用程序 |
| groplb | 用于 Canon LBP-4 和 LBP-8 激光打印机的 groff 驱动程序 |
| gs | Ghostscript 解释器 |
| gsbj[dj500, lp] | Ghostscript BubbleJet 打印机驱动程序 |
| gsdj[dj500, ij, lp] | Ghostscript DeskJet 打印机驱动程序 |
| lpadmin | 基于 CUPS 命令行的打印机实用程序 |
| lp | 启动 CUPS 打印作业 |
| lpc | Berkeley 子集 CUPS 打印机控制客户端 |
| lpf | 通用打印机过滤器 |
| lprm | Berkeley 兼容的 CUPS 作业队列实用程序 |
| lpstat | 显示 CUPS 打印作业和打印机状态 |
| mpage | PostScript 文本格式化实用程序 |
| pbm[2ppa, page, to10x, toepson, toppa, toptx] | 便携式位图转换实用程序 |
| pr | 文本格式化命令 |
| psmandup | 用于非双面打印机的双面打印实用程序 |
| reject | 控制 CUPS 打印作业目标 |
| setup | 启动打印机配置工具 |
| smbclient | SMB 打印 spooler |
| smbprint | SMB 打印 shell 脚本 |
| smbspool | SMB 打印机 spooler |
| thinkjettopbm | 便携式位图到 ThinkJet 打印机转换实用程序 |

大多数 Linux 系统使用 PostScript 作为打印的默认文档格式。Ubuntu 使用 `gs` 命令以及 CUPS 来管理本地和远程打印作业以及打印作业期间传输的数据类型。`gs` 命令用于将文档流翻译成目标打印机接受的格式（该打印机很可能使用 HPCL）。

你可以使用 Ghostscript 解释器 `gs` 通过使用其 `--help` 命令行选项来显示其内置打印机设备，如下所示：

```
# gs --help
```

### 注意

Ubuntu 包含多种图形客户端，可用于查看许多不同类型的文档。例如，要显示 PostScript 文档（包括压缩的 PostScript 文档）或 PostScript 图像，请使用 `gv` 客户端。要显示便携式文档格式（PDF）文档，可以使用 `xpdf` 客户端。

`gs` 命令会输出多行关于命令行用法的帮助文本，然后列出内置的打印机和图形设备。获取此信息的另一种方法是启动 `gs`，然后使用 `devicenames ==` 命令，如下所示：

```
# gs
GPL Ghostscript SVN PRE-RELEASE 8.61 (2007-08-02)

Copyright (C) 2007 Artifex Software, Inc.  All rights reserved.

This software comes with NO WARRANTY: see the file PUBLIC for details.

GS>devicenames ==

/epson /pnggray /lp3000c /ep12050 /pgm /ijet4d/
/cljet5pr /pbmraw /lips4v /cdj550 /mag16 /laserjet/
/bj200 /dfaxhigh /ibmp ro /alc8500 /bmpgray/
/hpj600 /tiffgray /hpdj310 /pswrite/
...
```

此示例中并未列出所有设备。

### Aladdin 还是 GNU？

Linux 至少有两个版本的 Ghostscript 可用。一个版本名为 AFPL Ghostscript，以前称为 Aladdin Ghostscript。该版本根据 Aladdin 免费公共许可证授权，该许可证禁止商业分发。另一个版本称为 GNU Ghostscript，根据 GNU 通用公共许可证分发。有关不同版本的详细信息或有关许可问题的解答，请参阅 Ghostscript 主页：http://www.cs.wisc.edu/~ghost/。

### 创建和配置本地打印机

为 Ubuntu 系统创建本地打印机只需几个简单步骤即可完成。在开始之前，`cupsd` 守护进程应该已经运行（如本章前面所示，手动启动该守护进程）。

要启动 `system-config-printer`，请转到“系统”、“管理”，然后选择“打印”菜单选项。

### 创建打印队列

Ubuntu 的 `system-config-printer` 工具将引导您完成创建新打印机的过程。要开始配置本地（已连接）打印机，请在 `system-config-printer` 的主窗口中单击“新建打印机”工具栏按钮。将出现“添加新打印机”配置对话框，如图 8.1 所示。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_205_0.png)

**图 8.1** 单击“新建打印机”工具栏按钮，开始为您的系统配置新打印机。

将出现“打印机名称”对话框。为新打印机输入所需的名称（例如 `lp`），输入简短描述和可选的定位信息，然后单击“前进”按钮。将出现“连接类型”对话框，如图 8.2 所示。选择适合您的连接类型。根据您的具体需求，您可以选择多种不同的连接类型。如果打印机通过标准并行（或以前称为 Centronics）电缆连接，通常使用 LPT#1 选项。或者，如果您要连接到具有 JetDirect 端口的打印机（大多数 HP 网络打印机都属于此类别），请选择相应的选项并输入打印机的网络地址。

接下来，您需要选择所配置打印机的品牌/制造商，如图 8.3 所示。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_206_0.png)

图 8.2 为您的打印机选择适当的连接方法并输入相关详细信息。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_206_1.png)

图 8.3 从此对话框中选择打印机的品牌或制造商，以帮助 Ubuntu 缩小驱动程序选项的范围。

请注意，即使打印机未连接到您的计算机，也可以为 Ubuntu 配置打印机。选择打印机制造商后，将出现该制造商的打印机列表（例如 HP，如图 8.4 所示）。从列表中选择您的打印机，然后单击“前进”按钮。

图 8.5 为打印机起一个有意义的名称，如果需要，还可以添加描述和位置。

图 8.6 在 `system-config-printer` 的主窗口中显示在 `/etc/printcap` 中创建的新打印机条目。

### 编辑打印机设置

您还可以使用 `system-config-printer` 工具来编辑新定义的打印机。要编辑打印机设置，请在打印机浏览窗口中突出显示打印机的列表项。然后，您可以使用对话框右侧出现的选项卡，选择与该打印机相关的特定设置。“设置”对话框如图 8.7 所示。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_209_0.png)

## 图 8.7 通过 `system-config-printer` 中的选项卡编辑打印机设置。

此对话框中的第一个选项卡允许您为打印机指定新名称。在此示例中，打印机名称为 `laserjet`。对话框中的其他选项卡允许您更改队列类型或队列选项（例如是否打印标题页或设置页面的图像区域）、选择或更新驱动程序，或选择打印机可用的打印选项（如图 8.8 所示）。

完成打印机编辑后，单击“应用”按钮保存更改并自动重启 `cupsd` 守护进程。这一步极其重要；您必须更新打印机设置并重启 `cupsd` 守护进程，以强制其重新读取您的新设置。完成后，从“文件”菜单中选择“退出”。
