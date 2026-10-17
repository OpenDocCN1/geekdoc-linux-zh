
NFS 是一个用于跨网络客户端共享存储卷/文件系统的强大工具。在使用它尝试满足您的环境资源共享需求之前，请务必花一些时间对其进行实验。

# 第 24 章 Samba

Samba 是一套强大的应用程序包，可帮助基于 UNIX 的系统（如 Linux）与基于 Windows 的其他操作系统实现互操作。它是服务器消息块/通用互联网文件系统（SMB/CIFS）协议套件的开源实现。

Samba 能够透明地为 Windows 客户端以及运行其他操作系统的其他网络客户端提供文件和打印服务。它通过使用原生的微软网络协议 SMB/CIFS 实现这一点。从系统管理员的角度来看，你可以部署一个基于 Linux/UNIX 的服务器，并用它为非原生 Linux 客户端（如 Microsoft Windows 系统）提供文件共享、身份验证、打印和其他服务。Samba 意味着系统可以使用它们的母语言与 Linux 服务器进行通信——这为您减少了麻烦，并为您的用户实现了无缝集成。

与任何同水平的软件一样，Samba 提供了丰富的配置选项，这使其在各种环境中使用都非常合适且灵活。但庆幸的是，你应该能够对默认配置进行极少数更改即可让 Samba 运行起来。我们将重点关注如何使用 Samba 执行自定义任务、如何避免某些 Samba 陷阱，并简要介绍如 `smbclient` 等一些命令行实用程序。

无论你选择 Samba 处理什么内容，请务必花时间阅读该程序的文档。它编写得很好、完整且详尽。只需花一个下午的时间读完大部分内容，你就能获得大量的知识。

> 注意：Samba 已经移植到大量平台——你所想象的几乎任何 UNIX 变体，甚至还有几个非 UNIX 环境。在本文讨论中，我们自然对感兴趣的是基于 Linux 平台上的 Samba，但请记住，Samba 也可以部署在其他平台上。

# SMB 的机制

为了完全理解 Linux/Samba/Windows 之间的关系，你需要理解操作系统与其文件、打印机、用户和网络之间的关系。为了比较这些关系，让我们来看一下在同一环境中同时与基于 Linux 的系统和 Windows 工作时的一些基础性问题。

## 用户名和密码

Linux/UNIX 的登录/密码机制与 Windows Active Directory 在登录和域控制器（DC）中的一致性有着本质的差异。因此，系统管理员在两个平台之间维护一致性至关重要。用户可能需要在异构环境中工作，并可能出于各种原因访问不同的平台。让此类环境下的工作尽可能无缝是很有用的，这样就无需担心用户是否需要在不同平台之间重新进行身份验证，无需担心服务器之间缓存密码不匹配以及其他问题。

相对于 Samba 来说，有几种选项可以处理异构环境中的用户名和密码问题，包括以下项：

- **Linux 可插拔认证模块 (PAMs)**：这意味着你有两个用户列表——一个在本地，一个在 DC 上——但你的用户只需要在 Windows 系统上记住他们的密码即可。
- **将 Samba 作为 DC**：允许你在 Linux 系统上保留所有的登录名和密码，而你的 Windows 机器通过 Samba 进行身份验证。当 Samba 配合轻量目录访问协议（LDAP）后端使用时，你将获得一个可扩展且灵活的解决方案。
- **自定义脚本**：允许你使用自己的自定义脚本。对于那些拥有完善的登录和密码维护系统的站点来说，编写自定义脚本是不现实的。这可以使用具有良好跨平台支持的脚本语言来完成。此类脚本可以被引导以允许安全访问管理器（SAM）始终更新 DC 的密码列表。例如，Linux 端的 Perl 或 Python 脚本可以与 Windows 端的 Perl 或 Python 脚本进行通信（Perl 和 Python 都已通过各种机制成功移植到 Windows 平台）。

在最坏的情况下，你始终手动维护不同平台的用户名和密码数据库（某些早期系统管理员确实这样做过！），但这种方法容易出错且不利于管理。

## 加密密码

基于 Windows 的系统与 DC 以及任何需要身份验证的服务器（包括 UNIX 和 Samba）通信时使用加密密码。然而，Windows 使用的加密算法与 UNIX 不同，因此是不兼容的。

以下是你处理此冲突的选项：

- 编辑 Windows 客户端上的注册表以禁用加密密码。需要更改的注册表项列在 Samba 包的 `docs` 目录中。对于 Samba 3 版本，此选项已不再需要。
- 配置 Samba 使用 Windows 风格的加密密码。

第一种方案的优点是不会强制你转向更复杂的密码方案。另一方面，你可能必须在所有客户端上应用注册表修复。第二种方案的效果显然相反：通过在服务器端增加一点复杂性，你就不需要修改任何客户端。

## Samba 守护进程

`nmbd` 守护进程负责处理 NetBIOS 名称服务请求。`nmbd` 也可以作为 Windows 互联网名称服务器（WINS）的替代品。它开始绑定到端口 137；但与 `smbd` 不同，`nmbd` 不会为每个查询都创建一个新实例。除了名称服务请求外，`nmbd` 还处理来自主浏览器、域浏览器和 WINS 服务器的请求——因此，它参与了构成 Windows 系统网络位置的浏览协议。`smbd` 和 `nmbd` 守护进程提供的服务互为补充。

最后，`winbind` 的服务可用于查询原生 Windows 服务器的用户和组信息，这些信息可以在纯 Linux/Unix 平台上使用。它通过远程过程调用（RPC）调用、PAM 以及现代 C 库中的服务切换（NSS）功能来实现。这种用法可以通过使用 PAM 模块（`pam_winbind`）来扩展身份验证服务。该服务与主 `smb` 服务分开控制并可以独立运行。

# 通过 RPM 安装 Samba

大多数 Linux 发行版都有 Samba 的预编译二进制文件。本节将介绍如何在 Fedora 发行版通过红帽软件包管理器（RPM）安装 Samba。为了提供 Samba 的服务端服务，在 Fedora、CentOS 和红帽企业 Linux (RHEL) 类系统上需要三个软件包：

- `samba*.rpm`：此包提供一个 SMB 服务器，可为 SMB/CIFS 客户端提供网络服务。
- `samba-common*.rpm`：此包提供 Samba 服务端和客户端所需的文件——如配置文件、日志文件、手册页、PAM 模块和其他库。
- `samba-client*.rpm`：此包提供 SMB 客户端工具，允许访问 Linux 和非 Linux 系统上的 SMB 共享和打印服务。该包用于 Fedora，

openSUSE 以及其他 RHEL 类型的系统。

假设你已经连接到互联网，安装 Samba 只需执行此命令：

```
[root@fedora-server ~]# dnf -y install samba
```

运行以下命令安装 `samba-common-tools` 包：

```
[root@fedora-server ~]# dnf -y install samba-common-tools
```

你也可以类似地安装 `samba-client` 包：

```
[root@fedora-server ~]# dnf -y install samba-client
```

你也可以选择常用的 RPM 命令从发行版安装介的 `/mount_point/Packages/`目录下安装 RPM 包。例如，如果安装介挂载在 `/media/dvd`，你可以输入：

```
[root@fedora-server ~]# rpm -ivh /media/dvd/Packages/s/samba-*.rpm
```

## 通过 APT 安装 Samba

在 Ubuntu 等类 Debian 派发行版中，Samba 软件的核心组件被分为 `samba.deb` 和 `samba-common*.deb` 包。在 Ubuntu 中安装 Samba 客户端和服务器组件与运行以下 apt-get 命令一样简单：

```
master@ubuntu-server:-$ sudo apt-get -y install samba
```

与在 Ubuntu 下安装大多数其他服务一样，安装程序会在安装后自动启动 Samba 守护进程。

## 从源码编译并安装 Samba

大多数 Linux 发行版以二进制格式预装了 Samba。但与本书中讨论的所有其他应用程序一样，如果你想将包升级到新版本，就应该能够编译该软件。自诞生以来，Samba 拥有跨越许多 UNIX/Linux 平台的用户，因此它的设计能够兼容许多变体。在编译过程中很少出现问题。

我们使用 Samba 4.3.0 版本进行编译，因此请记住将后续步骤中所有对版本号（4.3.0）的引用更改为适应你正在使用的版本。

首先，从 www.samba.org 下载 Samba 源码到你想要编译的目录。例如，假设该目录为 `/usr/local/src`。你可以直接从 https://www.samba.org/samba/ftp/samba-latest.tar.gz 下载最新版本。

1. 在下载软件的目录中，使用 `tar` 命令解压 Samba：

2. 步骤 1 创建了一个名称与下载的 Samba 最新版本对应的源码子目录。进入该目录：

```
[root@server src]# # cd samba-4.*
```

在继续后续步骤之前，先阅读标题为 "Readme" 或类似的文件来对 Samba 构建过程进行准备工作是一个好主意。此文件提供了 Samba 的概览，告知你文档的位置等。虽然这在目前不是至关重要的，但这些信息从长远来看可能会有所帮助。

3. 我们将使用 `--prefix` 选项运行 Samba 的配置脚本以指定产物的位置。你可能想要考虑的其他选项列表 24-1 中。

### Samba 配置 (/configure) 选项

| 选项 | 说明 |
| :--- | :--- |
| --prefix=PREFIX | 在 PREFIX 指定的路径或目录下安装与架构无关的文件。 |
| --with-pam | 包含 PAM 支持（默认 = no）。 |
| --with-ads | 活动目录支持（默认 = auto）。 |
| --with-ldap | LDAP 支持（默认 = yes）。 |
| --with-pam_smbpass | 构建用于针对 passdb 后端进行认证的 PAM 模块。 |
| --with-systemd | 启用 systemd 集成。 |
| --without-systemd | 禁用 systemd 集成。 |
| --enable-cups | 开启通用 打印系统 (CUPS) 支持（默认 = auto）。 |

```
[root@server samba-4*] # ./configure --prefix=/usr/local/samba
```

4. 如果配置过程由于系统上缺少各种开发库或头文件而报错或失败，你可以使用 `dnf` 或 `apt-get` 安装任何需要的依赖，例如 `python-devel`、`gnuts-devel`、`libacel-devel`、`opensldap-dev` 等。

5. 运行 `make` 命令开始编译 Samba：

```
[root@server Name*] # make install
```

```
[root@server samba-4~] # make install
```

你发现所有的二进制文件和配置文件都安装在 `/usr/local/samba/` 目录下。你现在可以继续使用它们，就像通过 RPM/ 安装 Samba 一样。但是，你应该注意，`/usr/local/samba/bin` 目录通常不在大多数 shell 的搜索路径中。你可以将它添加到路径，或者简单地将二进制文件从 `/usr/local/samba/bin` 复制到会被搜索的位置（例如 `/usr/sbin/` 或 `/usr/bin/`）。换句话说，只要留意路径和一切，一切都会没问题的！

## Samba 管理

本节描述了一些典型的 Samba 管理功能。你将学习如何启动和停止 Samba，如何使用 Samba 执行一些管理任务，如何使用 `smbclient` 等。

### 启动和停止 Samba

大多数 Linux 发行版都有脚本和程序，可以启动和停止 Samba，而无需你做任何特殊操作。它们会处理开机时的启动和关机时的停止。在我们通过 RPM 安装 Samba 的启用 system 的 Fedora 系统上，`systemctl` 工具可以管理启动和停止。例如，要启动守护进程，你可以使用：

```
[root@server ~]# systemctl start
```

要停止服务，你可以：

```
[root@server ~]# systemctl stop
```

对 Samba 进行任何更改后，你可以重启它：

```
[root@server ~]# systemctl restart
```

在启用 system 的发行版中，smamba 服务可能不会自动启动。你可以使用 `systemctl` 确保它自动启动：

```
[root@server ~]# systemctl enable
```

不使用脚本停止 Samba 稍微复杂一些。通常情况下，你可能需要使用 `ps` 列出所有进程，找到 `smbd` 实例然后将其 `kill` 掉。

### 创建共享

我们将引导你完成在 `/tmp` 下创建共享的过程。我们将首先创建要共享的目录，然后编辑 Samba 配置文件 (`/etc/samba/smb.conf`)。如果你安装并运行了任何图形桌面环境，通常可以使用内置工具完成文件共享任务。但是，了解如何以原始形式配置 Samba 是很有用的。让我们开始吧：

1. 在 `/tmp` 下创建一个名为 `testshare` 的目录：

```
[root@server ~]# mkdir /tmp/testshare
```

2. 在步骤 1 创建的目录下创建空文件：

```
[root@server ~]# touch /tmp/testshare/{foo1,foo2,moo3}
```

3. 设置目录权限，以便系统中的其他用户浏览其内容：

```
[root@server ~]# chmod -R 755 /tmp/testshare
```

4. 使用你喜欢的任何文本编辑器打开 Samba 配置文件 (`/etc/samba/smb.conf`) 进行编辑。滚动到文件末尾，在文件底部附加条目列表。（请忽略行号 1-5。这些行仅用于提高可读性。）

```
[sample-share]

comment=此文件夹包含文档

path=/tmp/testshare

public=yes

writable=no
```

- 第 1 行是 Samba 术语中的共享名称（或“服务”）。这是 SMB 客户端尝试浏览存储在 Samba 服务器上的共享时使用的名称。
- 第 2 行只是注释，用户在浏览时会在旁边看到。
- 第 3 行非常重要。它指定了存储实际共享内容的文件系统位置。
- 第 4 行指定访问共享不需要密码（Samba 术语称为“连接到服务”）。共享的权限将转换为访客账户的权限。如果该值设置为 no，则该共享将无法被

并非面向公众，而是经过身份验证并许可的用户。
- 第 5 行，将指令的值设置为 **no**，意味着此服务的用户无法创建或修改存储其中的文件。

> **提示** Samba 的配置文件包含许多选项和指令，多到无法在此处全部列出。但您可以通过阅读 **smb.conf** 的帮助页（man **smb.conf**）来了解更多其他可能的选项。

- 5. 将更改保存到 `/etc/samba/smb.conf` 文件并退出编辑器。

请注意，我们接受了文件中所有的其他默认值。您可能希望返回并根据您的环境对某些设置进行个性化处理。

您可能想要更改的一项设置是定义工作组的 **(workgroup)** 指令。它控制了当客户端查询或在 Windows 的“我的网络位置”中查看时，您的服务器显示为哪个工作组。

另外注意，默认配置可能包含其他共享定义。如果您的目的不是包含它们，则应该注释掉（或删除）这些项目。

- 6. 使用 **testparam** 工具检查 **smb.conf** 文件的内部正确性（即是否存在语法错误）：
```
[root@server ~]# testparam -s | less
...<OUTPUT TRUNCATED>...
[samba-share]

comment = This folder contains shared documents

path = /tmp/testshare

guest ok = Yes
```
研究输出以查找任何严重错误，并尝试通过返回 **smb.conf** 文件进行修正来修复它们。

> **注意** 由于您将 **testparam** 的输出通过管道给了 **less** 命令，您可能需要按下键盘上的 Q 键来退出命令（即退出输出界面）。

- 7. 现在重启（或启动）Samba 使软件识别您的更改。在 Fedora 等启用了 **systemd** 的 Linux 发行版中，您可以使用 **systemctl** 命令通过以下方式重启动 **smb** 服务：
```
[root@fedora-server ~]# systemctl restart smb.service
```
