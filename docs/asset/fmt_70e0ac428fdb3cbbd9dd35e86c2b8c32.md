
![](img/ba933c244f3be8993f8191427d25c74c_212_0.png)

在你的 Linux 内核中，必须使用 `ipfwadm` 命令启用防火墙功能（`ipfwadm`）。这取决于你使用的 Linux 系统，这可能需要重新编译内核。向内核添加防火墙规则的命令位于防火墙配置文件中，系统每次启动时都会执行该文件。

在最新的 Linux 内核中，使用一种名为 IP Chains 的修订防火墙系统。与之前的 `ipfwadm` 系统相比，该系统在性能和安全性上都有提高。类似的工具用于基于链的防火墙（示例见下一节）。

用于管理最新内核防火墙功能的 IP Chains 包位于 CD 的 `/Source/System Tools/`。

## 在 KDE 或 Gnome 中管理防火墙

如果你还没有完全掌握 Linux 内核防火墙功能的原理，可以使用 `kfi` 防火墙工具设置基本规则来保护你的网络（见图 37.5）。该程序允许你通过图形界面查看它创建的实际防火墙规则。通过查看这些规则，新手可以学习更多防火墙知识，专家可以检查他们是否实现了目标。

## 将你的系统变为超级服务器

图 37.5 使用 `kindfire`，你可以图形化地配置规则来保护你的网络。

![](img/ba933c244f3be8993f8191427d25c74c_213_0.png)

`firewall` 在 KDE 桌面中使用。它适用于 Linux 内核的 IP Chains 功能（2.2 或更高版本）。如果你使用的是旧的 `iptables-adm` 防火墙系统，则无法使用 `kfire`。你必须以 `root` 登录才能使用 `kfire`。

`kfire` 位于 CD 上的 `/Source/System Tools/`。`/Binaries/System Tools/` 也包含一个 `rpm` 格式二进制文件。当你安装 `kfire` 时，它会被添加到你的 KDE 菜单中。

适用于 Gnome（或使用 GTK+ 图形库的用户）的类似程序是 GTK+ 防火墙控制中心 `gffcc`。该程序的源码包位于 `/Source/System Tools/`；一个 `rpm` 格式二进制文件位于 `/Binaries/System Tools/gffcc`。图 37.7 显示了 `gffcc` 的主窗口，你可以在这里开始为入站、转发和出站数据包定义防火墙规则。

# 增强你的网络安全 199

图 37.6 防火墙可以根据你的图形选择显示规则摘要。

![](img/ba933c244f3be8993f8191427d25c74c_214_0.png)

图 37.7 通过 `gfcc` 你可以为传入、转发和传出的 IP 数据包定义规则。

![](img/ba933c244f3be8993f8191427d25c74c_214_1.png)

# 200 将你的系统变为超级服务器

你在 `gfcc` 中定义的每条规则都可以包含防止拒绝服务的规范。源和目的 IP 地址以及端口也包含在每条规则中（参见图 37.8）。

图 37.8 在 `gfcc` 中定义的每条规则都可以包含此定义对话框显示的所有字段。

![](img/ba933c244f3be8993f8191427d25c74c_215_0.png)

## 克隆 Windows NT

每个操作系统都有其优缺点；因此，你为不同的任务选择不同的工具。然而，我似乎越来越对几乎所有事情都选择 Linux。在这一部分，你将学习如何使用 Linux 自带的功能，让它能够连接到你的 NetWare 和 Windows NT 服务器（以及你的 Windows 95/98/2000 系统）。Linux 系统将看起来就像另一个 Windows 客户端，这使得与那些你不了解 Linux 的系统进行交互变得更加容易。

如果你的网络中已经有了 NetWare 和 Windows NT 服务器，你将学习如何使用它们的原生协议连接到这些服务器。对于 NetWare 或 NT 服务器来说，你的 Linux 系统将看起来就像另一个 Windows 客户端。

# 38 在 Linux 上克隆 Windows NT 服务器

让你的 Linux 服务器在网络中的其他人看起来就像是一个 Windows NT 服务器，这种能力可以让其他人更容易接受你正在使用 Linux——因为他们并不知道你正在使用。

通过使用 `Samba` 服务器及其相关工具，Linux 在其他 Windows 系统（95, 98, 2000 和 NT）看来就像是另一个 Windows 系统。你的 Linux 计算机出现在 Windows 网络邻域窗口中，你可以共享文件和打印机、维护用户密码安全、定义共享等。

`Samba` 服务器是一个旨在让 Windows 使用的 `SMB` 协议适用于许多其他系统的项目，以便它们能够共享资源。目前，除 Linux 外，`Samba` 还可用于几十个 Unix 系统。所有这些系统都可以相互以及与“真实的”Windows 系统共享文件和打印机。你可以通过访问 `Samba` 组织的网站 `http://www.samba.org` 了解更多关于 `Samba` 项目的信息并阅读有关本节内容的更详细文档。镜像站点遍布全球。

在 Linux 上运行 `Samba` 服务器与使用真实的 Windows NT 服务器相比有一个明显的优势：Linux 很少崩溃。网络上的其他人可能不知道提供文件和打印共享的 Windows NT 服务器实际上是一个 Linux 系统——他们可能会赞美你没有 Windows 用户抱怨的机机。

## 设置 Samba 服务器

`Samba` 服务器套件包含大多数 Linux 发行版。如果你在安装 Red Hat 6 时没有包含 `Samba` 包（通过使用 `rpm -q samba` 命令检查），你可以从 Red Hat CD 使用此命令将其添加到你的系统：

![](img/ba933c244f3be8993f8191427d25c74c_218_0.png)

```
rpm -Uvh /mnt/cdrom/RedHat/ms/samba-2.0.3-i386.rpm
```

此外，`/Binaries/samba` 目录包含了你可以安装在 Linux 副本上的各种格式存档。源码存档也包含在 CD 的 `/Source/samba`。根据你的 Linux 发行版，你可能可以使用 `LinuxConf`（Red Hat）、`YAST`（use）或 `COAS`（Caldera）等工具来设置 `Samba` 工作。一旦安装了 `Samba` 包，`Samba` 服务器通常每次启动系统时启动。问题在于当 `Samba` 运行时，如果找不到有效的配置文件，它就会停止。你可以使用以下命令判断 `Samba` 服务器是否运行，它会搜索系统上的进程列表：

```
$ ps aux | grep .mbnd

root 556 0 1312 652 ? 13:46 smbd

root 558 0 1914 608 ? 13:46 mbnd
```
