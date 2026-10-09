
# Red Hat Linux 9 基础

从上方的图中我们可以看到，该列表中唯一的以太网控制器是瑞昱（Realtek）8139/8139C/8139C+ 型号。请注意，该输出还确认了系统中的其他设备——如声卡、电视调谐器和视频卡。当我们在本章后续部分涉及这些设备时，会利用这些信息。

我们可以通过检查为该设备加载的网络驱动程序来确认这个以太网控制器是否被配置为 `eth0` 设备。为此，请查看文件 `/etc/modules.conf` 的内容。此文件指定了要为各种设备加载的驱动程序及其相应的加载参数：

![](img/b852150740856958b10aff9e8c9d2adc_86_0.png)
![](img/b852150740856958b10aff9e8c9d2adc_86_1.png)

在上方图中文件内容的第二行，我们找到了一条为 `eth0` 设备加载 `8139too` 驱动程序的指令。这证实了 `eth0` 网络设备实际上是一块瑞昱网卡。顺便一提，该文件的第三行揭示了该机器上的声卡属于 VIA82xxx 系列音频控制器。

使用 `netstat` 和 `route` 程序可以了解网络的详细信息。`route` 程序显示系统中激活的路由，包括该桌面用于从互联网发送和接收网络流量的网关。`netstat` 程序显示当前活动的网络连接以及机器上可用的网络服务。我们将在第 12 章中了解 `netstat`，你可以通过在终端输入 `man route` 来了解更多关于 `route` 的信息。

Red Hat Linux 用于配置鼠标的工具是程序 `redhat-config-mouse` – 你可以通过命令行运行它，或者通过选择 主菜单 | 系统设置 | 鼠标。你之前可能已经接触过这个程序，因为它在安装过程中被运行过。以下是该对话框的回顾：

![](img/b852150740856958b10aff9e8c9d2adc_87_0.png)

对话框显示了系统中的当前鼠标配置。在上方的截图中，鼠标是一个基于 PS/2 的滚轮鼠标。该程序将鼠标配置存储在 `/etc/sysconfig/mouse` 中，它在系统启动时加载鼠标驱动程序（称为 gpm）时使用该配置。

对于配置键盘布局，要使用的图形用户界面工具是 `redhat-config-keyboard` 程序。运行此程序会弹出以下对话框，显示你当前的键盘布局：

![](img/b852150740856958b10aff9e8c9d2adc_87_1.png)

你也可以从此对话框中更改键盘布局。该程序将键盘配置存储在文件 `/etc/sysconfig/keyboard` 中。你在这里选择的选项将确保在启动时加载适当的键盘映射。

# 关于显示器的信息

可以使用 `lspci` 命令（我们之前提到过）查找系统中显卡的信息。这通常揭示了系统中实际的视频硬件。在 `lspci` 输出（我们之前也看到过）中，视频硬件被揭示为 S3 ProSavage 显卡。

X 服务器软件负责桌面的基本图形显示。该服务器根据视频硬件加载适当的显示驱动程序。对于像 S3 这样被识别的优质显卡，有硬件加速驱动程序；而未识别的显卡则通过加载性能较低的通用显示驱动程序来使用。因此，如果你看到显示出现卡顿，可能是因为你的显卡被错误检测，并且加载了如 Vesa 这样的通用显示驱动程序。

要检查或修改显示器的显卡和监视器设置，你可以使用 Red Hat 配置工具 `redhat-config-xfree86`（通过在命令行输入该命令，或者通过选择 **主菜单 | 系统设置 | 显示**）。以下是执行该工具时得到的对话框：

![](img/b852150740856958b10aff9e8c9d2adc_88_0.png)

这些对话框表明显卡已被正确检测，分辨率和色深符合预期。如果你愿意，可以更改这些值。更改仅在 X 服务器重启后生效。

然而，它们还表明监视器似乎未被正确检测。监视器的型号名称被设置为通用的 **Monitor Model**（监视器型号），这表明安装期间提供的手动配置详情已生效。如果你对在显示使用这些设置生成的显示效果感到满意，那么你只需点击 **OK**（确定）并退出程序。如果你想调整设置以尝试获得更好的效果，请点击 **Configure**（配置）按钮来选择监视器和显卡的精确配置（正如你在安装期间配置 X 服务器所做的那样）。

### 关于声卡的信息

声卡配置工具是 `redhat-config-soundcard`（同样，你可以从命令行运行，或者从菜单快捷方式 **主菜单 | 系统设置 | 声卡检测** 中运行）。该程序显示一个简单的对话框，其中显示检测到的声卡和加载的内核声音驱动程序：

![](img/b852150740856958b10aff9e8c9d2adc_89_0.png)

你可以使用 **Play test sound**（播放测试声音）按钮来测试声音配置。

### 关于各种 PCI 和 USB 设备的信息

可以使用 `lspci` 和 `lsusb` 程序查看其他各种 PCI 和 USB 设备的信息。我们在前面的章节中查看过 `lspci` 程序的输出。作为回顾，以下是我们之前看到的输出：

```
[sandip@localhost sandip]$ /sbin/lspci
00:00.0 Host bridge: VIA Technologies, Inc. VT8363/8365 (KT133/KM133) (rev 81)
00:01.0 PCI bridge: VIA Technologies, Inc. VT8363/8365 (KT133/KM133 AGP)
00:07.0 ISA bridge: VIA Technologies, Inc. VT82C686 (Apollo Super South) (rev 40)
00:07.1 IDE interface: VIA Technologies, Inc. VT82C586B PIPC Bus Master IDE (rev 06)
00:07.2 USB Controller: VIA Technologies, Inc. USB (rev 16)
00:07.3 USB Controller: VIA Technologies, Inc. USB (rev 16)
00:07.4 Bridge: VIA Technologies, Inc. VT82C686 (Apollo Super ACPI) (rev 40)
00:07.5 Multimedia audio controller: VIA Technologies, Inc. VT82C686 AC97 Audio Controller (rev 50)
00:0e.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8139/8139C/8139C+ (rev 10)
00:0f.0 Multimedia video controller: Brooktree Corporation Bt878 Video Capture (rev 11)
00:0f.1 Multimedia controller: Brooktree Corporation Bt878 Audio Capture (rev 11)
01:00.0 VGA compatible controller: S3 Inc. ProSavage KM133
[sandip@localhost sandip]$
```

该输出允许我们确认机器中基于 PCI 的硬件。例如，我们可以找到音频控制器卡（`VT82C686`）、以太网网络控制器卡（`RTL-8139`）、视频采集卡（`Bt878`）和图形卡（`S3 ProSavage`）。当硬件自动检测未按计划完成时，这些细节非常有用，你需要明确告诉配置程序你想配置的硬件。

`lsusb` 程序的输出列出了插入计算机的所有 USB 设备的特性。其输出非常详细，对于普通用户来说可能过于技术性。但是，当你热插拔 USB 设备时，可以从 `lsusb` 输出中验证设备特性。

# 配置桌面

工作区和面板都是桌面环境的一部分。你迄今为止使用的默认桌面环境是 GNOME 桌面环境。此环境控制面板和应用 GUI 窗口的行为、会话管理以及其它各种行为 GUI 功能。在 Red Hat Linux 9 中，默认 GNOME 桌面具有一个新外观，称为 Bluecurve 主题。

此主题涵盖了菜单、面板、桌面背景和窗口装饰中的所有颜色设计。当然，这不是桌面上唯一可用的主题，但无疑是 Red Hat 设计团队投入精力最多的主题。结果是一个外观和感觉远优于其前代产品且更具美感的桌面。

## 使用桌面控制中心

你可以使用 GNOME 桌面控制中心控制桌面的许多功能。控制中心程序显示了若干用于配置桌面的选项（如果你熟悉 Windows 操作系统，你会发现控制中心与 Windows 的控制面板非常相似）。

你可以通过选择 主菜单 | 首选项 | 控制中心 来访问控制中心：

![](img/b852150740856958b10aff9e8c9d2adc_90_0.png)
