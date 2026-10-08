

在 Wine 中安装 Windows 字体只需将字体从 Windows 字体目录复制到您的 Wine `.wine/drive_c/Windows/fonts` 目录即可。您只需将任何 Windows `.ttf` 文件复制到该目录即可安装字体。

Wine 对于按钮和标题栏等功能会简化窗口样式。如果您想使用 XP 风格，请从 Microsoft 下载并安装 Royal 主题。但请注意，支持此主题非常消耗资源，可能会降低系统速度。

> **提示**
> 或者，您可以使用名为 CrossoverOffice 的商业 Windows 兼容性层。这是一款经过测试、可运行某些应用程序（如 Microsoft Office）的商业产品。请访问 www.codeweavers.com 了解更多详情。CrossoverOffice 基于 Wine，而 CodeWeavers 直接支持 Wine。

## 第 4 章
### 系统配置

本章回顾了您通常会使用的主要系统配置任务和工具。大多数工具在早期版本中已经熟悉。全面的概述有助于为那些新工具或已变更的工具建立更好的上下文。

为了有效利用您的 Linux 系统，您必须知道如何配置某些功能和服务。诸如添加用户和安装软件等管理操作现在可以使用用户友好的系统工具来完成。本章讨论了基本系统管理操作，这些操作对于让您的系统运行起来以及执行基本维护（如添加新用户或打印机）至关重要。

> *提示* 如果您在系统配置方面遇到困难，请查看 fedorasky.org 网站以寻找可能的解决方案。该网站提供了从视频和网络问题到游戏、浏览器和多媒体解决方案等有用的帮助。

您可能需要处理的四种基本系统配置任务是：用户管理、打印机设置、显示配置和软件管理。您可以管理用户，添加新用户，删除其他用户，并更新用户属性。可以为您的系统设置不同类型的打印机，包括远程和本地打印机。对于您的视频卡和显示器，您可以选择想要的分辨率和颜色深度。您还可以安装新的软件包，并更新或移除现有的软件包。在安装过程中，您被要求执行所有这些任务。此外，还有其他工具可用于配置键盘、声卡和鼠标等设备，以及执行设置系统日期和时间或选择要使用的语言等任务。您可以使用本章描述的管理工具轻松地进行更改或添加。

配置操作可以通过图形用户界面（如 GNOME 或 KDE）执行，也可以通过简单的 shell 命令行执行，在该命令行中键入配置命令。您可以手动访问系统配置文件，自行编辑它们并输入条目。例如，域名服务器条目保存在 `/etc/resolv.conf` 文件中。您可以编辑此文件并输入服务器地址。

> *注意* 配置工具仅对 root 用户可访问。您需要先以 root 作为用户名登录，并输入安装期间指定的 root 密码。

### Fedora 管理工具

在 Fedora 中，管理由 Fedora 开发和支持的一组独立的专用管理工具处理，例如用于用户管理和显示配置的工具（见表 4-1）。要访问基于 GUI 的 Fedora 工具，您需要以 root 用户身份登录到 GNOME 桌面并选择主菜单。系统管理工具列在主菜单中包含的系统管理（System Administration）菜单中。在这里，您可以找到设置时间和日期、管理用户、配置打印机和更新软件的工具。*Users & Groups* 允许您创建和修改用户和组。*Printing* 允许您安装和重新配置打印机。所有工具都提供非常直观的 GUI 界面，易于使用。在系统管理菜单中，工具由简单的描述性术语标识，而它们的实际名称通常以术语 `system-config` 开头。例如，打印机配置工具列示为 Printing，但其实际名称是 `system-config-printer`。您可以在终端窗口中通过输入其名称单独调用任何工具。

> *注意* 许多配置任务也可以在命令行上处理，直接调用程序。要使用命令行，请通过选择“应用程序 | 系统工具”菜单中的“终端”条目来打开终端窗口。这将打开一个带有命令行提示符的终端窗口。稍后讨论的 `rpm` 和 `make` 等命令将需要终端窗口。

### 直接编辑配置文件

虽然管理工具会为您处理所有配置设置，但有时您可能需要直接编辑配置文件来进行更改。这些通常是 /etc 目录中的文本文件或用户主目录中的点文件，如 `bash_profile`。要更改这些文件中的任何一个，您需要管理员权限，这要求您首先以 `root` 用户身份登录。

您可以使用任何标准编辑器（如 Vi 或 Emacs）来编辑这些文件，但其中一种最简单的方法是在 GNOME 桌面上使用 Gedit 编辑器。从附件（Accessories）菜单中选择“文本编辑器”。这将打开一个 Gedit 窗口。点击“打开”以打开文件浏览器，您可以在其中浏览文件系统以找到要编辑的文件。

> *警告* 编辑配置文件时要小心。编辑错误可能会损坏您的配置。建议在修改原始文件之前，先对正在处理的任何配置文件进行备份。

Gedit 允许您同时编辑多个文件，为每个文件打开一个选项卡窗格。您可以使用 Gedit 编辑任何文本文件，包括您自己创建的文件。在图 4-1 中打开了三个配置文件：`bash_profile`、`/boot/grub/grub.conf` 和 `/etc/fstab`。`bash_profile` 文件配置您的登录 shell，`/etc/fstab` 列出了您所有的文件系统及其挂载方式，而 `/boot/grub/grub.conf` 是您的 Grub 引导加载程序的配置文件。

像 `bash_profile` 这样的点文件必须从文件管理器窗口中选择。首先，通过打开“首选项”对话框（在任何文件管理器窗口中，选择“编辑”菜单中的“首选项”）并将“显示隐藏文件”条目设为选中状态，然后关闭对话框来配置文件管理器以显示点文件。然后，在“查看”菜单中选择“恢复默认设置”。这将在您的文件管理器窗口中显示点文件。双击即可在 Gedit 中打开其中一个。

| Fedora 管理工具 | 描述 |
| --- | --- |
| Pirut Package Manager | 使用在线存储库的 Yum 软件管理 |
| Package Update Program (PUP) | 使用 Yum 存储库的更新工具（取代 RHN） |
| System \| Administration | 用于访问管理工具的 Fedora 菜单 |
| System \| Preferences | 用于 GNOME 桌面配置的 Fedora 菜单 |
| Applications \| System Tools | 用于访问专用管理应用程序的 Fedora 菜单 |
| system-config-authentication | 设置身份验证配置 |
| system-config-boot | 设置启动默认操作系统 |
| system-config-date | 更改系统时间和日期 |
| system-config-display | Fedora 显示配置工具（视频卡和显示器） |
| system-config-httpd | 配置 Apache Web 服务器 |
| system-config-keyboard | 更改键盘配置 |
| system-config-kickstart | 配置自动安装脚本 |
| system-config-language | 选择要使用的语言 |
| system-config-lvm | 配置 LVM 文件系统卷 |
| system-config-nfs | 配置您的网络接口 |
| system-config-network | 配置您的网络接口 |
| system-config-network-tui | 使用命令行配置您的网络接口；它是基于光标的，没有 GUI |
| system-config-cluster | 全局文件系统（GFS）管理 |
| system-config-printer | 打印机配置工具 |
| system-config-rootpassword | 更改 root 用户密码 |
| system-config-samba | 配置您的 Samba 服务器 |
| system-config-securitylevel | 配置您的网络防火墙 |
| system-config-securitylevel-tui | 在命令行界面上配置您的网络防火墙 |
| system-config-selinux | 管理和配置 SELinux 策略 |
| system-config-services | 管理系统和网络服务，如启动和停止服务器 |
| system-config-soundcard | 配置您的声卡（参见本章稍后的“简单管理任务”） |
| system-config-switch-mail | 选择邮件传输代理（服务器） |
| system-config-users | 用户和组配置工具 |

**表 4-1** Fedora 管理工具

