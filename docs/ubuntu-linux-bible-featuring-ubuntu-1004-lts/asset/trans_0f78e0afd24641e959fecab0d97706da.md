

# 第 35 章：设置 Samba 服务器

在最新进展中

## 简介 Samba

根结底，Windows 系统中存储的数据可能比任何其他类型的计算机系统都要多。这些 10-GB 的家庭和办公系统加起来形成了海量的 Windows 文件系统，存储着惊人的数据量。Samba 让 Linux 用户能够访问 Windows 文件系统，但更常被 Windows 用户用于访问 Linux、UNIX 和类 UNIX 系统。Samba 通过提供一个与 Windows 系统之间的网络化文件和打印机共享协议兼容的网络接口来实现这一功能。对于 Windows 系统来说，运行 Samba 的 Linux 系统看起来完全就像一个在网络上共享文件系统的随机 Windows 系统。这使得 Windows 用户能够利用 Linux 系统的速度、威力和存储容量，而无需察觉到他们正在访问 Linux 文件系统。

Samba 是一个免费且令人印象深刻的接口，允许 Linux、UNIX 以及其他类型的系统与任何可以使用 SMB 协议进行通信的网络设备进行交互，最著名的是提供文件、目录和打印机访问的 Windows 系统。Samba 让 Windows 用户能够像访问其他 Windows 共享文件系统或网络资源一样访问 Linux 文件系统和资源。例如，通过在网络中的 Linux 系统上运行 Samba，Windows 用户可以将他们的家目录挂载为网络 Windows 驱动器，并像使用其他网络打印机一样自动打印到 Linux 打印机。Samba 由 Andrew Turnbull 编写，它是人类开发的最令人印象深刻的互操作性作品之一。

Samba 包含了客户端和服务器软件 —— 句话说，允许用户从 Linux 机器到网络上 SMB 主机的客户端软件，以及为你的 Linux 提供 SMB 接口的服务器软件。使用 Samba 客户端软件将在第 26 章“文件传输与共享”中讨论。本章重点在于介绍如何安装和设置 Samba 服务器。

一个 Samba 服务器实际上由两个进程组成，这两个进程都可以从命令行启动，也可以将其集成到系统启动程序中。这两个进程是 `smbd`（Samba 守护进程，为 Windows 客户端提供文件共享和打印服务）和 `nmbd`（NetBIOS 服务器，将 Windows SMB 请求中使用的 NetBIOS 节点映射到 Linux 系统使用的 IP 地址）。Samba 守护进程通过修改其配置文件 `/etc/samba/smb.conf` 进行配置。在 Ubuntu 系统上，配置你想要通过 Samba 出的特定目录的最简单且最标准的方法是手动修改 Samba 配置文件，正如后文章节“Samba 服务器配置要点”中讨论的那样。

Linux 和 Windows 系统之间的互操作性不仅仅需要 Samba。虽然 Samba 对网络 Windows 文件系统的支持，但 Linux 内核提供了对访问物理 Windows 文件系统（如 FAT 和 NTFS）协议的内置支持，使得 Linux 用户可以通过 `/etc/fstab` 中的条目挂载 Windows 文件系统，就像挂载其他文件系统资源一样。

# 注意

Ubuntu 仓库提供了 Samba 的当前版本以及下一个版本 Samba 4 的初步软件包。本章侧重于 Samba 的当前版本（Samba 3.x），因为它是完全稳定的。尽管 Samba 将在性能、功能和灵活性方面提供改进，但它目前尚未准备好投入生产环境。请保持关注！

## 安装 Samba 服务器及相关组件

Samba 客户端包默认安装在 Ubuntu 桌面系统中，使得任何 Ubuntu 系统都能轻松地访问并连接来自 Microsoft Windows 系统或 Samba 服务器的 SMB/CIFS 共享目录。要安装运行和监控 Samba 服务器所需的包，以便从你的 Ubuntu 系统共享目录，你必须使用你喜欢的包管理工具（Synaptic、Adept 或 apt-get）安装 `samba` 包。有关安装和使用这些包管理工具的详细信息，请参见第 19 章“添加、删除和更新软件”。

在安装 `samba` 包时，你可能还想安装 `samba-doc` 包，它们分别所有官方项目文档的 HTML 和 PDF 版本，以及 Samba 项目负责人之一 John H. Terstra 的《Samba-3 by Example: Practical Exercises in Successful Samba Deployment》（Prentice Hall, 2005, ISBN:013188221X）第一版的 PDF 副本（这本书的第一版现在采用 GPL —— 有更新印刷版）。

## Samba 服务器配置要点

虽然存在用于配置 Samba 的图形化工具，但它们在 Ubuntu 系统上处于变化状态。之前的 Ubuntu 版本包含一个“共享文件夹”（Shared Folders）工具，允许你识别想要通过 NFS 或 Samba 导出的 Linux 目录，但该工具不再是 Ubuntu 的一部分。一个名为 `system-config-samba` 的工具最初为 Red Hat Linux 发行版开发，适用于 Ubuntu 系统，但它无法提供你在大多数情况下可能想要使用的所有配置选项。作为一个图形化工具，除非你安装了窗口管理器或桌面环境，否则它无法在 Ubuntu 服务器系统上使用。

因此，本章重点在于通过老旧但可靠的 Linux 方式进行 Samba 服务器配置 —— 使用文本编辑器编辑配置文件 `/etc/samba/smb.conf`。Samba 配置包含许多有用的注释，即以 `#` 号开头的行。它还包含许多示例性的、未启用的配置命令，即以 `;` 开头的行。这些表示你可能通过删除开头的分号来激活的配置命令。

正如你在接下来几节中看到的，编辑 `/etc/samba/smb.conf` 文件来配置 Samba 实际上非常简单，但与 Ubuntu Linux 其他系统管理环境相比，显得有些不足。

# 注意

基于 Web 的系统管理工具如 `swat`（Samba Web 管理工具）和 `webmin`（一个更通用的基于 Web 的管理环境）可以通过 Ubuntu 仓库获取，但在 Ubuntu 中正常工作之前需要特殊的配置。与其承担解释如何使用这些工具的构想性任务，我将继续等待 Ubuntu 系统上 Samba 设置和配置的桌面解决方案。

接下来的几节重点关注 Samba 配置文件中你可能需要根据环境更新的特定条目，而不是讨论整个 Samba 配置文件。在 Samba 官方文档、`samba-doc` 和 `samba-doc-pdf` 包提供的在线文档以及许多 Samba 籍之间，关于 Samba 细节的信息并不匮乏 —— 本章的其余部分专注于如何尽可能快速、方便地让其运行。

## 识别你的工作组或域

Samba 配置文件分为几个部分，每个部分由方括号内的部分名称标识。这些条目与你的 Samba 服务器的网络身份以及你如何在 `/etc/samba/smb.conf` 文件的 `[global]` 部分中对其进行身份验证有关。

定义 Ubuntu 服务器如何与 Windows 系统交互的关键条目是 `workgroup`，它标识了 Samba 服务器所属的工作组或 Windows 域。在我的一个示例系统中，它看起来如下：

```
[global]
workgroup = WVH
```

此条目识别我的系统属于名为 WVH 的 Windows 工作组或域。在这个小型家庭办公（SOHO）示例中，它是一个工作组，但这本质上是透明的 —— 这里的关键在于你的 Samba 服务器要么是你站点正在使用的工作组/域的成员，或者是你想要托管的域的主域控制器。

