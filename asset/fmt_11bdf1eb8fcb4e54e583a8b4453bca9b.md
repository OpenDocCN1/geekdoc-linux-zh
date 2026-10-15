
> 如果你希望在请求使用 TSIG 密钥签名时允许 DNS 配置的动态更新，则可以使用 `allow-update { key keyname; };` 语句。例如，本示例中的 `allow-update { key zone-xfr-key; };` 语句将允许此处讨论的主机之间进行动态更新。例如，假设密钥名为 `zone-xfr-key` 的公钥和私钥文件位于 `/var/named/keys` 目录中，你可以运行 `/usr/local/bin/nsupdate -k /var/named/keys:zone-xfr-key` 来更新 `yourdomain.com` 域的 DNS 区域信息。

## 以非 root 用户运行 BIND

在 Linux 内核大于 2.3.99 的系统上，你可以使用 `-u` 选项以非 root 用户运行 BIND。例如，`/usr/local/sbin/named -u nobody` 命令以 `nobody` 用户启动 BIND。

## 隐藏 BIND 版本号

由于软件漏洞与特定版本的软件相关联，版本信息就成为恶意黑客的重要信息。通过查明你运行的 BIND 版本，他可以弄清楚针对它的有哪些漏洞（如果有的话）并尝试入侵。例如：

```
dig @nameserver bind.version TXT chaos
```

该命令试图揭示 `named` DNS 服务器的 BIND 版本号。最好不要主动提供版本号。你可以通过在 `options` 部分添加 `version` 语句来简单地覆盖 BIND 提供的信息。例如，以下配置段告诉 `named` 在请求版本信息时显示“Unsupported on this platform”：

```
options {
    # other global options go here
    version "Unsupported on this platform";
};
```

![](img/9eb7e89292d2f85707b4d49102c865b7_512_0.png)

与版本号一样，你也不希望泄露主机信息。为了让潜在攻击者的工作更困难，我建议你在 DNS 配置文件中不要使用 `HINFO` 或 `TXT` 资源记录。

## 限制查询

Internet 上大多数 DNS 服务器可以被任何人用来执行查询。对于安全环境来说，这绝对不可接受。DNS 欺骗攻击通常依赖于这一事实：攻击者可以要求你的 DNS 服务器解析一个它（你的服务器）无法提供权威答案的查询。换句话说，典型的欺骗技术是要求你的服务器解析一个查询，而你的服务器最终可能会从黑客自己的 DNS 服务器获取数据。例如，假设黑客为 `id10t.com` 域运行 DNS 服务器，而你的 DNS 服务器对 `yourdomain.com` 域具有权威性。现在，如果你允许任何人查询你的服务器的任何内容，黑客可以要求你的服务器解析 `gotcha.id10t.com`。你的 DNS 服务器最终会从黑客的机器获取数据，这时黑客会施展他的欺骗技巧来污染你的 DNS 缓存。

现在假设你的网络地址是 `192.168.1.0`。为了确保网络外部的任何人不能查询你的 DNS 服务器除其管理的域之外的任何内容，你需要以下语句：

```
options {
    allow-query { 192.168.1.0/24; };
};
```

`allow-query` 指令确保 `192.168.1.0` 网络中的所有主机可以查询 DNS 服务器。现在如果你的 DNS 服务器对 `yourdomain.com` 区域具有权威性，你可以有以下 `/etc/named.conf` 段：

```
options {
    allow-query { 192.168.1.0/24; };
};
```

```
zone "yourdomain.com" {
    type master;
    file "yourdomain.com";
    allow-query { any; };
};
```

```
zone "1.168.192.in-addr.arpa" {
    type master;
    file "db.192.168.1";
    allow-query { any; };
};
```

这确保了任何人从任何地方都可以查询 `yourdomain.com` 的 DNS 服务器，但只有 `192.168.1.0` 网络中的用户才能查询 DNS 服务器的任何内容。

此外，您不应允许网络外的任何人执行递归查询。要禁用除您网络外的所有人的递归查询，请在全局选项部分添加以下内容：

```
allow-recursion { 192.168.1.0/24; };
```

您也可以使用以下选项在全局选项部分完全禁用所有人的递归。

```
recursion no;
```

![](img/9eb7e89292d2f85707b4d49102c865b7_514_0.png)

> 如果其他名称服务器将其用作转发器，则无法在名称服务器上禁用递归。

理想情况下，您应设置权威名称服务器以不执行递归。只有负责为内部网络解析 DNS 查询的名称服务器才应执行递归。这种类型的设置称为拆分 DNS 配置。

例如，假设您有两个名称服务器——`ns1.yourdomain.com`（主服务器）和 `ns2.yourdomain.com`（辅助服务器）——它们负责一个名为 `yourdomain.com` 的单个域。同时您有一个名为 `ns3.yourdomain.com` 的 DNS 服务器，负责解析您 `192.168.1.0` 网络的 DNS 查询。在拆分 DNS 配置中，您可以设置 `ns1` 和 `ns2` 服务器对 `yourdomain.com` 以外的任何域都不使用递归，并通过前面讨论的 `allow-recursion` 语句允许 `ns3` 进行递归。

## 关闭胶水获取

当 DNS 服务器返回域的名称服务器记录（NS）并且没有 NS 记录的 A 记录时，它会尝试检索一个。这称为胶水获取，可被欺骗攻击者滥用。关闭胶水获取只需在 `/etc/named.conf` 的全局选项部分添加以下语句即可。

```
options no-fetch-glue
```

## 为 DNS 服务器设置 chroot

BIND 的 9.x 版本使为 DNS 服务器创建 chroot jail 变得非常容易。以下是为 BIND 创建 chroot jail 的方法。

- 1. 以 root 身份，通过运行 `useradd dns -d /home/dns` 命令创建一个名为 `dns` 的新用户。
- 2. 运行 `mkdir -p /home/dns/var/log /home/dns/var/run /home/dns/var/named /home/dns/etc` 命令以创建所有必要的目录。
- 3. 通过运行 `cp /etc/named.conf /home/dns/etc/` 命令复制 `/etc/named.conf` 文件。
- 4. 使用 `cp -r /var/named/* /home/dns/var/named/` 命令将 `/var/named` 中的所有内容复制到 `/home/dns/var/named`。
- 5. 运行 `chown -R dns:dns /home/dns` 命令以确保 `named` 所需的所有文件和目录都由 `dns` 用户及其名为 `dns` 的私有组拥有。请注意，如果您计划以 root 身份运行 `named`，请在此命令中使用 `root:root` 而不是 `dns:dns` 作为用户名:组名。
- 6. 现在通过执行 `/usr/local/sbin/named -t /home/dns -u dns` 命令运行名称服务器。

![](img/9eb7e89292d2f85707b4d49102c865b7_515_0.png)

如果您计划以 root 身份运行 `named`，请不要指定 `-u dns` 选项。

## 使用 DNSSEC（签名区域）

DNSSEC（DNS 安全扩展的简称）是一种基于公钥加密的身份验证模型，它引入了两种新的资源记录类型——`KEY` 和 `SIG`——以允许解析器和名称服务器对任何 DNS 数据的来源进行加密身份验证。换句话说，DNS 客户端现在可以证明它从 DNS 服务器收到的响应是真实的。不幸的是，直到 DNSSEC 使用变得广泛，其好处无法实现。在这里，我将向您展示如何为名为 `domain.com` 的域创建必要的 DNSSEC 配置。

- 1. 首先，您必须为 `domain.com` 域创建一个公钥和私钥对。从 `/var/named` 目录运行 `/usr/local/sbin/dnssec-keygen -a DSA -b 768 -n ZONE domain.com` 命令。此命令创建一个 768 位基于 DSA 的私钥和公钥对：一个名为 `Kdomain.com.+003+29462.key` 的公钥文件和一个名为 `Kdomain.com.+003+29462.private` 的私钥文件。请注意，29462 这个数字称为 *密钥标签* 并且会有所不同。您应该在区域文件（`domain.com.db`）的开头插入一行来插入公钥：
