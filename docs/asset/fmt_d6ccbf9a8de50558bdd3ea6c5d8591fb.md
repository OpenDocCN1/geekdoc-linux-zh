
# 表 12.1 crontab 字段描述，从左到右（从 crontab 读取）

| 字段 | 格式 |
|---|---|
| 分钟 | 0–59 或 * |
| 小时 | 0–23 或 * |
| 日 | 1–31 或 * |
| 月份 | 1–12 或 * |
| 星期 | 0–6 (0=星期日) 或 * |
| 命令 | 要执行的命令 |

每个字段可以包含多个由逗号分隔的值，星号表示该字段的所有可能值。此外，大多数 Linux 发行版提供的 vixie-cron 允许你使用斜杠后续间隔来指定时间间隔。例如，要每 5 分钟运行一次`/usr/local/bin/cleanup`命令，你可以输入：

```bash
*/5 * * * /usr/local/bin/cleanup
```

而 System V 的 crontab 将强制要求单独指定每个时间，如下：

```bash
0,5,10,15,20,25,30,35,40,45,50,55 * * * * /usr/local/bin/cleanup
```

# 自动化 root 登录

大多数管理任务都需要 root 权限。在单机上任务很容易，但在多用户环境中，情况会变得复杂，因为你可能需要以 root 身份运行或复制文件。在交互式情况下，管理员可以简单使用 root 密码登录；然而，这种选项并不自动化进程。你不需要在脚本中放置密码。

## 无需密码使用 Berkeley r-commands

在远程系统上执行命令的最旧方法之一是使用 Berkeley r-commands，它因其远程访问能力命名。三个 r-commands 可以在远程系统上执行任务：

- `rcp`——从或到远程系统复制文件
- `rlogin`——登录到远程系统
- `rsh`——在远程系统上运行命令

r-commands 允许你在没有密码的情况下登录远程机器或在其运行进程，即使是 root 身份。远程服务器上的两个配置文件控制你的访问：`/etc/hosts.equiv`和`.rhosts`。这两个文件包含以下内容的行：

`hostname`是允许无密码登录的主机名；`username`是允许从该主机登录的可选用户名。同一个主机可以指定多个用户名；如果未指定，则允许所有用户无密码登录。使用 r-commands 的唯一要求是两台机器的用户 UID 必须相同。可以使用`+`替换主机或用户名，以匹配该主机或用户之前的项并拒绝访问。

`/etc/hosts.equiv`控制机器上所有用户的访问规则；`.rhosts`位于用户目录下，仅控制对特定账户的访问。为了增加安全性，`/etc/hosts.equiv`文件必须由 root 所有，`.rhosts`必须由尝试访问的用户所有。整个认证机制通常被称为“主机”认证机制。

一些配置示例可能会帮助。

要让`server1`的`Jeremy`远程访问自己的账户，请在`Jeremy`的`.rhosts`中添加以下内容：

```text
server1
```

要授予用户`Jason`和`Scott`在任何远程主机上访问本地系统上任何账户的权限，请在`/etc/hosts.equiv`中添加以下内容：

```text
+ jason scott
```

就本章内容而言，你可以允许从特定主机访问 root 账户。例如，要允许从机器`server1`访问，你可以将`server1`添加到 root 的 hosts 文件中。相反，如果你将`server1 root`添加到`/etc/hosts.equiv`，那么你允许的不仅是远程 root 用户对 root 的访问，还允许了客户端上的任何用户对 root 账户的访问。

既然你已经以 root 身份登录了，就可以执行各种远程管理任务。例如，使用这些命令将新版本的`/etc/inetd.conf`复制到另一台服务器并重启`inetd`。

```bash
# rcp /etc/inetd.conf server1:/etc/inetd.conf
# rsh server1 -kill HUP inetd
```

为两或三台服务器设置这种访问权限似乎有些多此一举，但当你需要干预几十或上百台服务器时，r-commands 可以成为极其宝贵的管理工具。

# r-commands 的安全风险

在 20 世纪 90 年代初期出现之前，Berkeley r-commands 是远程命令执行的首选工具。但 r-commands 提供的安全性很低——这是当今公共访问网络中的首要问题。不仅 r-command 的网络流量是不加密的，更令人担忧的是服务器对客户端的信任。

在允许用户从任何主机登录的服务器上，例如，恶意用户可以轻松地在同一网络上为与服务器上具有相同 UID 的用户安装他自己的系统。那么，后一个用户就可以无需密码登录服务器了。如果你有多个 root 访问权限，这种前景就变得更加可怕了。

![](img/894492738e879267320b8d6f9a044180_361_0.png)

> 主机限制可能被破解
>
> 即使是 r-command 限制也可以通过伪造 IP 数据包中的源地址来破解。这被称为身份欺骗，你可以在第 13 章“实现系统安全”中阅读更多相关信息。

# 使用 SSH 代替 r-commands

解决 r-command 安全问题的一种方案是在受信网络上仅使用 r-commands。当无法这样做时，可以使用 SSH（安全外壳）。除了使用加密通道外，SSH 还提供了公钥身份验证，可用于无密码登录。OpenSSH 源自 OpenBSD 操作系统，正迅速成为 Unix 系统最受欢迎的 SSH 服务器。它可以从`http://www.openssh.org`免费获取，并作为许多 Linux 版本的标准配置包含。

# 尽可能使用 SSH，但记住如何使用 r-commands

尽可能时始终使用 SSH 代替 r-commands，特别是在远程向 root 运行命令时。加密和高级安全机制为执行管理任务提供了一个更安全的环境。然而，记住 r-commands 是什么以及如何使用它们是非常重要的，因为 SSH 并不总是可用的，特别是在新加载的系统上。

公钥身份验证的细节超出了本书的范围，但总的来说，系统使用两个非对称密钥，其中一个密钥可以解密由另一个密钥加密的数据。其中一个密钥是私钥，应该保持保密，但另一个是公钥，可以分发而不必担心破坏安全性。

在传统的对称密钥加密中，用于加密和解密的密钥是相同的。客户端使用私钥生成签名，任何没有该密钥的人都无法伪造。服务器通过其公钥副本解密签名来验证签名，身份验证完成。

# SSH 可以使用 hosts 验证

SSH 也可以配置为使用 hosts 验证，但除非配合公钥身份验证，否则不建议这样做。尽管流量是加密的，源地址仍然可以被伪造，导致 Berkeley r-commands 无法解决相同的问题。

为 root SSH 设置公钥身份验证非常简单。你可以使用 OpenSSH 3.1pl（大多数 Unix 版本免费提供）来执行以下设置。首先，你需要使用`ssh-keygen`生成密钥对（公钥和私钥）。

```bash
# ssh-keygen -t rsa -b 1024
Generating public/private rsa key pair.
Enter file in which to save the key (~/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in ~/.ssh/id_rsa.
Your public key has been saved in ~/.ssh/id_rsa.pub.
The key fingerprint is:
1a:7e:c0:72:2a:74:41:36:db:1bf:3f:fe:d5:54@server1
```

你创建了一个 1024 位的 RSA 密钥，并将密钥存储在`~/.ssh/id_rsa`，将公钥存储在`~/.ssh/id_rsa.pub`。如所述，SSH 支持使用密码短语来加密私钥，但由于你用它来辅助身份验证，你使用了空密码短语，保持密钥未加密状态。由于其敏感性，私钥仅对 root 可读，但公钥用于分发，并以人类可读的格式存储。

```text
# id_rsa.pub
ssh-rsa AAAAB3NzaN1yc2AAAAAAAABQAAABAIAYtn8V3prqrQtaMFG0kXM/81YPRLUbJrROvqh/HHQEYWW54KaWbbt+Dw7GsfFRvvkHtrCcVZMMyq04C0sGsjV1APMyq0zcMgy8ltvsVOEFPAH@server1
```

# UNIX 系统管理进

# 密钥对长度
