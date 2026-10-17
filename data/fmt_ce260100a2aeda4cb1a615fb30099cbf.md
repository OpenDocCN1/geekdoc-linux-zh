
或者，你可以使用后续章节中描述的会话管理工具。GNOME 和 KDE 都包含了它们自己的工具，用户可以运行这些工具来定制他们自己的桌面环境。

我们建议使用 `.xinitrc` 或这些 GUI 工具之一，而不要两者兼用。否则，这些工具的效果将是累积的，配置控制可能会变得困难。

# GNOME 自定义

在 GNOME 中，你可以使用我们之前描述的各种控制中心小组件来定制桌面的外观。该领域重要的小组件包括背景、菜单与工具栏、屏幕保护和主题。

GNOME 会话（GNOME Sessions）允许用户自定义自己的桌面环境。它非常易用。你可以从主菜单开始：点击“主菜单 > 偏好 > 更多偏好 > 会话”。

会话允许你配置进入 GNOME 桌面时启动的程序。它还允许你配置 GNOME 启动时监控当前加载程序的行为。如表 30.7 所示，该窗口包含三个选项卡，描述在表 30.5 中。

# 图 30.7：GNOME 会话

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_898_0.png)

# 表 30.5：GNOME 会话

| 选项卡 | 描述 |
|---|---|
| 会话选项 | 管理 GNOME 登录和注销期间的行为 |
| 当前会话 | 列出 GNOME 中当前运行的程序 |
| 启动程序 | 记录 GNOME 启动时启动的程序 |

“启动程序”选项卡是关键。你可以添加选择的程序，如图 30.7 所示。点击“添加”，输入你选择的文本命令。与你的账户相关的 PATH；例如，如果你想在启动 GNOME 桌面时启动 GNOME 终端会话，你不需要输入 `gnome-terminal` 命令的完整路径。

# KDE 自定义

在 KDE 中，你可以通过 KDE 控制中心的“外观与主题”和“桌面”菜单来定制桌面。你可以在这些菜单下配置桌面壁纸、屏幕保护等。

KDE 默认保留你打开的程序和应用程序。如果你在关闭 KDE 桌面环境之前没有关闭这些程序，下次启动 KDE 会打开这些程序。你可以使用控制中心、KDE 组件菜单或会话管理器修改各种设置。

# 学习常用的 GNOME 和 KDE 扩展

GNOME 和 KDE 都带有扩展，可以通过菜单按钮访问。它们分为几类：辅助、互联网、偏好、多媒体和系统工具。虽然大多数是基于 GNOME 和 KDE 项目的工作，但本章也包含了一些第三方实用。

如果你在 GNOME 或 KDE 桌面环境中没有看到特定的应用程序或扩展，可能是你没有安装该包。由于这不是 Linux 桌面的全面指南，我们没有包含所有安装在 Red Enterprise Linux 3 工作站上的工具。

在某些情况下，特定的应用程序需要更新。某些即时通讯工具已经升级，某些浏览器在没有最新 Java 的情况下可能无法工作。如果从 Red Hat 获取更新，你可能从应用程序开发者那里下载更新。

# 辅助

GNOME 了一些帮助你完成简单计算任务的辅助工具。可以通过主菜单 ► 辅助子菜单访问。GNOME 和 KDE 桌面在这个子菜单之间略有差异。要对这些扩展进行简要概述，请参见表 30.6。GNOME 和 KDE 将其中的某些扩展位于主辅助子菜单或更多辅助子菜单。在许多情况下，GNOME 和 KDE 版本的每个工具略有不同（或更多）。

| 表 30.6：辅助菜单 |
| 选项 | 描述 |
| 计算器 | 启动一个连接到标准键盘数字区的科学计算器。 |
| 字符映射 | 打开一个与罗马字母相关的字符的界面 |

### 表 30.6：附件菜单（继续）

| 选项 | 描述 |
| --- | --- |
| Dictionary | 连接到 dict.org 的在线字典服务器。 |
| File Roller | 为 tar.gz 压缩包提供一个类似于 Windows Zip 实用程序的前端。 |
| Handheld PDA | 打开 Pilot Link 工具。 |
| Print Manager | 启动 GNOME 打印管理器。 |
| Text Editor | 打开一个图形界面文本编辑器。 |
| Address Manager | 启动联系人信息管理器。 |
| KAlarm | 转到基于 KDE 的事件报警工具。 |
| Kandy | 支持通讯录与手机之间的同步。 |
| KArm | 帮助你跟踪在不同任务上花费的时间。 |
| Kdeprint | 允许你查看打印到传真机的文件。 |
| KXEdit | KHexEdit 工具是一个自定义的十六进制编辑器，可以以十六进制、八进制和二进制模式显示并帮助你编辑数据。（这对应于数学专业的 16 、8 和 2 进制）。它还可以以文本模式显示文件。 |
| KJots | Kjots 允许你以组织的方式记录短记。你创建的任何“书”都可以添加到热点中。 |
| KNotes | KNotes 工具允许你向列表中添加一些短记，你可以对其进行打印或发送电子邮件。 |
| K | The Organizer 使用最新版本的 Desktop HotSync 软件；旨在作为 Palm 桌面软件的替代品。 |
| KTimer | KTimer 允许你在指定的延迟后启动命令；默认为 100 秒。 |

## 文档

如果你从 Red Hat Enterprise Linux 文档光盘中安装了软件包，将看到一个“文档”菜单，它支持在默认 Web 浏览器中轻松访问这些文档。这只是为了你的方便；Red Hat Enterprise Linux 手册的 PDF 版本可以在文档光盘上找到。

## 游戏

如果你在系统上安装了任何标准的 GNOME 或 KDE 软件包，你可以通过主菜单 ➤ 游戏来访问它们。我们不涵盖任何 Linux 游戏的启动或操作。另一方面，有些人认为游戏可以为 Microsoft Windows 用户在过渡到 Linux 的期间感到更加舒适。

## 互联网实用工具

GNOME 包含了许多实用工具和一个用于在互联网上通信的应用程序。在这种情况下，实用工具和应用程序之间的区别有些随意；我们将查看互联网应用程序中的 Mozilla 浏览器、Ximian Evolution 个人信息管理器以及 Gaim 即时消息（IM）实用工具。

在这一节中，我们将查看更多基础的程序，包括即时消息软件、程序和其他杂杂连接工具。这些程序可以通过主菜单 > 互联网 > 互联网应用程序访问。有关这些程序的简要描述，请参见表 30.7。其中一些与 GNOME 关联，另一些与 KDE 关联。

## 表 30.7：附件菜单

| 选项 | 描述 |
| --- | --- |
| Ethereal | 打开协议分析器；参见第 17 章。 |
| gFTP | 启动图形界面 FTP 客户端；参见第 22 章。 |
| IRC Client | 访问互联网相对聊天客户端。 |
| KGet | 转到 KDE 下载管理器。 |
| Kit | 打开用于 AOL 的 KDE 即时消息客户端。 |
| KMail | 启动 KDE 电子邮件客户端。 |
| KNewsTicker | 访问新闻滚动；默认配置包含了指向 Slashdot 故事的链接。 |
| KNode | 转到 KDE 新闻组阅读器 |
| Konqeror | 打开 KDE 浏览器；与 Mozilla 相比相对“轻量”。 |
| Korn | 启动入站邮件监控。 |
| KPPP | 访问 KDE PPP 连接工具，该工具支持通过移动电话连接到 ISP。 |
| KIRC | 转到 KDE IRC 聊天客户端。 |
| Mozilla Mail | 打开 Mozilla 电子邮件客户端 |
| Mozilla Mail Message | 启动 Mozilla 电子邮件客户端，配置为发出的消息。 |
| Remote Desktop Connection | 支持访问远程计算机上的 VNC 服务器。 |

## 互联网应用程序

在这一节中，我们将涵盖 Linux 用户在互联网上常用的运行的三个基础应用程序。这些是 Red Hat 的默认程序：网络浏览器 Mozilla；个人信息管理器 Evolution；以及即时消息（IM）客户端 Gaim，它们可以通过主菜单 > 互联网 访问。

## MOZILLA

Red Hat 浏览器是 Mozilla。它是一个功能全 Web的浏览器，基于 Netscape 代码构建，于 1998 年重新发布。你可以在功能之间进行切换，如图 30.8 所示。从左到右，这些图标与邮件、新闻组和 IRC 客户端相关。

官方缩写是 Gaim，是流行 IM 程序的 GNU 版本缩写。实际上，这个缩写并没有完全体现其价值。Gaim 使用插件（本质上是程序适配器）连接到多种类型的 IM 网络。Gaim 的登录界面如图 30.9 所示。

要访问特定网络，点击“账户”（Accounts）。然后你可以在选择的网络上选择并配置账户。显示名称（Screen Name）对应你的账户；别名（Alias）是通常在聊天区域看到的。

## EVOLUTION

Evolution 是一个个人信息管理器，类似于 Outlook。当你第一次启动 Evolution 时，系统会提示你配置配置文件。如图 30.10 所示，它可以处理各种电子邮件和即将进行的任务。

## 即时消息

GNOME 包含一个即时消息（IM）客户端，适用于由美国在线 (AOL)、Yahoo! 和微软网络 (MSN) 提供的服务。Gaim 的登录界面如图 30.11。

## 偏好

大多数与主菜单偏好子菜单关联的实用工具在本章早前的讨论 GNOME 控制中心时已经介绍过。本节涉及与主菜单 > 偏好 > 更多引用子菜单关联的实用工具。

## 多媒体

当你点击主菜单 > 声音与视频时，可以使用几个 GNOME 多媒体应用程序。这些包括各种音频和 CD 播放器以及声音控制工具。有关这些实用工具的简要概述，请参见表 30.8。

### 表 30.8：多媒体菜单

| 程序 | 描述 |
| --- | --- |
| Audio Player | 启动 X 多媒体系统 (XMMS)。 |
| CD Player | 打开音频 CD 播放器；KDE 版本是 KsCD。 |
| Sound Recorder | 进入一个可以录制声音、播放 .wav 文件并混合不同声音的工具。 |
| Volume Control | 访问多个系统的音量控制。 |
| Grip | 启动 GNOME CD 播放器和刻录机。 |
| aRts Builder | 打开声音服务器。 |

## 第 30 章 红帽 GUI 工作站

| 表格 30.8：多媒体菜单（续） |
| 程序 | 描述 |
| --- | --- |
| Kaboodle | 进入单个文件的媒体播放器。 |
| KMid | 支持 midi (.mid) 和卡拉拉 OK (.kar) 文件格式。 |
| KMidi | 打开 Midi 合成器的前端。 |

## 系统设置

有很多系统设置程序可用。其中许多是 `redhat-config-*` 工具，这些工具在其他章节中有所介绍。有关这些工具的简要概述，请参见表 30.9。

> 注意：如果你熟悉 Fedora Linux，你会发现这些 `redhat-config-*` 工具的名称略有不同：`system-config-*`

| 表格 30.9：系统设置 |
| 程序 | 描述 |
| 桌面切换工具 | 打开 `switchdesk` 工具，允许你设置默认的 GUI 桌面环境。 |
| 域名系统 | 启动域名服务器服务管理工具 (`redhat-config-bind`) |
| HTTP | 进入 HTTP 服务器配置工具 (`redhat-config-httpd`)。 |
| 网络启动服务 | 访问网络安装和磁盘环境工具，支持工作站和网络安装 (`redhat-config-netboot`)。 |
| NFS | 打开 NFS 服务器配置工具 (`redhat-config-nfs`) |
| Samba | 启动 Samba 服务器配置工具 (`redhat-config-samba`) |
| 服务 | 进入服务配置工具 (`redhat-config-services`) |
| 添加/删除应用程序 | 访问红帽包管理工具 (`redhat-config-packages`) |
| 认证 | 打开红帽认证工具 (`redhat-config-authentication`) |
| 日期与时间 | 启动日期/时间属性工具 (`redhat-config-date`)。 |
| 显示 | 进入显示设置工具 (`redhat-config-xfree86`)。 |
| 键盘 | 访问键盘工具 (`redhat-config-keyboard`)。 |
| 语言 | 打开语言选择工具 (`redhat-config-languages`)。 |
| 登录界面 | 启动 GDM 设置工具 (`gdmsetup`)。 |
| 鼠标 | 进入鼠标配置工具 (`redhat-config-mouse`)。 |
| 网络 | 访问网络配置工具 (`redhat-config-network`)。 |

| 表格 30.9：系统设置（续） |
| 程序 | 描述 |
| --- | --- |
| 打印 | 打开打印机配置工具 (`redhat-config-printer`)。 |
| Root 密码 | 允许 root 用户更改根密码 (`redhat-config-password`)。 |
| 安全级别 | 启动安全级别配置工具 (`redhat-config-securitylevel`)。 |
| 声卡设备 | 打开音频设备工具，告知红帽是否在你的电脑上检测到声卡 (`redhat-config-soundcard`)。 |
| 用户和组 | 访问红帽用户管理器 (`redhat-config-users`)。 |

## 系统工具

有多种系统工具可用。有关这些工具的简要概述，请参见表 30.10。

| 表格 30.10：系统工具 |
| 程序 | 描述 |
| 磁盘管理 | 启动 Mount 工具，它根据 `/etc/fstab` 显示当前挂载的 Linux 文件系统的状态。可用于挂载或格式化文件系统。 |
| 软盘格式化器 | 仅限 GNOME；打开一个将软盘驱动器格式化为 Linux 或 DOS 格式的工具。 |
| 浏览器 | 显示电脑上检测到的设备，仅供参考。 |
| 信息中心 | 仅限 KDE；连接到 KDE 控制中心信息菜单。 |
| 互联网配置向导 | 导航到红帽配置向导 `redhat-network-wizard`；更多信息请参阅第 16 章。 |
| Kickstart | 打开红帽配置器；更多信息请参阅第 5 章。 |
| 网络设备控制 | 允许为已配置的设备激活或打开网络配置工具。 |
| 打印图标 | 激活拖放打印。 |
| 红帽网络 | 设置连接到红帽网络管理服务器的默认值。 |
| 红帽网络警报图标 | 在任务栏上添加圆形图标；默认情况下应已安装。 |
| 屏幕缩放和旋转 | 仅限 KDE；启动屏幕缩放和旋转。 |
| 系统日志 | 打开系统日志工具。 |
| 系统监视器 | 启动系统监视器。 |

| 表格 30.10：系统工具（续） |
| 程序 | 描述 |
| --- | --- |
| 终端 | 启动终端模拟器。 |
| 配置编辑器 | 打开配置编辑器。 |
| 文件管理器 | 访问文件管理器。 |
| 音频录音器 | 打开音频录音器。 |
| DiskFree | 检查可用磁盘空间。 |
| 内核调优 | 启动内核调优工具。 |
| 邮件客户端 | 打开邮件客户端。 |
| 邮件传输 | 启动邮件传输代理。 |

## 浏览 OpenOffice 套件

最大的优势可能是办公套件，这些套件价值数百美元。办公套件通常包括文字处理器、电子表格、图形和演示文稿。OpenOffice.org 是基于 Microsystems 相同的代码开发的。它包含了几个应用程序，表 30.11 简要描述。

你可以从选择的 GUI 启动 OpenOffice.org 应用。点击应用程序图标即可。

| 表格 30.11：OpenOffice.ORG 应用程序 |
| 应用程序 | 描述 |
| --- | --- |
| Calc | 电子表格 |
| Draw | 图表创建器 |
| Impress | 演示文稿管理器 |
| Math | 公式创建器 |
| Printer Setup | 管理打印机 |
| Writer | 文字处理器 |

## OpenOffice.org Calc

第一个关键的 PC 应用可能是电子表格。你可以使用电子表格来定义许多范围。通过你选择的公式，你可以设置电子表格在不同场景下执行各种计算。它对于从统计分析到业务建模和预测的一切非常有用。

你可以通过选择“主菜单 > Office > OpenOffice.org”打开 OpenOffice.Calc，或者在 GUI 终端窗口中运行 `oofficec` 命令。图 30.12 显示了 OpenOffice.org Calc 以及当年的一些基本数据。

正如图中所示，OpenOffice.org Calc 具有电子表格的基本外观和感受。Calc 在功能上与 Microsoft Excel 相似，它包含了几个工具栏，如表 30.12 所示。

### 表 30.12：OPENOFFICE.ORG CALC 工具栏

| 工具栏 | 描述 |
|---|---|
| 公式 (Formula) | 反映单元格位置以及与该单元格相关的公式 |
| 功能 (Function) | 配置打开、打印和撤销等基本功能 |
| 超链接 (Hyperlink) | 设置对网页的访问 |
| 主要 (Main) | 允许创建图表；支持格式和拼写检查；允许排序和分组 |
| 对象 (Object) | 支持格式选项，包括字体、对齐、编号系统、边框和对齐 |

OpenOffice.org Calc 支持许多不同类型的电子表格，包括表 30.13 中描述的格式。如你所示，OpenOffice.org Calc 可以处理来自许多应用程序的电子表格，包括 Microsoft Excel、StarOffice Calc、dBASE/FoxPro 数据库等。你还可以设置 OpenOffice.org Calc 使用逗号分隔格式的文本文件（参见侧边栏）。

### 表 30.13：OPENOFFICE.ORG CALC 文件格式

| 格式 | 描述 |
|---|---|
| .sxc | OpenOffice.org 电子表格 |
| .stc | OpenOffice.org 电子表格模板 |
| .dif | 数据交换格式 (Data Interchange Format) |
| .dbf | dBASE/FoxPro 数据库文件 |
| .xls | Microsoft Excel 97/2000/XP 或 Excel 95/5.0 |
| .xlt | Microsoft Excel 97/2000/XP 或 Excel 95/5.0 模板 |
| .sdc | StarOffice Calc 5.0/4.0/3.0 (Sun StarOffice 电子表格) |
| .vor | StarOffice Calc 5.0/4.0/3.0 模板 |
| .slk | 符号格式；包含公式、单元格和文件链接 |
| .wks | Lotus 1-2-3 |
| .csv | 逗号分隔格式；文本文件中的电子表格 |
| .html | 网页 |

## 逗号分隔格式

电子表格和其他数据表通常以逗号分隔格式表示在文本文件中。换句话说，下面这一行中的每个值都可以导入电子表格行中的连续单元格中：

```
height, 00, 61, 44, 78, 56, 66
```

## OpenOffice.org Draw

你可以使用 OpenOffice.org Draw 来管理各种图形格式的文件，从 AutoCAD 文件到位图。换句话说，OpenOffice.org Draw 是一种设计工具，适用于任何从事图形相关工作的人员，从设计工程师到图形设计师。

你可以通过选择主菜单 > OpenOffice.org Draw 来启动 OpenOffice.org Draw，或者在 GUI 终端窗口中运行 `odraw` 命令。图 30.13 显示了带有 GNOME 桌面

### 图 30.13
OpenOffice.org Draw 画作

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_910_0.png)

正如图中所示，OpenOffice.org Draw 包含各种工具栏，其中一些允许你管理颜色，另一些允许你绘制和添加对象。这些工具栏描述在表 30.14 中。

### 表 30.14：OPENOFFICE.ORG DRAW 工具栏

| 工具栏 | 描述 |
|---|---|
| 颜色 (Color) | 允许从多种颜色中选择 |
| 功能 (Function) | 配置打开、打印和撤销等基本功能 |
| 超链接 (Hyperlink) | 设置对网页的访问 |
| 主要 (Main) | 允许缩放；插入对象（如文本和几何形状）；对象对齐等 |
| 对象 (Object) | 配置网格创建、文本编辑、旋转、颜色等 |
| 选项 (Option) | 支持线条的编辑和绘制选项，包括粗度和颜色 |

OpenOffice.org Draw 支持许多类型的绘图，包括表 30.15 中描述的格式。如你所示，OpenOffice.org 图形可以来自许多不同的应用程序，包括 Microsoft Excel、StarOffice Calc、dBASE/FoxPro 数据库等。你还可以设置 OpenOffice.org Calc 使用逗号分隔格式的文本文件。

### 表 30.15：OPENOFFICE.ORG DRAW 文件格式

| 格式 | 描述 |
|---|---|
| .sxd | OpenOffice.org 绘图 |
| .std | OpenOffice.org 绘图模板 |
| .bmp | Microsoft Windows 位图 |
| .dxf | AutoCAD 交换格式 |
| .emf | 增强元文件 (Enhanced metafile) |
| .eps | 封装 PostScript (Encapsulated PostScript) |
| .gif | 图形交换格式 (Graphics Interchange Format) |
| .jpg | 联合图像专家小组 (Joint Photographic Experts Group) |
| .met | OS/2 元文件 |
| .pbm | 便携式位图 (Portable bitmap) |
| .pcd | 照片 CD (Kodak) |
| .pct | Macintosh Pict 绘图 |
| .pcx | Zsoft paintbrush |
| .pgm | 便携灰度图 (Portable gray map) |
| .png | 便携式网络图形 (Portable Network Graphic) |

### 表 30.15：OPENOFFICE.ORG DRAW 文件格式

| 格式 | 描述 |
| --- | --- |
| .ppm | 便携式像素图 (Portable pixel map) |
| .psd | Adobe Photoshop |
| .ras | Sun 栅化图像 (Sun raster image) |
| .sda | StarOffice 5.0 Draw |
| .sdd | StarOffice Draw |
| .sgf | StarDraw |
| .sgv | StarView |
| .svm | StarView 元文件 |
| .tga | Truega |
| .tiff | 标记图像格式 |
| .vor | StarOffice 5.0 模板 |
| .wmf | Windows 元文件 |
| .xbm | Windows 位图 |
| .xpm | Windows |

## OpenOffice.org Impress

正如图中所示，OpenOffice.org Impress 具有演示文稿的基本外观。功能上与 Microsoft PowerPoint 相似，Impress 包含了几个工具栏，如下表 30.16 所示。

你可以通过选择主菜单 > OpenOffice.org Impress，或者在 GUI 终端窗口中运行 `impress` 命令来启动 OpenOffice.org Impress。图 30.14 显示了带有最新的演示文稿界面。

正如图中所示，OpenOffice.org Impress 包含了各种工具栏，其中一些允许你管理颜色，另一些允许你绘制和添加对象。这些工具栏描述在表 30.16 中。

### 表 30.16：OPENOFFICE.ORG IMPRESS 工具栏

| 工具栏 | 描述 |
| --- | --- |
| 颜色 (Color) | 允许从多种颜色中选择 |
| 功能 (Function) | 配置打开、打印和撤销等基本功能 |
| 超链接 (Hyperlink) | 设置对网页的访问 |
| 主要 (Main) | 允许缩放；插入对象（如文本和几何形状）；对象对齐等 |
| 对象 (Object) | 配置网格创建、文本编辑、旋转、颜色等 |
| 选项 (Option) | 支持线条的编辑和绘制选项，包括粗度和颜色 |
| 演示文稿 (Presentation) | 允许管理幻灯片 |

### 图 30.14
OpenOffice.org Impress 艺术作品

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_910_0.png)

正如图中所示，OpenOffice.org Impress 支持许多类型的演示文稿，包括表 30.17 中描述的格式。如你所示，OpenOffice.org 演示文稿可以来自许多不同的应用程序，包括 Microsoft Excel、StarOffice Calc、dBASE/FoxPro 数据库等。你还可以设置 OpenOffice.org Calc 使用逗号分隔格式的文本文件。

### 表 30.17：OPENOFFICE.ORG IMPRESS 文件格式

| 格式 | 描述 |
|---|---|
| .sxi | OpenOffice.org 演示文稿 |
| .sti | OpenOffice.org 演示文稿模板 |
| .ppt | Microsoft PowerPoint |
| .sda | StarOffice 5.0 绘图 |
| .sdd | StarDraw 3.0/StarImpress 4.0/5.0 |
| .vor | StarImpress 4.0/5.0 模板 |

## OpenOffice.org Writer

文字处理软件和其他数据表通常以逗号分隔格式表示在文本文件中。换句话说，下面这一行中的每个值都可以导入电子表格行中的连续单元格中：

```
height, 00, 61, 44, 78, 56, 66
```

## OpenOffice.org Draw

你可以使用 OpenOffice.org Draw 来管理各种图形格式的文件，从 AutoCAD 文件到位图。换句话说，OpenOffice.org Draw 是一种设计工具，适用于任何从事图形相关工作的人员，从设计工程师到图形设计师。

你可以通过选择主菜单 > OpenOffice.org Draw 来启动 OpenOffice.org Draw，或者在 GUI 终端窗口中运行 `odraw` 命令。图 30.13 显示了带有 GNOME 桌面

# 第 30 章：红帽工作站

图 30.15

OpenOffice.org Writer 中的一个 Word 文档

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_915_0.png)

# 表 30.19：OpenOffice.ORG Writer 文件格式

| 格式 | 说明 |
| --- | --- |
| .sxw | OpenOffice.org “文本”文档；它并不是真正的文本格式。 |
| .stw | OpenOffice.org “文本”文档模板。 |
| .doc | Microsoft Word 97/2000/XP；也提供适用于 Microsoft Word 95 和 6.0 的替代 .doc 格式。 |
| .html | 超文本标记语言，适用于网页。 |
| .rtf | 丰富文本格式；一种相对通用的格式，可被多个文字处理器读取。 |
| .sdw | StarWriter 3.0/4.0/5.0。 |
| .vor | StarWriter 3.0/4.0/5.0 模板。 |
| .txt | 普通文本；也提供带有换行符编码的替代 .txt 格式。 |

注意 当经验丰富的 Linux 用户需要进行桌面出版时，他们会使用基于文本的工具。例如，TeX 和 LaTeX 等工具包含了文本命令，用于在文本文件中格式化标题、斜体等。这并非空所未有；即使 WordPerfect 在 5.2 版本中也设置了类似的命令。

# 其他 OpenOffice.org 工具

其他值得关注的 OpenOffice.org 工具包括：

- OpenOffice.org Math 允许用户创建并记录各种复杂程度的方程；它支持三角函数、积分、极限、指数等。你可以通过 `oath` 命令从命令行启动它。

- OpenOffice.org Printer Setup 允许你为 OpenOffice.org 软件套件的其他部分配置驱动程序和打印格式。你可以通过 `oopadmin` 命令从命令行启动它。

# 打开图形化应用程序

红帽企业 Linux 3 带有许多图形化应用程序，包括 PDF（便携式文档格式）阅读器、图像查看器和截图程序。你可以从“主菜单 > 图形”或“主菜单 > 图形 > 更多应用程序”子菜单中选择大多数工具。

# CrossOver

如果你想迁移到 Linux 但绝对需要 Microsoft 应用程序，一个选项是 CodeWeavers 的 CrossOver Office。只需 39.95 美元（零售价），它就利用 WINE 项目（WINE 不是模拟器）让你能够在 Linux 计算机上运行一些最流行的 Windows 应用程序。这些应用程序包括（但不限于）：

- Microsoft Word 97/2000/XP
- Microsoft Excel 97/2000/XP
- Microsoft Outlook 97/2000/XP
- Microsoft PowerPoint 97/2000/XP
- Microsoft Visio
- Microsoft Internet Explorer
- Intuit Quicken
- Lotus Notes 5.0 和 6.51
- Adobe Photoshop

根据 CodeWeavers 的说法，并非所有应用程序都能完美兼容。请访问其网站以了解你所需应用程序的现状。如果你希望某个应用程序在 Microsoft Windows 中运行，请确保其兼容性达到“金牌”级别。当你使用 CrossOver Office 在 Linux 下运行其他应用程序时，可能会出现严重的错误。CodeWeavers 软件提供专业版和标准版。欲更多信息，请访问 codewavers.com。

# 图形化文档阅读器

你可以用 Linux 应用程序读取的三种图形化文档格式是 PDF（便携式文档格式）、PS（PostScript）和 DVI（设备无关）。

虽然你可以下载 Adobe Acrobat 来读取文档，但红帽企业 Linux 包含了两个原生 PDF 阅读器：PDF Viewer 和 PS/PDF viewer。你可以使用 DVI 查看器 KViewShell 来读取 DVI 文档。

# PDF 查看器

要启动 PDF Viewer，选择“主菜单 > 图形 > PDF Viewer”，或运行 `xpdf` 命令。这会打开一个没有工具栏的简单界面；你可以点击右键访问一些基础键盘命令。如果你想打开 PDF 文档，输入 `o`；或者在图 30.16 所示的打开框中，你将访问 PDF 文件。

图 30.16
访问 PDF 文件

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_917_0.png)

一旦 PDF 文件打开，可以使用屏幕底部的方向键浏览文档。或者，你可以使用表 30.20 中列出的基础命令。还有其他命令可用；请点击问号按钮。

| 表 30.20：基础 PDF 命令 |
| 命令 | 说明 |
| --- | --- |
| o | 打开新文件 |
| f | 查找文本 |
| n | 跳到下一页 |
| p | 回到上一页 |

# PS/PDF 查看器

PS/PDF Viewer 也称为 KGhostView。要启动此应用程序，选择“主菜单 > 图形 > 更多应用程序 > PS/PDF Viewer”，或运行 `pdfviewer` 命令。该应用程序为查看 PDF 和 PS 文件提供了更直观的界面，如图 30.17 所示。

图 30.17
PS/PDF 查看器

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_918_0.png)

# DVI 查看器

你可以用 Linux 应用程序读取的三种图形化文档格式是 PDF（便携式文档格式）、PS（PostScript）和 DVI（设备无关）。

虽然你可以下载 Adobe Acrobat 来读取文档，但红帽企业 Linux 包含了两个 PDF 阅读器：PDF Viewer 和 PS/PDF viewer。你可以使用 DVI 查看器 KViewShell 来读取 DVI 文档。

# PDF 查看器

要启动 PDF Viewer，选择“主菜单 > 图形 > PDF Viewer”，或运行 `xpdf` 命令。这会打开一个没有工具栏的简单界面；你可以点击右键访问一些基础键盘命令。如果你想打开 PDF 文档，输入 `o`；或者在图 30.16 所示的打开框中，你将访问 PDF 文件。

图 30.16
访问 PDF 文件

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_917_0.png)

一旦 PDF 文件打开，可以使用屏幕底部的方向键浏览文档。或者，你可以使用表 30.20 中列出的基础命令。还有其他命令可用；请点击问号按钮。

| 表 30.20：基础 PDF 命令 |
| 命令 | 说明 |
| --- | --- |
| o | 打开新文件 |
| f | 查找文本 |
| n | 跳到下一页 |
| p | 回到上一页 |

# PS/PDF 查看器

PS/PDF Viewer 也称为 KGhostView。要启动此应用程序，选择“主菜单 > 图形 > 更多应用程序 > PS/PDF Viewer”，或运行 `pdfviewer` 命令。该应用程序为查看 PDF 和 PS 文件提供了更直观的界面，如图 30.17 所示。

图 30.17
PS/PDF 查看器

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_918.

# 图像查看器

你可以用 Linux 应用程序读取的三种图形化文档格式是 PDF（便携式文档格式）、PS（PostScript）和 DVI（设备无关）。

虽然你可以下载 Adobe Acrobat 来读取文档，但红帽企业 Linux 包含了两个 PDF 阅读器：PDF Viewer 和 PS/PDF viewer。你可以使用 DVI 查看器 KViewShell 来读取 DVI 文档。

Eye of GNOME 是一个图形文件查看器。它允许你查看各种格式的图像。该程序的写入功能相当有限；默认情况下你只能写入 JPEG 和 PNG 格式。

# 图标编辑器

图标编辑器 IconEdit 允许你打开并修改图标的外观。要启动此应用程序，选择“主菜单 > 图形 > 更多应用程序 > 图标编辑器”，或运行 `iconedit` 命令。

# 查看器

图像查看器 KView 是另一个与 Eye of GNOME 类似的图形文件查看器。要启动此应用程序，选择“主菜单 > 图形 > 输出到”。

# Quickshow

Quickshow 是一个图像浏览器，列出你选择目录中的可用图像。要启动此应用程序，选择“主菜单 > 图形 > 更多应用程序 > Quickshow”，或运行 `quickshow` 命令。

当双击图像文件时，Quickshow 会自己的窗口中打开图像。然后你可以右键点击图像，打开一个让你操作图像外观的菜单。

# 绘画程序

绘画程序（也称为 KPaint）允许你打开、添加和修改选择的图像。要启动此应用程序，选择“主菜单 > 图形 > 更多应用程序 > 绘画程序”，或运行 `kpaint` 命令。

# 截图程序

有时你想记录屏幕上的设置。如果你在向某人描述问题，可以设置一张包含桌面外观的图片。

某些程序从其他硬件获取图像，例如数字相机和扫描仪。另一些程序直接从桌面屏幕或活跃的桌面窗口获取图像。

# 数字相机

有几个 gphoto2-* RPM 的图形化相机前端。你可以启动关联的 Linux 相机应用程序；选择“主菜单 > 图形 > 数字相机工具”，或运行 `gtcam` 命令。它能检测到的相机列表并不完整；更多信息请访问 www.gphoto.org。

## 打开图形化应用程序

## 扫描

标准的红帽（Red Hat）GUI 扫描程序被称为 `xsane`，你可以通过选择主菜单 > 图形 > 扫描，或者运行 `xsane` 命令来启动。并不是所有的扫描仪都能被 `xsane` 检测到；在这种情况下，你会收到此信息提示，且 `xsane` 不会打开。

还有一个 KDE 扫描程序名为 Kooka。它支持 `xsane` 并提供字符识别功能。你可以通过选择主菜单 > 图形 > 更多图形化应用程序 > 扫描与 OCR 程序，或使用 `kooka` 命令来启动 Kooka。

## GIMP

我最喜欢的 Linux 程序是 GIMP，它是 GNU 图像处理程序。许多用户偏喜欢 GIMP 而非其他高端图像程序，例如 Adobe 的 Photoshop 和 Jace 的 Paint Shop Pro。它是 GNOME 办公套件的一部分。我曾为这本书配置了大部分艺术作品。要启动此应用程序，请选择主菜单 > 图形 > GIMP，或运行 `gimp` 命令。

例如，当我为 Mozilla 浏览器截屏时，我启动了 GIMP，然后选择文件 > 获取 > 屏幕截图。我打开了屏幕窗口。当 Mozilla 准备就绪后，我点击截图窗口中的确定；这把光标变成了加号 (+)。我用它来选择 KPPP 窗口。当我右键点击截图时，它会打开一个菜单，我用它按我的选择保存图像。不同的屏幕和结果如图 30.18 所示。

图 30.18

工作中的 GIMP

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_920_0.png)

## 另一个图形程序：颜色选择器

KColorChooser 也称为 KColorEdit，允许你编辑色板。要启动此应用程序，请选择主菜单 > 图形 > 更多应用程序 > 颜色选择器，或运行 `kcolorchooser` 命令。在此工具中，你可以测量 RGB（红、绿、蓝）的相对水平；每种颜色的红绿蓝水平都在 0 到 255 之间。

## 设置默认语言

你可以使用多种语言之一配置 GUI。如果你在安装过程中安装了所需的语言，这个过程会非常简单。你只需要使用语言选择工具选择所需的语言即可。但如果你作为一家国际企业运营，你可能需要额外的语言。

## 基础配置文件

如果你需要额外的语言，可以安装所需的配置文件。列表列表请回阅第 5 章描述的 `comps.xml` 配置文件。例如，假设我们要为计算机添加韩语语言配置。查看 `comps.xml` 文件的韩语支持配置：
