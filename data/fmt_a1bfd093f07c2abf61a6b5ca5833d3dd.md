
```text
Server rpc stats:
    calls        badcalls       badauth        badclnt      xdrcll
     8            0               0              0            0
Server nfs v2:
    null         getattr        setattr         root         lookup       readlink
     0          0x 2          25x 0          0x 0         0x 5        62x 0     0x
    read         wrcache        write         create        remove       rename
     0          0x 0          0x 0           0x 0         0x 0        0x 0     0x
    link         symlink        mkdir         rmdir        readdir      fsstat
     0          0x 0          0x 0           0x 0         0x 1       12x 0     0x

Client rpc stats:
    calls        retrans        authrefrsh
     8            0               0
Client nfs v2:
    null         getattr        setattr         root         lookup       readlink
     0          0x 2          25x 0          0x 0         0x 5        62x 0     0x
    read         wrcache        write         create        remove       rename
     0          0x 0          0x 0           0x 0         0x 0        0x 0     0x
    link         symlink        mkdir         rmdir        readdir      fsstat
     0          0x 0          0x 0           0x 0         0x 1       12x 0     0x
```

## 表 16-21 `nfsstat` 选项

| 选项 | 功能 |
| :--- | :--- |
| `-s` | 仅打印服务器端统计信息。 |
| `-c` | 仅打印客户端统计信息（当前不支持）。 |
| `-n` | 仅打印 NFS 统计信息；默认情况下还包括 RPC 统计信息。 |
| `-r` | 仅打印 RPC 统计信息。 |
| `-z` | 将内核统计计数器清零。 |
| `-o <facility>` | 仅显示请求的功能。可用的功能如下：<br>`nfs`：NFS 协议信息<br>`rpc`：RPC 信息<br>`net`：网络层统计信息和数据<br>`fh`：文件句柄信息<br>`rc`：请求响应缓存信息 |

### 安全注意事项

NFS 在设计时并未考虑安全性，因此必须特别注意保护 NFS 系统的安全。NFS 使用客户端用户的 `UID`（用户 ID）和 `GID`（组 ID）来授予权限。`UID` 是 `/etc/passwd` 文件中代表用户的数字编号，`GID` 是 `/etc/group` 文件中代表组的数字编号。客户端的 `UID` 和 `GID` 会与 `/etc/passwd` 和 `/etc/group` 中的本地 ID 进行匹配。要建立安全的 NFS 配置，唯一的办法是确保所有系统上的所有 ID 都匹配。用户应始终具有相同的数字。还要考虑到，用户在他们的工作站上拥有 `root` 权限，他们可以使用任何 ID 来冒充他们想要冒充的任何用户。

可以通过 `/etc/exports` 文件中的限制来控制远程系统的访问。作为另一项预防措施，对于任何导出目录的服务器，您应该始终阻止或过滤 NFS 和 RPC 端口。虽然您可以限制哪些客户端可以连接，但 `DNS` 服务器被入侵以及主机名或域名被更改以允许未授权访问的情况并非不可能。表 16-22 显示了应该阻止的端口。

## 表 16-22 NFS 端口

| 端口 | 协议 | 进程 |
| :--- | :--- | :--- |
| 111 | TCP 和 UDP | `portmapper` |
| 745 | UDP | `mountd` |
| 747 | TCP | `mountd` |
| 2049 | TCP 和 UDP | `nfsd` |

还要记住，通过 NFS 传输的所有数据均以明文发送。不使用加密。基于这些原因，建议仅在受信任且用户在其自己的工作站上没有 `root` 控制权的网络中使用 NFS。

### 使用 Samba

- 目标
    - 正确管理 `NFS`、`smb` 和 `nmb` 守护进程。使用 `NFS` 挂载远程文件系统。配置 `NFS` 以导出本地文件系统。启动、停止和重新启动 `NFS` 服务器。使用包含的 GUI 工具或直接编辑 `/etc/smb.conf` 文件来安装和配置 `Samba`。（注意：这特意排除了高级 `NT` 域问题，但包括主目录和打印机的简单共享，以及正确将 `nmbd` 设置为 `WINS` 客户端。）

`Samba` 是一个非常流行的套件，它允许 `Linux` 和其他 `UNIX` 计算机与 `Windows` PC 共享网络资源。可以配置 `Samba` 以提供以下功能：

- 文件共享
- 打印机共享
- 用户身份验证
- 名称解析（`WINS` 客户端和服务器）
- 服务公告（浏览）

`Samba` 使用两个守护进程提供服务：`smbd`（服务器消息块守护进程）和 `nmbd`（名称消息块守护进程）。文件服务、打印服务以及用户身份验证均由 `smbd` 提供。`nmbd` 守护进程处理名称解析、服务公告和浏览。

> 有关 `Samba` 的更多信息和文档可在 `www.samba.org` 上找到。

### 配置 Samba

`Samba` 通过一个文档完善的文件 `/etc/smb.conf` 进行配置。该文件由许多配置条目组成。有些是可选的，有些则不是。以下是一个 `/etc/smb.conf` 文件的示例。
