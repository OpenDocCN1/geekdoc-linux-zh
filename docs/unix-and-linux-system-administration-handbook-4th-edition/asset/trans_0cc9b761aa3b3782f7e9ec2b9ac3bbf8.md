

只能有一个 server 语句。它指定全局选项。zone 语句列出区域特定的选项，而 key 语句定义加密密钥，这些密钥对于主服务器和从服务器之间的通信以及控制 nsd 是必需的。空白字符分隔属性和值。值可以被引用，但不必如此。

与 BIND 类似，nsd 概括了 IP 地址，但方式略有不同于 BIND 的地址匹配列表构造。它被称为 ip-spec，可以是

- 一个普通的 IP 地址（IPv4 或 IPv6）
- CIDR 记法的子网，例如 1.2.3.0/24
- 带有显式掩码的子网，例如 1.2.3.4&255.255.255.0
- IP 地址范围，例如 1.2.3.4-1.2.3.25

这些形式中都不允许有空格。

另一个根本区别是使用密钥值对区域传输和通知消息进行身份验证。在 BIND 中，密钥与 IP 地址相关联，与该地址的通信都用该密钥签名并验证。在 NSD 中，密钥更精细，因此 nsd 可以为通知使用一个密钥，为发送区域传输使用另一个密钥，再为接收该传输使用第三个密钥。有用吗？嗯……

nsd 中 notify 的语义类似于 BIND 的 notify explicit 子句：只有明确列出的服务器才会被通知。默认情况下，BIND 会通知区域文件中列出的该域的所有名称服务器。

NSD 文档指的是主区域和从区域，而 BIND 文档用这些形容词指的是服务器。这基本上是同一回事。名称服务器的“实例”是特定区域的主服务器或从服务器。

nsd 更倾向于合理的默认行为而不是可配置性。例如，DNSSEC 对于已签名的区域默认开启，对于未签名的区域默认关闭。默认情况下，nsd 在 IPv4 和 IPv6 套接字上监听。日志记录要么开启要么关闭，而不是 BIND 范式中无限的色调和渐变。nsd 使用 TSIG 进行服务器之间的通信（区域传输、通知等）。

文件 doc/NSD-FOR-BIND-USERS 给出了 BIND 与 NSD 之间差异的简要描述，并包含了一个示例配置文件。配置文件 nsd.conf 的 man 手册和 doc/README 文件也有示例，但遗憾的是它们之间没有一致性。

## NSD 配置示例

我们行使了一些编辑许可，将发行版中的三个示例合并，并添加了我们自己的编辑评论，以便在更详细地介绍各种选项之前让你感受 NSD 配置。这里我们将 nsd 配置为主服务器管理域名 atrust.com，并作为域名 admin.com 的从服务器。

```
server:
  username: nsd          # User nsd should run as after chroot
  database: /var/db/nsd/nsd.db   # Precompiled zone database file
  logfile: /var/log/nsd.log      # Log file, default is to stderr + syslog
  pidfile: /var/run/nsd.pid      # nsd process id

key:
  name: tsig.atrust.com.         # Key for atrust.com zone transfers
  algorithm: hmac-md5
  secret: "base64 secret goes here"

zone:
  name: atrust.com               # Name of the zone
  zonefile: /var/nsd/primary/atrust.com
  provide-xfr: 1.2.3.4 tsig.atrust.com.  # Address of atrust.com slave
  notify: 1.2.3.4 tsig.atrust.com       # And key for notify or xfrs.
  provide-xfr: 1.2.30.40 tsig.atrust.com. # Address of another slave
  notify: 1.2.30.40 tsig.atrust.com     # And key for notify or xfrs.

key:
  name: tsig.admin.com.          # Key to get admin.com slave data
  algorithm: hmac-md5
  secret: "base64 secret goes here"

zone:
  name: admin.com                # Zone we are a slave for
  zonefile: "/var/nsd/secondary/admin.com.signed"
  allow-notify: 5.6.7.8 NOKEY    # Its master server
  request-xfr: 5.6.7.8 tsig.admin.com.  # And key for xfrs
```

此示例 nsd.conf 文件将服务器配置为主服务器管理 atrust.com，并通知并向两个从服务器提供区域传输，一个位于 IP 地址 1.2.3.4，另一个位于 IP 地址 1.2.30.40。服务器将使用名为 tsig.atrust.com 的 TSIG 密钥对两个从服务器的传输和通知进行身份验证。 你可以，也应该，为每个从服务器使用单独的密钥。

此服务器也是已签名区域 admin.com 的从服务器，其主服务器位于 IP 地址 5.6.7.8。我们可以在没有密钥的情况下接收区域数据更改的通知，但必须使用 tsig.admin.com 密钥来接收区域传输。主区域具有 provide-xfr 子句，而从区域具有 request-xfr 子句。

在你安装 nsd 并设置配置文件后，使用 nsd-checkconf 检查配置文件的语法。它的错误报告有点简略；例如，“error: syntax error”以及行号。修复 nsd-checkconf 的抱怨后，再次运行它并重复该过程，直到 nsd-checkconf 不再报告错误。

## NSD 密钥定义

key 子句定义一个命名密钥，供后续访问控制选项使用。每个密钥有三个属性：名称、算法和共享密钥（又名密码）。考虑将密钥定义，或至少其密钥部分，放入具有受限权限的文件中。你可以使用 include 语句导入

