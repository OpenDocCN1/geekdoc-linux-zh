
此设置启用 NFS 输入/输出守护进程 nfsiod，它有助于简化 NFS 客户端请求并调整一些内核设置以改善访问时间。所有这些在启动时都会在 /etc/rc.network 脚本中自动处理，同时处理 NFS 服务器设置（你之前看到的）。

## 挂载远程文件系统

挂载 NFS 共享使用 mount_nfs 命令，它是 mount -t nfs 的简写命令（如你在第 8 章“存储系统和备份实用程序”中看到的）。在最常见的形式中，你会向它传递两个参数：组合字符串中的主机和共享名称，以及本地挂载点：

```
# mount_nfs spots:/home /home2
```

成功挂载不会产生任何输出。使用 df 命令检查挂载是否成功：

```
# df
Filesystem     1K-blocks    Used   Avail Capacity Mounted on
/dev/ad0s1a      992239   54353  858507      6% /
/dev/ad0s1f    26704179 4872963 19694882     20% /home
/dev/ad0s1e      992475 1642343 7488174     18% /usr
procfs                4       0       4    100% /proc
spots:/home     9924475 1642343 7488174     18% /home2
```

如果进入 /home2 目录，你会看到 NFS 服务器上 /home 中的所有目录，每个文件的属主都会基于 UID 进行映射，正如我们之前讨论的那样。文件系统将保持挂载状态，直到你使用 umount 命令显式卸载它为止：

```
# umount /home2
```

![](img/ba0161b65b37e94cffc801ecbacaba5e_413_0.png)

> 在尝试使用 umount 卸载之前，请先离开任何 NFS 挂载的目录。如果你尝试在仍位于文件系统内部时卸载它，将会收到设备繁忙错误。

NFS 共享可以用多种不同的方式挂载，选项在 man mount_nfs 页面中列出。其中更有用的一些是 -T 选项，它强制使用 TCP 传输而不是 UDP（适用于通过长距离 WAN 链路进行的挂载）；以及 -s 和 -x <seconds> 标志，它们允许挂载在指定时间后超时并消失而失败（软挂载）。

```
# mount_nfs -s -x 60 spots:/home /home2
```

> 另一个有用的选项是 -i，它启用可中断性。通常，如果你已挂载 NFS 共享并且服务器变得无响应或无法到达，你所做的任何文件系统调用（处理共享文件的命令，例如 ls）都可能以这样的方式挂起，以至于即使按 Ctrl+C 也无法停止它们。-i 选项使得 Ctrl+C（终止信号）会强制命令失败，将控制权交还给你。

与其他文件系统类型一样，你可以将 NFS 挂载添加到 /etc/fstab 以设置预定义的挂载点，从而简化挂载过程。将你原本会传递给 mount_nfs 的任何选项放在 Options 列中，用逗号分隔：

| 设备 | 挂载点 | 文件系统类型 | 选项 | 转储 | 遍历 |
|---|---|---|---|---|---|
| spots:/home | /home2 | nfs | rw,-T,-i,noauto | 0 | 0 |

有了这样的表项，你可以使用 mount 命令挂载 NFS 文件系统：

```
# mount /home2
```

## 系统启动时自动挂载远程文件系统

/etc/fstab 中的所有文件系统在启动时都会自动挂载，除非存在 noauto 选项。你可以通过简单地将它们添加到 /etc/fstab 来指定远程 NFS 共享应在启动时挂载，就像你刚才看到的那样。然而，有一些需要注意的地方。

最值得注意的是，NFS 有一个极长的默认超时时间，而启动时挂载文件系统的阶段是一个同步、阻塞的过程。如果你的 NFS 服务器或服务器找不到——例如，如果服务器机器未运行，或者你自己的机器的网络连接未正确配置——启动过程可能会在放弃并完成启动程序之前挂起不可容忍的长时间。

你可以通过在 /etc/fstab 中放置 noauto 选项来解决这个问题，就像我们在之前的示例中看到的那样。然而，这意味着你必须在系统完全启动后手动挂载每个 NFS 共享。有更好的处理方法：-b 选项。

| 设备 | 挂载点 | 文件系统类型 | 选项 | 转储 | 遍历 |
|---|---|---|---|---|---|
| spots:/home | /home2 | nfs | rw,-b | 0 | 0 |

将其放到后台并返回到命令提示符。以下是在尝试 60 秒后尝试挂载前一个示例 /etc/fstab 行中指定的共享时你会得到的输出：

```
# mount /home2
spots:/home: nfsd: RPCPROG_NFS: RPC: Port mapper failure - RPC: Timed out

nfs: Cannot immediately mount spots:/home, backgrounding
```

后台 mount_nfs 进程将继续尝试挂载共享，直到成功为止。这种方法在计算集群或实验室中特别有用，在这些环境中 NFS 挂载的资源很好有但不是正确操作所必需的——例如，一个 NFS 挂载包含流行的用户程序或游戏的集群，但所有关键系统功能都可在本地系统磁盘上使用。

## Samba 与 Windows 文件共享

FTP 和 NFS 适用于在两台 UNIX 机器之间通信和共享文件。但事实是这是一个 Windows 世界，无论你的机器处于何种网络环境中，它很可能都被 Windows 机器包围。如果你想与使用 Windows 的朋友共享文件，你就必须遵守他们的规则。

幸运的是，FreeBSD 具有执行 Windows 风格文件共享的能力，具有 Windows 机器所具有的所有功能。具体来说，它拥有 Samba，这是一个软件包，允许 UNIX 机器在本地网络上表现为另一台 Windows 机器；Windows 机器可以像连接到另一台 Windows 机器一样连接到它。Samba 甚至处理打印机共享和域登录，并且可以充当自己的 Windows 域控制器。

Windows NetBIOS/SMB 协议相对于 NFS 等系统的一个优势是它支持自动服务器发现或浏览。在 Windows 中，如果你打开“网络邻居”或“我的网络位置”窗口，它将显示本地网络上所有可用的 SMB 服务器的名称。这样，你就可以在事先不知道它们名称的情况下知道可以连接哪些服务器。

网络浏览器窗口中显示的每台机器的名称（如图 24.4 所示）是其 NetBIOS 名称，这是 Windows 允许长达 15 个字符的标识。虽然 Windows 要求你以大写形式输入 NetBIOS 名称，但它在网络浏览器窗口中以首字母大写、小写形式显示。在其他操作系统（例如 FreeBSD）下，NetBIOS 名称与机器的主机名相同，如果必要则截断为 15 个字符。

**图 24.4**
*显示运行 Samba 的 FreeBSD 机器的 Windows 网络浏览器窗口。*

![](img/ba0161b65b37e94cffc801ecbacaba5e_416_0.png)

NetBIOS 名称由一种名称服务处理，类似于 DNS 名称，但将显示的 NetBIOS 机器名称映射到特定机器不仅基于 IP 地址，还基于其他标准（因为 NetBIOS 不限于 IP）。Samba 的名称服务器组件与实际的 SMB 数据服务器是分开的，正如你将看到的那样。

NetBIOS 的一个缺点是它仅在局域网上运行；NetBIOS 数据包基于广播，因此不会被路由器转发。WINS（Windows Internet Name Service）协议存在于连接不同网络上的 Windows 共享区域，部分缓解了这个问题。

### 安装和配置 Samba

Samba 在 ports 中的 `/usr/ports/net/samba` 或在 packages 中可用。有关如何安装软件包或端口的详细信息，请参阅第 6 小时“添加和删除第三方软件”。

安装 Samba 软件包后，将安装各种新项目：守护进程可执行文件（在 `/usr/local/sbin` 中）、管理工具（在 `/usr/local/bin` 中）、文档和示例（在 `/usr/local/share` 中），以及进入 `/usr/local/etc` 的配置文件。一些可能的配置文件在默认安装中不存在；如果你想利用其功能，必须从头创建它们。还有代码页（在 `/usr/local/etc/codepages` 中），用于将 Windows 字符集映射到 UNIX 字符集。

该软件包中存在的唯一配置文件是 `/usr/local/etc/smb.conf.default`，你必须将其重命名为 `smb.conf` 才能使其工作。同样，`/usr/local/etc/rc.d/samba.sh.sample` 启动脚本必须重命名为 `samba.sh`。以最简单的方式运行 Samba，你只需编辑 `smb.conf` 并修改 workgroup 行以反映你的机器所属的工作组或域。例如，如果你的工作组名为 MYGROUP，请按如下方式更改 workgroup 行：
