
在本章中，你学习了如何配置 Fedora Core 4 计算机作为其他 Linux 或 Unix 计算机的文件服务器，以及网络上 Windows 计算机的文件服务器。

为了启用你的网络文件系统 `NFS` 服务，你学习了以下操作：

- 安装 NFS 配置工具以方便地添加和配置 NFS 导出
- 使用 NFS Server 配置工具或直接编辑 `/etc/exports` 文件来添加 NFS 共享
- 通过使用服务配置工具或 `chkconfig` 命令，配置 NFS 服务器在每次启动 Linux 时自动启动
- 编辑你的数据包过滤配置以允许 NFS 网络流量

# 第 33 章：提供网络文件服务

为了启用你的 Windows 文件共享服务，你学习了以下操作：

- 安装 Windows File Server 软件包组
- 使用 Samba Server 配置工具创建并编辑用户列表和共享列表
- 配置 Samba 服务器在每次启动 Linux 时自动启动，通过使用服务配置工具或 `chkconfig` 命令
- 编辑你的数据包过滤配置以允许 Windows 网络流量

本章让你学习了如何配置 Fedora Core 4 计算机作为其他 Linux 或 Unix 计算机的文件服务器，以及网络上 Windows 计算机的文件服务器。

为了启用你的网络文件系统 `NFS` 服务，你学习了以下操作：

- 安装 NFS 配置工具以方便地添加和配置 NFS 导出
- 使用 NFS Server 配置工具或直接编辑 `/etc/exports` 文件来添加 NFS 共享
- 通过使用服务配置工具或 `chkconfig` 命令，配置 NFS 服务器在每次启动 Linux 时自动启动
- 编辑你的数据包过滤配置以允许 NFS 网络流量

为了启用你的 Windows 文件共享服务，你学习了以下操作：

- 安装 Windows File Server 软件包组
- 使用 Samba Server 配置工具创建并编辑用户列表和共享列表
- 配置 Samba 服务器在每次启动 Linux 时自动启动，通过使用服务配置工具或 `chkconfig` 命令
- 编辑你的数据包过滤配置以允许 Windows 网络流量

本章介绍的信息足以让你让 Fedora Core 4 计算机作为文件服务器运行起来。然而，如果你计划运行高流量或知名文件服务器，你应该认真考虑更高级的文档。Linux 世界中最著名的文档来源之一是 Linux 文档项目 `Linux Documentation Project`。

# 问答

- 如何从 Linux 或 Unix 系统访问 NFS 共享？

正如第 29 章所解释，你可以使用以下命令在 Linux 或 Unix 上挂载远程文件系统：

```
mount -t nfs host:/tree /point
```

将 `host` 替换为服务器主机，将 `/tree` 替换为共享目录，将 `/point` 替换为你希望文件出现的地方。例如，要将 `lack` 上的 `publicfiles` 目录挂载到本地，输入：

```
mount -t nfs lack:publicfiles /network/publicfiles
```

- 我可以使用 Samba 与 Windows 机器共享打印机吗？

可以，但由于 Windows 打印驱动程序问题，过程有时非常复杂，因此超出了本入门书籍的范围。有关使用 Samba 打印的详情，请参考在线 Samba 文档。

# 我可以使用 Mac OS 计算机提供文件吗？

是的。Mac OS X 包含使用 Windows 文件共享或 NFS 共享文件；你可以选择你喜欢的任何方法。参考你的 Mac OS 文档有关挂载 NFS 或 Windows 共享的详情。

# 工作

工作旨在帮助你预测可能的问题、回顾所学内容，并开始学习如何将知识付诸实践。

# 练习

1. `/etc/exports` 文件的作用是什么？
2. NFS 正常工作 必须使用哪种通用安全级别？
3. 如果你创建一个指向被 Linux 权限标记为只读目录的公开读/写共享会发生什么？

# 答案

1. `/etc/exports` 文件包含了你的计算机系统提供的 NFS 共享列表。
2. 为了提供 NFS 服务，必须使用 Medium 安全级别并接受端口 `111`、`369` 和 `2049`。
3. 因为 Linux 文件所有权权限优于任何 Samba 配置，没有任何远程用户能够写入被 Linux 权限标记为只读的读/写共享。

# 第 34 章

## 提供 Web 和 FTP 服务

### 在本章中你将学到：

- 如何安装并启用 Apache Web 服务器
- 如何使用 Web 服务器提供基础内容
- 如何配置 FTP 服务以允许登录和访问主目录
- 如何启用匿名 FTP 登录

在本章中，你将学习如何配置你的 Fedora Core 4 计算机系统，作为 Web 服务器或 FTP 服务器。这些服务代表了除了简单的电子邮件之外，互联网最可见的用途。它们结合在一起，可以将你的 Linux 计算机变成一个强大的互联网服务器平台。

## 在开始之前

本章经常提到前面章节中涵盖的主题。如果你没有读过这些章节或者最近没有看过，请在继续之前，考虑重新熟悉以下主题和章节：

- 使用包管理工具 `Package Management tool` 安装 Fedora Core 4 组件，见第 31 章“安装 Linux 软件”。
- 使用文本编辑器对纯文本文件进行修改，见第 5 章“在桌面上处理文件”和第 20 章“创建、编辑和保存文本文件”。
- 使用 Fedora Core 4 和 Linux 系统管理工具为指定的运行级别 `runlevel` 启用或禁用已安装的服务，见第 28 章“命令行系统管理”和第 29 章“桌面系统管理”。
- 管理 Linux 防火墙配置，包括安全级别配置工具中的“其他端口 `Other Ports`”框，见第 30 章“安全基础”。

在使用这些工具时，你会在本章中看到插图和示例；如需深入讨论，请参考上述列表中列出的章节。

正如我们之前所说的，当开始认真讨论网络服务时，某些网络术语是不可避免的。如果你完全不熟悉传输控制协议/网协议 `TCP/IP` 网络——Linux、Unix 以及大多数互联网所使用的类型——你应该考虑随手准备一份 TCP/IP 的参考资料，以帮助你理解基本概念和不熟悉的术语。

## 运行 Web 服务器

使用 Linux，你可以配置你的计算机作为 Web 服务器——这种计算机向运行在你网络或整个互联网上计算机上运行的 Web 浏览器提供 Web 内容。

Fedora Core 4 自带的 Web 服务器软件是目前世界上最流行的 Web 服务器平台，被称为 Apache Web 服务器。要使用现有 Web 内容将你的 Fedora Core 4 系统作为 Web 服务器，你必须完成以下任务：

1. 通过安装 Web 服务器软件组安装 Apache Web 服务器
2. 通过在“服务器配置工具 `Server Configuration Tools`”软件组中检查 `system-config-httpd` 安装配置 Apache Web 服务器的工具
3. 配置 Linux 在每次启动时自动启动 Apache Web 服务器
4. 配置你的 Linux 防火墙以允许与 Web 请求相关的流量

## 安装 Apache

你可以使用包管理工具安装 Apache Web 服务器。通过选择“桌面 `Desktop`”、“系统设置 `System Settings`”、“添加/删除应用程序 `Add/Remove Applications`”启动该工具。在包管理工具中，滚动到“服务器 `Servers`”类别，并如图 34.1 所示勾选“Web 服务器”包组旁边的框。然后点击“更新 `Update`”按钮安装新软件。

在使用 Apache Web 服务器之前，你还应该安装 Apache 配置工具，这样如果你决定，就可以对 Apache 的配置进行更复杂的更改。你可以按照以下步骤在软件配置工具中完成此操作：

![](img/2d355c162ea76302aa136ba324839b24_642_0.png)

图 34.1

使用包管理工具安装 Fedora Core 4 自带的 Apache Web 服务器。

1. 在包管理工具中点击“服务器配置工具”软件组旁边的“详细信息 `Details`”按钮，如图 34.2 所示。
2. 勾选 `system-config-httpd` 软件包旁框。
3. 点击“关闭”关闭详细视图，然后点击“更新”在你的系统上安装软件。
4. 注销桌面并重新登录以更新你的桌面菜单。

![](img/2d355c162ea76302aa136ba324839b24_642_1.png)

图 34.2

在“服务器配置工具”软件组的详细视图中，勾选 `system-config-httpd`

## 运行 Web 服务器

627

提供 Web 和 FTP 服务

### 配置 Apache 启动
