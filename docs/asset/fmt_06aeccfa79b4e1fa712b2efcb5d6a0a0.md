
可用命令：

- `cd path` 将远程目录更改为 'path'
- `chmod mode path` 将 'path' 的权限更改为 'mode'
- `chown own path` 将文件 'path' 的所有者更改为 'own'
- .....输出已截断......

注意，某些命令与第 17 节中讨论的 FTP 命令看起来非常相似。除其他外，如果你忘记了正在查找的文件的全名，`sftp` 会非常方便，因为你可以使用熟悉的 FTP 命令悠闲地浏览远程文件系统。

## OpenSSH 客户端使用的

在大多数 Linux 发行版中，SSH 客户端和 SSH 服务器的配置文件通常位于 `/etc/ssh/` 目录下。（如果你是从源代码安装的 ssh，则完整路径为 `/usr/local/ssh/etc/`）。如果你想对 SSH 客户端默认设置进行任何范围范围修改，你需要修改 `/etc/ssh/ssh_config` 文件或等效文件。

> 注意：请记住 `sshd_config` 文件用于服务器守护进程的，而 `ssh_config` 文件用于 SSH 客户端！请注意服务器配置文件名中的字母“d”代表守护进程 (daemon)。

在用户的家目录下，SSH 信息存储在 `username/.ssh` 目录中。这也被用于防止中间人攻击。当主机密钥发生变化时，SSH 会提醒你。如果密钥由于有效原因发生变化——例如服务器重新安装了——你需要编辑 `known_hosts` 文件并删除引用已更改服务器标识的行。

## 总结

Secure Shell 工具是 Telnet 更优替代方案。采用 OpenSSH 包将你加入许多其他禁用了 Telnet 访问的服务器和网络管理员。以下是需要记住的关键问题：

- SSH 易于安装
- 无费即可替换 Telnet
- SSH 存在于许多平台
- 仅使用 SSH 并不会让它神奇地变得安全

## NFS 背后的协议

NFS 协议多年来一直在演变和变化。标准委员会帮助 NFS 演进，以利用新技术以及适应使用模式的变化。在编写此时，存在三个广版本的协议版本：NFS 第2 版 (`NFS2`)、`NFS` 第3 版 (`NFSv3`) 和 NFS 第4 版 (`NFSv4`)。虽然以前也存在过 NFS 第1 版，但它完全是 Sun Microsystems 内部使用的，因此从未问世。

`NFSv2` 是这三者中最旧的。`NFSv3` 是标准版本，也是最新的版本。可能应该尽量避免 `NFSv2`，仅出于遗留考虑考虑它。如果追求稳定性和广泛的客户端支持，应该考虑 `NFSv3`。如果需要其前沿功能，并且可能用于不需要向后兼容问题的新部署，则应该考虑 `NFSv4`。

在决定考虑哪个版本的 NFS 时，可能最重要的因素是你的 NFS 客户端所使用的版本。

以下是每个 NFS 版本的一些特性：

- `NFSv2`：挂载请求是基于主机的授予的，而不是基于用户的。此版本使用传输控制协议 (`TCP`) 或用户数据报协议 (`UDP`) 作为其传输协议。版本 2 的客户端可以访问的文件大小限制小于 2GB。
- `NFSv3`：此版本包含许多对 NFS Bug 的修复。它比版本 2 更多功能，性能比版本 2 有提升，并且可以使用 `TCP` 或 `UDP` 作为其传输协议。取决于 NFS 服务器本身的本地文件系统限制，客户端可以访问大于 2GB 的文件。挂载请求也是基于主机的授予的，而不是基于用户的。
- `NFSv4`：该版本的协议使用有状态的协议（如 `TCP` 或流传输协议 `TCP`）作为传输。得益于对 Kerberos 的支持，它改进了安全功能；例如，客户端身份验证可以基于用户进行。它的设计考虑了互联网环境，因此该版本的协议对防火墙友好，并监听在已知端口 `2049` 上。不再需要 `portmap` 服务；它包含了对文件访问控制 (`ACL`) 属性的支持，并可以同时支持第2版和第3版。`NFSv4` 引入了伪文件系统的概念，允许客户端通过单一协议查看并访问在 NFS 服务器上导出的文件系统。它结合了以前分散的 NFS 协议（如 `rpc_mountd`、`rpc_lockd` 和 `rpc_statd`）。客户端可以在挂载时通过挂载选项指定使用的版本。要让客户端使用特定的 NFS 版本，必须指定 `nfsvers` 选项（例如 `nfsvers=3`）。本章的其余部分主要集中在 `NFSv3` 和 `NFSv4` 上，因为它们非常稳定、广为人知，并且具有广泛的跨平台支持。

## NFS 的安全性考虑

在默认状态下，NFS 不是一种安全的磁盘共享方法。适用于保护网络服务的规则也适用于保护 NFS 安全。你应该能够信任访问你服务器的客户端，但如果你无法保证这一点，就应该采取相应措施来缓解安全问题。例如，如果你在客户端和服务器上都是 root 用户，那就没什么好担心的！你还应该严格考虑使用 NFS 标志，例如 `root_squash`。如果你无法完全信任需要共享的对象，那么花费精力寻找替代的共享方法（如只读共享）是值得的。请始终关注计算机应急响应小组 (`www.cert.org`) 的最新安全公告，并跟进你发行发行版的所有补丁。

## 挂载与访问

客户端请求挂载服务器导出的文件系统涉及几个步骤（这些步骤主要涉及 `NFSv2` 和 `NFSv3`）：

1. 客户端联系服务器的 `portmapper`，以找到哪个端口被分配为 NFS 挂载服务。
2. 客户端联系挂载服务并请求挂载文件系统。挂载服务检查客户端是否有权限挂载请求的分区（客户端挂载的权限基于 `/etc/exports` 文件中的指令或选项）。如果客户端有权限，挂载服务将返回确认。
3. 客户端再次联系 `portmapper`——这次是为了确定 NFS 服务器位于哪个端口（通常，这是 `2049` 端口）。
4. 每当客户端想要向 NFS 服务器发送请求时（例如，读取目录），就会向 NFS 服务器发送一个 `RPC`。
5. 当客户端完成操作后，它会更新自己的挂载表，但不通知服务器。

通知服务器是没有必要的，因为服务器不会跟踪所有挂载了其文件系统的客户端。服务器不维护关于客户端的状态信息，客户端也不维护关于服务器的状态；客户端和服务器无法区分崩溃的服务器和运行缓慢的系统。因此，如果 NFS 服务器重启，理想情况下，所有客户端都应该在服务器恢复上线后自动恢复与服务器的操作。

## 在 Fedora、RHEL 和 CentOS 中启用 NFS

几乎所有主要的 Linux 发行版都以某种形式支持 NFS。管理员留下的唯一任务就是配置并启用它。在我们的示例 Fedora 系统上，启用 NFS 是很的。

由于 NFS 第3 版（旧版）及其辅助程序是基于 RPC 的，因此你首先需要确保系统 `rpcbind` 已安装并运行。首先确保系统上安装了 `rpcbind` 包。在 Fedora 发行版中，输入以下命令：

```bash
root@fedora-server ~# rpm -q rpcbind
```

如果输出显示软件未安装，你可以运行以下命令使用 `dnf` 安装它：

```bash
root@fedora-server ~# dnf -y install rpcbind
```

在 Fedora 等启用 `systemd` 的 Linux 发行版上检查状态，可以使用 `systemctl` 命令：

```bash
root@fedora-server ~# systemctl status rpcbind.service
```

如果 `rpcbind` 服务已停止，可以这样启动它：

```bash
root@fedora-server ~# systemctl start rpcbind.service
```

在使用之前，使用 `rpcinfo` 命令查看可能注册到 `portmap` 的任何 RPC 服务的状态：

```bash
root@server ~# rpcinfo -p
program vers port service
100000 4 tcp 111 portmapper
100000 4 udp 111 portmapper
...<OUTPUT TRUNCATED>...
```

由于示例系统上尚未运行 NFS 服务，输出可能不会显示许多 RPC 服务。要在 Fedora 等启用 `systemd` 的 Linux 发行版上启动 NFS 服务，可以输入以下命令：

```bash
root@fedora-server ~# systemctl start nfs.service
```

再次运行 `rpcinfo` 命令查看向 `portmapper` 注册的 RPC 程序状态，显示如下：

```
root@server ~# rpcinfo -p
program vers port service
100000 4 tcp 111 portmapper
...<OUTPUT TRUNCATED>...
100003 4 tcp 2049 nfs
100005 1 udp 32892 mountd
```

该服务在 Fedora 系统上默认是禁用的；输入以下命令将其设置为自动启动：
`[root@fedora-server ~]# systemctl enable nfs-server`

## 在 Ubuntu 中启用 NFS

在 Ubuntu 中安装并启用 NFS 服务器与安装以下组件一样简单：`nfs-common`, `nfs-kernel-server`, 以及 `rpcbind`。

要使用高级软件包工具 (`APT`) 启用这些服务，请运行以下命令：

```
master@ubuntu-server:~$ sudo apt-get -y install nfs-common nfs-kernel-server rpcbind
```

安装过程将自动为你启动 NFS 服务器及其所有相关的从服务。你可以运行以下命令来检查状态：

```
master@ubuntu-server:~$ rpcinfo -p
```

要停止 Ubuntu 上的 NFS 服务器，请输入以下命令：

```
master@ubuntu-server:~$ sudo /etc/init.d/nfs-kernel-server stop
```

## NFS 的组件

NFS 协议的第 2 和第 3 版本严重依赖 RPC 来处理客户端与服务器之间的通信。Linux 中的 RPC 服务由 `portmap` 服务管理。如前所述，此辅助服务在 `NFSv4` 及更高版本中不再需要。

以下列表显示了 Linux 下促进 NFS 服务的各种 RPC 进程。这些 RPC 进程主要适用于 NFS 版本 2 和 3，但文中也提到了在 `NFSv4` 中的适用情况。

- `statd`：此进程负责在 NFS 服务器在未正常关闭的情况下重启时，向客户端发送通知。它向 `rpc.lockd` 提供有关服务器的状态信息。这是通过网络状态管理器 (`NSM`) RPC 协议实现的。这是一个可选服务，在 Fedora 系统上由 `nfslock` 服务自动启动。它在 `NFSv4` 中不需要。
- `quota`：顾如其名，`rpc.quota` 提供了 NFS 与配额管理器之间的接口。NFS 用户/客户端将受到配额限制，这些限制与它们在本地文件系统（而非 NFS）上工作时将适用的限制相同。它在 `NFSv4` 中不需要。
- `mount`：当请求某个分区时，`rpc.mount` 守护进程负责验证客户端是否具有相应的权限发出该请求。该权限存储在 `/etc/exports` 文件中。（接下来的章节“/etc/exports 配置文件”将为你介绍更多关于 `/etc/exports` 文件的内容。）它由 NFS 服务器初始化脚本自动启动。它在 `NFSv4` 中不需要。
- `nfsd`：NFS 系统的核心组件，即 NFS 服务器/守护进程。它与 Linux 内核配合，根据需要加载或卸载内核模块。当然，它在 `NFSv4` 中仍然相关。
- `rpc.lockd`：`rpc.statd` 守护进程使用此守护进程来处理系统崩溃后的恢复。NFS4 不再使用 `nfslock` 服务。
- `rpc.idmapd`：这是 NFS4 ID 映射守护进程。它为 NFS4 客户端/服务器提供此功能，将用户组 ID 转换为名称，反之亦然。
- `rpc.gssd`：这是服务器端的 `rpcsec_gss` 守护进程。`rpcsec_gss` 协议允许使用 `gss-api` 通用 API 在 NFS4 中提供高级安全防护。
- `rpc.gssd`：为 NFS4 及更高版本中的身份验证机制提供客户端传输机制。

> **注意** 你应该理解，NFS 本身是一种基于 RPC 的服务，无论协议版本如何。因此，即使是 NFS4，它本质上也是基于 RPC 的。这里的关键在于，大多数以前使用的辅助和独立基于 RPC 的服务（如 `mountd` 和 `statd`）已不再需要，因为它们单独的功能已经整合到了 NFS4 守护进程中。

## 内核对 NFS 的支持

在不同的 Linux 发行版中，NFS 以两种形式实现。大多数发行版在内核中都默认启用了 NFS 支持。少数 Linux 发行版还以独立守护进程的形式提供 NFS 支持，该守护进程可以通过软件包安装。从 Linux 2.2 开始，就有基于内核的 NFS 支持，其运行速度明显快于早期的实现。在编写本文时，基于内核的 NFS 服务器支持被认为是标准做法。它并不是强制性的——如果你没有将该支持编译到内核中，你就无法使用它。然而，如果你有机会尝试内核对 NFS 的支持，强烈建议你这样做。如果你选择不使用，也不必——处理 NFS 服务器服务的 `nfsfd` 程序是完全自包含的，并提供了提供 NFS 所的所有内容。

> **注意** 另一方面，客户端必须在内核中支持 NFS。这种内核支持已经存在很长时间，并且以稳定著称。几乎所有现代 Linux 发行版都默认启用了内核对 NFS 的支持。

## 配置 NFS 服务器

设置 NFS 服务器是一个两个步骤的过程。第一步是创建 `/etc/exports` 文件，该文件定义了服务器文件系统或磁盘的哪些部分与网络其他部分共享，以及共享的规则（例如，仅允许客户端对文件系统具有读取权限，但也允许对文件系统进行写入）。

## /etc/exports 配置文件

此主配置文件列出了可共享的文件系统、可以共享的主机以及对应的选项 `/etc/exports` 的格式简单如下：

```
/directory/to client(mask) options...
```

每个条目的格式在此处解释：

- `/directory/to`：要导出的目录路径。
- `client`：允许访问的主机（主机）。
- `(mask)`：子网掩码。
- `options`：选项。

此处解释了每个条目的格式：

- `/directory/to`：要导出的目录路径。
- `client`：允许访问目录的主机。
- `(mask)`：如果指定了网络，则掩码。
- `options`：权限和设置（例如 `rw`, `ro`）。

选项包括：

- `ro`：只读。
- `rw`：读写。
- `no_root_squash`：允许客户端的 root 用户拥有 root 权限。
- `root_squash`：将客户端的 root 用户映射为匿名用户。
- `all_squash`：将客户端的所有用户映射为匿名用户。

这是一个 `/etc/exports` 文件的示例：

```
/home  192.168.1.0/24(rw,no_root_squash)
/data  any(ro,root_squash)
```

## 安全选项

`exports` 文件中的选项控制导出目录的安全。

- `secure`：省略此选项时的默认设置。客户端必须使用特权端口（1024 以下）。
- `insecure`：允许客户端从任何端口连接。这对于无法使用特权端口的客户端通常是需要的。
- `root_squash`：将客户端的 root 用户映射为匿名用户（通常为 "nobody"）。
- `no_root_squash`：允许客户端在服务器上拥有 root 权限。
- `all_squash`：将客户端的所有用户映射为匿名用户。

## 通知 NFS 服务器 /etc/

一旦写好了 `/etc/exports` 文件，使用 `exportsfs` 命令通知 NFS 服务器重新读取配置。`exportsfs` 的参数如下：

| exportsfs 选项 | 说明 |
|---|---|
| `-a` | 导出 `/etc/exports` 中的所有条目。当与 `u` 选项使用时也可导出文件系统——例如 `exportsfs -ua`。 |
| `-r` | 重新导出 `/etc/exports` 中的所有条目。这将 `/var/lib/nfs/stab` 与 `/etc/exports` 的内容同步。例如，它会删除 `/var/lib/nfs/stab` 中不再存在的条目。 |
| `-u clientA:/dir/to/mount` | 从主机 `clientA` 取消导出 `/dir/to/mount`。 |
| `-o options` | 此指定的选项与表 23-1 相同。这些选项仅适用于命令行命令行指定的文件系统，而不是 `/etc/exports` 中的。 |

以下是 `exportsfs` 命令行的示例。
要导出 `/etc/exports` 中指定的所有文件系统，请输入：

```
[root@server ~]# exportsfs -a
```

要以读写和 `no_root_squash` 权限将 `/usr/local` 目录导出给 `clientA`，请输入：

```
[root@server ~]# exportsfs -o rw,no_root_squash clientA:/usr/local
```

在大多数情况下，你只想使用带有 `-r` 选项的 `exportsfs`（意味着重新导出所有目录并完成其他清理工作）。

## showmount 命令

在配置 NFS 时，你会发现使用 `showmount` 命令来检查所有操作是否运行正常非常有帮助。该命令用于显示 NFS 服务器的挂载信息。

通过使用 `showmount` 命令，你可以快速判断你是否已正确配置了 `nfsd`。

在你配置了 `/etc/exports` 文件并使用 `exportfs` 导出了所有文件系统后，可以运行 `showmount -e` 来查看本地 NFS 服务器上导出的文件系统列表。`-e` 选项告诉 `showmount` 显示 NFS 服务器的导出列表。这是一个示例：

```
[root@server ~]# showmount -e localhost
Export list for localhost:
home *
```
