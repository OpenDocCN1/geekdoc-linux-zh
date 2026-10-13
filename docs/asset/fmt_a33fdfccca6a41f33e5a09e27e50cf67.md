
![](img/7925b180044e741c5a0343b922cd9e81_593_0.png)

- 3. 点击电源管理器工具中的“自定义”（Customized）按钮，将出现一个下拉菜单，如图 15.4 所示。

# 图 15.4

电源管理下拉菜单。

![](img/7925b180044e741c5a0343b922cd9e81_593_1.png)

- 4. 点击“禁用”（Disabled）选项以禁用电源管理。完成后，点击 `OK` 按钮退出。

禁用电源管理的另一种方法是从命令行进行的，如下所示：

按照如下方式永久禁用来自 `/etc/rc2.d` 目录的启动脚本：

```
mv /etc/rc2.d/s85power /etc/rc2.d/s85power
```

禁用电源管理的第三种方法是更改 `/etc/power.conf` 文件，将 `Behavior`（行为）字段从 `shutdown` 改为 `noshutdown`。以下是配置了电源管理的系统上的 `/etc/power.conf` 所示：

```
# /etc/power.conf
# Copyright (c) 1996-1999 by Sun Microsystems, Inc.
# All rights reserved.
#pragma ident "@(power.conf 1.14 99/10/18 SMI"
# Power Management Configuration File
# NOTE: 下方的条目仅在没有运行窗口 \
# 环境时使用。当运行窗口环境时，监控 \
# 管理由窗口系统控制。
# Statefile Path
statefile /usr/CPR
# Auto-Shutdown Idle(min) Start/Finish(hh:mm) Behavior \
autoshutdown 60 17:00 7:00
device-dependency /dev/fb /dev/kbd removable-media /dev/fb \
autotom disable
```

在之前的示例中，电源管理被配置为：在下午 5:00 到上午 7:00 之间的任何时间空闲 60 分钟时自动关闭系统。

要禁用自动关机，请按如下方式更改 `/etc/power.conf` 文件中的以下行：

```
# Auto-Shutdown Idle(min) Start/Finish(hh:mm) Behavior \
autoshutdown 60 17:00 7:00 noshutdown
```

`shutdown` 已更改为 `noshutdown`。

# 560 第二部分章节

## 章节总结

### 关键术语

- 客户端-服务器（了解本章描述的每种类型的服务器和客户端）
- 迭代安装
- Web Start
- 初始安装
- 升级
- 电源管理

本章描述了 Solaris 环境中提供的各种类型的服务器。在设置服务器时，系统管理员必须识别要安装的服务器类型。所有将提供的服务器都必须提前确定，以便操作系统能够正确设置以提供这些服务。再次，每种服务器都是不同的，因此需求会因地而异。

本章讨论了在安装 Solaris 8 之前系统必须满足的所有前提。此外，它还讨论了在安装之前必须收集的信息列表。

最后，我描述了如何使用交互式安装程序在服务器上安装 Solaris 8 环境。交互式安装程序提供了一个对话框，允许系统管理员选择软件软件包并在新服务器上创建文件系统。另一种使用 Web Start 安装操作系统的方法将在稍后的附录 A 中介绍。

在安装操作系统后，还会进行许多额外任务，例如设置 NIS 和网络环境。这些主题将在第 13 章“Solaris 网络环境”和第 17 章“NFS 环境”中涵盖。此外，在完成服务器设置后，不要忘记备份你的分区（参见第 11 章“备份与恢复”）。

下一章将描述设备配置和命名规范。现在由于你已经安装了操作系统，

# 第 15 章 安装服务器 561

### 应用知识

### 15.1 使用交互式程序安装 Solaris8

对于此练习，你将使用交互式程序安装操作系统。

**预计时间：** 1–2 小时，取决于你系统的速度。

1. 禁用电源管理的最简单方法是使用电源管理工具 `dtpower`。`Dpower` 是通用桌面环境（Common Desktop Environment）中的可用 GUI 工具。点击前面板弹出菜单中的桌面控制图标进入电源管理器，如图 15.1 所示。

2. 在应用程序管理器（Application Manager）窗口中，点击电源管理器图标，如图 15.2 所示。

3. 电源管理器工具将出现，如图 15.3 所示。

4. 点击电源管理器工具中的“自定义”（Customized）按钮，将出现一个下拉菜单，如图 15.4 所示。

5. 点击“禁用”（Disabled）选项以禁用电源管理。完成后，点击 `OK` 按钮退出。

禁用电源管理的另一种方法是从命令行进行的，如下所示：

按照如下方式永久禁用来自 `/etc/rc2.d` 目录的启动脚本：

6. 下列哪个是服务器？

### 复习题

1. 下列哪项是为网络上的其他设备提供服务的系统？

A. Server

B. Client

C. File Server

D. AutoClient

2. 下列哪项是使用网络上提供的服务、磁盘容量有限或可能没有磁盘；必须依赖远程文件系统才能工作？

A. AutoClient

B. File Server

C. Client

D. shutdown

3. 哪种安装类型保留数据？

A. Initial

B. Upgrade

C. Preserve

D. Web Start

4. 安装的三个阶段是？

A. 系统配置, 安装, 安装后

B. 从 CD, 系统配置, 安装后

C. 从 CD, 开始安装, 安装后

D.

5. 下列哪项是配置集群？

A. Developer System Support

B. User System Support

C. Core System Support

D. Enterprise Distribution

6. 下列哪项是 Sun 的 Java 安装程序？

A. WebFS

B. JumpStart

C. Interactive Installation

D. Web Start

7. 在交互式安装程序中，哪些文件系统会自动设置？

A. /swap, /usr, /opt, /var

B. /swap, /usr

C. /swap, /usr, /opt

D. /swap, /usr, /opt, /var, /export/home

8. 下列哪项被称为零管理客户端？

A. The dataceless client

B. The JavaStation

C. The diskless client

D. The auto client

9. 安装期间的默认软件配置是什么？

A. End user distribution

B. Core distribution

C. Developer distribution

D. Entire distribution

10. ultra 的内核架构是？

A. sun4m

B. sun4c

C. sun4u

D. sun4s

11. 安装服务器系统时不需要哪些哪项信息？

A. The server’s Ethernet address

B. The server’s hostname

C. The server’s IP address

D. The server’s geographic region

### 复习题答案

1. A

2. C

3. B

4. A

5. D

6. C

7. D

8. C

9. B

10. C

11. D

### 应用你的知识

- 6. `Web Start` 是 Sun 的基于 Java 的安装程序。
- 7. 在交互式软件安装程序中，默认会设置好 `/swap` 和 `/usr` 文件系统。
- 8. `JavaStation` 也称为零管理客户端。该客户端没有本地文件系统，其 `/home` 是通过跨网络服务器进行访问的。
- 9. 在交互式安装期间，默认选择“终端用户系统支持”（End User System Support）集群。
- 10. `sun4u` 是所有 Ultra 系统的内核架构。
- 11. 安装服务器系统时不需要服务器的以太网地址。在安装过程中，系统将提示你输入 IP 地址、主机名和地理位置区域。

### 目标

本章涵盖了以下测试目标：

## 理解设备和驱动程序的命名规范

- Solaris 操作系统通过设备路径名访问设备（如磁盘和驱动器）。系统管理员必须熟悉指向连接到系统的每种硬件的各种路径名。

## 显示设备和驱动程序配置信息

- Solaris 提供了几种显示设备驱动信息的方法。将描述这些命令和技术，以帮助你识别哪些设备指向哪些外设设备，以及哪些驱动程序加载在内核中。

## 配置新设备

- 系统管理员负责在系统上添加和配置新硬件。本章描述了如何将新设备配置到 Solaris 运行环境中。
