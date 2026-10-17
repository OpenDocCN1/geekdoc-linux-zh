
| default-lease-time-time; | 分配给租约的秒数 |

| max-lease-time-time; | 租约的最大长度 |

| hardware-type hardware-address; | 网络硬件类型（以太网或环形）和地址 |

| filename "filename"; | 启动文件的名称 |

| server-name "name"; | 客户端启动的服务器名称 |

| next-server-name; | 加载文件名中指定的初始启动文件的服务器

## 706 第七部分：网络管理

| 条目 | 描述 |
| --- | --- |
| fixed-address address [, address ...]; | 为客户端分配固定地址 |
| get-lease-hostnames flag; | 决定是否查找并使用客户端的 IP 地址 |
| authoritative; not authoritative; | 拒绝无效的地址请求 |
| server-identifier hostname; | 指定服务器 |
| Options |  |
| option subnet-mask ip-address; | 客户端的子网掩码 |
| option routers ip-address [, ip-address...]; | 客户端子网上的路由器 IP 地址列表 |
| option domain-name-servers ip-address [, ip-address...]; | 客户端使用的域名服务器列表 |
| option log-servers ip-address [, ip-address...]; | 客户端使用的日志服务器列表 |
| option host-name string; | 客户端的主机 |
| option domain-name string; | 客户端的域名 |
| option broadcast-address ip-address; | 客户端的广播地址 |
| option nis-domain string; | 客户端的网络信息服务 (NIS) 域 |
| option nis-servers ip-address [, ip-address...]; | 客户端可以使用 NIS 服务器 |
| option smtp-server ip-address [, ip-address...]; | 客户端使用的 SMTP 服务器列表 |
| option pop-server ip-address [, ip-address...]; | 客户端使用的 POP 服务器列表 |
| option nntp-server ip-address [, ip-address...]; | 客户端使用的 NNTP 服务器列表 |
| option www-server ip-address [, ip-address...]; | 客户端使用的 Web 服务器列表 |

表 35-1 DHCP 声明、参数和选项（续）

## 章节：NFS 和 NIS

Linux 提供了多种工具用于访问连接到网络的远程文件。网络文件系统 (`NFS`) 允许你连接并直接访问另一机器上的资源，例如文件或 CD-ROM 设备。网络信息服务 (`NIS`) 维护网络上所有系统的配置文件。通过 Samba，你可以将 Microsoft Windows 网络上的客户端连接到由 Linux Samba 服务器控制的服务，如共享文件、系统和打印机（参见第 37 章）。

### 网络文件系统：NFS 和 `/etc/exports`

`NFS` 允许你将远程计算机上的文件系统挂载，就像它位于你本地系统上一样。这样做的好处是允许网络上的不同系统直接访问同一个文件系统，而无需每个系统都保留自己的副本。远程文件系统中只有一份副本，每台计算机都可以访问它。你可以在 `NFS` 网站 `nfs.sourceforge.net` 了解更多关于 `NFS` 的信息。

> 基于 BSD Unix 的 Macintosh 电脑 Mac OS X 现在支持用于文件共享的 `NFS`。要使用旧 Apple 操作系统访问 Apple 文件和打印机，你可以使用 Netatalk。Netatalk 在 Unix 和 Linux 系统上实现了经典的 AppleTalk 和 AppleShare IP 网络协议。目前的 Netatalk 网站为 `netatalk.sourceforge.net`，提供了指向常见问题（FAQ）和教程（HOW-TO）部分的链接。

### NFS 守护进程

`NFS` 运行在 TCP/IP 网络上。持有文件系统的远程计算机将其提供网络上的其他计算机。它通过导出文件系统来实现，这涉及到在名为 `/etc/exports` 的 `NFS` 配置文件中创建条目，并运行多个守护进程以支持其他系统的访问。这些包括 `rpc.mountd`、`rpc.nfsd` 和 `rpc.portmapper`。对 `NFS` 服务器的访问可以通过 `/etc/hosts.allow` 和 `/etc/hosts.deny` 控制。此处列出了 `NFS` 守护进程：

- `rpcfsd`: 接收来自远程系统的 `NFS` 请求并将其转换为对本地系统的请求。
- `rpcmountd`: 执行请求的挂载和卸载操作。
- `rpc.portmapper`: 将远程请求映射到相应的 `NFS` 守护进程。
- `rpcquota`: 提供用户磁盘配额管理。
- `rpcstat`: 当远程主机重启时提供锁定服务。
- `rpclockd`: 处理已崩溃系统的锁恢复。

注意：建议仅在本地安全网络上使用 `NFS`。如果在互联网上使用，`NFS` 将使你的系统面临不安全的访问风险。

### 启动和停止 NFS

在 Red Hat 上，你可以使用 `/etc/rc.init.d/nfs` 服务启动和关闭 `NFS` 守护进程，通过 `service` 命令 `service nfs start` 来调用它。要让 `NFS` 自动启动，可以使用 `chconfig` 或 `redhat-config-tools` 指定其运行的级别。以下示例将使 `NFS` 在 Red Hat 的运行级别 3 和 5 下自动启动：

```bash
chkconfig -level 35 nfs on
```

`nfs` 脚本将启动 `portmapper`、`nfsd`、`mountd` 和 `rquota` 守护进程。要启用 `NFS` 锁定，请使用 `nlock` 脚本。该脚本将使用 `stat` 和 `lockd` 守护进程。`NFS` 锁定可以为远程主机系统崩溃引起的中断操作提供更好的恢复。

要查看 `NFS` 是否真的在运行，你可以像这里一样带有 `-p` 选项的 `rpcinfo`。你应该能看到 `mount` 和 `nfs` 的条目。如果没有，说明 `NFS` 未在运行。

### NFS 分析工具

`NFS` 包还包含分析工具，你可以用它们测量 `NFS` 服务器的性能。`nfsstat` 将在指定的测试目录上生成性能数据，基于一系列不同的 `NFS` 生成分析负载（在服务器上）。

# 第 36 章：FS 和 NIS

会导致某些文件系统出现问题。如果导出的目录实际上是较大文件系统中的子目录，则会检查其父目录以确保该子目录是有效目录（子树检查）。此选项在只读文件系统中运行良好，但对于可以更改文件名和目录的可写文件系统可能会导致问题。你可以使用 `no_subtree_check` 选项取消此检查。

| 通用选项 | 说明 |
| --- | --- |
| secure | 要求请求源自安全端口，小于 1024。默认开启。 |
| insecure | 关闭仅限安全的选项。 |
| ro | 仅允许只读访问。这是默认值。 |
| rw | 允许读/写访问。 |
| sync | 在请求时执行所有写入操作。这是默认值。 |
| async | 在服务器准备好时执行所有写入操作。 |
| no_wdelay | 立即执行写入，不检查它们是否相关。 |
| wdelay | 检查文件是否已写入，如果是，则等待合并执行。这可能会降低性能。这是默认值。 |
| hide | 自动隐藏作为另一个导出目录子目录的导出目录。子目录必须显式挂载才能访问。挂载父目录不允许访问。这是默认值。 |
| no_hide | 不隐藏作为另一个导出目录子目录的导出目录（与 hide 相反）。仅对单主机有效，且可能不可靠。 |
| subtree_check | 检查文件系统中的父目录以验证导出的子目录。这是默认值。 |
| no_subtree_check | 不检查文件系统中的父目录以验证导出的子目录。 |
| insecure_locks | 不需要锁定请求的身份验证。用于旧版本的 NFS。 |

| 用户 ID 映射 | 说明 |
