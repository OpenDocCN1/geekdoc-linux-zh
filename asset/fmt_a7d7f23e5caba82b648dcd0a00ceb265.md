
在本章中，你学习了安装要求和方法。你学习了如何在文本模式下使用本地 CD/DVD 介质安装。你还了解文本模式和图形模式安装的区别。你执行了一些安装后步骤来进一步配置和修改系统设置。你查看了安装日志文件并查看了部分内容。最后，你介绍了安装期间虚拟控制台的基本信息。

# X Window 系统和桌面

本章涵盖以下主要主题：

- X Window 系统概述
- X 服务器以及如何配置它
- X 配置文件
- 管理 X 字体服务器启动和停止
- X 客户端应用程序和图形桌面
- 配置默认桌面
- 通过网络运行 X 客户端

取决于 RHEL 系统的用途，你可能需要安装并配置 X Window 软件。X Window（或简称 X）为运行图形应用程序提供了基础。在书中，你将使用需要图形环境操作的 RHEL 管理工具。此外，RHEL 提供了需要 X 功能才能运行的图形界面和桌面 GNOME 和 KDE。所有和其他图形应用程序都取决于系统中正确加载和配置的 X 软件。虽然并不是所有的 RHEL 系统都需要 X，但以备万一是种好主意。软件包占用的磁盘空间并不大。

## 概述

RHEL 使用 X.Org Foundation 提供的 X 系统，该开源组织专注于管理 X 及其周围的技术。X 基于客户端/服务器架构，软件守护进程在系统中运行并为本地或网络系统的图形请求提供服务。这意味着客户端和服务器可以运行在同一个系统或不同的系统中。X 服务器管理图形、视频硬件以及运行所需的 X 客户端。你只需要指向想要显示图形的计算机。单个 X 服务器守护进程可以处理系统允许的所有 X 应用程序。所有 Red Hat 配置工具都是 X 服务器的 X 客户端。

## X 服务器

X 服务器和图形桌面的配置是在 RHEL 安装期间完成的。硬件会被检测并自动配置以获得最佳性能和结果。为了让 X 服务器高效运行，请确保系统有足够的内存和支持的视频硬件（如显卡、显示器和鼠标）。默认情况下，X.Org 支持多个供应商的显卡、显示器和其他视频设备。访问 www.xorg 或咨询 Red Hat 的硬件兼容性文档获取详细信息。如果你打算使用的设备不在硬件兼容列表中，请使用内置的通用驱动程序（如显卡的通用 VGA 等）。

## 配置 X 服务器

在验证硬件后，执行以下命令或 Red Hat 显示配置器（又称 X 配置器）来修改显示和显卡设置：

```
# system-config-display --noui --reconfig --set-resolution=800x600 --set-depth=16
```

如果无法为找到硬件找到适当的驱动程序，将列出内置的支持显卡列表。图 10-1 显示显示配置器（Display Configurator）的主界面。

![](img/3f35ec29a294974bc1a4fdae3ae46652_204_0.png)

图 10-1 显示配置器 – 显示设置

该工具中有三个可用标签页，允许您配置视频硬件。设置（Settings）标签页允许您设置显示器分辨率和色彩深度。硬件（Hardware）标签页允许您配置显示器类型（Monitor Type）和显卡（Video Card）。当前显示器设置为“自动配置（autoconfigured）”，显卡设置为“VMWare SVGA PCI Display Adapter”。这些设置是在安装期间自动检测并设置的。如果您需要修改它们，请点击相应的配置（Configure）按钮并选择合适的硬件。对于不支持的硬件，请选择类似的显卡或使用通用显卡（如 VESA 驱动，相应修改 `/etc/X11.xorg.conf` 文件）、使用任何兼容的 VGA 或 SVG 显，或前往 www.x.org 下载最新驱动程序。

![](img/3f35ec29a294974bc1a4fdae3ae46652_204_1.png)

图 10-2 显示配置器 – 硬件设置

如果系统连接了双显示器，您可以在双头（Dual Head）标签页下配置第二个显示器。基本上，它要求您选择第二个显示器类型、其连接的显卡、显示器分辨率、色彩深度以及桌面布局——独立（individual）或跨越（spanning）。参见图 10-3。

![](img/3f35ec29a294974bc1a4fdae3ae46652_205_0.png)

图 10-3 显示配置器 – 双头设置

X Window 系统与桌面管理器

165

## X Server

使用显示配置器进行的修改将保存存在 `/etc/X11/xorg.conf` 中，这是 X Server 的主要配置文件。默认内容看起来如下：

```
# cat /etc/X11/xorg.conf
# Xorg configuration created by pyxf86config
```

```
Section "ServerLayout"
    Identifier "Default Layout"
    Screen 0 "Screen0" 0 0
    InputDevice "Keyboard0" "CoreKeyboard"
EndSection

Section "InputDevice"
    Identifier "Keyboard0"
    Driver "kbd"
    Option "XkbModel" "pc105"
    Option "XkbLayout" "us"
EndSection

Section "Device"
    Identifier "Videocard0"
    Driver "vmware"
EndSection

Section "Screen"
    Identifier "Screen0"
    Device "Videocard0"
    # DefaultDepth 24
    SubSection "Display"
    Viewport 0 0
    Depth 24
    EndSubSection
EndSection
```

第一行表示该文件是在安装期间创建的，之后未进行更新。如果您使用显示配置器修改配置，该行将显示“Xorg configuration created by system-config-display”。默认情况下，文件中包含四个部分，它们被包含在 `Section` 和 `EndSection` 关键字之间。这些部分的解释如下：

- `ServerLayout` 部分以一个标识符开头，其设置为 `Default Layout` 并指向正在使用的屏幕和输入设备。如果您连接并配置了两个显示器，标识符将更改为“dual head configuration”。
- `InputDevice` 部分定义了输入设备（即键盘）的配置。它列出了键盘的类型和按键数量（105）。它还告诉您键盘使用的驱动程序（`kbd`）。
- `Device` 部分显示了 RHEL 安装时检测到的显卡以及用于该显卡的驱动程序。
- `Screen` 部分使用了之前部分定义的标识符和设备。它还定义了显示特性。

## 探测硬件并重建 X Server 配置文件

除了运行显示配置器来更新 `/etc/X11/xorg.conf` 中的视频硬件配置外，您可以在运行级别 3 下使用 `X` 命令来探测图形硬件并构建新的 `xorg.conf` 文件。然后您可以测试配置并用它替换原始的 `xorg.conf` 文件。请按照以下步骤操作：

> 默认情况下，RHEL 系统启动到运行级别 5，所有包括 X 在内的图形化程序都会启动。运行级别 3 不自动运行 X。关于运行级别的详细讨论见第 15 章“关机与启动”。

1. 执行以下命令切换到运行级别 3。这将自动停止所有正在运行的图形化程序以及 X。

```bash
# init 3
```

一旦进入此运行级别，运行 `X` 命令来探测图形硬件：

```
# X -probeonly
X Window System System Version 7.1.1
Release Date: 12 May 2006
X Protocol Version 11, Revision 0, Release 7.1.1
Building System: Linux 2.6.9-67.0.EL5m x86_64 Red Hat, Inc.
Current Operating System: Linux caat0j0p1 2.6.18-92.el5 #1 SMP Tue Apr 29 13:16:15 EDT 2008 x86_64
```

X Window 系统与桌面管理器

167

Build Date: 02 April 2008

Build ID: xorg-x11-server 1.1

在报告问题之前，检查 http://wiki.x.org 以确保您拥有最新版本。

Module Loader

Markers: (--) probed, (**) from config, (=) default.

(++) command line, (II) notice, (WW) warning, (EE) error, (NI) not implemented, (??) unknown.
