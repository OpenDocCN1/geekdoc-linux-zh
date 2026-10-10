
NOTE 配置工具仅供 root 用户访问。你首先需要以你的用户名登录并提供你在安装期间指定的 root 密码。

# Fedora 管理工具

在 Fedora 上，管理工作由一组 Fedora 开发并支持的独立专用管理工具来完成。要访问基于 GUI 的 Fedora 工具，您需要以 root 用户登录 GNOME 桌面并选择主菜单。系统管理工具列在主菜单包含的“系统管理”（System Administration）菜单中。在这里，您将找到设置日期时间、管理用户、配置打印机以及更新软件的工具。“用户与组”（Users & Groups）可以帮助您创建和修改用户及组。“打印”（Printing）允许您安装和重新配置打印机。所有菜单工具都提供了直观易用的 GUI 界面。在系统管理菜单中，工具通过简单的描述性名称识别，而它们的实际名称以 `system-config-` 开头。例如，打印机配置工具列为“Printing”，但其实际名称为 `system-config-printer`。您可以在终端窗口中输入其名称来单独调用任何工具。

> 注意：许多配置任务也可以通过命令行直接调用程序来处理。要使用命令行，请通过选择“应用程序 | 系统工具”菜单中的“终端”（Terminal）项打开终端。这将打开一个带有命令行提示符的终端窗口。像 `make` 以及稍后讨论的命令将需要终端窗口。

# 直接编辑配置文件

虽然管理工具会为您处理所有的配置设置，但有时您可能需要通过直接编辑配置文件来做出更改。这些通常是位于 `/etc` 目录下的文本文件或用户主目录下的点文件（如 `.bash_profile`）。要更改这些任何文件，您将需要管理权限，这要求您先以 root 用户登录。

您可以使用任何标准编辑器（如 Vi 或 Emacs）来编辑这些文件，最简单的方法之一是使用 GNOME 桌面上的 Gedit。从“辅助工具”（Accessories）菜单中选择“文本编辑器”（Text Editor）。这将打开一个“编辑”窗口。点击“打开”（Open）打开文件浏览器，您可以在其中浏览文件系统以找到您要编辑的文件。

> 警告：编辑配置文件时务必小心。编辑错误可能会损坏您的配置。建议在对原始文件进行重大更改之前，先对正在操作的任何配置文件进行备份。

Gedit 允许您同时编辑多个文件，为每个文件打开一个标签页。您可以使用 Gedit 编辑任何文本文件，包括您创建的文件。在图 4-1 中打开了三个配置文件：`.bash_profile`、`/boot/grub.conf` 和 `/etc/fstab`。`.bash_profile` 文件配置您的登录 shell，`/etc/fstab` 列出了所有文件系统及其挂载方式，而 `/boot/grub/grub.conf` 是您的引导加载程序的配置文件。

点文件（如 `.bash_profile`）必须从文件管理器窗口中选择。首先，通过打开“首选项”对话框（在任何文件管理器窗口的“编辑”菜单中选择“首选项”）来配置文件管理器显示点文件，然后勾选“显示隐藏文件”并关闭对话框。接着在“查看”菜单中点击“恢复默认设置”。这会在您的文件管理器窗口中显示点文件。双击即可打开一个 Gedit。

# 第 4 章：系统配置

| Fedora 管理器 | 描述 |
| --- | --- |
| Pirut 包管理器 | 使用在线仓库进行 Yum 软件管理 |
| 包更新程序 (PUP) | 使用 Yum 仓库的更新工具（替换 RHN） |
| 系统 | 管理 | 用于访问管理工具的 Fedora 菜单 |
| 系统 | 首选项 | 用于配置 GNOME 桌面的 Fedora 菜单 |
| 应用程序 | 系统工具 | 用于访问专用应用程序的 Fedora 菜单 |
| `system-config-authentication` | 设置认证设置 |
| `system-config-boot` | 设置操作系统默认启动 |
| `system-config-date` | 更改系统时和日期 |
| `system-config-display` | Fedora 显示配置工具（显卡和显示器） |
| `system-config-httpd` | 配置 Apache Web 服务器 |
| `system-config-keyboard` | 更改键盘配置 |
| `system-config-kickstart` | 配置自动安装脚本 |
| `system-config-language` | 选择要使用的语言 |
| `system-config-lvm` | 配置 LVM 文件系统 |
| `system-config-nfs` | 配置您的网络接口 |
| `system-config-network` | 配置您的网络接口 |
| `system-config-network-tui` | 使用命令行配置您的网络接口；基于光标，无 GUI |
| `system-config-language` | 选择要使用的语言 |
| `system-config-cluster` | 全局文件系统 (GFS) 管理 |
| `system-config-printer` | 打印机配置工具 |
| `system-config-rootpassword` | 更改 root 用户密码 |
| `system-config-samba` | 配置您的 Samba 服务器 |
| `system-config-securitylevel` | 配置您的网络防火墙 |
| `system-config-securitylevel-tui` | 在命令行界面上配置网络防火墙 |
| `system-config-selinux` | 管理和配置 SELinux 策略 |
| `system-config-services` | 管理系统和网络服务，如启动和停止服务器 |
| `system-config-soundcard` | 配置您的声卡（本章后文“简单管理任务”） |
| `system-config-switch-mail` | 选择邮件传输代理（服务器） |
| `system-config-users` | 用户和组配置工具 |

**表 4-1** Fedora 管理工具

![](img/af27012edddcf42a8b40fad81183c10b_129_0.png)

图 4-1 文本编辑器和配置文件

# 简单管理任务

某些管理任务可以使用一些 `system-config` 工具完成。这些工具大部分在“管理”菜单中有明显的条目。其他工具在您拥有配置工具时，如“登录屏幕”（Login Screen）。

鼠标配置和日志显示现在由 GNOME 工具处理。检查 GNOME 偏好设置进行鼠标配置，并使用系统日志查看器（`gnome-system-log`）来显示日志。

# 登录屏幕

如果您想更改登录屏幕，可以使用从“管理”菜单“登录屏幕”项访问的“登录屏幕设置”窗口。这配置了运行您的登录过程的 GNOME 显示管理器（GNOME Display Manager）。在这里，您可以设置背景图像、显示的图标、使用的主题、要列出的用户，甚至是欢迎信息。登录屏幕可以为本地或远程用户进行配置。您可以在纯屏幕、带人脸浏览器的纯屏幕或用于为本地用户选择显示内容的登录面板（以及各种可用主题）之间进行选择。从远程面板，您可以选择纯屏幕、纯屏幕，或与本地用户使用相同的配置。

在“用户”面板上，您可以选择在使用人脸浏览器时显示哪个用户。在“本地”面板上，您可以从多个主题中进行选择。默认选择 Fedora 主题、带人脸浏览器的 Fedora 高级主题（这是 Fedora 7 的默认主题）。您也可以选择随机选择主题。

在“安全”面板上，您可以设置自动登录，跳过启动时的登录屏幕。您甚至可以设置定时登录，在显示规定时间的登录屏幕后自动登录特定用户。在面板的“安全”部分，您可以设置安全选项，例如允许 root 登录或允许 TCP（互联网）访问，以及设置允许登录次数。点击此面板上的“配置 X 服务器”按钮将打开一个配置 X 服务器访问的窗口。详情请通过“帮助”按钮访问《GNOME 显示管理器参考手册》。

# 配置用户

目前，向 Fedora 添加新用户最简单且有效的方法是使用 `system-config-users`，也称为 Fedora 用户管理器。您可以从 GNOME 桌面菜单中的“系统 | 管理 | 用户与组”项访问它。`system-config-users` 窗口将显示列出用户和组的面板（见图 4-2）。

![](img/af27012edddcf42a8b40fad81183c10b_130_0.png)

> 图 4-2 Fedora 用户管理器，`system-config-users`

## 第一部分：入门指南

按钮栏将列出你可以执行的各种任务，包括创建用户或组、编辑现有项（编辑）、或删除选定的用户或组。
