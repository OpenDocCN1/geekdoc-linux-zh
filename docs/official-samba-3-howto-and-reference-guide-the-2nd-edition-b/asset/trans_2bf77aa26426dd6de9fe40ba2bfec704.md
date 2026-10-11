
## 该选项告知 smbd(8) 在作为 WINS 服务器（wins support = yes）时，nmbd 授予的 NetBIOS 名称的最大“生存时间”（以秒为单位）

该选项告知 smbd(8) 在作为 WINS 服务器（*wins support = yes*）时，**nmbd** 授予的 NetBIOS 名称的最大“生存时间”（以秒为单位）。您永远不需要更改此参数。默认值为 6 天（518400 秒）。

## max xmit (G)

**默认值：** `max xmit = 65535`

**示例：** `max xmit = 8192`

此选项控制 Samba 协商的最大数据包大小。默认值为 65535，这是最大值。在某些情况下，您可能会发现使用较小的值能获得更好的性能。低于 2048 的值可能会导致问题。

## message command (G)

**默认值：** `No default`

**示例：** `message command = csh -c ‘xedit %s;rm %s’ &`

这指定了当服务器接收到 WinPopup 风格的消息时运行的命令。

通常，这将是一个以某种方式传递消息的命令。具体如何操作取决于您的想象力。

一个示例如下：

```
message command = csh -c ‘xedit %s;rm %s’ &
```

这使用 xedit 传递消息，然后将其删除。*请注意，该命令必须立即返回这一点非常重要。* 这就是我末尾加上 ‘&’ 的原因。如果它不立即返回，您的计算机在发送消息时可能会冻结（希望它们能在 30 秒后恢复）。

所有消息都以全局来宾用户的身份传递。该命令采用标准替换，尽管 *%u* 不起作用（*%U* 在这种情况下可能更好）。

除了标准替换外，还有一些额外的替换适用。特别是：

- *%s* = 包含消息的文件名。
- *%t* = 消息发送到的目标（通常是服务器名称）。
- *%f* = 消息的发送者。

您可以让此命令发送邮件，或者做其他您感兴趣的事情。请让我们知道您有任何真正有趣的主意。

以下是将消息作为邮件发送给 root 的一种方法：

```
message command = /bin/mail -s ‘message from %f on %m’ root < %s; rm %s
```

如果您没有设置消息命令，那么消息将不会被传递，Samba 会告知发送者发生了一个错误。不幸的是，*Windows* 会完全忽略错误代码并继续操作，声称消息已被传递。

如果您想静默删除它，请尝试：

```
message command = rm %s
```

## min passwd length

此参数是 *min password length* 的同义词。

## min password length (G)

**默认值：** `min password length = 5`

此选项设置在执行 UNIX 密码更改时，**smbd** 接受的明文密码的最小字符长度。

## min print space (S)

**默认值：** `min print space = 0`

**示例：** `min print space = 2000`

这设置了在用户能够调度打印作业之前必须可用的最小空闲磁盘空间。以千字节为单位。默认值为 0，这意味着用户始终可以调度打印作业。

## min protocol (G)

**默认值：** `min protocol = CORE`

**示例：** `min protocol = NT1`

该参数的值（字符串）是 Samba 将支持的最底层 SMB 协议方言。请参阅 *max protocol* 参数以获取有效协议名称列表及每个协议的简要描述。您还可以参考 *source/smbd/negprot.c* 中的 C 源代码，以了解客户端支持的已知协议方言列表。

如果您将此参数视为安全措施，您还应参考 *lanman auth* 参数。否则，您永远不需要更改此参数。

## min wins ttl (G)

**默认值：** `min wins ttl = 21600`

此选项告知 **nmbd(8)** 在作为 WINS 服务器（*wins support = yes*）时，**nmbd** 授予的 NetBIOS 名称的最小“生存时间”（以秒为单位）。您永远不需要更改此参数。默认值为 6 小时（21600 秒）。

## msdfs proxy (S)

**默认值：** `No default`

**示例：** `msdfs proxy = \otherserver\someshare`

此参数指示该共享是另一个 CIFS 共享的替代项，其位置由该参数的值指定。当客户端尝试连接到此共享时，它们将使用 SMB-Dfs 协议重定向到被代理的共享。

只有 *Dfs 根* 才能充当代理共享。查看 *msdfs root* 和 *host msdfs* 选项以了解如何设置 Dfs 根共享。

## msdfs root (S)

**默认值：** `msdfs root = no`

如果设置为 **yes**，Samba 会将该共享视为 Dfs 根，并允许客户端浏览以该共享目录为根的分层文件系统树。Dfs 链接通过共享目录中形如 **msdfs:serverA\shareA,serverB\shareB** 等的符号链接指定。有关在 Samba 上设置 Dfs 树的更多信息，请参阅第 19 章，“托管 Microsoft 分布式文件系统树”。

## name cache timeout (G)

**默认值：** `name cache timeout = 6600`

**示例：** `name cache timeout = 0`

指定在 samba 的主机名解析缓存中的条目超时之前经过的秒数。如果超时设置为 0，则禁用缓存。

## name resolve order (G)

**默认值：** `name resolve order = lmhosts host wins bcast`

**示例：** `name resolve order = lmhosts bcast host`

Samba 套件中的程序使用此选项来确定使用哪些命名服务以及按什么顺序将主机名解析为 IP 地址。其主要目的是控制如何进行 netbios 名称解析。该选项接受由空格分隔的名称解析选项字符串。

选项包括："lmhosts"、"host"、"wins" 和 "bcast"。它们导致名称按以下方式解析：

- **lmhosts**：在 Samba lmhosts 文件中查找 IP 地址。如果 lmhosts 中的行未附加 NetBIOS 名称类型（有关详细信息，请参阅 [smb.conf(5)](index.html) [lmhosts(5)](index.html) [smb.conf info](index.html)），则任何名称类型都匹配查找。
- **host**：执行标准的主机名到 IP 地址的解析，使用系统的 /etc/hosts、NIS 或 DNS 查找。这种名称解析方法取决于操作系统，例如在 IRIX 或 Solaris 上，这可能由 /etc/nsswitch.conf 文件控制。请注意，仅当被查询的 NetBIOS 名称类型是 0x20（服务器）名称类型或 0x1c（域控制器）时才使用此方法。后者仅对活动目录域有用，并导致针对与 _ldap._tcp.domain 匹配的 SRV RR 条目的 DNS 查询。
- **wins**：使用 WINSSERVER 参数中列出的 IP 地址查询名称。如果未指定 WINS 服务器，则忽略此方法。
- **bcast**：在 interfaces 参数中列出的每个已知本地接口上进行广播。这是名称解析方法中最不可靠的一种，因为它取决于目标主机位于本地连接的子网中。

以下示例将导致首先检查本地 lmhosts 文件，然后尝试广播，最后进行正常的系统主机名查找。

当 Samba 以 ADS 安全模式（security = ads）运行时，建议使用以下 name resolve order 设置：

```
name resolve order = wins bcast
```

DC 查找仍将通过 DNS 进行，但对 netbios 名称的回退将不会使您的 DNS 服务器充满对 DOMAIN<0x1c> 查找的不必要查询。

## netbios aliases (G)

**默认值：** `netbios aliases = empty string (no additional names)`

**示例：** `netbios aliases = TEST TEST1 TEST2`

这是 nmbd 将作为附加名称广播的 NetBIOS 名称列表，Samba 服务器通过这些名称被识别。这使得一台机器可以在浏览列表中以多个名称出现。如果一台机器充当浏览服务器或登录服务器，这些名称都不会作为浏览服务器或登录服务器广播，只有该机器的主名称才带有这些能力被广播。

## netbios name (G)

**默认值：** `netbios name = machine DNS name`

**示例：** `netbios name = MYNAME`

这设置了 Samba 服务器已知的 NetBIOS 名称。默认情况下，它与主机 DNS 名称的第一部分相同。如果一台机器是浏览服务器或登录服务器，此名称（或主机 DNS 名称的第一部分）将是这些服务被广播的名称。

## netbios scope (G)

**默认值：** `No default`

这设置了 Samba 将在其下运行的 NetBIOS 范围。除非局域网上的每台机器都设置了此值，否则不应设置此项。

## nis homedir (G)

**默认值：** `nis homedir = no`
