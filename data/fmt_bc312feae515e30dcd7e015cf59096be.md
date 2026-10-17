
几分钟后，我们收到了结果，并发现端口 `80`、`135` 和 `3389` 都是开启的。

> 针对此 Windows 主机的扫描速度稍慢——可能是因为当端口关闭时，Windows 防火墙的响应与 Linux 不同。

在本节中，我们使用 SSH 远程端口转发，通过从远程受损主机发起 SSH 连接，在我们的 Kali 上开启一个 SOCKS 代理端口。然后，我们使用 `Proxychains` 通过 SOCKS 代理端口扫描内网中的主机。

### 18.3.5 使用 sshuttle

在我们可以直接访问位于复杂内部网络后的 SSH 服务器的情况下，经典的动态端口转发可能难以管理。`sshuttle`⁴ 是一种工具，它通过设置本地路由并强制流量通过 SSH 隧道，从而将 SSH 连接转换为类似于 VPN 的形式。然而，它要求 SSH 客户端具有 root 权限并安装 `Python3`，因此并不总是最轻量级的选项。但在适当的情况下，它可以非常有用。

在我们的环境中，我们拥有对 `PGDATABASE0` 的 SSH 权限，可以通过 `CONFLUENCE1` 上设置的端口转发访问它。让我们通过它运行 `sshuttle` 来观察其功能。

首先，我们在 `CONFLUENCE1` 的 shell 中设置了一个端口转发，监听 WAN 接口上的 `2222` 端口，并转发到 `PGDATABASE0` 的 `22` 端口。

⁴(`sshuttle`, 2022), https://github.com/sshuttle

```
confluence@01:/opt/atlassian/confluence/bin$ socat TCP-LISTEN:2222,fork TCP:10.4.50.215:22
```

列表 554 - 将 `CONFLUENCE0` 上的 `2222` 端口转发到 `PGDATABASE0` 的 `22` 端口。

接下来，我们可以运行 `sshuttle`，指定要使用的 SSH 连接以及我们想要通过该连接进行隧道的子网（`10.4.50.0/24` 和 `172.16.50.0/24`）。

```
kali@kali:$ sshuttle -r database_admin@192.168.50.63:2222 10.4.50.0/24 172.16.50.0/24
[local sudo] Password:
```

```
database_admin@192.168.50.63:~ password:
Connected to server.
Failed to flush caches: dbus-org.frektop.service not found.
Received non-zero return code 1 when flushing DNS.
```

列表 555 - 从我们的 Kali 机器运行 `sshuttle`，指向 `CONFLUENCE1` 上的端口。

虽然我们没有运行 `sshuttle`，但理论上它应该会在 Kali 机器上设置路由，使得我们对子网的任何请求都会推送到 SSH 连接。让我们在一个新的终端中尝试连接 `SHARES` 上的 SMB 共享来测试是否有效。

```
kali@kali:$ smclient -L //172.16.50.217 -U hr_admin --password=Welcome123
```

| 共享类型 | 注释 |
| :--- | :--- |
| ADMIN | 远程管理 |
| CS | 默认共享 |
| IPC | 脚本 |

重新连接 SMB 工作组：连接到 `172.16.50.217` 失败 (`NT_STATUS_RESOURCE_NOT_FOUND`)

无法连接 SMB 工作组

列表 556 - 在没有任何显式转发的情况下连接到 `SHARES` 上的 SMB 共享。

太棒了！我们现在正在透明地连接 `SHARES`，因为我们处于同一网络并具有直接访问权限。在本节中，我们使用 `sshuttle` 创建了一个类似 VPN 的环境。随后，我们能够从 Kali 机器透明地连接到 `SHARES`，尽管我们和 `PGDATABASE1` 处于同一网络。

### 18.4 在 Windows 上进行端口转发

本学习单元涵盖以下目标：

- 使用 `ssh.exe` 和 `Plink` 为 Windows 创建端口转发
- 理解使用 `Netsh` 进行端口转发

到目前为止，我们讨论了使用 Linux 工具进行端口转发的机制。然而，我们经常遇到需要端口转发的 Windows 主机。坦率地说，有很多方法可以进行这种端口转发，我们将在本单元中介绍。

`OpenSSH` 客户端从 `1803` 版本开始已内置在 Windows 中⁵。在 Windows 版本中，我们找到了 `scp.exe`。

只要我们有凭据，就可以连接到任何 SSH 服务器。在这种情况下，端口转发是 `MULTSERVER03`。如图：![](img/336dea891746f)

图 253: 端口转发⁶

使用 `sshuttle` 建立连接到我们的 Kali 机器。

```
kali@kali:~ 
```

## OffSec

使用 Kali Linux 进行渗透测试

| 端口 | 状态 | 原因 |
| :--- | :--- | :--- |
| 22/tcp | 关闭 ssh | conn-refused |
| 23/tcp | 关闭 telnet | conn-refused |
| 25/tcp | 关闭 smtp | conn-refused |
| 53/tcp | 关闭 domain | conn-refused |
| 80/tcp | 开启 http | syn-ack |
| 110/tcp | 关闭 pop3 | conn-refused |
| 111/tcp | 关闭 rbind | conn-refused |
| 135/tcp | 开启 msprpc | syn-ack |
| 139/tcp | 关闭 netbios-sn | conn-refused |
| 143/tcp | 关闭 imap | conn-refused |
| 443/tcp | 关闭 https | conn-refused |
| 445/tcp | 关闭 microsoft-ds | conn-refused |
| 993/tcp | 关闭 imaps | conn-refused |
| 995/tcp | 关闭 pop3 | conn-refused |
| 1723/tcp | 关闭 pptp | conn-refused |
| 3386/tcp | 关闭 mysql | conn-refused |
| 3389/tcp | 开启 ms-wbt-server | syn-ack |
| 5900/tcp | 关闭 vnc | conn-refused |
| 8080/tcp | 关闭 http-proxy | conn-refused |

从：`/usr/bin/share/nmap` 读取数据文件

扫描完成：1 IP (使用了 1 个主机)，耗时 21.30 秒

列表 553 - 扫描 `MULTISERVER` 结果并使用 `Proxychains` 发现远程 SOCKS 端口。
