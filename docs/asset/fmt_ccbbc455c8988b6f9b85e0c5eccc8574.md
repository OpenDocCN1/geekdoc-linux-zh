
# 使用基于 Web 管理

许多开源项目提供了基于 Web 的管理工具，使这些项目对普通用户更容易使用。使用这些工具只需要一个 Web 浏览器（如 Firefox）、服务的端口号以及 root 密码。Samba 和 CUPS 等项目自带了自己的管理工具。Webmin 是一项通用工具，可以从你的浏览器管理各种 Linux 系统。

基于 Web 管理工具的优势在于，你可以从熟悉的界面（你的 Web 浏览器）进行操作，并且可以远程访问它们。

> 某些 Linux 发行版自带了一套图形化管理工具（例如 SUSE 的 YaSt 界面或红帽的 `system-config` 工具）。通常情况下，你应该使用这些工具，而不是使用该项目的任何 Web 界面，因为该发行版自带的工具与其启动和停止服务的工具集成得更好。

# 提供 Web 管理的开源项目

主要的开源项目都提供了用于配置这些项目的 Web 界面。无论你正在使用哪种 Linux，都可以使用 Web 浏览器配置以下项目：

- Samba —— 要设置 Samba 以在局域网上与 Microsoft Windows 系统进行文件和打印机共享，请从任何 Web 浏览器使用 SWAT Web 管理工具。安装并运行 SWAT 后，你可以在浏览器的地址栏中输入以下 URL 来访问 Samba 服务器配置：

```
http://localhost:901
```

> 如果你收到“Unable to Connect”（无法连接）消息，说明 Samba 未安装或未运行。

Samba 项目还提供了其他管理 Samba 的图形化工具。你可以访问 `http://samba.org/samba/GUI` 查看。有关这些工具的描述，请参阅第 26 章和第 27 章。

# 学习基础管理

- CUPS —— Common UNIX 打印服务（CUPS）有自己的 Web 管理工具。安装并配置 CUPS 后，你通常可以通过 Web 浏览器的地址栏输入以下 URL 来使用 CUPS Web 管理：

Samba 和 CUPS 包含许多 Linux 发行版。其他提供基于 Web 管理的项目（可能包含不包含你的发行版）包括 SquirrelMail（一个 Web 界面）和 Mailman（邮件列表设施）。

由于许多管理界面以明文发送数据，因此它们最适合用于本地系统。然而，由于它们是基于 Web 的，你应该考虑对通信进行加密。Webmin 管理工具

Webmin 家族（`www.webmin.com`）已将 Webmin 移植到 70 多操作系统。支持的 Linux 发行版包括 SUSE、Red Hat（Fedora）、Debian、Ubuntu、CentOS、Slackware、Mandriva、Yellow Dog 等（完整列表参见 `www.webmin.com/support.html`）。一旦从 Webmin.com 下载并安装了 Webmin，你就可以从浏览器使用它。要启动 Webmin 界面，请在浏览器中输入以下：

```
http://localhost:10000
```

以 root 登录后，将显示 Webmin 主页，如图 4-1 所示。

# 不同发行版的图形化管理

有些人担心离开熟悉的 Windows 系统进入 Linux 后，将陷入从命令行执行一切工作的困境。为了获得更广泛的受众，红帽企业 Linux 和 SUSE 等商业 Linux 发行版创建了自己的图形化工具，为新用户提供易操作的切入点。以下章节介绍了红帽的 `system-config` 和 SUSE 的 YaST。

# 第二部分

# 运行演示

图 4-1

Webmin 提供了一个用于管理 Linux 的 Web 浏览器界面。

![](img/d7f79c91d15076e71790c1b4e1d072d0_172_0.png)

# 红帽配置工具

Fedora 和红帽企业 Linux 系统的一系列图形化工具可以从系统菜单的管理子菜单或从命令行启动。大多数从命令行启动的 Fedora 和 RHEL 工具以 `system-config` 字符串开头（例如 `system-config-network`）。

> 注意

在 Core 和之前的红帽版本中，GUI 管理工具都以 `redhat-` 开头，例如 `red-config-network` 和 `redhat-logviewer`。从 Fedora 2 开始，这些名称更改为 `system-`，导致了像 `system-config-network` 这样的名称。

管理任务需要 root 权限；如果你以普通用户登录，在 GUI 应用程序打开后必须输入 root 密码。输入密码后，大多数系统配置工具在本次登录会话期间无需再次密码即可工作。查看面板右上角的黄色徽章图标，它表示你拥有 root 权限。点击徽章可以弹出一个窗口，允许你移除权限。否则，权限会在关闭窗口时消失。

以下列表描述了许多用于管理 Fedora 或红帽企业 Linux 系统的图形化工具。这些工具从系统菜单的管理子菜单中启动窗口。获取该功能所需的软件包名称显示在括号中。

## 基础管理学习

下述选项的可用取决于您安装了哪些功能。

+ 服务器设置 — 从此子菜单访问以下服务器配置窗口：
- 域名系统 (`system-config-bind`) — 如果您的计算机充当 DNS 服务器，则在此配置并配置区域。
- HTTP (`system-config-httpd`) — 将您的计算机配置为 Apache Web 服务器。
- NFS (`system-config-nfs`) — 设置系统中的目录，通过 NFS 服务将其与网络上的其他计算机共享。
- Samba NFS (`system-config-nfs`) — 配置 Windows (SMB) 文件共享。（如需配置其他 Samba 功能，您可以使用 SWAT 窗口）。
- 服务 (`system-config-services`) — 在“服务配置”窗口中显示并更改在 Fedora 系统上以不同运行级别运行的服务。
+ 认证 (`auth-config-gtk`) — 更改用户在系统上的身份验证方式。通常选择 影子密码（Shadow Passwords）和 MD5 密码。如果您的网络支持 LDAP、Kerberos、SMB、NIS 或 Hetis 验证，您可以选择使用其中任何一种验证类型。
+ 引导加载程序 — 如果您的计算机上有多个操作系统，或者 Linux 中有多个可启动的 Linux 内核，请选择默认引导。如果您在同一块硬盘上安装了 Fedora Linux、SUSE 和 Windows XP，在没有显式选择的情况下，您可以选择其中一个自动启动（在指定的秒数后）。
+ 日期与时间 (`system-config-date`) — 设置日期和时间，或选择通过 NTP 服务器同步时间。
+ 显示 (`system-config-display`) — 更改您的 Y 桌面设置，包括显示器的色彩深度和分辨率。您还可以选择显卡和显示器的设置。
+ 防火墙 (`system-config-firewall`) — 配置您的防火墙，以允许或拒绝来自网络计算机的服务。
+ 硬件浏览器 (`hwbrowser`) — 查看有关您的计算机硬件的信息。
+ 键盘 (`system-config-keyboard`) — 根据语言选择正在使用的键盘类型。
+ 语言 (`system-config-language`) — 选择系统默认语言。
+ 逻辑卷管理 (`system-config-lvm`) — 管理您的 LVM 分区。
+ 登录屏幕 (`gdm`) — 控制登录界面的显示和行为。

## 第二部分 运行演示

+ 网络 (`system-config-network`) — 管理您当前的网络接口并添加接口。
- 打印 (`system-config-printer`) — 配置本地和网络打印机。
- Root 密码 (`system-config-rootpassword`) — 修改 root 密码。
- SELinux 管理 (`system-config-selinux`) — 设置 SELinux 强制模式和默认策略。
- SELinux 故障排除器 (`setroubleshoot-server`) — 监控和诊断 SELinux 设备。
- 声卡检测 (`system-config-soundcard`) — 尝试检测并配置声卡。
- 系统日志 (`gnome-utils`) — 查看系统日志文件并进行关键词搜索。
- 用户与组 (`system-config-users`) — 为您的系统添加、显示和更改用户及账户。

其他管理工具可以通过顶部面板上的应用程序菜单进行访问。“添加/删除软件”选项允许您从网络上任何可用的 yum 启用软件库中选择软件。对于其他管理工具，选择“系统工具”子菜单查看以下某些选项。

+ 配置编辑器 (`conf-editor`) — 直接编辑 GNOME 配置数据。
- 磁盘使用分析器 (`gnome-utils`) — 显示有关硬盘和可移动存储设备的详尽信息。
- Kickstart (`system-config-kickstart`) — 创建 kickstart 配置文件，可用于在无用户交互的情况下安装多个 Fedora 系统。
