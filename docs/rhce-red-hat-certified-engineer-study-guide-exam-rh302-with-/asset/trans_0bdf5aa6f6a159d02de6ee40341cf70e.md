
现在花时间完成练习 21.1，这涉及 Apache 的安装和配置。

## 练习 21.1

### 安装和配置 Apache

为了获得 Apache 经验，请安装 apache-manual 包。配置两个共享单个 IP 地址的虚拟主机。使用浏览器验证你是否可以访问每个虚拟主机。通过修改根文档以使其内容各不相同，请确保每个主机都在访问其自身的根文档。

你可能需要参考本章和 Apache 文档来完成此练习。但在参加 RHCE 之前，请确保你可以在不使用外部文档的情况下执行这些及类似的操作。

## BIND 域名服务器

伯克互联网命名守护进程（BIND）将 IP 地址解析为主机名并将主机名解析为 IP 地址。此服务通常被称为域名服务（DNS）。互联网上绝大多数 DNS 服务器运行着作为 Red Hat Linux 分发的相同服务器程序。许多服务器的名称与其关联程序的名称相似；然而，BIND 关联程序 `/usr/sbin/bind` 的命名非常奇怪。Red Hat Linux 帮助你配置这两类 DNS：

- 仅缓存 DNS 服务器
- 常规 DNS 服务器

仅缓存 DNS 服务器可以提高与互联网连接速度缓慢的主机的 DNS 性能。仅缓存命名服务器会联系常规命名服务器来解析 IP 地址和主机名。一旦 IP 地址或主机名被解析，仅缓存命名服务器就会存储该结果，这样将来对该 IP 地址或主机名的引用无需查询命名服务器即可完成解析。

## 安装

Red Hat Linux 包含了以下与 BIND 相关的包：

- bind，提供常规 DNS 服务器
- bind-utils，一组用于管理 BIND 的实用实用程序
- caching-nameserver，配置 BIND 提供仅缓存的命名服务器

此外，它还包含 `bind-devel` 包，该包仅在对调用 BIND 编程接口的程序进行软件开发时需要。

要安装 BIND，请进入包含这些包的目录并执行以下命令

```
rpm -Uvh bind-*.rpm
```

如果你想配置仅缓存的命名服务器，请也执行以下命令

```
rpm -Uvh caching-nameserver-*.rpm
```

## BIND 基本配置

要建立域名服务（DNS），你必须配置主 DNS 配置文件 `/etc/named.conf`。通常，你还必须配置一组被称为区域文件（zone files）的文件，这些文件通常位于 `/var/named`。区域文件可以是以下一种：

- 正向区域文件，用于将主机名映射到 IP 地址
- 反向区域文件，用于将 IP 地址映射到主机名
- 提示文件（hint file），用于标识负责为所有注册域名回答 DNS 查询的根命名服务器

如果你需要仅缓存的命名服务器，安装 `caching-nameserver` 包会正确配置 BIND。然而，你可以通过修改默认的仅缓存命名服务器配置，在 `/etc/named.conf` 中包含 `forwarders` 语句来提高名称查找的效率。`forwarders` 语句的形式为 `IP_address`，其中指定了无法从缓存解析的 DNS 服务 IP 地址。如果你愿意，可以指定多个服务器的 IP 地址；用分号将其隔开。`/etc/named.conf` 文件标识区域文件所属的域名；如果是反向区域,/etc/named.conf` 指明本地 DNS 是主 DNS 还是从 DNS。主 DNS 是该区域的主命名服务器。从 DNS 定期联系的主 DNS 获取信息以保持数据最新。这是一个典型的 `/etc/named.conf` 文件，其格式由 man 页面描述：

```
options {
    directory "var/named";
    zone "*" {
        type hint;
        file "named.hint";
    }
    zone "example.com" {
        type master;
        file "example.com";
    }
    zone "0.0.0.127.in-addr.arpa" {
        type master;
        file "named.local";
    }
    zone "168.192.in-addr.arpa" {
        type master;
        file "named.reverse";
    }
```

正确的提示文件可以通过 `ftp://ftp.example.net/domain/named` 获取。剩余的文件必须手动编写。正向区域文件通常指定：

- 区域的起始起始（SOA）
- 负责该区域的管理员邮箱
- 区域内主机名到 IP 地址的映射

此外，区域文件可能指定辅助命名服务器、邮件交换记录（MX）以及主机别名（CNAME）。这是一个典型的正向区域文件：

```
@ IN SOA example.com.
root.example.com. (
200002501 ; serial
43200 ; refresh
3600 ; retry
360000 ; expire
241900 ; default_ttl
)
@ IN NS example.com.
@ MX 10 example.com.
localhost 127.0.0.1
example.com. IN 192.168.1.1
bill IN 192.168.1.2
toshiba IN 192.168.1.99
router IN CNAME example.com.
www IN CNAME example.com.
ftp IN CNAME example.com.
mail IN CNAME example.com.
```

注意管理员邮箱（`root.example.com.`）和域名（`example.com.`）后面使用了点。底层概念是主机名无论是否完全，在区域文件中指定时都以点结尾。文件的格式在 `named` man 页面中有详细描述。SOA 记录中的系列数字指定了：

字体 用于判断信息已更改的序列号
- 从 DNS检查序列号的刷新间隔（单位：秒）
- 刷新失败后从 DNS重试的间隔（单位：秒）
- 如果刷新失败，丢弃缓存信息的间隔（单位：秒）
- 缓存负面响应的默认间隔（单位：秒）

这是一个典型的反向区域文件：

```
@ IN SOA example.com.
root.example.com. (
200003502 ; serial
43200 ; refresh
3600 ; retry
360000 ; expire
241900 ; default_ttl
)
@ IN NS example.com.
1 IN PTR wall.example.com.
2 IN PTR p3.example.com.
3 IN PTR p2.example.com.
99 IN PTR laptop.example.com.
```

## 管理

named 的服务器管理脚本为 `/etc/rc.d/init.d/named`。通过带有正确的参数调用此脚本，你可以控制服务器的运行。

## 启动和重启服务

要启动 BIND，执行命令

```
/etc/rc.d/init.d/named start
```

要重启 BIND，执行命令

```
/etc/rc.d/init.d/named restart
```

## 停止服务

要停止 BIND，执行命令

```
/etc/rc.d/init.d/named stop
```

## 检查状态

要检查 BIND 的状态，执行命令

```
/etc/rc.d/init.d/named status
```

## 强制重载数据库

每当你更改 BIND 配置文件时，都应该指示 BIND 重载数据库。要指示 BIND 重载数据库，执行命令

```
/etc/rc.d/init.d/named reload
```

## 日志

默认情况下，BIND 将记录到系统日志 `/var/log/messages`。如果 BIND 运行异常，请检查日志中指向问题的错误信息。

## 更多信息

关于 BIND 的大量文档可以在 `/usr/doc/bind-*` 找到。你也可以在互联网软件协会网站 www.isc.org 上找到信息。

现在花时间完成练习 21.2，它将为你提供配置 BIND 的实践经验。

### 练习 21.2
### 安装和配置 BIND

除了 SENDMAIL 之外，BIND 可能是 Unix 服务中最难配置的。然而，你不需要成为 BIND 专家也能通过 RHCE 考试。执行以下步骤以获得使用 BIND 的经验：

1. 安装 BIND。
2. 为一个假设域名创建一组区域文件。使用预留块中的 IP 地址，例如 192.168.1.0-192.168.1.255。
3. 配置 `/etc/named.conf` 以引用你的区域文件。

