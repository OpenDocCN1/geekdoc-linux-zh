
要将书籍添加到 Mobipocket 阅读器库中，只需将书籍拖到打开的 Mobipocket 窗口中。

# 配置

- 第4章：管理任务
- 第5章：网络连接
- 第6章：软件安装
- 第7章：使用 DEB、APT 和 dpkg 进行软件管理

# 第4章 管理任务

## 管理任务概述

本章回顾了你通常可能使用的某些管理任务和工具。大多数管理配置任务由 Ubuntu 自动为你完成。例如，打印机、硬盘分区和显卡等设备由操作系统自动检测并设置。你可能需要手动执行某些任务——例如添加新用户或排查显示问题。管理操作将在第6章中详细介绍。

本章讨论了几个系统管理操作以及如何执行常见任务，如添加新用户和配置远程打印机。软件管理将另行介绍。

提示：如果你在系统配置方面遇到困难，请检查 `http://ubuntuforums.org` 站点获取解决方案。该网站提供了各种论坛，涵盖从桌面和安装问题到游戏、浏览器和多媒体的解决方案。请检查 `www.ubuntu.com` 上的支持链接以获取文档、在线聊天和邮件列表。

## Ubuntu 管理工具

在 Ubuntu 上，管理由一组独立的专用管理工具处理，例如用于用户管理和打印机配置的工具（见表 4-1）。要访问基于 GUI 的管理工具，你需要以具有管理权限的用户身份登录——这就是你首次安装 Ubuntu 时创建的用户。

在 GNOME 面上，通过选择“会话管理”`Session Administration` 访问系统管理工具。在这里你将找到设置日期、管理用户、配置打印机和安装软件的工具。“用户和组”`Users and Groups` 允许你创建和修改用户及组。“打印”`Printing` 允许你创建和重新配置打印机。所有工具都提供了易用且直观的图形用户界面 `GUI`。在管理菜单中，工具通过简单的描述性术语识别，而实际名称以 `admin` 或 `system-config` 等术语开头。例如，打印机配置工具列为“打印”，其实际名称为 `system-config-printer`，而“用户和组”则是 `admin-users`。你可以在终端窗口中输入名称来单独调用任何工具。

## 第二部分：配置

| Ubuntu 管理工具 | 描述 |
| --- | --- |
| Synaptic 软件包管理器 | 使用在线仓库的 Apt 软件管理 |
| 安装和删除应用程序 | 使用在线仓库的 Apt 软件管理，添加/删除应用程序 |
| 更新管理器 | 使用 apt 仓库的更新工具 |
| system-config-kickstart | 配置自动安装脚本 (Fedora/Red Hat) |
| network-admin | 配置你的网络接口 (GNOME) |
| services-admin | 服务工具，管理系统和网络服务，如启动和停止服务器 (GNOME) |
| shares-admin | 为 Linux 系统配置通用共享目录或文件 |
| time-admin | 更改系统时间和日期 (GNOME) |
| users-admin | 用户和组配置工具 |
| system-config-cluster | 全局文件系统 (GFS) 管理 (Fedora/Red Hat) |
| system-config-printer | 打印机配置工具 (Fedora/Red Hat) |
| system-config-samba | 配置 Samba 服务器 (Fedora/Red Hat)，支持用户级认证 |
| gnome-language-selector | 选择使用的语言 |
| display-config-gtk | Ubuntu 显示配置工具，显卡和显示器 (GNOME) |
| Firestarter | 配置你的网络防火墙 |
| polkit-gnome-authorization | 为设备和管理任务设置身份验证，PolicyKit |
| system-config-lvm | 配置逻辑卷管理器 (LVM) 文件系统卷 (Fedora/Red Hat, 不支持) |
| ClamAV | 病毒防护应用程序 |

**表 4-1** Ubuntu 系统管理工具及相关应用程序

Ubuntu 使用 Red Hat Linux 支持的 KDE 发行版中的 GNOME 管理工具，以及独立的工具，如用于设备授权的防火墙；PolicyKit 以及用于软件安装的 Synaptic 软件包管理器。GNOME 管理工具带有后缀 `admin`，而 Fedora 的工具带有前缀 `system-config`。从 Ubuntu 7.10 开始，打印管理工具变为 Fedora 的 `system-config-printer`，取代了之前 Ubuntu 版本中使用的 GNOME `printer-admin` 工具。Ubuntu 现在有了 Samba GUI，它拥有 Fedora 的 `system-config-samba` 工具。

某些工具可以在 Ubuntu 上运行但尚未获得支持。Fedora 的 `system-config-lvm` 工具提供了一种管理 LVM 文件系统的简单有效方法，但 Ubuntu 并不直接支持它。不过，你可以在 Ubuntu 上下载、转换并安装该包，它将正常运行。此外，病毒防护由 ClamAV 等完全独立的应用程序处理。

> 注意：许多配置任务也可以通过命令行处理，直接调用程序：选择“应用程序 | 附件 | 终端”打开终端窗口。`sudo` 和 `make` 等命令需要终端。

## 受控管理访问：PolicyKit、sudo 和 gksu

要访问管理工具，你需要以具有管理权限的用户登录（安装时创建的用户）。当你选择要使用的工具时（例如通过“系统管理”选择工具），将通过 PolicyKit 授权或 `sudo`/`gksu` 操作授予访问。许多管理应用程序（如 GNOME 管理 `users-admin`）配置为使用 PolicyKit。其他应用程序（如 Synaptic 软件包管理器）可以通过使用 `sudo` 或 `gksu` 命令启动来授予任何应用程序管理权限，例如使用 `gksu gedit` 编辑配置文件。你可以在 `www.sudo.ws` 找到更多关于 `sudo` 的信息。

你可以使用“用户和组”工具授予或拒绝特定用户的管理权限。PolicyKit 和 `gksu` 都会提示输入密码。

### PolicyKit

对于启用了 PolicyKit 管理工具，应用程序将以读取权限启动。要使用应用程序执行管理任务，必须先解锁。点击窗口底部的解锁按钮打开对话框，在其中输入用户密码。然后管理工具窗口将显示并授予完全访问。你现在可以执行添加新用户等任务。在锁定的应用程序中，由于只有读取权限，例如你可以在 `users-admin` 应用程序中滚动用户列表，但无法进行任何更改或添加新用户（见图 4-1）。

点击解锁按钮打开 PolicyKit 提示，在其中输入你的用户密码（见图 4-2）。

## 72 第二部分：配置

![](img/d22ed937599b6dc8b332dd6901899cb6_103_0.png)

图 4-2 PolicyKit 授权提示

解锁“用户-管理员”窗口后，“解锁”按钮将变为灰色状态，你现在可以进行更改（参见图 4-3）。

### gksu

许多应用程序（例如 Synaptic 软件包管理器）仍在使用 `gksu` 来授予访问。在包管理器启动之前，系统会提示你输入密码（参见图 4-4）。只有这样 Synaptic 软件包管理器才会启动并允许你完全访问。对于桌面应用程序的管理员级访问，请使用 `gksu` 命令。在终端窗口中输入 `gksu` 命令以及应用程序名称。例如，要使用 GNOME 编辑器 `edit` 来编辑系统配置文件，你需要在终端窗口中使用 `gksu` 命令启动 `edit`，并将 `edit` 和文件名作为其参数。这将以管理员权限启动 `edit`。你不能简单地通过选择“应用程序 | 辅助程序 | 文本编辑器”直接从桌面启动 `edit`。下面的示例显示了如何编辑 `/boot/grub/menu.lst` 文件，以为引导管理器添加或编辑启动条目。系统首先会提示输入用户密码。

```bash
gksu edit /boot/grub/menu.lst
```

![](img/d22ed937599b6dc8b332dd6901899cb6_103_1.png)

图 4-3 用户设置窗口，已解锁

## 第 4 章：管理任务 73

![](img/d22ed937599b6dc8b332dd6901899cb6_104_0.png)

**图 4-4** 使用 gksu 进行管理员访问

**注意** *若要访问命令行，可以使用“终端”工具打开终端窗口：选择“应用程序 | 辅助程序 | 终端”。为了方便访问终端窗口，可以右键点击“终端”工具的菜单项并选择“将此启动器添加到桌面”，以便在桌面上放置终端图标。*

### sudo

`sudo` 和 `gksu` 命令允许普通用户获得某些任务的有限 root 用户级管理员访问权限，以便他们执行特定的监督操作，而无需完全的管理员级控制权限。

`sudo` 命令通常用于以管理员权限运行命令行命令。若要访问命令行，可以使用“应用程序 | 辅助程序”窗口中的“终端”工具打开终端窗口。使用 `sudo` 运行管理员命令，用户在命令前加上 `sudo` 命令。系统将向用户发放一个时间限制的票据以允许访问。这是一个示例：

```bash
sudo date
```
