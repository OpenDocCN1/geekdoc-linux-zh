
向 `booklab.astrust.com` DNS 域内的所有主机导出读写权限，但 `192.168.10` 网络上的主机除外。在命令中，`-F` 标志表示 `share` 应该使用 NFS 文件系统类型，而不是 `/etc/dfs/ftypes` 中的任何类型。

可以向某些客户端只读导出目录并向另一些客户端读写。只需包含 `rw=` 和 `ro=` 选项即可。

`share` 手页记录了一些基本的 NFS 选项。完整列表，请参考 `share_nfs` 手页。

## exports 命令和 exports 文件 (Linux, AIX)

`exports` 文件左侧列包含导出目录列表，随后是相关选项的列表。例如，AIX 的 `exports` 行：
`/home -vers=4.sec=sys,access=harpatrust.com`

允许机器 `harpatrust.com` 使用第 4 版本的 NFS 协议和 UNIX 认证 (`sec=sys`) 挂载 `/home`。

`exports` 文件中列出的未指定特定主机组的文件系统通常由所有机器挂载。这是一个巨大的安全漏洞。

`exports` 文件中使用的精确选项和语法在不同系统中有所不同，尽管具有某些主题上的相似性。以下章节描述了 Linux 和 AIX 的通用格式。一如既常，请务必检查你系统的页面。

### AIX 中的 Exports

AIX 拥有我们示例系统中最“经典”的 `exports` 格式。权限如表 18.5 所示。

#### 表 18.5 AIX 常用导出选项

| 选项 | 描述 |
| --- | --- |
| `access=list` | 列出可以挂载文件系统的主机，没有客户端可以在文件系统上写入。 |
| `ro` | 向所有人导出只读； |
| `rw` | 向所有人导出读写（默认值）。 |
| `rw=list` | 导出为大部分可读。列表列出了经过认证可以写入挂载的主机；所有所有必须只读。 |
| `root=list` | 列出可以以 root 身份访问文件系统的主机。如果没有此选项，来自客户端的 root 访问等同于用户 nobody 的访问。 |
| `vers=n` | 使用版本 n 向客户端导出目录。有效值为 2, 3 和 4。指定 2 或 3 均包含 2 和 3。 |
| `sec=flavor` | 指定导出目录的安全方法列表。值包括 `sys` (UNIX 认证), `dh` (DES), `krb5` (Kerberos 认证、完整性), `krbsp` (Kerberos 认证、完整性和私密性) 以及 `none` (匿名访问，不推荐)。 |
| `anon=n` | 指定远程 root 映射的 UID。默认为 -2 (nobody)。将此值设置为 -1 将完全拒绝 root 访问。 |

在表 18.5 中，列表由冒号分隔的主机名和网络名称组成。表 18.5 中的选项与 `share` 命令理解的选项相似。然而，存在一些细微的。例如，选项
`rw=leopard.atrust.com:ross.com`

### Linux 中的 Exports

在 `share` 语法中，意味着仅向列出的主机读写导出目录。在 AI 下，此选项允许所有人只读模式挂载目录。注意陷阱！在 AI 下，你必须使用 `access` 子句来限制挂载到。

可以向某些客户端只读导出目录并向另一些客户端读写。只需包含 `rw=` 和 `ro=` 选项。

`share` 手页记录了一些基本的 NFS 选项。完整列表，请参考 `share_nfs` 手页。

## nfsd: 提供文件服务

当客户端打开文件时，如果请求的文件被重命名，可能会出现偶尔的问题。如果你预料会有此类情况，请考虑设置 `no_subtree_check`。

`secure_locks` 选项需要授权和验证才能对文件进行锁定。某些 NFS 客户端在发送锁定请求时不发送凭据，因此无法与 `secure_locks` 工作。在这种情况下，你只能锁定 world可读的文件。将这些客户端替换为正确支持凭据的客户端是最佳解决方案。不过，你可以指定 `insecure_locks` 选项作为临时措施。

Linux 的 `mountd` 允许使用 `inet` 而不是连续运行。此配置允许通过 TCP wrap 程序 `tcpd` 执行辅助的访问控制。更多信息请参阅第 917 页。

一旦客户端请求通过 `mountd` 验证，客户端就可以请求文件系统操作。这些请求由服务器端的 `nfsd`（NFS 操作守护进程）处理。除非客户端导出了自己的文件系统，否则不需要在 NFS 客户端上运行 `nfsd`。

`nfsd` 接受一个数字参数，用于指定 fork 多少服务器线程。选择适当数量的 `nfsds` 非常重要，遗憾的是这某种程度上是一门“黑艺术”。如果数量太低或太高，NFS 性能可能会受到影响。

`nfsd` 线程的最佳数量取决于所使用的操作系统和硬件。如果你发现 `ps` 通常显示 `nfsds` 处于 D 状态（不可中断睡眠）且有空闲 CPU 可用，请增加线程数量。如果你发随着添加 `nfsds` 发现负载平均值（由 `uptime` 报告）在上升，说明你做得过头了；请从阈值处回退一点。你还应该定期运行 `nfsstat` 以检查可能与 `nfsd` 线程数量相关的性能问题。有关 `nfsstat` 的更多细节请参阅第 710 页。

在带有大量 UDP 包的负载型 NFS 2 或 3 服务器上，如果请求在所有 `nfsd` 线程都已占用时到达，UDP 套接将发生溢出。你可以通过 `netstat -s` 溢出的数量。添加更多 `nfsd` 线程，直到 UDP 套接丢包至零。溢出表示服务器守护进程严重不足，因此你可能应该比此指标指示的再加几个。

`nfsd` 线程的数量在系统范围 NFS 配置文件配置。文件的位置和可用设置差异很大。下一页的表 18.8 显示了我们示例系统的设置。在修改 `nfsd` 配置文件后，务必使用表 18.1 中的脚本重启服务。

实际上，`nfsd` 只是对嵌入在内核中的 NFS 服务器代码执行了一个非返回的系统调用。

#### 表 18.8 如何指定 nfs 守护进程的数量

| 系统 | 配置文件 (在 `/etc` 中) | 设置选项 | 默认值 |
| --- | --- | --- | --- |
| Ubuntu | `default/nfs-kernel-server` | `RPCNFSDCOUNT` | 8 |
| SUSE | `sysconfig/nfs` | `USE_KERNEL_NFSD_NUMBER` | 4 |
| Red Hat | `sysconfig/nfs` | `RPCNFSDCOUNT` | 8 |
| Solaris | `default/nfs` | `NFSD_SERVERS` | 16 |
| HP-UX | `default/nfs` | `NFSD_SERVERS` | 16 |
| AIX | | 使用 SMIT 或 `chnfs` 更改 nfs 守护进程的数量。 | |

## 18.4 客户端 NFS

NFS 文件系统的挂载方式与本地磁盘文件系统非常相似。`mount` 命令理解 `hostname:directory` 记法，其表示远程主机上的路径目录。与本地文件系统一样，`mount` 将远程主机上的目录映射到本地文件树内的目录中。挂载完成后，你就像访问本地文件系统一样访问挂载的 NFS 文件系统。`mount` 命令及其相关的 NFS 扩展是 NFS 客户端系统管理员最关心的问题。

在挂载 NFS 文件系统之前，它必须被正确地导出（参见第 698 页的服务器端 NFS）。要从客户端角度验证服务器已正确导出了其文件系统，请使用客户端的 `showmount` 命令：

```
$ showmount -e monk

Export list for monk

/home/ben harp.trust.com
```

此示例报告服务器 `monk` 上的目录 `/home/ben` 已导出到客户端系统 `harp.trust.com`。如果 NFS 挂载不起作用，首先验证已通过 `exportfs` 将文件系统正确地导出到服务器（你可能忘记在更新 `exports` 文件后运行 `exportfs -a`）。接下来，检查 `showmount` 输出：

如果目录在服务器上已正确导出，但 `showmount` 返回错误或空列表，请双击服务器上是否运行了所有必要的进程（`portmap, mount, nfs, statd, lockd`），`hosts.allow` 是否允许所有守护进程访问，以及它们位于正确的客户端系统上。

`showmount` 显示的路径信息（如上面的 `/home/ben`）仅适用于 NFS 版本 2 和 3 服务器。NFS 版本 4 服务器导出单个唯一的伪文件系统。传统的 NFS 独立挂载点概念与版本 4 的模型不相符，因此 `showmount` 并不适用。

遗憾的是，NFSv4 中没有 `showmount` 的替代品。在服务器上，`exportfs -v` 命令显示现有的导出项，但此仅在本地有效。如果你无法直接访问服务器，请挂载服务器伪文件系统的根目录并手动遍历目录结构，而不是挂载点。

要在版本 2 和 3 中实际挂载文件系统，使用：
```bash
mount -t nfs -o rw,hard hostname:directory /mnt
```

在版本 4 中挂载文件系统，使用：
```bash
mount -t nfs -o rw,intr hostname:directory /mnt
```

### NFS 挂载选项

| 标志 | 描述 |
|---|---|
| `rw` | 挂载为读写（必须导出） |
| `ro` | 挂载为只读（必须导出） |
| `bg` | 挂载在后台执行 |
| `hard` | 如果服务器宕机，导致访问的操作被挂起，直到服务器恢复 |
| `soft` | 如果服务器宕机，导致访问的操作失败并返回错误 |
| `intr` | 允许用户中断 |
| `nointr` | 不允许中断 |
| `retrans=n` | 指定返回之前的重试次数 |
| `timeout=n` | 设置超时时间（秒） |
| `rsize=n` | 设置读取大小 |
| `wsize=n` | 设置写入大小 |
| `sec=flavor` | 指定安全方案 |
| `vers=n` | 设置 NFS 版本 |
| `proto=proto` | 选择传输协议 |

在负载上有大量 UDP 包的情况下，如果在所有 `nfsd` 线程都已占用时到达请求，UDP 套接将发生溢出。你可以通过 `netstat -s` 监控溢出的数量。添加更多 `nfsd` 线程，直到 UDP 套接丢包至零。溢出表示服务器守护进程严重不足，因此你可能应该比此指标指示的再加几个。

`nfsd` 线程的数量在系统范围 NFS 配置文件中配置。文件的位置和可用设置差异很大。下一页的表 18.8 显示了我们示例系统的设置。在修改 `nfsd` 配置文件后，务必使用表 18.1 中的脚本重启服务。

实际上，`nfsd` 只是对嵌入在内核中的 NFS 服务器代码执行了一个非返回的系统调用。

## NFS 4 的身份映射

有关 `fstab` 文件的更多信息，请参阅第 260 页。

使用 SMIT 在 AIX 上配置启动时的 NFS 挂载。不要手动修改 `/etc/filesystems`，因为它在卷组导入或导出过程中可能会被覆盖。

在向 `fstab/vfstab` 添加条目时，请务必通过 `mkdir` 创建相应的挂载点目录。你可以在 Solaris 或 HP-UX 上运行 `mount -a` 来立即生效更改（无需重启）；在 Linux 上使用 `-t nfs`；对于版本 4，使用 `mount -a nfs4`。在 AIX 上，你可以使用 `-v nfs` 挂载 NFS 文件系统。

`/etc/fstab` 的 `flags` 字段指定了 NFS 挂载选项；这些选项与你在 `mount` 命令行中指定的选项相同。

### 限制导出到特权端口

NFS 客户端在连接 NFS 服务器时，可以自由使用任何所需的 TCP 或 UDP 源端口。然而，某些服务器可能要求连接来自特权端口（小于 1024 的端口号）。其他服务器允许将此行为设置为一个选项。在 PC 和桌面级 Linux 世界中，特权端口的使用并没有提供多少实际安全性。

大多数 NFS 客户端采用传统的（仍然推荐的）方法，即默认使用特权端口以避免潜在冲突。在 Linux 下，你可以使用 `insecure` 导出选项接受来自非特权端口的挂载。

## 18.5 NFS 版本 4 的身份映射

与早期版本的 NFS（使用原始 UID 和 GID 识别用户）不同，版本 4 使用 `user@nfs-domain` 和 `group@nfs-domain` 格式的字符串。在 NFS 服务器和客户端上，身份映射在字符串标识符与本地 UID 和 GID 值之间进行转换。映射值用于转换文件属性信息，但它们不用于访问控制，访问控制由单独处理。

所有参与 NFSv4 系统应具有相同的 NFS 域。大多数情况下，使用你的 DNS 名称作为 NFS 域是合理的。例如，对于服务器 `harp.atrust.com`，`atrust.com` 是一个直接的选择。子域中的客户端（例如 `booklab.atrust.com`）可能想或不想使用站点级名称（例如 `atrust.com`）来促进 NFS 通信。

令管理员遗憾的是，NFSv4 UID 映射没有标准实现，因此系统之间的细节略有不同。下一页的表 18.10 列出了我们每个系统的映射守护进程，并注明了其配置文件的位置。

除了设置 NFS 域之外，身份映射服务很少需要管理员的帮助。守护进程在启动时从管理 NFS 的相同脚本启动。在进行配置更改后，你需要重启守护进程。通常提供如详细日志和 nobody 账户备用管理等选项；请查看特定守护进程的帮助页。

#### 表 18.10 身份映射守护进程与配置

| 系统 | 守护进程 | 配置 |
| --- | --- | --- |
| Linux | `/usr/sbin/rpc.idmapd` | `/etc/idmap.conf` |
| Solaris | `/usr/lib/nfs/nfsmapid` | `/etc/default/nfs/` |
| HP-UX | `/usr/sbin/nfsmapid` | `/etc/default/nfs/` |
| AIX | `/usr/sbin/nfsrg` | `chfsdom domain` |

a. 域在 `NFSMAPID_DOMAIN` 参数中设置。

## 18.6 NFSSTAT：转储 NFS 统计信息

`nfsstat` 显示 NFS 系统维护的各种统计数据。`nfsstat -s` 显示服务器端统计数据，`nfsstat -c` 显示客户端操作操作信息。默认情况下，`nfsstat` 显示所有协议版本的统计数据。

```bash
$ nfsstat -c
```
