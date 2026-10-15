
KIO（K 输入输出）是 KDE 架构的一部分。它以本地存储的方式访问文件、网站和其他资源。`KIO`可以连接单个协议（例如`HTTP`、`FTP`、`SMB`、`SSH`、`SFTP`、`SVN`、`TAR`）。KDE 帮助中心简要列出了可用术语。

## Solid – 设备组框架

`Solid`是一个设备集成框架。它在底层操作系统之外提供查询和硬件接口。它提供了针对应用程序开发者的后续功能：硬件发现、电源管理和网络管理。

# KDE Plasma 桌面环境 ■ 33

## Sonnet

`Sonnet`是一个基于`Qt`应用程序插件的拼写检查库。它支持多个插件，包括`HSpell`、`Enchant`、`ASpell`和`hun-spell`。它还支持基于不同算法组合的自动语言检测。

## ThreadWeaver

`ThreadWeaver`最初为`KDE`软件编译 4 开发的系统库，后来在`KDE Frameworks 5`中经过重新设计。它允许开发者轻松地使用多核处理器和多线程。在`ThreadWeaver`中，工作负载被划分为单独的任务。然后，函数之间存在关系。`ThreadWeaver`将使用最有效的方式来利用它们。`Krita`使用`ThreadWeaver`进行视觉过滤预览，以禁用`GUI`锁。

## KDE 应用

由`KDE`创建的关键应用程序包括：

### 编辑器

- `Kate`: 适用于编辑者的高级文本编辑器
- `Kedit`: 一个简单的文本编辑器，具有一些功能，类似于`Windows`记事本
- `Kile`: `LaTeX`编辑器
- `KWrite`: 文本编辑器

### 教育

- `KGeography`: 一个扫描本地信息的应用程序
- `Kiten`: 一种日语学习工具
- `KLAid`: 使用电脑时通过卡片学习的工具
- `Konjie`: 用于编译和整理法语动词的工具
- `Kalzium`: 显示`Linux`元素表信息
- `KStars`: 天文馆程序
- `Step`: 交互式物理模拟
- `KAlgebra`: 符号计算器

### 游戏

- `KAtomic`: 益智游戏
- `KFoulEggs`: 泡泡泡龙游戏
- `Klickety`: 益智游戏
- `KMines`: 扫雷大游戏
- `Kolf Game`: 高尔夫游戏
- `KReversi`: 黑白/五陆棋游戏
- `KSirtet`: 俄罗斯俄罗斯游戏

### 照片

- `DigiKam`: 数字胶摄影管理
- `Gwenview`: 照片查看器
- `KGhostView`: `pdf`/`ps`文件查看器
- `Kolourpaint`: 一个小型位图照片编辑器（与`MSPaint`非常相似）
- `KPDF`: `PDF`查看器
- `KPovAlbum`: 数字照片和照片管理器
- `KPovModeler`: 用于`POV-Ray`场景的建模和设计程序
- `Krita`: 位图照片编辑器
- `KSnapshot`: 截图查看器
- `Kuickshow`: 照片查看器
- `KColorEdit`: `KDE`调色板编辑器
- `KView`: 图片查看器
- `Okular`: 国际文学查看器
- `ShowImg`: 图片查看器

## 主题应用组

- `KDE-Plasma-Addons`: 额外的`Plasma`小部件
  - `KDE-Network`
  - `KDE-PIM`
  - `KDE-Graphics`
  - `KDE-Multimedia`
- `KDE Accessibility`: 辅助功能应用程序
  - `KDE-Utilities`
  - `KDE-Edu`
- `Calligra Suite`: 集成办公套件
  - `KDE-Games`
  - `KDE-Toys`
- `KDE-Art`: 额外的图标、样式等
  - `KDE-SDK`
  - `KDE-Bindings`
- `KDEWebdev`: 这是一个Web开发工具
- `KDE-Extragear`: 这是一个非`KDE`核心应用程序和工具的集合
- `KDE-Playground`: 包含新的且不稳定的软件

## 其他项目

- `KDE Connect`: 用于将`Plasma`桌面连接到手机进行远程控制的`Android`应用
- `KDE Neon`: 基于`Ubuntu`的包含最新`KDE`软件包的发行版
- `Wiki2Learn`: 人们参与和共享信息的Web框架

## 系统

- `Filelight`: 展示磁盘空间是如何被使用的，将其描绘为一组固定饼图
- `KBluetooth`: 蓝牙连接
- `KDE Control Center`: 集中式配置工具
- `KDE System Guard`: 增强的任务管理器和系统监控
- `KDirStat`: 图形磁盘工具
- `KDM`: 登录管理器
- `Infocenter`: 关于你电脑的信息
- `KlamAV`: 用于`KDE`的`ClamAV`杀病毒软件
- `Konsole`: 终端模拟器
- `KWallet`: 密码管理器保护
- `Yakuake`: 出的终端模拟器
- `KDE Session Manager`: 会话编辑器

# KDE 开发

所有`KDE`项目的源代码都存储在`Git`源代码中。稳定版本带有文档下载到`KDE FTP`服务器。它们已准备好由操作系统供应商集成并在分发前与其他系统集成。大多数用户仅使用稳定且经过测试的`KDE`程序或应用程序，为您提供易于安装的预包。

# 许可证

`KDE`软件项目必须在可访问的许可条款下发布。1998 年 11 月，`Qt`框架有两个许可证：开源的`Q Public`许可证（`QPL`）和面向软件开发者的商业许可证。同年，成立了`KDE Free Qt`基金，保证如果`Trolltech`停止存在或在 12 个月内发布免费版本的`Qt`，则`Qt`将处于唯一的`BSD`许可证下。

# KDE Plasma 桌面环境 ■ 37

关于遵守`GNU`通用公共许可证（`GPL`）的辩论持续，这就是为什么在 2000 年 9 月，`Trolltech`在`QPL`之上提供了`GPL`下的`UNIX`版本的`Qt`库，消除了自由软件基金会的顾虑。`Trolltech`继续要求开发`Qt`相关软件需要获得许可证。`KDE`的主要库集成了`GNU LGPL`下的许可证。尽管如此，对于专利软件的唯一方法是在`Qt`专利许可证条款下开发。从`Qt 4.5`开始，`Qt`也开始以`LGPL 2.1`版本提供，允许专利应用程序正式使用开源的`Qt`版本。

# 实现

许多`KDE`项目使用使用`Qt`框架，该框架运行在`UNIX`、`macOS`和`Microsoft Windows`等许多应用程序上。自 2011 年以来，`CMake`一直作为构建工具运行。它允许`KDE`支持广泛的平台，包括`Windows`。使用`gettext`进行翻译。使用`Doxygen`生成`API`文档。

# KDE 版本历史

首先，我们将讨论格式。有五个版本：

- 桌面环境 1
- 桌面环境 2
- 桌面环境 3
- `KDE`软件编译 4
- `KDE Plasma 5`

我们将详细讨论上述所有版本。

# 桌面环境 1

它是基于`UNIX`系统的首次发布。有几个桌面环境版本。最初，`KDE`在 1996 年 10 月 14 日`Matthias Etrich`的公告后不久推出了桌面环境。从那时起，`Kool`的名称逐渐减少，并变成了桌面环境。最初，`Kool`被开发者社区接受。`KDE`的首次联系邮件列表是`kde@fiwi2.uni-Tubingen.de`。

第一个发布是 1997 年 10 月 20 日，在首次公告后约一年。随后是三个`Beta`版本分别为 1997 年 11 月 23 日、1998 年 2 月 1 日和 1998 年 4 月 19 日。

# 桌面环境 1.0

`KDE`桌面环境 1.0 的第一个版本于 1998 年 7 月 12 日发布。`KDE`是一个具有`UNIX`工作站网络的桌面平台。它寻求满足`macOS`或`Windows`等`UNIX`操作系统对易用桌面的需求。`UNIX`是今天使用的操作系统。多年来一直是信息技术无可争议的选择。如果你考虑稳定性、可用性和开放性，`UNIX`的现代易用桌面防止了`UNIX`进入办公室和家庭用户。现在带有`KDE`的`UNIX`/`KDE`是完全开放的平台，包括必须修改的源代码。我们希望`UNIX`/`KDE`的结合最终为普通计算机带来开放、可靠、稳定且合规的计算机。

该版本在`Qt`免费许可证下获得了`Qt`框架，该许可证与自由软件不兼容并建议使用`Motif`。此外，`KDE`受许多用户的欢迎并进入了第一个`Linux`流。

# 桌面环境 1.1

桌面环境 1.1 版本更快、更稳定，并包含了一些小的改进。它有一组新的图像、背景和样式。某些部分收到了额外的更新，例如`Konquer`管理器、`kpanel`启动器和`KWin`窗口。然后，最近引入了地址管理库以及`KMail`重写（称为`Kmail2`），它们与旧版`KMail`一起作为`alpha`安装。`Kmail2`没有离开`alpha`状态，升级在旧`KMail`更新中完成。桌面环境 1.1 受到了评论者的好评。

# KDE Plasma 桌面环境 ■ 39
