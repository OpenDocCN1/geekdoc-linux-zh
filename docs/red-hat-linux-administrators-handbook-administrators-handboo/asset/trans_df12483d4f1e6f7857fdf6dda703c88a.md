
![](img/c2419364ebb911c809b6a79991707c27_186_0.png)

## 注意

你可以将 nameserver 指令设置为 Internet 上任何域名服务器的 IP 地址。然而，你应仅使用最近的域名服务器 IP 地址，以减少域名解析的延迟。此外，切勿在未获得许可的情况下在你的解析器配置文件中使用他人的域名服务器 IP 地址。这被认为是不礼貌的，如果你的解析器给他人的名称服务器带来沉重负载，还可能产生法律后果。

也可能将一个或多个 IP 地址硬编码到其对应的主机名中，写入 /etc/hosts 文件。该文件具有非常简单的格式，如下所示：

```
IP address host name short-cut host name
```

以下是 /etc/hosts 文件的一个示例：

```
206.171.50.50 picaso.nitec.com picaso
127.0.0.1 localhost localhost
```

解析器可以在远程 DNS 服务器不可用时使用此文件来解析地址。此外，如果你有一个小型网络并且不想运行本地 DNS 服务器，你可以使用此文件来解析本地主机名。然而，当远程 DNS 服务器和 /etc/hosts 文件都可用时，解析器需要知道尝试处理 DNS 查询时使用哪个顺序。你可以在 /etc/host.conf 文件中使用 order 指令来设置顺序。例如，

```
order hosts,bind
```

如果你的 /etc/host.conf 文件具有此 order 指令，则解析器首先尝试使用 /etc/hosts 文件来响应查询。如果文件中不包含可用的条目，则将使用 /etc/resolv.conf 文件中指定的 bind 或 DNS 服务器。

![](img/c2419364ebb911c809b6a79991707c27_186_1.png)

## 提示

如果你拥有大量用户，可以通过使用本地 DNS 服务器而不是 /etc/hosts 文件来改善与 DNS 相关的性能，因为为每个新的 DNS 请求读取文件可能会相当缓慢。

在设置完上面描述的文件后，你的 DNS 解析器配置就完成了。测试 DNS 配置最简单的方法是尝试 ping Internet 上的计算机。如果 ping 程序因未知主机名而失败，请仔细检查你的 DNS 解析器配置是否有拼写错误。

## 设置 DNS 服务器

Red Hat Linux 附带 Berkeley Internet Name Domain (BIND) 服务器软件。如果你在操作系统安装阶段未安装它，你可以安装该软件的 RPM 版本。例如，要为 Intel x86 平台安装 BIND 软件的 8.2-6 版本，我在 Red Hat Linux CD-ROM 的 RPMS 目录中找到了 bind-8.2.6-i386.rpm 包并运行了以下命令来安装 BIND：

```
rpm -ivh bind-8.2.6-i386.rpm
```

上面描述的 BIND 软件的 RPM 包安装了以下四个程序：

- /usr/sbin/named. 名称服务器本身。
- /usr/sbin/named-xfer. 名称服务器的辅助程序。
- /usr/sbin/ndc. 用于控制名称服务器的程序。
- /usr/doc/bind-8.1.2/named-bootconf.pl. 用于将旧配置文件转换为新格式的辅助 Perl 脚本。

### 配置主/主 DNS 服务器

假设我在 ns.nitec.com 主机上运行着 BIND 域名服务器（named），并且我刚刚在 InterNIC 注册了一个名为 classifiedworks.com 的域名，并希望在 ns.nitec.com 上设置 named 为此新域名提供主 DNS。方法如下。

首先，我需要在 /etc/named.conf 文件中创建以下区域声明：

```
zone "classifiedworks.com" {
    type master;
    file "classifiedworks.db";
};
```

这表明我的名称服务器是 classifiedworks.com 域的主名称服务器。现在，我需要在名称服务器的工作目录中创建一个名为 classifiedworks.db 的区域文件（由 options { directory path_name }; 语句指定）。清单 8-2 是 classifiedworks.com 域此类区域文件的一个示例。

### 清单 8-2 classifiedworks.com 域的区域文件

```
@ IN SOA ns.nitec.com. kabir.nitec.com. (
    1999020100    ; Serial
    7200          ; Refresh - 2 hours
    3600          ; Retry - 1 hour
    43200         ; Expire - 12 hours
    3600 )        ; Minimum - 1 hour

IN NS ns.nitec.com.
IN MX 10 mail.nitec.com.

www IN CNAME www.nitec.com.
ftp IN A 206.171.50.55
```

我已设置 SOA 和 NS 记录以声明 ns.nitec.com 是 classifiedworks.com 域的名称服务器。因为我想在 mail.nitec.com 主机上接收该域的邮件，所以我设置了一个 MX 记录来实现这一点。我为 www.nitec.com 设置了一个名为 www.classifiedworks.com 的别名。最后，我为 ftp.classifiedworks.com 设置了一个 A 记录，使其指向 206.171.50.55

正如你所见，通过使用各种资源记录，你可以根据需要配置区域文件。在配置区域文件并将其存储在 DNS 服务器的工作目录中后，该域的主名称服务器配置就完成了。

### 配置从/辅助 DNS 服务器

配置从或辅助 DNS 服务器相当简单。你唯一需要手工更新的文件是 /etc/named.conf 文件。例如，假设我想使用名为 ns2.nitec.com 的 DNS 服务器作为 classifiedworks.com 域的辅助名称服务器。我需要做的第一件事是在 ns2.nitec.com named 服务器的 /etc/named.conf 文件中创建如下区域声明：

```
zone "classifiedworks.com" {
    type slave;
    file "classifiedworks.db";
};
```

因为这是一个从或辅助服务器，所以我不需要手工创建 classifiedworks.db 文件。我可以使用名为 named-xfer 的程序从 classifiedworks.com 域的主名称服务器获取该文件，该程序随 named 发行版提供。因为我知道 classifiedworks.com 域的主名称服务器名为 ns1.nitec.com，所以我可以按如下方式运行 named-xfer 命令：

```
named-xfer -z classifiedworks.com -f classifiedworks.db \
-s 0 ns1.nitec.com
```

这里，-z 选项用于指定区域名称，-f 选项用于指定区域文件名，-s 选项用于指定信息当前所在的名称服务器。

运行此程序后，当前目录中会创建一个名为 classifiedworks.db 的文件。将文件移动到 ns2.nitec.com 机器上 named 服务器的工作目录后，classifiedworks.com 域的辅助 DNS 配置就完成了。

### 配置反向 DNS 服务器

如果你拥有自己的网络 IP 地址，就必须为它们做反向 DNS。例如，如果你拥有一个名为 206.171.50.0 的 IP 网络，并在名为 nitec.com 的域的正向 DNS 配置中使用它，你就必须为此网络设置反向 DNS 区域。方法如下。

首先，修改 /etc/named.conf 文件以包含一个新的区域，如下所示：

```
zone "50.171.206.in-addr.arpa" {
    type master;
    file "db.206.171.50";
};
```

前面区域配置中使用的特殊区域名称（50.171.206.in-addr.arpa）是必需的，用于反转你的网络号码并在名称末尾附加 in-addr.arpa 以创建反向 DNS 区域名称。

接下来，在 named 服务器的工作目录中创建 db.206.171.50。反向 DNS 区域的文件名可以是任意名称，但通常使用 db.network-address 名称。此文件与迄今为止显示的区域文件类似；唯一的区别是它将具有 PTR 记录而不是 A、CNAME 等。清单 8-3 显示了 db.206.171.50 文件的一个示例。

### 清单 8-3 反向 DNS 区域文件示例（db.206.171.50）

```
@ IN SOA ns.nitec.com. (
    1999020100 ; Serial
    7200      ; Refresh - 2 hours
    3600      ; Retry - 1 hour
    43200     ; Expire - 12 hours
    3600 )    ; Minimum - 1 hour

IN NS ns.nitec.com.

51.50.171.206.in-addr.arpa. IN PTR ns.nitec.com.
52.50.171.206.in-addr.arpa. IN PTR mail.nitec.com.
53.50.171.206.in-addr.arpa. IN PTR www.nitec.com.
```

这里，PTR 记录用于将三个不同的 IP 地址映射到三个不同的主机名。你也可以按如下方式以缩写形式指定前面的 PTR 记录：

```
51 IN PTR ns.nitec.com.
52 IN PTR mail.nitec.com.
53 IN PTR www.nitec.com.
```

在大多数情况下，你的 ISP 拥有你网络的 IP 地址，应准备提供主反向 DNS 服务。然而，对于一个特殊网络 127.0.0，你必须提供反向名称服务。此网络用于本地回环接口 IP（127.0.0.1）。由于没有人对这个回环网络拥有管辖权，因此每个人都必须提供反向
