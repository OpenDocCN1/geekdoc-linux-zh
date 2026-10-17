
- 12. 为了确保挂载在重启后依然存在，向`/etc/fstab`文件添加以下行：

```
serverA:/usr/local /mnt/usr/local nfs defaults 0 0
```

## NFS Common用途

以下想法仅为示例：

- **共享主目录**：NFS 经常用于在网络上的多台机器间共享主目录。
- **集中软件分发**：软件可以安装在单个服务器上并由多个客户端访问。
- **数据备份和归档**：NFS 为从各种客户端备份数据提供了中心位置。
- **应用数据存储**：许多应用程序需要共享文件系统进行数据存储，NFS 可以提供这一点。

## 总结

在本章中，我们讨论了设置 NFS 服务器和客户端的过程。这在服务器端需要的配置很少。客户端端需要的配置稍微多一点。但通常来说，让 NFS 运行的过程并不困难。以下是一些需要记住的关键点：

- NFS 已经存在了很久，因此它经历了协议规范的多次修订。修订大多向后兼容，每个后续修订版本都将支持使用旧版本的客户端。
- NFS 版本 4.* 是最新的修订，包含了许多以前不可用的改进和功能。在编写本文时，NFSv4.* 可能仍然不是现实环境中部署最广泛的协议版本。然而，它是主流 Linux 发行版实现并提供的标准版本。因此，与旧的 NFSv3 相比，它正成为规范/标准。
- 旧的 NFS 协议（版本 2 和 3）被实现无状态协议。客户端无法区分崩溃的服务器和缓慢的服务器；因此，当服务器恢复时，恢复是自动的。在相反情况下，当客户端崩溃而服务器保持运行时，恢复也是自动的。
- NFSv2 和 NFSv3 中的关键服务器进程是 `rpc.stat`、`rpc.quotad`、`rpc.mount` 和 `rpc.nfsd`。这些功能的大部分已集成到 NFSv4 中。

NFS 是一个跨网络客户端共享存储卷/文件系统的强大工具。在使用它满足您的环境的资源共享需求之前，请务必花时间进行实验。

## 第 25 章 Samba

Samba 是一个强大的应用程序套，提供了服务器消息块/通用互联网文件系统 (`SMB/CIFS`) 协议的开源实现。除此之外，Samba 帮助基于 Linux 的系统与基于 Windows 的操作系统实现互操作。

Samba 透明地为 Windows 客户端以及运行其他操作系统的其他网络客户端提供文件和打印服务。它通过使用原生的微软网络协议 `SMB/CIFS` 实现这一点。从系统管理员的角度来看，这意味着您可以部署基于 Linux 的服务器，并用它为非原生 Linux 客户端（如 Microsoft Windows 系统）提供文件共享、验证、打印等服务。使用 Samba 意味着 Windows 系统可以使用它们的“母语”与 Linux 服务器通信——这意味着为您减少了许多麻烦，并为您的用户提供了无缝集成。

本章涵盖了下载、编译和安装 Samba 的步骤。对于任何这种水平的软件，Samba 都提供了极其丰富的配置选项，使其在各种环境中都非常适用且灵活。而且，幸好的是，您应该能够通过默认配置进行极少的更改就让 Samba 运行起来。我们将重点关注如何使用 Samba 执行自定义任务以及如何避免一些常见的陷阱。我们还将简要介绍一些常用的命令行工具，如 `client`。

无论您选择让 Samba 处理什么，请务必花时间阅读该程序的文档。它编写得很好、完整且详尽。

> 注意：Samba 已移植到大量平台和几乎您可以想象的任何一种 UNIX 变体，甚至还有几个非 UNIX 环境。

## SMB 的机制

为了完全理解 Linux/Samba/Windows 之间的关系，您需要理解操作系统与其文件、打印机、用户和网络之间的关系。为了比较这些关系，让我们检查在同一环境中同时使用基于 Linux 的系统和 Windows 的一些基本问题。

### 用户名和密码

Linux 的登录/密码机制与使用域控制器（DC）的 Windows Active Directory 模型完全不同。为了实现互操作性，系统管理员维护所有平台登录和密码的一致性至关重要。用户可能需要在异构环境中工作，并可能出于各种原因访问不同的平台。因此，在这些环境中尽可能实现无缝操作是很有用的，这样就无需担心用户需要在不同平台进行重新验证，无需担心与服务器不匹配的缓存密码等问题。

对于 Samba，有几种选项可以处理异构环境中的用户名和密码问题，包括以下：

- Linux 可插拔认证模块 (`PAMs`)：允许您针对 DC 验证用户。这意味着您仍然有两个用户列表——一个本地的，一个在 DC 上——但用户只需要在 Windows 系统上跟踪它们的密码。
- Samba 作为 DC：允许您让所有的 Windows 机器通过 Samba 进行身份验证。当 Samba 配合轻量级目录访问协议 (`LDAP`) 后端使用时，您将获得一个可扩展且灵活的解决方案。
- 自定义脚本：允许您使用自己的自定义脚本。对于已经建立了良好的登录和密码维护系统的站点，编写一个自定义脚本并不是不合理的。这可以使用具有良好跨平台支持的脚本语言来完成。此类脚本可以被诱导安全访问管理器 (`SAM`) 发生更改以更新 DC 的密码列表。例如，Linux 端的 Perl 或 Python 脚本可以与 Windows 端的 Perl 或 Python 脚本通信以保持账户同步。（Perl 和 Python 都已通过各种机制成功移植到 Windows 平台。）

在最坏的情况下，您始终可以手动维护不同平台的用户名和密码数据库（一些早期的系统管理员确实这样做过！但这种方法容易出错，而且管理起来并不有趣。

### 加密密码

基于 Windows 的系统在与 DC 以及任何请求验证的服务器（包括 Linux 和 Samba）通信时使用加密密码。然而，Windows 使用的加密算法与 Linux 不同，因此不兼容。

> 注意：随着微软 Active Directory 的出现，您可能不再需要 `nmbd` 服务，但现实是您仍然需要，特别是如果您打算让网络上非常老的 Windows 主机访问您的 Samba 共享。

## 通过 RPM 安装 Samba

大多数 Linux 发行版都有 Samba 的预编译二进制文件。本节将展示如何在基于 Red Hat Package Manager (`RPM`) 的发行版（如 Fedora、RHEL、CentOS 等）上安装 Samba。提供 Samba 的服务端服务需要三个包：

- `samba.rpm`：此包提供一个 SMB 服务器，可为 SMB/CIFS 客户端提供网络服务。
- `samba-common*.rpm`：此包提供了 Samba 服务端和客户端包所需的文件——例如配置文件、日志文件、页面、`PAM` 模块和其他库。
- `samba-client*.rpm`：此包提供了 SMB 客户端工具，允许在 Linux 和非 Linux 类型系统中访问 SMB 共享和打印服务。该包用于 Fedora、openSUSE 和其他 RHEL 类型系统。

假设您已连接到互联网，安装 Samba 可以像使用以下命令一样简单：

```
master@fedora-server ~$ sudo dnf -y install samba
```

运行以下命令安装 `samba-common-tools` 包：

```
master@fedora-server ~$ sudo dnf -y install samba-common-tools
```

您可以以类似的方式安装 `samba-client` 包：

```
master@fedora-server ~$ sudo dnf -y install samba
```

## 通过 APT 安装 Samba

在 Debian 类发行版（如 Ubuntu）中，Samba 的核心组件被分为 `samba*.deb` 和 `samba-common*.deb` 包。在 Ubuntu 中安装 Samba 的客户端和服务端组件只需运行：

```
master@ubuntu-server ~$ sudo apt-get -y samba
```

安装完成后，Ubuntu 会自动启动 Samba。

## Samba 管理

本节介绍了典型的 Samba 功能。您将学习如何启动和停止 Samba 以及如何进行管理。

### 启动和停止 Samba

在我们启用了 systemd 的 Linux 服务器上，可以使用 `systemctl` 工具管理 Samba 的启动和关闭。

例如，要启动 `smbd` 守护进程，可以执行：

```
master@fedora-server ~$ sudo systemctl start smbd
```

要停止它，输入：

```
master@fedora-server ~$ sudo systemctl stop smbd
```

对 Samba 进行任何更改后，可以使用此命令重启以使更改生效：

```
master@fedora-server ~$ sudo systemctl restart smbd
```

默认情况下，`smbd` 服务可能在下次重启时不会自动启动。您可以在现代发行版中使用 `systemctl` 命令确保 `smbd` 服务单元在系统启动时自动启用，如下：
