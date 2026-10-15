
用户若依据看似来自此域名的伪造电子邮件来行事，可能会造成灾难性后果，因此最好能在邮件送达收件人之前将其拒绝或丢弃。

ADSP TXT 记录还可以包含 `t=y` 子句，如果你只是在测试 DKIM，不希望接收者过于看重你的签名。

在 ADSP 系统开发过程中，也就是 RFC5617 之前，域名的 ADSP TXT 记录存储在不同的子域中（`_domainkey.domain`，没有 `_adsp` 前缀），且语法略有不同。`o=~` 表示该域名对其部分邮件进行签名，而 `o=-` 表示其对所有邮件进行签名。

由于这两种约定使用不同的子域，因此它们可以共存。在撰写本文时，原始形式仍占主导地位。如果你确实希望接收者仔细检查你的签名，那么在接下来的几年里，最好同时使用这两种约定，直到所有人都符合 RFC5617 标准。

我们来看一个例子。Gmail 没有 ADSP 记录，但 Yahoo! 有：

```
_domainkey.yahoo.com. 7200 IN TXT "t=y; O=~;" n=http://antispam.yahoo.com/domainkeys"
```

`n=` 子句是一条注释，引导人类用户查看有关 Yahoo! 使用 DKIM 记录的更多信息。有些站点改用电子邮件地址（不含任何 @ 符号，以避免垃圾邮件）。下面是 yahoo.com 针对密钥（选择器）s1024 的 DKIM TXT 记录：

```
s1024._domainkey.yahoo.com. 86400 IN TXT "k=rsa; t=y; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDRreeOi4juz+QfWYui /E9GXSXau/2PBLjNTD8V4UUnn+2FAZVG3L23BzeoULYY4PeeleB3gfm /JDJ0GX3N5L4KJA UUHfWwDeb0NPs+BK0VeKTATLY5/Y3SbT7xhy+1xtJ4Rk dV7V7xTn56Lb4udUnwuxK4V5b5PdOKj/XcwID4AQAB; n=A 1024 bit key,"
```

这里再次出现 `n=` 子句，这次它是一条关于密钥本身的注释。

本节中展示的 DKIM 记录都是 TXT 记录，但它们最终将迁移到具有相同格式的 DKIM 记录类型。在此期间，站点可以同时使用两种记录类型，以确保不会出现过渡问题。

第 20 章涵盖在邮件系统中实施 DKIM 所需的步骤。

## SSHFP 资源记录

SSH（安全外壳）允许在不安全的网络上进行安全远程登录。它使用两种认证方案：一种用于主机本身，另一种用于尝试登录的用户。不幸的是，用户通常接受 ssh 呈现给他们的任何主机密钥，而不进行验证。DNS 的 SSHFP 记录类型让 ssh 自动验证主机密钥，确保用户连接的是预期机器，而不是冒名顶替者。

为了减小数据包大小，SSHFP 记录不存储主机公钥的完整副本，而是存储这些密钥的摘要（即加密哈希）。语法如下：

`name [ttl] [IN] SSHFP algorithm# fingerprint_algorithm# fingerprint`

*算法编号#* 标识用于生成主机密钥的公钥加密系统。该算法实际上并不用于验证过程；它只是与远程主机提供的密钥进行比较，以确保双方讨论的是同一种密钥。RSA 是算法 1，DSA 是算法 2。

*指纹* 是要匹配的哈希，而 *指纹算法编号#* 指示如何处理远程主机提供的公钥，以生成用于比较的哈希。目前只定义了一种哈希算法（SHA-1），因此该字段的内容目前始终为 1。

以下是 RFC4255 中的示例：

`host.example.    SSHFP 2 1 123456789abcdef67890123456789abcdef67890`

SSH 通常同时创建 RSA 和 DSS 主机密钥对；它们通常存储在 **/etc/ssh** 中，名称类似于 **ssh_host_rsa_key.pub** 和 **ssh_host_dsa_key.pub**。在用户端，SSH 将接受的主机公钥存储在用户主目录下的 **.ssh/known_hosts** 文件中。

你可以从该目录获取主机密钥来构建 SSHFP 资源记录。较新版本的 **ssh-keygen** 可以使用 **-r** 和 **-g** 标志生成 SSHFP DNS 记录。Linux 上还有一个 **sshfp** 命令，也可用于 UNIX（freshports.org/dns/sshfp），它将密钥转换为指纹并生成必要的 DNS 记录。

> 更多关于 SSHFP 记录的信息，请参阅第 928 页。

你可以通过将 VerifyHostKeyDNS 选项设置为 yes，让 OpenSSH 使用 SSHFP 记录。SSH 支持多种认证和验证方法，由于 SSHFP 记录尚未广泛使用，你不应将其作为唯一可能的选项。先尝试 SSHFP，如果失败，则退回到有 SSHFP 之前的方式，提示用户手动确认主机密钥。有关配置 SSH 的更多信息，请参阅第 22 章 *安全* 中的第 926 页。

与 SPF 和 DKIM 记录一样，SSHFP 系统或多或少假设你正在使用 DNSSEC，因此 DNS 记录是可信的。目前这可能并非事实，但 DNSSEC 正逐渐获得认可，最终会得到广泛应用。有关 DNSSEC 的覆盖内容，请参阅第 648 页。

## DNSSEC 资源记录

目前有六种资源记录类型与 DNSSEC 相关。DS、DLV 和 DNSKEY 用于存储各种类型的密钥或指纹。RRSIG 包含区域中其他记录（实际上是记录集）的签名。最后，NSEC 和 NSEC3 为 DNS 服务器提供了一种对不存在的记录进行签名的方式，为查询的否定答案提供加密安全。这六种记录各不相同
