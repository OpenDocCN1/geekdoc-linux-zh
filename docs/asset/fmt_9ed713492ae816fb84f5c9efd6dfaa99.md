
在远程系统上，只需将 `identity.pub` 的完整内容粘贴到相应用户的 `$HOME/.ssh/authorized_keys` 文件中。例如，假设您希望使用 RSA 认证从 `caldera.example.com` 和 `redhat.example.com` 以 `ramon` 身份登录到 `suse.example.com`。只需获取 `caldera.example.com` 和 `redhat.example.com` 上 `identity.pub` 文件的内容，并将它们插入到 `suse.example.com` 的 `.ssh/authorized_keys` 中，如下所示：

```
[ramon]$ more .ssh/authorized_keys
1024  35  26176632424407803465195431089535298792515594463718945638870
09604555778782718989579135711356899802512356584624119858367310429373
619374038515642525995896839408208733045515172702470073209042978615
060322444446644529326292l876776658946288815292526320347023048092384
080921427992348792734979234701 ramon@caldera.example.com

1024 35 239048023495285104318364350181929090082244038957726458073723
565897353708317804367538174812197037594693987194l8848857474810l78479
54020737l6338624148l285585501347l3088523618l26l6l60458988l194l99349l
027939235137895964935l038996402419l71l520040453399005458087l2560344ll
802109537l6628465097l8l09183l89 ramon@redhat.example.com
```

请注意，您在远程机器上使用了两个不同的用户名（`caldera.example.com` 上的 `ramon` 和 `redhat.example.com` 上的 `ramon`）。只要您将这些密钥正确输入到 `suse.example.com` 的 `.ssh/authorized_keys` 文件中，这样完全没有问题。

#### 使用 OpenSSH

第一次启动 `sshd` 守护进程时，您会看到以下内容：

```
[ramon]$ sudo /etc/rc.d/init.d/sshd start
Generating RSA keys:  Key generation complete.
Your identification has been saved in /etc/ssh/ssh_host_key.
Your public key has been saved in /etc/ssh/ssh_host_key.pub.
The key fingerprint is:
96:26:e0:4b:4e:9b:28:6d:e7:b9:92:65:lb:7a:7c:09 root@redhat.example.com
Generating DSA parameter and key.
Your identification has been saved in /etc/ssh/ssh_host_dsa_key.
Your public key has been saved in /etc/ssh/ssh_host_dsa_key.pub.
The key fingerprint is:
09:92:6c:84:28:54:8b:45:7d:a7:d6:76:80:ld:2l:b2 root@redhat.example.com
Starting sshd: [ OK ]
```

如前所述，守护进程知道这是它第一次运行，并创建了两组密钥，即 RSA 和 DSA 密钥，以兼容旧版本。从现在开始，`sshd` 守护进程将使用这些密钥向远程主机进行身份验证，类似于在用户级别使用 RSA 进行身份验证的方式。

RSA 密钥存储在以下文件中：

- `/etc/ssh/ssh_host_key`（私有部分）

- `/etc/ssh/ssh_host_key.pub`（公有部分）

DSA 密钥位于以下文件中：

- `/etc/ssh/ssh_host_dsa_key`（私有部分）

- `/etc/ssh/ssh_host_dsa_key.pub`（公有部分）

现在，你已准备好通过 22 端口接受 SSH 连接。请确保位于 OpenSSH 服务器前面的任何外围安全设备都允许对 TCP 22 端口的入站连接。

SSH 客户端接受许多命令行选项。表 12.3 列出了其中最重要的一些。

**表 12.3：** `ssh` 客户端命令行选项

| 选项 | 含义 |
|:-----------|:-----------|
| `-l user` | 以用户名 `user` 登录。 |
| `-i file` | RSA 身份验证的身份文件（而非 `$HOME/.ssh/identity`）。 |
| `-v` | 显示详细输出（对调试很有用）。 |
| `-V` | 显示版本号。 |
| `-q` | 不显示任何消息（安静模式）。 |
| `-c [3des` `blowfish]` | 选择一种加密算法。 |
| `-C` | 启用压缩。 |
| `-o option` | 仅为当前会话指定一个选项（使用与 `/etc/ssh/ssh_config` 相同的格式）。 |

例如，要使用 Blowfish 加密算法以 `root` 用户身份连接到远程 SSH 服务器 `remote.example.com`，请使用以下命令：

```bash
[ramon]$ ssh -l root -c 'blowfish' remote.example.com
root@remote.example.com's password:
Last login: Wed Feb 7 16:55:33 2001 from redhat.example.com
remote:~ #
```

或者，要连接到同一服务器并关闭 `StrictHostKeyChecking` 选项（列在表 12.2 中），请使用以下命令：

```bash
[ramon]$ ssh -l root -c 'blowfish' -o StrictHostKeyChecking=no \
remote.example.com
Warning: Permanently added 'remote.example.com,209.207.155.67' (DSA)
to the list of known hosts.
root@remote.example.com's password:
Last login: Wed Feb 7 17:03:37 2001 from redhat.example.com
remote:~ #
```

请注意，本地 SSH 客户端已警告你，你已从远端接收到一个 DSA 主机密钥。如果你需要禁用 `StrictHostKeyChecking` 选项，我建议你与服务器管理员一起检查结果主机密钥的有效性（最好在离线状态下进行）。

### 总结

本章介绍了虚拟专用网络的概念以及该技术在你的 Linux 网络中日益普及的作用，尤其是如果你的公司有几个需要互联的分支机构的话。IPsec 规范已被普遍接受为实现 VPN 端点的首选方案，并且 FreeS/WAN Linux 实现包含了你将其作为生产解决方案推出的所有必要功能。

对于受保护内部资源的远程访问，PPTP 协议允许你利用大量可能已安装的符合 PPTP 标准的 Windows 远程用户。与强制你推出专有客户端的 VPN 技术相比，这是一个巨大的优势。虽然 Windows 2000 现在附带 IPsec 功能，但较旧的 Windows 版本（95、98 和 NT）缺乏成熟的 IPsec 客户端。PopTop Linux PPTP 包现在处于 1.1 版本，并且为基于 Windows NT 或 2000 的 PPTP 服务器提供了一个很好的替代方案。

安全外壳（SSH）是你 Linux 服务器的必备补充，特别是当你需要交互式登录并使用密码认证时。虽然 SSH 对用户名/密码交换进行了加密，但使用 RSA 身份验证进一步确保了你不在线路上暴露密码信息。

下一章将本书收尾，探讨使用秘钥技术、一次性密码以及 Linux 如何为异构认证机制提供无缝支持等强认证问题。

# 强用户身份验证

大量安全漏洞是由于通过窃听和暴力猜测攻击窃取认证凭证（密码或其他密钥）所致。本章通过介绍两种强身份验证机制来解决这两个问题：Kerberos 密钥身份验证系统和 S/Key 一次性密码系统。
