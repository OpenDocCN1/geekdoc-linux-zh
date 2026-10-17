
```
<!--
NOTE: Mike, please use the following username and password
to access the local mysql server: root, drdr3emenem
Comment placed by John at 12:15am, 2/12/2003
-->
```

### 审计源代码注释

定期审计源代码注释是个好主意。使用如 `grep` 和 `wget` 等工具查找 web 应用程序源代码和 HTML 代码中的注释。

## Web 服务器漏洞

Apache 是当今使用最广泛的 web 服务器。多年来，它一直相当安全。以下段落代表了一个近期的 Apache 漏洞。

- **Apache Web 服务器分块处理漏洞** 在 Apache web 服务器处理分块编码数据的方式中发现了一个可远程利用的漏洞。此漏洞使得能够在 Apache 服务器上远程执行任意命令。更多详细信息可以在 [http://www.cert.org/advisories/CA-2002-17.html](http://www.cert.org/advisories/CA-2002-17.html) 找到。

## POP2 (Post Office Protocol 2)：109 (TCP)

POP2 是用于从邮件服务器访问电子邮件的协议。

**暴力破解** 由于 POP2 认证使用用户名和密码对完成，该协议容易受到暴力破解攻击。

**嗅探** 由于 POP2 是明文协议，因此可以嗅探通过网上传输的 POP2 流量。

### 嗅探 POP2 流量

可以使用如 Ettercap 这样的工具来嗅探 POP2 数据。当使用 `~C` 选项时，`ettercap` 命令会自动过滤并显示通过网络传输的 POP2 用户名和密码。

### 通过 SSH 隧道传输 POP2 流量

使用 SSH 的端口转发选项安全地隧道传输 POP2 流量：

```
ssh -L109:127.0.0.1:109 username@pop2server.somecompanysanexanmple.com
```

## POP3 (Post Office Protocol 3)：110 (TCP)

POP3 是用于从邮件服务器访问电子邮件的协议。

**暴力破解** 由于 POP3 认证使用用户名和密码对完成，该协议容易受到暴力破解攻击。

### 暴力破解 POP3

可以使用 Hydra 来暴力破解 POP3 账户：

```
(bash)$ hydra -L usernames.txt -P passwords.txt 10.0.0.1 pop3
Hydra v2.2 (c) 2002 by van Hauser / THC - use allowed only for legal purposes.
Hydra is starting: !parallel tasks: 4, login tries: 16 (1:4/p:4)
[110][pop3] login: root password: n4mr4t441550cuc3
Hydra finished.
```

### 防止 POP3 暴力破解

请参阅“防止暴力破解攻击的通用防御措施”。

**嗅探** 由于 POP3 是明文协议，因此可以嗅探在网上传输的 POP3 数据。

### 嗅探 POP3 密码

可以使用如 Ettercap 这样的工具来嗅探网络上的 POP3 用户名和密码：

```
(bash)$ ettercap -C -n -m

tettercap 0.6.7 (c) 2002 LloR & NaGA

Your IP: 192.168.1.1 with MAC: 00:01:1A:32:AB:32 on iface: eth0

Loading plugins... Done.

Resolving 1 hostnames...

* | =================== | 100.00 %

Press 'h' for help...

Sniffing (MAC based): ANY <---> ANY
```

```
TCP + UDP packets... (default)

Collecting passwords...

03:35:26 192.168.1.1:49565 <--> 10.0.0.1:110

USER: blamkzman
PASS: b11l13j34h
```

## 通过 SSH 隧道传输 POP3 流量

使用 SSH 的端口转发选项可安全地通过隧道传输 POP3 流量：

```
ssh -L110:127.0.0.1:110 username@pop3server.somecompanyasanexample.com
```

## 端口映射器 (Portmapper)：111 (TCP)

基于 RPC（远程过程调用）的服务，如 NIS（网络信息服务），并不监听静态端口。这些服务会将其端口号注册到端口映射器中。

> 可以使用 `rpcinfo` 命令查询端口映射器中注册的 RPC 服务：`rpcinfo -p hostname`。

**配置错误** NFS 是一种允许通过网络远程访问共享文件的协议。配置不当的 NFS 安装允许未认证用户访问存储关键或隐私数据的网络共享。

### 查询并挂载远程 NFS 共享

使用 `showmount` 程序查询远程主机上的 NFS 共享：

```
[bash]$ /usr/sbin/showmount --all sun1.somecompanyasanexample.com
All mount points on sun1.somecompanyasanexample.com:
all:/etc
```

在此示例中，sun1.somecompanyasanexample.com 的配置错误，导致其 /etc 目录向所有人共享。攻击者可以挂载该 /etc 目录：

```
[bash]$ mount -t NFS sun1.somecompanyasanexample.com:/etc /mnt/etc
```

现在，攻击者可以通过发出以下命令查看 sun1.somecompanyasanexample.com 的 /etc/passwd 文件：

```
cat /mnt/etc/passwd
```

### 阻止和加固 NFS

如果主机上正在运行 NFS，请考虑以下建议：

- 如果未使用 NFS，考虑将其关闭。

- 配置防火墙以阻止 NFS 流量。NFS 运行在端口 2049 上。

- 编辑 `/etc/dfs/dfstab` 和 `/etc/exports`，确保没有向未授权主机提供共享服务。

**软件漏洞** RPC 服务易受许多漏洞的影响，这些漏洞可能导致远程系统被入侵。以下漏洞列举了一些 RPC 服务的安全公告。

- **xdr_array 中的缓冲区溢出漏洞** 由于 `xdr_array()` RPC 中存在缓冲区溢出漏洞，远程攻击者有可能在目标主机上执行任意代码。更多信息请参见 http://securityfocus.com/bid/5356。

- **xfsmd 中的远程命令执行漏洞** 此漏洞影响了 SGI IRIX 实现。由于传递给 RPC 的参数未进行适当的过滤，攻击者可以嵌入 `";"` 和 `"|"` 等元字符。这些参数随后被传递给 `popen()` 函数调用，使攻击者能够在目标机器上执行命令。详细信息请参见 http://securityfocus.com/bid/5075。

- **yppasswd 中的缓冲区溢出漏洞** 在 `yppasswd` 的实现中发现了一个由于边界检查不当引起的缓冲区溢出漏洞。利用此漏洞可能以管理员权限在目标机器上执行命令。更多信息请参见 http://securityfocus.com/bid/2763。

- **statd 中的远程格式化字符串漏洞** 此漏洞影响了随各种 Linux 发行版分发的 `rpc.statd` 程序。由于 `rpc.statd` 无法对用于调用 `syslog()` 函数的用户输入数据进行适当的输入验证，恶意用户可以提供特制数据使其在目标主机上执行。详情可在 http://securityfocus.com/bid/1480 获取。

因此，如果主机正在运行任何 RPC 服务，请考虑以下建议：

- 许多发行版在安装时会启用各种 RPC 服务。请禁用不需要的 RPC 服务。

- 如果不需要 RPC 服务，请禁用端口映射器服务。

- 配置防火墙以禁止远程用户连接到 RPC 服务。

## NNTP（网络新闻传输协议）：119 (TCP)

NNTP 是一种用于分发、查询、检索和发布新闻文章的协议。

**暴力破解** 许多 NNTP 服务器不需要身份验证。然而，可以使用 Hydra 等暴力破解工具对需要身份验证的 NNTP 服务器进行暴力破解。

### 暴力破解 NNTP

使用 Hydra 暴力破解 NNTP 账户。以下是操作方法示例：

```
hydra -L usernames.txt -P passwords.txt 10.0.0.1 nntp
```

### 防止 NNTP 暴力破解
