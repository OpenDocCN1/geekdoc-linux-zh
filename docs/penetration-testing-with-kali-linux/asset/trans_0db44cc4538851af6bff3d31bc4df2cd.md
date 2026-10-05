

# OffSec

使用 Kali Linux 进行渗透测试

```
0.0.0.0*: users:(("chisel",pid=50121,fd=2))
tcp             LISTEN   4096*:8080
tcp             *:users:(("chisel",pid=50121,fd=2))
tcp             LISTEN   511*:8080
```

列表 597 - 使用 ss 检查 SOCKS 端口是否打开

SOCKS 端口 1080 正在监听 Kali 机器的环回接口上。让我们利用它连接到 PGDATABASE01 上的 SSH 服务器。在“重定向和 SSH 隧道”中，我们创建了带有动态转发的 SOCKS 端口，但尚未通过 SOCKS 代理运行 SSH 本。SSH 不提供通用的 SOCKS 代理命令，而是提供了一个 `ProxyCommand` 选项。我们可以将其写入配置文件，或者作为命令行的一部分传递。`ProxyCommand` 接受一个用于打开启用代理通道的 shell 命令。文档建议使用 OpenBSD 版本的 Netcat，但它不支持 SOCKS 代理。然而，我们使用了编写者提供的替代方案 Ncat。

列表 598 - 使用 apt 安装 Ncat

```bash
kali@kali:~# sudo apt install ncat
Reading package lists...
Building dependency tree...
Reading state information...
The NEW packages will be installed:
ncat
0 upgraded, 1 newly installed, 85 not upgraded.
Need to get 487 KB of archives.
Get: http://kali.org/kali-rolling/main/amd64 7.92-2kali1 (487 KB)
Fetched 487 KB in 5s (97.3 KB/s)
Selecting previously installed ncat
(Reading database 28679 files and directories currently.)
Preparing to unpack ...ncat_7.92-2kali1_amd64.deb ...
Unpacking ncat (7.92-2kali1_amd64) ...
Setting up ncat (7.92-2kali1) ...
update-alternatives: using /usr/bin/ncat (nc) in auto mode
Processing triggers for man-db (2022.2-0) ...
Processing triggers for kali-menu ...
kali@kali-00$
```

# OffSec

使用 Kali Linux 进行渗透测试

现在我们使用 Ncat 命令作为 `ProxyCommand`。该命令构建了 Ncat 使用 socks5 协议以及 127.0.0.1:1080 处的套套字。`%h` 和 `%p` 代表 SSH 主机和端口，它们将在命令内部运行。

```bash
kali@kali:~$ ssh -o ProxyCommand='ncat --proxy-type socks5 127.0.0.1:1080 %h' dabase_admin@10.40.50.215
The authenticity of '10.40.50.215 (no host for proxy command)' can't be established.
ED25519 key fingerprint is SHA256:IGZ427YQAL3fCKYWncTAZ/emmWWR5gQP8vQ.
Are sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added to list of known hosts.
dabase_admin@10.40.50.215:Welcome to Ubuntu 22.04 LTS (Ubuntu/Linux 5.15.0-generic x86_64)
```

- 帮助: https://help.ubuntu.com
- 管理: https://landscape.canonical.com
- 支持: https://ubuntu.com/advantage

```
0 updates can be applied immediately.
Last login: Jul 21 14:04:11 2022 from 192.168.97.19
dabase_admin@pgbackup1:$
```

列表 599 - 通过我们的 Chisel HTTP 隧道成功连接 SSH

非常漂亮！我们通过我们的 Chisel SOCKS 代理，通过反向 HTTP 隧道访问了 SSH 服务器。

在本单元中，我们使用 Chisel 创建了一个反向隧道，然后通过该隧道登录 PGDATABASE01 上的 SSH。我们仅使用 HTTP 格式的流量访问了被攻击的 CONFLUENCE01 枢板服务器。

## 19.2 DNS 隧道理论与实践

本学习单元涵盖了以下目标：

- 学习 DNS 隧道
- 使用 dnscat2 执行 DNS 隧道

DNS 是基础协议之一，经常被攻击者滥用于恶意目的。例如，它可以用于隧道传输。为了确切理解它是如何工作的，让我们展示一个简化的课程。我们将学习如何使用名为 dnscat2 的工具执行 DNS 隧道。

 19.2.1 DNS 基础

IP 地址不是人类可读的名称。每当我们通过名称访问域名时，首先都会获取其 IP 地址。让我们回顾这个过程。大多数情况下，我们使用 ISP 提供的递归解析器（通常预装在现有的路由器中），也可以使用其他著名的公共递归名称服务器。例如，Google 在 8.8.8.8 处有一个公共 DNS 服务器。

