

91.189.94.8. DNS 服务器维护着一个本地目录，其中包含其具有权威性的名称和 IP 地址，因此如果您向 DNS 服务器请求其具有权威性的名称的 IP 地址，它通常会直接给出答案。许多 DNS 服务器也可以提供递归请求服务。对于递归查询，DNS 服务器本身可能不包含您要查找的记录，但它可以访问互联网为您找到答案。

在 Ubuntu 上提供 DNS 服务的程序有很多种，但最常见且历史最悠久的还是 BIND。BIND 是 Berkeley Internet Name Domain 的缩写，具有许多高级功能，但功能越多，配置文件往往就越复杂。说实话，让大多数管理员困惑的只是从零开始构建 BIND 服务器，但正如您将看到的，在 Ubuntu 下，繁重的工作已经为您完成。

## 安装 BIND

在 Ubuntu 下安装 BIND 有几种方法。在初始 Ubuntu 安装过程中，您可以从服务器类型列表中选择 DNS 服务器。如果您已经安装了 Ubuntu，可以输入 sudo tasksel 进入同一菜单。选择 DNS 服务器然后按 OK 后，bind9 和 bind9-doc 软件包将被自动下载并安装。或者您也可以直接运行

```
$ sudo apt-get install bind9 bind9-doc
```

您会发现（我将在下一部分详细介绍）一旦 Ubuntu 的 BIND 软件包安装完成，您实际上已经拥有一个完全配置并可正常运行的域名服务器，至少可以作为递归查询的缓存域名服务器使用。示例配置文件、根区域文件、本地区域文件，甚至 rndc 密钥都已为您预先配置好。

## Ubuntu 约定

Ubuntu 的 BIND 使用了一些关键的文件约定，这可能与您习惯的不同，具体取决于您使用过的其他

- **/var/log/syslog**
  这是 BIND 的默认日志文件。许多不同的服务都会向此文件写入日志，但 BIND 的日志条目会以关键字 named 为前缀，因此如果您只想查看 BIND 的日志条目，可以运行 sudo grep named /var/log/syslog。

## 缓存域名服务器

默认的 Ubuntu BIND 配置开箱即用即可作为缓存域名服务器。基本上，缓存域名服务器充当 DNS 查询的中介。一旦您将一些主机配置为指向缓存域名服务器，当某台主机请求特定记录时，缓存域名服务器会访问互联网，检索该记录并将其本地存储。如果第二台主机请求同一记录，且该记录尚未从缓存中过期，缓存域名服务器只需返回缓存的结果即可。这可以显著提高主机网络的响应时间，尤其是在网页浏览时，因为通常相同的记录（例如 www.google.com）会被多个主机请求。

## DNS 主服务器

缓存域名服务器非常有用，但大多数人在安装 BIND 时，意图是托管自己的一些区域文件。当一台域名服务器在本地托管区域文件且无需从其他来源检索时，它被称为主服务器。当您想向 DNS 服务器添加区域时，基本上分为三个步骤：创建区域文件、在 named.conf 中添加对该区域文件的引用，并通知 BIND 重新加载其配置。

以我的示例为例，假设我在网络内部有一个位于 192.168.0.5 的域名服务器，并且我注册了 example.net。我希望此域名服务器具有以下条目：

- ns1.example.net 指向 192.168.0.5（域名服务器本身）。
- example.net 也指向 192.168.0.7。
- www.example.net 指向 192.168.0.7。
- gateway.example.net 指向 192.168.0.1。

创建新区域文件最简单的方法是复制已有的文件并进行修改。在这种情况下，最合适的候选文件是 /etc/bind/ db.local 文件，因此我将其复制为 db.example.net：

```
$ sudo cp /etc/bind/db.local /etc/bind/db.example.net
```

当我用文本编辑器打开 db.example.net 时，会看到以下配置：

```
; 
; BIND data file for local loopback interface
; 
$TTL 604800
@ IN SOA localhost. root.localhost. (
 2 ; Serial
 604800 ; Refresh
 86400 ; Retry
 2419200 ; Expire
 604800 ) ; Negative Cache TTL

@ IN NS localhost.
@ IN A 127.0.0.1
@ IN AAAA ::1
```

由于本文并非 BIND 的完整指南，我不会详细介绍此文件中的每个选项，但默认情况下它配置的 $TTL（生存时间，即请求记录的域名服务器认为该记录过时的时长）为 604,800 秒，即七天。接下来它列出 localhost 作为 SOA（起始授权机构，应被视为信息最佳来源），而 root@localhost 是用于此主机的联系电子邮件地址（由 root.localhost 引用）。更下方，文件将 localhost 列为该区域的域名服务器，使用 NS 记录，然后将 localhost 的 IP 地址设置为 127.0.0.1，甚至使用 AAAA 记录为 localhost 添加了 IPv6 地址。

我随后根据之前设定的要求修改了此记录，这就是 resulting 区域文件：

```
; 
; BIND data file for example.net
; 
$TTL 1d
```
