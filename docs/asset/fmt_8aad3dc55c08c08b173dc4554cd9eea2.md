
在此示例中，只有位于 `124.30.*.*` 网络的系统可以通过此名称服务器查询有关域 `lab.sun.com` 信息。

## 注意

尽管 `allow-query` 函数提供了可能（仅允许来自特定网络的域查询），仍应使用防火墙或过滤路由器来防止来自互联网的 DNS 查询到达内部 DNS 服务器。这是分层保护的一个示例（参见第 2 章）。

## 来自 DNS 服务器的非法区域传输

区域传输是将 DNS 数据库从一个服务器复制到另一个服务器的机制。某些 UNIX/网络管理员可能不想仅仅从他们的公共 DNS 服务器拉取区域传输（绝对不想从他们的私有/内部 DNS 服务器传输！）。有多种方法可以防止区域传输。

- 1. 设置防火墙以阻止从内部 DNS 服务器到互联网的所有 TCP 43（DNS 区域传输）数据包。这将阻止内部 DNS 服务器与互联网之间所有的区域传输尝试。为注册和旧的 DNS 辅助在防火墙上开启该端口。
- 2. 获取并应用来自 Sun 的 BIND 4.9.3 补丁 [2]，然后在 `named.conf` 文件中使用 `xfernets` 指令。

> [2] Solaris 6 附带 BIND 4.9.4，因此不需要补丁。Solaris 2.5 及更早版本需要补丁。请参见“知道你的 BIND 版本”章节以获取更多信息。

- 3. 获取并应用公域 BIND (4.9.3 或更高版本)，并在 `named.conf` 文件中使用 `xfernets` 指令。
- 4. 在 BIND 8.1 中使用 `allow-transfer` 选项来指定哪些主机或网络可以从主服务器拉取区域传输。

> [3] Solaris 7 附带 BIND 8.1 或更高版本。请参见“知道你的 BIND 版本”章节以获取更多信息。

## nslookup 与实际 DNS 查询之间的差异

我应该指出，在查找主机或 IP 地址时，`nslookup` 和应用程序可能会得到不同的结果。这是因为 `nslookup` 使用它自己的名称查找程序，而不是 Solaris 工具和应用程序使用的系统标准 `gethostbyname()` 和 `gethostbyaddr()`。建议获取并使用 `DIG` 工具（下文将讨论）进行 DNS 故障排除。

## 公域 DNS (BIND)

任何需要最新 BIND 功能或需要代码本身进行以定制的人员，都可以获取 BIND 的完整源代码和文档。可以在 `http://www.isc.org/` 或 `http://www.dns.net/dnsrd/` 获取。

> 注意
Sun Microsystems 不支持替换随 Solaris 提供的 BIND 程序。BIND 应该由对 DNS 机制有深入知识和经验的人进行替换。

## DIG 公域工具

域名信息分组器（`DIG`）现在包含在公域 BIND 中，是一个 DNS 服务器和客户端诊断工具。`DIG` 是一种用于诊断组织内部和互联网上 DNS 查询的 DNS 调试工具。`DIG` 可 `http://www.isc.org/` 获取。

## 禁用 nscd 缓存

考虑禁用 `nscd` 缓存。众，在某些情况下 `nscd` 会产生异常行为。
请参见本章节稍后关于禁用 `nscd` 缓存的章节。

## 知道你的 BIND 版本

高级且设备齐全的 UNIX 管理员关注 BIND 的最新功能，但如果你使用 Solaris 的 BIND，如何判断运行的是哪个版本呢？
下面的示例说明了如何使用 `what` 命令来确定系统中运行的是哪个版本的 BIND。

```
# /usr/ccs/bin/what /usr/sbin/in.named

/usr/sbin/in:named:

in:named: 8.1 Tue Oct 6 00:50 PDT 1998 Generic

...
options {

allow-query { 128.126.120/24; 128.126.130/24 };

};

...
```

在此示例中，名称服务器将仅接受来自 `128.126.120.*` 和 `128.126.130.*` 网络系统的查询。
在 BIND 8.1 及更高版本中，`allow-query` 函数还可以在区域级别强制执行。一个文件片段示例：

```
zone "lab.sun.com" {

type primary;

file "db.lab.sun.com";

allow-query { 124.30/16 };

};
```

在此示例中，只有位于 `124.30.*.*` 网络的系统可以通过此名称服务器查询有关域 `lab.sun.com` 信息。
