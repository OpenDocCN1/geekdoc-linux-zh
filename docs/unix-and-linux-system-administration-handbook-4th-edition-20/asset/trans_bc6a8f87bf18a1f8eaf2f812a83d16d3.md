

## 第 22 章 安全

互联网上的软件软件包随附 PGP 签名文件分发，该文件旨在保证软件的来源和纯洁性。然而，对于不是硬核 PGP 用户的人来说很难验证这些签名——这并不是因为过程复杂，而是因为真正的安全只能来自于一个你直接验证过身份的个人公密钥库。下载带有签名文件的单个公密钥和软件发行包与下载发行包本身相当。

某些客户端（如 Mozilla Thunderbird）拥有插件，可以为加密的进出消息提供简单的 GUI。作为 Thunderbird 的解决方案，Enigmail 即使你的接收者不在你的密钥环中，它也可以搜索在线公密钥数据库。详情请参见 enigmail.moz.dev。

## SSH：安全外壳

SSH 系统由 Tatu Yönen 编写，是登录、rcp 和 telnet 的安全替代方案。它使用加密认证来确认用户身份，并加密两个主机之间的所有通信。SSH 使用的协议旨在抵御各种潜在攻击。该协议由 RFC 4250 至 4256 文档，现在是一项提议中的 IETF 标准。

SSH 已从一个免费分发的开源项目（SSH1）演变为略有不同（且更安全）的协议 SSH2。幸运的是，开源社区做出了响应，发布了优秀的 OpenSSH 软件包（由 FreeBSD 维护），该包现在实现了这些协议。

SSH 的主要组件是一个服务器守护进程 `sshd` 和一些用户级命令，特别是用于远程登录的 `ssh` 以及用于复制文件的 `sftp/scp`。其他组件包括一个生成公密钥的 `ssh-keygen` 命令以及几个帮助保护 X Windows 的实用程序。

sshd 可以以不同的方式验证用户登录。由管理员决定这些方法哪些是可以接受的：

- 方法 A：如果用户登录的远程主机名列在 `~/.hosts`、`~/shosts`、`/etc/hosts.equiv` 或 `/etc/hosts` 中，ssh 将自动登录无需密码检查。这种方案镜像了旧的 login 守护进程，在我们看来，在正常情况下是永远不可接受的。

- 方法 B：作为方法 A 的改进，sshd 还可以使用公钥加密来验证远程主机的身份。要实现这一点，远程主机的公密钥（安装时生成）必须列在本地主机的 `/etc/ssh/known_hosts` 文件或用户的 `~/.ssh/known_hosts` 文件中。

如果远程主机可以证明它知道相应的私钥（通常存储在 `/etc/ssh_host_key`，一个世界不可读的文件），则 sshd 将在不询问密码的情况下登录用户。

方法 B 比方法 A 更严格，但我们认为它仍然不够充分。如果源主机的安全性被破坏，本地站点也将受到破坏。

- 方法 C：sshd 可以使用公钥加密来建立用户身份。登录时，用户必须能够访问其私钥文件的副本，并提供密码来解密它。密钥也可以在没有密码的情况下创建，这对于从远程系统自动登录来说是一个合理的选项。

这种方法最安全，但设置起来很麻烦。它意味着用户在旅行时，除非带上私钥文件的副本（可能在 USB 闪盘上，最好已加密），否则无法登录。

如果你决定使用密钥对，请在故障排除过程中充分使用 `/ssh -y`。

- 方法 D：最后，sshd 允许用户输入其普通登录密码。这使得 ssh 的行为非常像 telnet，但密码和会话都是加密的。这种方法的主要缺点是，如果你没有加强安全，系统登录密码可能是弱的，而且现成的工具（如 John Ripper）被设计用来破解它们。然而，这种方法可能是正常使用的最佳选择。

认证策略设置在 `/etc/ssh_config` 中。在安装过程中，该文件会为你填充配置内容，你可以安全地忽略它的大部分内容。与认证相关的选项所示表 22.2。

## 表 22.2 /etc/ssh_config 中的认证相关选项

| 选项 | 方法 | 默认 | 开启时的含义 |
| --- | --- | --- | --- |
| RhostsAuthentication | A | No | 遵循 ~hosts, /etc/ssh.equiv, 等 |
| RhostsRSAAuthentication | B | Yes | 允许通过密钥 ~hosts，但需要主机密钥 |
| IgnoreHosts | A | No | 忽略 ~/hosts 和 hosts.equivᵇ |
| IgnoreRootHosts | A | Noᶜ | 阻止 root 的/hosts 认证 |
| RSAAuthentication | C | Yes | 允许每个用户的公钥认证 |
| PasswordAuthentication | D | Yes | 允许使用普通登录密码 |

a. 此变量相关的认证方法
b. 但继续尊重 ~/hosts 和 hosts.equiv
c. 默认为 IgnoreHosts 的值

我们建议的配置允许方法 C 和 D 但不允许方法 A 或 B，如下：

```
RhostsAuthentication no
RhostsRSAAuthentication no
RSAAuthentication yes
PasswordAuthentication yes
```

允许 root 通过 sudo 登录永远是不明智的。超级用户访问应该通过使用 sudo 实现。为了鼓励这种行为，你使用选项：

```
PermitRootLogin no
```

当你第一次通过 SSH 连接到新系统时，会提示你接受服务器的公密钥（这通常是服务器安装 OpenSSH 的一部分生成的，或在此之后不久）。真正偏执的用户可能会手动验证它，但我们大多数人都会盲目接受密钥，然后将其存储在 `~/.ssh/known_hosts` 文件中供以后使用。除非密钥更改，否则 SSH 不会提到服务器密钥。用户盲按键，如果主机密钥实际上是由攻击者的系统提供的，你就会受到中间人攻击。

已经开发了一种名为 SSHFP 的 DNS 记录来解决这一漏洞。前提是服务器的密钥被存储为 DNS 记录。当客户端连接到未知系统时，SSH 会查找 SSHFP 记录来验证服务器密钥，而不是请求用户验证。

从 xelerance/software/sshfp 获取的 `sshfp` 工具通过扫描远程服务器或解析从 known_hosts 文件中之前接受的密钥来生成 SSHFP DNS 资源记录。（当然，任何一种选择都假设密钥源是正确的）。用法非常简单：使用 -s 标志从网络扫描生成密钥，或使用 -k 更改 known_hosts 文件（默认值）。例如，以下命令为 solaris.booklab.astrust.com 生成一个兼容 BIND 的 SSHFP 记录。

```
solaris$ sshfp solaris.booklab.astrust.com
solaris.booklab.astrust.com IN SSHFP 1 1 94a2678ee713a3f6a78110fad9bd
saris.booklab.astrust.com IN SSHFP 2 1 7cf7d202e3d2f93a47125bcde0a6...
```

将这些记录添加到域区域文件（注意名称和 ORIGIN），重新加载域，并使用 dig 验证密钥：

```
solaris$ dig solaris.booklab.astrust.com IN SSHFP | grep SSHFP
;>>> 9.5.1-P2 << solaris.booklab.astrust.com IN SSHFP
solaris.booklab.astrust.com IN SSHFP 1 1 94a2678ee713a3f6a78110fad9bd
saris.booklab.astrust.com IN SSHFP 2 1 7cf7d202e3d2f93a47125bcde0a6
```

ssh 默认情况下不查询 SSHFP 记录。在 /etc/ssh_config 中添加 `VerifyHostDNS` 选项以启用它。在大多数 SSH 客户端中，你可以在首次访问新系统时在命令行使用 -o "VerifyHostDNS yes"。

SSH 还有一些辅助功能对系统管理员很有用。其中之一是可以通过加密通道传输 TCP 连接，从而允许访问不安全或受防火墙保护的服务器。这种功能在 SSH 客户端中非常通用且配置简单。图 A 展示了一个典型的隧道用法，并有助于理解其工作原理。

## 图 A 用于 RDP 的 SSH 隧道

![](img/579ec8c67772f31ecf348bbb71a2_977_0.png)

在这种场景下，远程用户想要与企业网络上的 Windows 系统建立 RDP（远程桌面）连接。对该主机或3389端口的访问被防火墙拦截，但由于用户拥有 SSH 权限，可以通过 SSH 服务器路由连接。

要进行设置，用户使用 ssh 登录到远程 SSH 服务器。在命令行上，他指定了一个任意但特定的（在本例中为9989）本地端口，ssh 通过安全隧道转发到远程 Windows 机器的3389端口。（对于标准的 OpenSSH 实现，请求此行为的选项是 -Llocalport:remote。）

为了访问 Windows 桌面，用户随后打开远程桌面客户端（此处是 rdesktop），并将 localhost:9989 作为连接服务器的地址。本地 ssh 接收端口 9989 的连接并通过现有连接传输流量到远程 ssh。随后，sshd 将连接转发到 Windows 主机。

当然，此类隧道也可能是故意或无意的后门。系统管理员在使用隧道时应保持谨慎，并留留意用户对该功能的未经授权的滥用。

