
让我们升级这一操作，使用 `Nmap` 通过我们的 `SOCKS` 代理对 `HRSHARES` 进行端口扫描。我们将使用 `TCP` 连接扫描 (`-sT`)、跳过 `DNS` 解析 (`-n`)、跳过主机发现 (`-Dn`) 并仅检查前 20 个端口 (`-top-ports=20`)。然后我们将在命令前加上 `proxchains`，将所有数据包推过 `SSH` 隧道转发 `SOCKS` 代理。我们还会使用 `-vv` 增加灵活性。

`Nmap` 内置了代理选项。然而，根据其文档，它“仍在开发中”*920，不适用于代理扫描。因此，我们在此示例中再次使用了 `Proxchains`。

```
kali@kali:~$ proxieschains nmap -vv -sST --top-ports 20 -Pn 172.16.0.217
[proxies] config file loaded /etc/proxchains4.conf
[proxies] reloading /usr/lib/x86_64-linux-gnu/libproxchains.so.4
DNS entry: proxies-ng 4.16
Host discovery disabled (-n). All addresses will be marked '*' and scan times may be slower.
Starting Nmap 7.92 (https://nmap.org) at 2022-08-28 17:26 EDT
Initiating DNS resolution of 1 host, at 17:26
Completed Parallel DNS resolution of 1 host, at 17:26, 0.09s elapsed
DNS resolution of 1 IPs took 0.180s. Async: 2; OK: 0; NX: 1; DR: 0; SF: 0; TR: 1; CN: 0
Initiating Connection to
Scanning 172.16.50.217 [20 ports]
[proxies] Strict chain 192.168.50.63999 ... 172.16.50.2111 <--socket
error or timeout!
[proxies] Strict chain 192.168.50.63999 ... 172.16.50.2122 <--timeout
error or timeout!
[proxies] Strict chain 192.168.50.63999 ... 172.16.50.21900 <--socket
error or timeout!
Completed Scan at 17:30, 244.3ms elapsed (20 total ports)
Nmap scan report for 172.16.50.217
Host is up, received user-set (9.0% latency).
Scanned 2022-08-28 17:26:47 EDT for 244 seconds
```

| PORT | STATE | SERVICE |
|---|---|---|
| 21/tcp | closed | conn-refused |
| 22/tcp | closed | conn-refused |
| 23/tcp | closed | conn-refused |
| 25/tcp | closed | conn-refused |
| 53/tcp | closed | conn-refused |
| 80/tcp | closed | conn-refused |
| 110/tcp | closed | conn-refused |
| 111/tcp | closed | conn-refused |
| 135/tcp | open | syn-ack |
| 139/tcp | open | syn-ack |
| 143/tcp | closed | conn-refused |
| 443/tcp | closed | conn-refused |
| 445/tcp | open | microsoft-ds syn-ack |
| 993/tcp | closed | conn-refused |
| 995/tcp | closed | conn-refused |
| 1723/tcp | closed | conn-refused |
| 3389/tcp | closed | conn-refused |
| 3389/tcp | open | ms-bt-server syn-ack |
| 5900/tcp | closed | conn-refused |
| 8080/tcp | closed | http-proxy |

> *920 (Gordon "fyodor" Lyon, 2022), https://nmap.org/book/man-bypass-firewalls.html

# 使用 Kali Linux 进行 OffSec 渗透测试

从以下路径读取数据文件：`usr/bin/../share/nmap`

扫描 1 个 `IP` 地址（1 个主机）耗时 244.62 秒

列出 544 - `Nmap-over-Proxies` 命令输出

扫描成功！代理让我们深入了解每个尝试的套接字，如果连接失败，它还会记录原因。`Nmap` 发现了 `TCP` 端口 135、139、445 和 3389。

默认情况下，代理配置了非常高的超时值。这可能导致端口扫描变得非常缓慢。在代理配置文件中降低 `tcp_read_time_out` 和 `tcp_connect_time_out` 值，将强制代理更快地对无响应连接进行超时。这可以大幅加快端口扫描速度。

在本节中，我们设置了动态端口转发，并使用代理将 `smblient` 和 `Nmap` 的流量通过创建的 `SOCKS` 代理端口推送。随后我们成功列出了共享资源 `HRSHARES`，并进行了端口扫描。

### 18.3.3 SSH 远程端口转发

在示例中，我们能够连接到在 `CONFLUENCE01` 的 `WAN` 接口上绑任何端口。这在现实世界中是挑战性的，因为通常会有防火墙（硬件和软件）存在。入站流量的控制比出站流量更严厉。在少数情况下，我们会获取 `SSH` 用户的凭据，允许我们直接 `SSH` 进入网络并进行端口转发。我们很少能够访问绑定到网络边界的端口。

然而，我们能够从网络使用 `SSH`。出站连接的控制比入站连接更困难。大多数企业网络出于简单性、易用性和业务需求，会允许许多类型的常见流量出站——包括 `SSH`。因此，连接到我们绑定到网络边界的端口是不可能的，但 `SSH` 出站是可能的。

这种 `SSH` 远程端口转发²¹ 可能非常有用。类似于攻击者可能执行远程 `shell` 负载以连接回攻击者控制的监听器，`SSH` 远程端口转发可以用于连接回攻击者控制的 `SSH` 服务器，并绑定监听端口。我们可以将其视为一种反向 `shell`（`reverse shell`），但是用于端口转发的。

在本地和动态端口转发中，监听端口绑定到 `SSH` 客户端；在远程端口转发中，监听端口绑定到 `SSH` 服务器。数据包转发不是由 `SSH` 服务器完成，而是在远程端口转发中由 `SSH` 客户端转发。

让我们重新考虑我们的实验室场景，后退几步。

和以前一样，我们使用 `CVE-2022-26134` 攻破 `CONFLUENCE01`。但在这种情况下，管理员决定通过在边界实施防火墙来提高网络安全。防火墙的配置为：无论我们是否在 `CONFLUENCE01` 的 `WAN` 接口上绑定端口，我们能够连接到 `Kali` 机器的端口只有 `TCP` 8090。

> ²¹ (OpenBSD 手册, 2022), https://man.openbsd.org/ssh#

`PWK` - © 2023 OffSec Services Limited. 版权所有。

正如我们在 `Socat` 中做的那样，我们要枚举运行在 `PGDATABASE01` 端口 5432 上的 `PostgreSQL` 数据库。`CONFLUENCE01` 没有执行此操作的工具。由于防火墙的存在，我们无法创建任何需要在 `CONFLUENCE01` 上打开监听端口的端口转发。

然而，我们能够从网络使用 `SSH`。出站连接比入站连接更困难。大多数企业网络出于简单性、易用性和业务需求，会允许许多类型的常见流量出站——包括 `SSH`。因此，连接到我们绑定到网络边界的端口是不可能的，但 `SSH` 出站是可能的。

这种 `SSH` 远程端口转发²¹ 可能非常有用。类似于攻击者可能执行远程 `shell` 负载以连接回攻击者控制的监听器，`SSH` 远程端口转发可以用于连接回攻击者控制的 `SSH` 服务器，并绑定监听端口。我们可以将其视为一种反向 `shell`，但是用于端口转发的。

在本地和动态端口转发中，监听端口绑定到 `SSH` 客户端；在远程端口转发中，监听端口绑定到 `SSH` 服务器。数据包转发不是由 `SSH` 服务器完成，而是在远程端口转发中由 `SSH` 客户端转发。

让我们重新考虑我们的实验室场景，后退几步。
