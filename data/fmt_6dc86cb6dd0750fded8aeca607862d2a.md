
```
# gs
GNU Ghostscript 7.05 (2002-04-22)
Copyright (C) 2002 Artifex LLC, Benicia, CA.  All rights reserved.
This software comes with NO WARRANTY; see the file PUBLIC for details.
[/decl250 /mgr8 /lj4dithp /cdj890 /dfaxlow
 /bjccmyk /bmpmono /iwlq /applepm /bmp16m /hpdj690c\
 /tiff24 /hpdj500 /psgr /tmpr /pksm /ep15800 /pcx2up\
 /deskjet /mgrgray2 /lj5gray /cdj970 /epswrite /lex3200\
 /bjcolor /bmpsep1 /jetp3852 /atx23 /bmp256 /hpdj850c /tiffpack /hpdj500c /pswrite
 /fs600\
 /pksmraw /ep15900 /pcxmyk /dj505j /mgrgray4 /lj5mono\
...]
```

并非所有设备都在此示例中列出。

> **Aladdin 还是 GNU？**
>
> Linux 上至少有两种 Ghostscript 版本可用。一个版本名为 AFPL Ghostscript，以前称为 Aladdin Ghostscript。该版本根据 Aladdin Free Public License 许可，该许可不允许商业分发。另一个版本称为 GNU Ghostscript，根据 GNU 通用公共许可证分发。有关不同版本详细信息或有关许可问题的答案，请参阅 Ghostscript 主页 http://www.cs.wisc.edu/~ghost/。

## 创建和配置本地打印机

为您的 Ubuntu 系统创建本地打印机可以通过六个简单步骤完成。在开始之前，`cupsd` 守护进程应正在运行（手动启动守护进程，如本章前面所示）。

要启动 `gnome-cups-manager`，请从 GNOME 或 KDE 桌面面板的系统设置菜单中选择打印菜单项，或从 X 终端窗口使用命令行，如下所示：

```
$ gksudo gnome-cups-manager &
```

## 创建打印队列

Ubuntu 的 `gnome-cups-manager` 工具会引导你完成创建新打印队列的过程，这实际上是在你的系统上定义一台新打印机。要开始配置本地（连接）打印机，请在 `gnome-cups-manager` 主窗口中双击添加打印机图标。会出现一个添加打印机对话框，如图 12.1 所示。

![](img/e464b828c497c99e41f61d4c55f1c0db_278_0.png)

**图 12.1**   双击添加打印机图标以开始为系统配置新打印机；当向导对话框出现时，选择打印机的连接方式。

第一步是告诉 Ubuntu 打印机如何连接到你的机器。你可以选择安装本地连接的打印机（即物理连接到计算机的打印机）或网络打印机。如果选择本地连接，你可以定义连接或仅使用 Ubuntu 的自动检测功能尝试检测正确的端口。图 12.2 显示 Ubuntu 已检测到通过 USB 接口连接的 Deskjet 5550 打印机。

单击前进后，你将被要求确认打印机的品牌和型号并选择要使用的打印机驱动程序（见图 12.3）。通常保留 Ubuntu 为你提供的推荐打印机驱动程序是安全的。如果这就是你遇到奇怪输出问题的原因，请将打印机驱动程序更改为其他选项之一，看看是否有帮助。

图 12.2 尝试使用 Ubuntu 的自动检测功能查找打印机。在选择连接和/或找到打印机后单击前进。

图 12.3 使用此屏幕指定制造商和打印机型号，并为 Ubuntu 选择驱动程序。

从列表中选择打印机，然后单击前进按钮（见图 12.4）。

![](img/e464b828c497c99e41f61d4c55f1c0db_281_0.png)

图 12.5 在 `/etc/printcap` 中创建的新打印机条目会显示在 `gnome-cups-manager` 的主窗口中。

![](img/e464b828c497c99e41f61d4c55f1c0db_281_1.png)

图 12.6 使用 `gnome-cups-manager` 的编辑打印队列对话框中的选项卡编辑打印机的设置。

此对话框中的第一个选项卡可让你更改打印机的描述和位置。在此示例中，打印机的描述为 HP DeskJet 5550。 此对话框中的其他选项卡可让你更改纸张类型和方向、选择或更新驱动程序，以及为打印机选择可用的驱动程序选项（见图 12.7）。

完成编辑打印机设置后，可以单击打印测试页按钮检查设置，或如果确信一切正常，则单击关闭按钮。

![](img/e464b828c497c99e41f61d4c55f1c0db_282_0.png)

图 12.7 可以在 `gnome-cups-manager` 的编辑打印队列对话框的驱动程序选项选项卡中更改打印机的驱动程序设置。

## 相关 Ubuntu 和 Linux 命令

以下命令可帮助你管理打印服务：

- `accept`—通过命令行控制打印作业对 CUPS 服务器的访问
- `cancel`—从命令行取消打印作业
- `cancel`—打印队列的命令行控制
- `disable`—通过命令行控制打印
- `enable`—命令行控制 CUPS 打印机
- `lp`—打印机和打印服务的命令行控制
- `lpc`—在控制台显示打印机和打印服务的状态
- `lpq`—在控制台查看打印队列（待处理打印作业）
- `lprm`—通过命令行从打印队列中删除打印作业
- `lpstat`—显示打印机和服务器状态
- `gnome-cups-manager`—Ubuntu 的 GUI 打印机配置工具

## 参考

http://www.linuxprinting.org/—在此浏览特定驱动程序以及有关 USB 和其他类型打印机的信息。

http://www.hp.com/wwsolutions/linux/products/printing_imaging/index.html—来自 HP 的关于 Linux 下打印产品支持的简短但权威的信息。

http://www.linuxdoc.org/HOWTO/Printing-HOWTO/—Grant Taylor 的 Printing HOWTO，其中包含有关在 Linux 下使用各种打印服务的信息。

http://www.cups.org/—CUPS 软件的综合仓库。

http://www.pwg.org/ipp/—Internet Printing Protocol 标准的

http://www.cups.org/—CUPS 软件的综合仓库。

http://www.pwg.org/ipp/—Internet Printing Protocol 标准的主页。

http://www.linuxprinting.org/cups-doc.html—关于 CUPS 的信息。

http://www.cs.wisc.edu/~ghost/—Ghostscript 解释器的主页。

## CHAPTER 13

## Games

要让任何操作系统具有大众市场吸引力，它必须拥有大量兼容的游戏。说实话，没有人只想用电脑进行文字处理或数据库——他们希望能够将其作为放松甚至娱乐的来源！在本章中，我们将探讨 Linux 游戏的现状，并告诉你如何在 Linux 环境中运行当前的一些大作。我们甚至会向你展示如何在 Linux 下运行基于 Windows 的游戏。

## Linux Gaming

Ubuntu 发行版自带了一些游戏，它们分为三个不同的阵营：KDE 游戏、GNOME 游戏和 X 游戏。我们最喜欢的是 Planet Penguin Racer 和 Torc（见图 13.1），但你也可以从中选择其他几款。当然最好的部分是尝试每一款并看看你自己的想法。网络上还有许多其他免费游戏可用，所以去 Google 搜索一下，看看你能找到什么。

然而，Linux 的游戏并不止于此——一些流行的基于 Windows 的游戏版本正在移植到 Linux 平台，包括 DOOM 3、Unreal Tournament 2004 和 Quake 4。这三款流行游戏都具有原生的 Linux 支持，在某些情况下，其运行速度甚至与 Windows 版本相似或更好。甚至还有一个模拟器可供使用，让你能够在 Linux 下原生地玩经典冒险游戏。

最后，有一个名为 Cedega 的 Wine 代码实现，专门针对游戏进行了优化。它使用应用程序接口使 Windows 游戏相信它们运行在 Windows 平台上而不是 Linux 平台。请记住 Wine 的含义是 wine is not an emulator，所以不要把它当作模拟器来想——社区对此会非常敏感！

### IN THIS CHAPTER

- Linux Gaming
- Reference

![](img/e464b828c497c99e41f61d4c55f1c0db_285_0.png)
