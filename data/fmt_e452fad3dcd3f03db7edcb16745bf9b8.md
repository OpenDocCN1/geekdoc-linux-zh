
`sftp user@host:file own`

# 安全性较低的服务

这些是不安全的服务，不应该使用，因为它们假设网络是绝对安全的。相反应该使用相应的安全替代方案。

## 第 11 章：什么是互联网服务？

你已成功登录到 FTP 服务器，可以输入 `help` 查看可用命令列表。需要记住的两个重要命令是：`put` 用于将文件从你的机器移动到远程机器，`get` 用于将文件从远程服务器拉到你的机器。要发送多个文件可以使用 `mput`，检索多个文件可以使用 `mget`。`ls` 或 `dir` 可以列出远程端可用的文件列表。

![](img/d1fb1ff3244ecb66d002a5e633e6f729_288_0.png)

要了解更多关于 FTP 命令的信息，请参见第 13 章。

## rsync

`rsync` 是一种类似于 `rcp` 的未加密文件传输程序。它包含一个额外功能，允许仅跨网络传输两台机器上两组文件之间的差异。由于它通过未加密发送流量，因此应该通过 `ssh` 隧道传输。否则请不要使用它。`rsync` 服务器监听在端口 `873`。

## rsh

`rsh` 是一种用于在远程主机上执行命令的未加密机制。在 `rsh` 的命令行中，如果没有给出命令，你将使用 `login` 登录到远程主机。`rsh` 的语法为：

```bash
rsh remotecommand
```

## login

`login` 是一种远程登录程序，将你的终端连接到远程机器的终端。`login` 是一个不安全的协议，因为它以明文形式发送所有信息（包括密码）。它还允许机器与机器之间存在隐式信任关系，使得你无需密码即可使用 `login`。

## finger

`finger` 允许远程系统上的用户查询另一个系统中用户的信息。通常，`finger` 会显示用户的登录名、真实姓名、终端名称、空闲时间、登录时间、办公室位置和电话号码。你应该在本地网络之外禁用 `finger`，因为从其中收集的用户信息可能被用于破坏你的系统。`finger` 守护进程监听端口 `79`。

## talk 和 ntalk

`Talk` 和 `ntalk` 是实时聊天协议。`talk` 服务器运行在端口 `517`，`ntalk` 服务器运行在端口 `518`。要向他人发送 `talk` 请求，请输入 `talk username@hostname` 或 `ntalk username@hostname`。如果他们的服务器正在运行 `talk` 或 `ntalk` 守护进程且他们已登录，他们将看到一条邀请与你聊天的消息。由于即时通讯客户端的流行，`talk` 和 `ntalk` 不如以前那样受欢迎了。

## 将你的 Linux 机器作为服务器

以下章节将为你概述 Linux 上可用的常用服务器协议。

### http

Linux 上最常用的 Web 服务器是 Apache。Apache 通过系统的 rc 脚本启动。Apache 易于配置，其配置文件位于 `/etc/httpd/conf/`。虽然 Apache 可以被设置为监听许多不同的网络端口，但它监听的最常用端口是 `80` 端口。

![](img/d1fb1ff3244ecb66d002a5e633e6f729_289_0.png)

> 需需更多关于安装和配置 Apache Web 服务器的信息，请参见第 15 章。

### sshd

安全 shell 守护进程 (`sshd`) 通过系统的 rc 脚本启动。它的全局系统配置文件位于 `/etc/ssh`，用户的 ssh 配置文件位于 `$HOME/.ssh/`。`ssh` 服务器监听端口 `22`。

![](img/d1fb1ff3244ecb66d002a5e633e6f729_289_1.png)

> `sshd` 可以配置为在备用端口运行。如果端口 `22` 被防火墙拦截，在 `22` 以外的端口运行 `ssh` 将非常有用。在不同端口运行 `ssh` 还增加了一种通过隐蔽实现的安全性。黑客使用的自动扫描器如果不在标准端口上发现 `ssh`，就会忽略你的机器上正在运行 `ssh`。

### ftpd

FTP 守护进程使用端口 `20` 和 `21` 来监听和发起 FTP 请求。
配置文件 `ftpaccess`、`ftpconversions`、`ftpgroups`、`fthosts` 和 `ftpusers` 位于 `/etc` 目录。

你可以在第 13 章找到更多关于设置 FTP 守护进程的信息。

### dns

域名服务 (`DNS`) 将 IP 地址映射到主机名，由 `named` 程序在端口 `53` 提供服务。它的配置文件名为 `/etc` 目录下的 `named.conf`。

要阅读更多关于在你的 Linux 机器上设置 DNS 的信息，请参见第 12 章。

### Inetd Server

`inetd` 被称为互联网超级服务器。它在启动时运行，并监听网络套字上的连接。当 `inetd` 启动时，它会检查 `inetd.conf` 文件查看哪些服务应该运行。它读取 `/etc/services` 文件查看这些服务运行在哪些端口上。列表 11-1 显示了 `/etc/services` 文件的摘录。`/etc/services` 文件是查找运行着哪些重要网络服务的良好参考。如果你好奇一个开放的端口在做什么，请务必查看 `/etc/services` 文件。

列表 11-2 列出的 `inetd.conf` 文件中大多数服务都用行首的 `#` 注释掉了，因此不会运行。在该文件中，某些服务取消注释，例如下面的 `finger` 守护进程，在 `inetd` 启动时运行：

```bash
finger stream tcp nowait /usr/sbin/tcpd.finger
```

`inetd` 启动后，如果 `inetd.conf` 中列出的（未注释的）端口有连接尝试，`inetd` 会启动相应的网络服务。如果 `inetd` 没有在某个端口监听该连接尝试，内核将响应一个重置包以关闭连接。这种设计的优势是，`inetd` 通过启动一个新的进程来减少了负载。

#### 列表 11-1：默认 `/etc/services` 摘录：

```
# /etc/services
# 网络服务, Internet 样式
# 注意，目前 IANA 分配给 TCP 和 UDP 的已知端口号 遵循 RFC 1700。因此，这里的条目仅包含常用端口。
# 每行描述一个服务，格式如下：
# service_name  port/protocol   aliases   comment
charg           19/tcp          nowait  19/udp
ftp-data         20/tcp
ftp-data         20/udp
ftp             21/tcp
ftp             21/udp
ssh              22/tcp          SSH Login
ssh              22/udp          SSH Login
telnet           23/tcp
telnet           23/udp
smtp            25/tcp          mail
smtp            25/udp          mail
time             37/tcp          timserver
time             37/udp          timserver
rlp              39/tcp          resource location
rip              39/udp          resource location
nameserver        42/tcp          name
nameserver        42/udp          name
nicname          43/tcp          whois
nicname          43/udp          whois
tacacs           49/tcp          Login Host (TACACS)
tacacs           49/udp          Login Host (TACACS)
mail-ck          50/tcp          Remote Mail Checking Protocol
mail-ck          50/udp          Remote Mail Checking Protocol
domain           53/tcp          nameserver server
domain           53/udp          nameserver server
whois++          63/tcp          whois
whois++          63/udp          whois
bootps           67/tcp          BOOTP server
bootps           67/udp          BOOTP server
```
