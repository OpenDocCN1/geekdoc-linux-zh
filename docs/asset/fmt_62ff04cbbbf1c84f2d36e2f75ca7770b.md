
```
n=MIGFMAQCSQsibbD3BEQAAAGNAADQIBKgQDreeOR4j/cutQFiUY
E9UGSAX/2PLjJnITDBV44nn+2FAVGE63Lb23eOUlyYv4PeleB3bfgm"
jJDIOUKN3sL4KJAUHHFwDetobn+s8VKKYETATL2Yr/s37Xhy+1t4JxRD
V77Xtn56Lub4donUnwXKV4b5PDOj+XcwiADAB;n=1024 bit key."
```

在这里，`n=` 子句再次是一个注释，这次是关于密钥本身的。

本节所示的 DKIM 记录都是 TXT 记录，但它们将迁移到 DKIM 记录类型，其格式相同。在此期间，站点可以使用两种记录类型以确保不会出现过渡问题。

第 20 章涵盖了在邮件系统中实现 DKIM 所的步骤。

# SSHFP 资源记录

SSH（安全外）允许在不安全的网络上进行安全登录。它使用了两种身份验证方案：针对主机本身以及针对登录的用户。遗憾的是，用户通常会接受 `ssh` 呈现给他们的任何密钥，而不进行验证。DNS 的 SSHFP 记录让 `ssh` 自动验证主机密钥，确保用户连接的是预期的机器而不是冒充者。

SSHFP 记录在 RFC4255 (2006) 中规定。

16. 然而，给定的 URL 重定向到 storeforge.net，关于 DomainKeys，这一标准大多已被遗弃。

# DNSSEC 资源记录

为了保持数据包大小最小，SSHFP 记录并不存储主机公钥的完整副本。相反，它们存储这些密钥的摘要（即加密哈希值）。其语法如下：

```
name [ttl] SSHFP algorithm# fingerprint_algorithm# fingerprint
```

`algorithm#` 标识生成主机密钥的公钥加密系统。该算法实际上并不用于验证过程；它通常由远程主机使用，以确保双方讨论的是同类型的密钥。RSA 是算法 1，DSA 是算法 2。

`fingerprint` 是要匹配的哈希值，`fingerprint_algorithm#` 告诉如何处理远程主机提供的公钥以生成用于比较的哈希。目前只定义了一种哈希算法（SHA-1），因此该字段的内容始终为 1。

以下是来自 RFC4255 的示例：

```
host.example. SSHFP 2 123456789abcdef6789123456789abcdef67890
```

SSH 同时需要 RSA 和 DSS 密钥；用户端通常将它们存储在 `/etc/ssh` 中，名称类似于 `ssh_host_rsa_key` 和 `ssh_host_dsa_key.pub`。SSH 接受用户主目录下 `.ssh/hosts` 文件中的公钥。

你可以从该目录获取主机密钥以构建你的 SSHFP 资源记录。最新版本的 `ssh-keygen` 可以通过 `-r` 和 `-g` 标志生成 SSHFP DNS 记录。Linux 上还有一个适用于 UNIX（`freesports.org/dns/sshfp`）的 `sshfp` 守护进程，可以将密钥转换为指纹并生成必要的 DNS 记录。

你可以通过将 `VerifyKeyDNS` 选项设置为 `yes` 来要求 OpenSSH 使用 SSHFP 记录。SSH 支持身份验证和验证方法，由于 SSHFP 记录尚未广泛使用，你不应该将其作为唯一的可能选项。先尝试 SSHFP，如果失败，则回到提示用户手动确认密钥（正如 SSHFP 出现之前）。有关配置 SSH 的更多信息，请参见第 22 章“安全”第 926 页。

与 SPF 和 DKIM 记录一样，SSHFP 系统在很大程度上保证了你正在使用 DNSSEC 且 DNS 记录是可靠的。目前可能并非如此，但 DNSSEC 正在受到关注。

# 第17章 DNS：域名系统

## 版本确定

厂商往往并不会在文档中记录他们在系统中包含了哪个版本的软件包包，因此你可能需要进行一些“侦探”工作才能准确找到你正在处理的软件到底是什么。你有时可以通过一个巧妙的挖掘——即一个与 BIND 附带的命令——来确定版本号。

```
$ dig @server version.bind txt chao
```

这将返回版本号，除非有人决定通过更改 BIND 配置文件中的设置来隐瞒信息。首先，通过以下命令确定相关域名的名称服务器的名称：

```
$ domain ns
```

然后查询 `version.bind` 查询。例如，该命令在 isrc 处可以工作：

```
$ dig @ns-ext.isc.org version.bind txt chao
version.bind 0 CH TXT "9.5.1"
```

但在 cs.colorado.edu 上却不起作用：

```
$ dig @mroe.cs.colorado.edu version.bind txt chao
version.bind 0 CH TXT "wouldn't you like to know..."
```

一些站点配置了 BIND 以隐藏其版本号，其理论是这可以提供某种程度的“模糊性安全性”。我们并不支持这种做法，但它可能有助于抵御一些脚本小子（script kiddies）。关于此主题的更详细描述请参见第603页。

此示例查询适用于其他 DNS 软件；例如，

```
$ dig @root-servers.net version.bind txt chao
version.bind 0 CH TXT "NSD 2.3.7"
```

显示 K 根名称服务器正在运行。

CHAOS 类中的另一部分数据标识了被查询的服务器名称。但是——如果你刚刚查询了服务器，你应该知道它的名字，对吧？实际上，最繁忙的服务器（例如根名称服务器）实际上是分布在全球各地的多台机器，具有相同的服务器名称和 IP 地址。这种复制方案被称为“任播路由（anycast routing）”。路由系统将你带到“最近”的实例。然而，如果你是试图调试问题的系统管理员，那么区分你访问的是复制服务器中的哪一个可能非常重要。例如，

```
$ dig @root-servers.net hostname.bind txt chao
hostname.bind 0 CH TXT "k2.nap.k.ripe.net"
```

> 17. 答案中的 0 是数据值。我们的一个报告员注意到，此查询的结果显示为“Name as Bind, James Bind!”

或者

```
$ dig @k.root-servers.net id.server txt chaos
id.server.    0 CH TXT "k2.nap.k.ripe.net"
```

IETF 试图将这些奇怪的 CHAOS 类名称标准化为独立的密集形式 `version.server` 和 `id.server`，但只有 `id.server` 通过了该过程；`version.server` 最终出现在了一个变成 RFC 的 IETF 草案中。NSD 使用所有四形式，但仅使用三个批准的形式。

作为管理员，你可以使用 `-v` 标志启动服务器（名为 `nsd`），将其版本打印到标准输出并退出。在 Linux 上，你可以询问你的包管理器安装了哪个版本。你也可以通过检查 `/var/log` 或其系统对应的日志文件来确定 BIND 版本。BIND 服务器在启动时会将版本记录到 `syslog` (daemon)。使用 `grep` 搜索 BIND 可以获取如下行：

```
Jul 13 07:19:55 nubark named[757]: starting BIND 9.5.0-P2 -u named
```
