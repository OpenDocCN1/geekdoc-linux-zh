
注意为 host brain 设置的三条 A 记录。重启 named 之后，使用 nslookup 查询 www 或 www.foo.edu 时会报告三个 IP 地址的列表，但每次查询都会轮换它们的顺序：

```text
> www
Default Server:  fake.foo.edu
Address:  192.168.1.1

Name:    brain.foo.edu
Addresses:  192.168.1.3, 192.168.1.5, 192.168.1.4
Aliases:  www.foo.edu

> www
Default Server:  fake.foo.edu
Address:  192.168.1.1

Name:    brain.foo.edu
Addresses:  192.168.1.4, 192.168.1.3, 192.168.1.5
Aliases:  www.foo.edu

> www
Default Server:  fake.foo.edu
Address:  192.168.1.1

Name:    brain.foo.edu
Addresses:  192.168.1.5, 192.168.1.4, 192.168.1.3
Aliases:  www.foo.edu
```

## Securing DNS

作为域管理员，你必须时刻警惕安全问题。

> **提示**
>
> 可以考虑加入 CERT 邮件列表，方法是发送邮件至 cert-advisory-request@cert.org。该列表包含新漏洞公告及建议的修复措施。虽然这些安全问题并非特定于 DNS，但它对于你所有的服务器和网络来说都是一个很好的安全信息来源。

BIND 版本 8 相比旧版本提供了一些额外的安全特性，包括：

- 仅允许将区域传输限制到指定的从属服务器
- 限制从辅助服务器的区域传输
- 限制对你的名称服务器的查询

## 限制区域传输到指定的从属服务器

你可以使用 named.conf 文件 options 段中的 `allow-transfer` 指令，将区域传输限制到指定的从属服务器：

```text
allow-transfer {
    <IP address of secondary 1>;
    <IP address of secondary 2>;
    ...
};
```

这会限制该服务器作为主 DNS 服务器的所有域的区域传输。或者，你也可以在 named.conf 文件的 zone 段中逐区域限制区域传输：

```text
zone "foo.edu" {
    type master;
    file "zone.foo.edu";
    allow-transfer {
        <IP address of secondary 1>;
        <IP address of secondary 2>;
        ...
    };
};
```

将区域传输限制到指定的从属服务器是一个很好的安全措施。这可以防止黑客列出你区域的内容，获取关于你网络的主机统计信息。你让黑客了解到的网络信息越少，你就越安全。

## 限制从辅助服务器的区域传输

除了限制从主服务器到辅助名称服务器的区域传输之外，你还应该限制从辅助服务器的区域传输。

如果你使用动态更新，请在主服务器上 named.conf 文件的 zone 段中使用 allow-update 指令来限制该域名的动态更新：

```text
zone "foo.edu" {
    type master;
    file "zone.foo.edu";
    allow-update {
        <IP address of updater 1>;
        <IP address of updater 2>;
        ...
    };
};
```

另外，你可以在名称服务器的 options 段中使用 recursion 指令禁用递归，以防止欺骗：

```text
recursion no;
```

## 限制对你的名称服务器的查询

你可以将对权威区域（即你的服务器作为主服务器或辅助服务器的区域）之外记录的查询，限制在一组受限制的主机中（通常仅为内部网络主机或权威区域中的域名）。要实现这种限制，可以使用访问控制列表（ACL）：在 named.conf 文件中添加一个 acl 段，然后在文件的 options 段中添加 allow-query 指令：

```text
acl internal {
    <network or host address>;
    <network or host address>;
};
options {
    ...
    allow-query {
        ... internal;
    };
};
```

你可以使用标准的 `<network address>/<bits>` 记法来指定主机网络，例如用 10.10.10.0/24 表示 10.10.10.0 C 类网络。

## 有用的脚本

BIND 版本 8 源码发行版中提供了一个有用的脚本 named-bootconf，用于将版本 4 的 named.boot 文件转换为版本 8 的 named.conf 文件。要获取这个脚本，请从 http://www.isc.org 下载并解压 BIND 源码发行版。

此外，还有其他一些实用工具可以帮助简化 DNS 区域文件的管理，包括：

- **h2n**：一个 Perl 脚本，将主机表（如 `/etc/hosts`）转换为区域数据文件。这个脚本在将网络上现有的基于主机表的名字解析环境迁移到基于 DNS 的解决方案时非常有用。你可以通过匿名 FTP 从 `ftp://ftp.uu.net/published/oreilly/nutshell/dnsbind/dns.tar.Z` 获取 h2n。
- **makezones**：一个 Perl 脚本，从具有特殊语法（用于特殊情形）的特殊文件生成区域文件。该脚本包含在当前版本的 BIND 中，可以通过 FTP 从 `ftp://ftp.uu.net/published/software/programs/DNS/makezones` 获取。

## 故障排除

DNS 问题通常由 named 配置和区域文件中的细微错误引起。其他 DNS 错误则是由父域和子域管理员之间缺乏沟通造成的。本节列出了一些常见的 DNS 错误，并讨论如何避免它们。

### 域名缺少末尾点

这个细微的错误可能造成潜在的灾难性后果。在 BIND 中，当域名不以点结尾时，它会被视为相对于当前正在定义的域的相对名称。

例如，如下条目：

```
foo.edu.     IN   NS   fake.foo.edu
```

将产生如下结果：

```
foo.edu.     IN   NS   fake.foo.edu.foo.edu
```

显然这完全不是本意。注意主机名 `fake.foo.edu` 末尾缺少一个点。如果没有末尾的点，该主机名会被视为相对名称，当前域名会被追加到它后面。因此，最终的主机名变成了 `fake.foo.edu.foo.edu`。

在区域文件中定义主机名和域名时，要特别注意末尾的点。始终使用 nslookup 测试你添加到区域文件中的条目，以确保名字解析符合你的预期。

### 忘记递增 SOA 序列号

这是导致 DNS 错误的一个非常常见的原因。对区域数据做出更改后，你必须记得递增起始授权记录中的序列号。如果序列号没有递增，辅助名称服务器将不会注意到主名称服务器上的区域数据已发生更改，这些更改也不会被辅助服务器下载。

对主名称服务器区域数据所做的任何更改，都必须同时更改 SOA 记录中的序列号。每次对区域文件进行更改时，序列号至少必须递增 1。域的辅助名称服务器会检查该编号，以决定主名称服务器上的区域信息是否已更新。当检测到序列号已递增时，它会从主名称服务器下载更新后的区域文件。每当你更改区域数据时，记得测试辅助名称服务器，以确保它识别到了该更改。辅助名称服务器多久查询一次主服务器以确定是否需要下载更改，取决于 SOA 记录中的刷新值或辅助名称服务器的设置。

如果需要强制立即更新辅助名称服务器上的区域数据，请在该辅助名称服务器上重启 named。当 named 在辅助名称服务器上启动时，它会检查主名称服务器区域文件的序列号，并下载所有已更新区域的新副本。

### 更改区域数据后忘记向 named 发送信号

有时，在更改 named.conf 文件或区域数据文件后，你会忘记向主名称服务器发送信号。名称服务器将不知道需要加载新数据。结果，你已做的更改将不会生效。

在更改区域数据并向 named 发送重启信号后，检查系统日志以确保名称服务器正确重新初始化非常重要。配置或区域文件中的语法错误可能会阻止 named 启动。还建议运行
