
| Gabber | Jabber 客户端 (XMPP) |
| psi | 使用 QT (KDE) 的 Jabber 客户端 |
| Finch | 命令行光标 IRC、ICQ 和 AIM |

### Ekiga

Ekiga 是 GNOME 的 VoIP 应用，提供互联网 IP 电话和视频支持（见图 8-8）。它以前被称为 GnomeMeeting，其网站仍为 www.gnomemeeting.org。

## 第2 部分：应用程序

Ekiga 同时支持 H.323 和 SIP（会话发起协议）。它与微软的 NetMeeting 兼容。H.323 是一项综合协议，包含了如 DVB 和 H.261 等视频流数字广播协议，以及用于管理的 H.450 系列支持协议。

![](img/9a8872dc6f2acaed163529fd9d421e05_277_0.png)

图 8-8：Ekiga VoIP

使用 Ekiga 需要一个 SIP 地址。你可以从 ekiga.net 获取免费地址。你首先需要订阅该服务。当你首次启动 Ekiga 时，会提示你配置连接。在这里你可以提供联系信息、连接方式、声音驱动程序和视频设备等信息。使用地址簿连接到另一个 Ekiga 用户。黄页目录允许你搜索同样在使用 Ekiga 的人。

# ICQ

ICQ 协议允许你像即时消息工具一样与在线用户直接通信。使用 ICQ 客户端，你可以发送消息、与他们聊天或发送文件。你可以设置一个可能在你上线时想要联系的用户列表。当他们连接时，系统会实时通知你，如果你愿意，可以与他们通信。支持多种通信模式，包括聊天、消息、电子邮件、文件传输和游戏。要使用 ICQ，你需要向 ICQ 服务器注册，服务器将为你提供一个 ICQ 号，也称为通用互联网编号（UIN）。你可以在 www.icq.com 了解更多关于 ICQ 协议的信息。

## 第 8 章：Web、FTP、Java 和网络信息

互联网相对聊天（IRC）的运作类似于聊天室，你可以进入频道并与那里的其他用户。首先，你选择一个要连接的 IRC 服务器。针对不同的地区和主题有各种服务器可用。连接到服务器后，你可以从通道列表中选择进入。其界面工作非常像聊天室。当你连接到服务器时，可以选择一个作为你的昵称。Linux 系统上有多个互联网相对聊天客户端可用。大多数客户端运行在 X Window 系统、KDE 或 GNOME 平台上。

有多个基于 GNOME 和 KDE 的 ICQ 和 IRC 客户端供你使用。请查看 www.gnomefiles.org 上的 GNOME 软件列表以获取新版本和近期更新。对于基于 KDE 的 ICQ 客户端，请查看 www.kde-apps.org（Network | Chat）。

![](img/9a8872dc6f2acaed163529fd9d421e05_280_0.png)

# 第 3 部分：接口

GNOME

KDE

外壳

# 9. GNOME

GNU 网络对象模型环境，也称为 GNOME，是一个强大且易用的环境，主要由面板、桌面和一组用于构建程序界面的 GUI 工具组成。GNOME 的设计目的是为开发强大的应用程序提供一个灵活的平台。目前，GNOME 受到多个发行版的支持，并且是 Fedora 的主要界面。GNOME 是免费的，并根据 GNU 公共许可证发布。你可以直接从 GNOME 网站 www.gnome.org 下载源代码以及文档和其他 GNOME 软件。几家公司联合组成了 GNOME 基金会，这是一个致力于协调 GNOME 和 GNOME 软件应用程序开发的组织。这些成员包括 Sun、IBM 和惠尔尔等公司，以及 Mandrake、Fedora 和 TurboLinux 等 Linux 发行版。GNOME 基金会参考开发了 Apache Web 服务器的 Apache 软件会，为 GNOME 开发提供方向以及组织、财务和法律支持。

GNOME 桌面的核心组件包括一个启动程序和桌面功能的面板。桌面中通常常见的其他组件（如文件管理器、Web 浏览器和窗口管理器）由符合 GNOME 标准的应用程序提供。GNOME 提供了 GNOME GUI 工具库，开发者可以使用这些库来创建 GNOME 应用程序。使用符合 GNOME 标准的按钮、菜单和窗口的程序可以认为是符合 GNOME 标准的。GNOME 桌面的官方文件管理器不像 KDE 那样拥有自己的管理器。相反，它使用任何符合 GNOME 标准的窗口管理器。Metacity 窗口管理器是随 GNOME 分发的。

对组件模型接口的支持已集成到 GNOME 中，允许软件组件无论其实现时使用的编程语言或其运行的机器类型，都能相互连接。

## 第 3 部分：接口

GNOME 架构中用于此类接口的标准是通用对象请求代理架构（CORBA），它由对象模型组为 Unix 系统开发。GNOME 使用 CORBA 的 ORBit 实现。通过这样一种框架，GNOME 应用程序和客户端可以直接相互通信，允许你在另一个应用程序中使用某个应用程序的组件。从 GNOME 2.0 开始，GNOME 正式采用 GConf 及其库作为配置 GNOME 及其应用程序的基础方法。GConf 可以独立地配置编程程序，例如制作 Nautilus 文件管理器的程序。

你可以在 GNOME 网站 www.gnome.org 了解 GNOME。该网站提供在线文档（如《GNOME 用户指南》和常见问题解答），并为 GNOME 项目维护了大量的邮件列表供你订阅。www.gnomefiles.org 网站提供了 GNOME 应用程序和项目的详细软件列表。详细信息请查看 library.gnome.org 的 GNOME 文档站点。文档按用户、管理员和开发者组织。《桌面用户指南》提供了关于桌面使用的完整教程。对于管理员，《GNOME 桌面系统管理指南》详细介绍了管理员如何管理用户桌面。《桌面管理员的 GNOME 锁定与预配置指南》展示了管理员如何控制对打印或保存文件等任务的访问。

| 网站 | 描述 |
| :--- | :--- |
| www.gnome.org | GNOME 官方网站 |
| library.gnome.org | 面向用户、管理员和开发者的 GNOME 文档网站 |
| art.gnome.org | 桌面主题和背景艺术 |
| http://www.gnomefiles.org | GNOME 软件应用程序、小程序和工具。 |
| www.gnome.org/gnome-office | GNOME 办公应用程序。 |
| developer.gnome.org | Gnome 开发者站点，详见 library.gnome.org |

# 表 9-1：GNOME 资源

如果你想开发 GNOME，请查看 developer.gnome.org 获取教程和开发工具。GNOME 控制中心为你的桌面配置提供了直观的组织和访问。这被集成在 Fedora 的子菜单中。

GNOME 控制中心为你的桌面配置提供了直观的组织和访问。这被集成在 Fedora 的“偏好设置”菜单中。偏好设置分为个人、外观、互联网和网络、硬件和系统类别。GNOME 控制中心也实现为一种 GUI 界面，在左侧显示个人和硬件等不同类别，并持续显示偏好。选择一个类别将跳转并高亮相应的偏好。你可以通过在终端输入 `gnome-control-center` 调用控制中心界面。

# 第 9 章：GNOME

GNOME 控制中心为你的桌面配置提供了直观的组织和访问。这被集成在 Fedora 的“偏好设置”菜单中。偏好设置分为个人、外观、互联网和网络、硬件和系统类别。GNOME 控制中心也实现为一种 GUI 界面，在左侧显示个人和硬件等不同类别，并持续显示偏好。选择一个类别将跳转并高亮相应的偏好。你可以通过在终端输入 `gnome-control-center` 调用控制中心界面。

## Fedora 9 桌面外观

Fedora 具有以 Fedora Logo 为默认屏幕背景的桌面外观。标志描绘了一个蓝色圆圈内的 F。在主面板上，你会看到 Fedora Logo 作为应用程序菜单的图标。有多种 Fedora 背景图像供选择：被气泡包围并在周围有其他气泡的蓝色 F、Fedora 双螺旋以及 Fedora 热气球。

默认主题是带有 Fedora 图标的 Nadoka。桌面图像基于 Cairo，具有更直观、用户友好的图标。按钮和窗口易于使用且更美观。Cairo 图像主题

提示：你可以通过外观面板（系统 | 偏好设置 | 外观）手动下载并添加图标。选择一个主题，然后点击“自定义”并选择“图标”面板。在那里你会找到下载的图标项。

Gnome 桌面的功能与之前的版本相同，具有应用程序、位置和系统菜单。

Fedora 9 使用 Gnome 2.22

提示：在“应用程序”（Applications）和“位置”（Places）旁边列出了三个带有各自按钮的菜单： “应用程序”主菜单中的“系统工具”（System Tools）子菜单（用于磁盘占用分析器、终端窗口和更新系统等专用系统工具），以及“偏好”（Preferences）菜单中的“系统”（System）子菜单（用于 GNOME 电源管理等 GNOME 配置工具）。

## GNOME 2.x Features
