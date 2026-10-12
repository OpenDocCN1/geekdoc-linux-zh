
首先，我们在 `CONFLUENCE01` 的 shell 中设置端口转发，监听 WAN 接口上的 `2222` 端口，并转发到 `PGDATABASE01` 的 `22` 端口。

> ²⁴ (`sshuttle`, 2022), https://github.com/sshuttle/sshuttle

```
confluence@01:/opt/atlassian/confluence/bin$ socat TCP-LISTEN:2222,fork TCP:10.4.50.215:22
<bin$ socat TCP-LISTEN:2222,fork TCP:10.4.50.215:22
```

列出 554 - 将 `CONFERENCE01` 上的 `2222` 端口转发到 `PGDATABASE` 的 `22` 端口

接下来，我们可以运行 `sshuttle`，使用我们使用的 SSH 连接字符串，以及我们将通过此连接建立隧的子网（`10.4.50.0/24` 和 `172.16.50.0/24`）。

```
kali@kali:-$ sshuttle -r database_admin@192.168.50.63:2222 10.4.50.0/24 172.16.50.0/24
[local] sudo Password:
```

```
database_admin@192.168.50.63's password:
```

```
c : Connected to server.
Failed to flush caches: Unit dbus-freesktop.resolve.service not found.
Received non-zero return code 1 when flushing DNS resolver cache.
```

列出 555 - 从我们的 Kali 机器上运行 `sshuttle`，指向 `CONFERENCE01` 上的转发端口。虽然我们不需要离开子网，但理论上，它应该已经在我们的 Kali 机器上设置了路由，使得我们对子网主机发出的任何请求都将通过 SSH 连接推送。让我们在新的终端中尝试连接 SMB `HRSHARES` 来测试这是否有效。

```
kali@kali:-$ smbclient -U //172.16.50.217 -U hr_admin --password=Welcome1234
```

| Sharename | Type | Comment |
|---|---|---|
| ADMIN$ | Disk | Remote Admin |
| CS | Disk | Default share |
| IPC$ | IPC | Remote IPC |
| scripts | Disk | |

重新连接到 SMB1 以列出工作组。

`do_connect`: Connection to `172.16.50.217` failed (Error `NT_STATUS_RESOURCE_NAME_NOT_FOUND`)

Unable to connect with SMB -- no workgroup available

```
kali@kali:-$
```

列出 556 - 连接到 `HRSHARES` 上的 SMB 共享，无需显式转发。太棒了！我们现在透明地连接到 `HRSHARES`，就像我们处于同一个网络并具有直接访问权限一样。在本节中，我们使用 `sshuttle` 创建一个类似 VPN 的环境。然后我们能够从 Kali 机器透明地连接到 `HRSHARES`，就像我们处于 `PGDATABASE` 同一个网络一样。

## 18.4 使用 Windows 工具进行端口转发

本单元涵盖了以下学习目标：

- 1. 使用 `ssh.exe` 和 `Plink` 在 Windows 上创建端口转发
- 2. 理解使用 `Netsh` 进行端口转发

到本模块为止，我们已经讨论了使用基于 Linux 的工具进行端口重定向和隧道机制。然而，我们在大型网络中经常会遇到 Windows 主机，它们也要求我们练习端口转发策略。坦率地说，Windows 上有多种进行端口转发和隧道的方法，我们在本单元中将涵盖其中。

### 18.41 ssh.exe

`OpenSSH` 客户端从版本 `1803`（2018 年 4 月更新）起默认捆绑在 Windows 中，并自 `1709`（Windows 10 秋创建者更新）起作为按需功能可用。在安装了 SSH 的 Windows 系统上，我们将找到 `scp.exe`、`sftp.exe`、`ssh.exe` 以及其他 `ssh-*` 工具，默认位置位于 `%systemdrive%\Windows\System32\OpenSSH`。

SSH 客户端是为 Windows 编译的并不意味着我们只能连接到 Windows 编译的 SSH 服务器。只要有凭据，我们可以连接到任何需要的 SSH 服务器。让我们通过从 `MULTISERVER03`（Windows 主机）到我们的 Kali 机器创建远程端口转发来练习。在这种情况下，`MULTISERVER03` 上的 RDP 端口已开放。我们可以将任何其他端口绑定到 WAN 接口。一旦设置好实验室，它应该显示为：![](img/987dc9f6ebd8893c565a1d124d7724e6_597_0.png) 图253：使用 Windows SSH 客户端设置 SSH 远程端口转发我们将使用之前发现的 `rdp_admin` 凭据 RDP 连接到我们的 Kali 机器。然后我们使用 `ssh.exe` 为我们的 Kali 机器创建远程端口转发。在本节中，我们使用 `sshuttle` 创建一个类似 VPN 的环境。然后我们能够从 Kali 机器透明地连接到 `HRSHARES`，就像我们处于 `PGDATABASE` 同一个网络一样。

# OffSec

使用 Kali Linux 进行渗透测试

（注意：根据 OCR 流程，某些文本似乎重复或合并了）

首先，我们在 `CONFLUENCE01` 的 shell 中设置端口转发，监听 WAN 接口上的 `2222` 端口，并转发到 `PGDATABASE01` 的 `22` 端口。

> ²⁴ (`sshuttle`, 2022), https://github.com/sshuttle/sshuttle

```
confluence@01:/opt/atlassian/confluence/bin$ socat TCP-LISTEN:2222,fork TCP:10.4.50.215:22
<bin$ socat TCP-LISTEN:2222,fork TCP:10.4.50.215:22
```

列出 554 - 将 `CONFERENCE01` 上的 `2222` 端口转发到 `PGDATABASE` 的 `22` 端口

接下来，我们可以运行 `sshuttle`，使用我们使用的 SSH 连接字符串，以及我们将通过此连接建立隧的子网（`10.4.50.0/24` 和 `172.16.50.0/24`）。

```
kali@kali:-$ sshuttle -r database_admin@192.168.50.63:2222 10.4.50.0/24 172.16.50.0/24
[local] sudo Password:
```

```
database_admin@192.168.50.63's password:
```

```
c : Connected to server.
Failed to flush caches: Unit dbus-freesktop.resolve.service not found.
Received non-zero return code 1 when flushing DNS resolver cache.
```

列出 555 - 从我们的 Kali 机器上运行 `sshuttle`，指向 `CONFERENCE01` 上的转发端口。虽然我们不需要离开子网，但理论上，它应该已经在我们的 Kali 机器上设置了路由，使得我们对子网主机发出的任何请求都将通过 SSH 连接推送。让我们在新的终端中尝试连接 SMB `HRSHARES` 来测试这是否有效。

```
kali@kali:-$ smbclient -U //172.16.50.217 -U hr_admin --password=Welcome1234
```

| Sharename | Type | Comment |
|---|---|---|
| ADMIN$ | Disk | Remote Admin |
| CS | Disk | Default share |
| IPC$ | IPC | Remote IPC |
| scripts | Disk | |

重新连接到 SMB1 以列出工作组。

`do_connect`: Connection to `172.16.50.217` failed (Error `NT_STATUS_RESOURCE_NAME_NOT_FOUND`)

Unable to connect with SMB -- no workgroup available

```
kali@kali:-$
```
