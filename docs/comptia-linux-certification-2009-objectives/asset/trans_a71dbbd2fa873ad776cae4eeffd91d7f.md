
## 桩解析器

*桩* 解析器是一种 DNS 解析器，它通过接收客户端的查询并将其分发给多个 DNS 服务器来提高解析速度。它支持所有应用程序和服务。桩解析器引用 */etc/nsswitch.conf* 文件，以获取查询的处理顺序并确定必须使用的服务。根据此文件中的设置，桩解析器从数据库中检索信息。名称服务器解析的默认设置为 *hosts: files dns*，这意味着解析器将首先使用本地文件中列出的主机名，然后使用 DNS 来解析查询。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_538_0.png)

桩解析器

![](img/477ccb2f05b6ba1b2d563ea74f18c197_538_1.png)

*图 12-32：桩解析器的功能。*

## dig 实用程序

*dig* 实用程序与名称服务器进行交互，并向用户显示结果。它可以配置为查询单个名称服务器，或以批处理形式查询多个名称服务器。它引用 */etc/resolv.conf* 文件以获取要查询的名称服务器列表。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_538_2.png)

dig 实用程序

可以根据用户要求使用各种选项来配置 *dig* 实用程序。一些常用的命令选项列在表中。

| 命令选项 | 描述 |
| :--- | :--- |
| -b | 设置查询的源 IP 地址。该实用程序将使用此 IP 地址查询名称服务器。 |
| -f | 启用该实用程序基于指定文件中列出的进程查询名称服务器。 |
| -P | 指定用于发送查询的端口。 |
| -4 | 强制该实用程序仅使用 IPv4 协议进行查询。 |
| -6 | 强制该实用程序仅使用 IPv6 协议进行查询。 |
| -t *查询类型* | 设置查询类型。一些有效的查询类型包括 *soa, axfr, ixfr* 和 *mx*。 |

可以根据用户要求使用各种查询选项来配置 *dig* 实用程序。一些常用的查询选项列在表中。

| 查询选项 | 允许你 |
|---|---|
| +tcp | 设置解析器使用 TCP 服务查询名称服务器。 |
| +domain=somename | 为所需的域名创建搜索列表。 |
| +search | 配置解析器使用 /etc/resolv.conf 文件或通过 +domain 选项指定的搜索列表。 |
| +nsearch | 配置解析器根据名称服务器所在的区域搜索名称服务器。 |
| +identify | 显示回答查询的名称服务器的 IP 地址和端口号。 |
| +trace | 跟踪 /etc/resolv.conf 文件中根名称服务器信息的 DNS 查询。 |

### 语法

dig 实用程序的语法为 `dig [command options] [query options] [Fully Qualified Domain Name | IP address]`。

## host 实用程序

*host* 实用程序是一种 DNS 查找实用程序，类似于 *dig* 实用程序。它用于将系统名称转换为 IP 地址，反之亦然。*host* 实用程序具有各种选项。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_539_0.png)

| 选项 | 允许你 |
|---|---|
| name | 设置 host 实用程序要查找的域名。 |
| -t {query type} | 设置发送到名称服务器的查询类型。 |
| -W {seconds} | 设置解析器在退出前必须等待回复的时间。 |
| -s | 强制解析器在失败后不重试，从而终止查询过程。 |

### 语法

*host* 实用程序的语法为 `host [Command Options] {FQDN | IP Address}`。

## nslookup 实用程序

`nslookup` 实用程序用于通过 Internet 查询名称服务器，并验证 DNS 配置文件中名称到 IP 地址的映射是否正确。它以两种模式运行——交互模式和交互模式。交互模式允许客户端查询名称服务器以获取特定信息。非交互模式仅显示主机上的标准信息。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_540_0.png)

nslookup 实用程序

### 语法

`nslookup` 命令的语法为 `nslookup host name or FQDN`。

## 解析器文件

使用各种文件来配置解析器以解析域名和主机名。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_540_1.png)

解析器文件

| 文件 | 描述 |
| :--- | :--- |
| hosts 文件 | /etc/hosts 文件包含网络上系统的主机名到 IP 地址的映射信息。在旧版本的 Linux 中，使用 /etc/networks 文件来此用途。 |
| host.conf 文件 | /etc/host.conf 文件包含关于如何执行主机名查找的信息。例如，如果 /etc/host.conf 文件包含行 “order hosts,bind”，则主机名查找将首先在本地 /etc/hosts 文件中执行，然后在 DNS 中执行。/etc/hosts 文件中的默认条目是 “order hosts,bind。” |
| nsswitch.conf 文件 | /etc/nsswitch.conf 文件，即名称服务器切换配置文件，包含关于每个数据库及其工作顺序的信息。第一列包含关于数据库的信息并以冒号结尾；其余列指定数据库使用服务的顺序。例如，在文件条目 hosts: files dns 中，hosts 指的是主机数据库。这意味着本地文件中的主机条目比 DNS 服务器中的条目具有更高的优先级。如果在本地文件中找不到主机名条目，则将在 DNS 中继续搜索。 |
| resolv.conf 文件 | /etc/resolv.conf 文件，即解析器配置文件，是 C 库中提供 Internet DNS 访问的一组例程。解析器配置文件包含一组带有值的关键词，这些关键词由解析器例程在进程第一次调用它们时读取。三种不同的配置选项是名称服务器、域名和搜索。 |

## named.conf 文件

**定义：**

*named.conf* 文件是一个用户定义的配置文件，用于管理 BIND 服务。当 named 服务启动时，会调用此文件。它包含语句和注释。语句定义区域设置，而注释包含文件中语句的消息或描述。注释可以是单行或多行文本。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_541_0.png)

named.conf 文件

> 单行注释以 `//` 开头，多行注释以 `/*` 开头并以 `*/` 结尾。

**示例：**

```
options {
    directory "/var/named";
};

zone "." {
    type hint;
    file "named.ca";
};

zone "1.0.0.127.in-addr.arpa" {
    type master;
    file "named.local";
};

zone "ourglobacompany.com" {
    type master;
    file "ogc.forward";
};

zone "0.168.192.in-addr.arpa" {
    type master;
    file "ogc.reverse";
};
```

*图 12-33：named.conf 文件中的各种声明。*

## DNS 资源记录

*DNS 资源记录* 定义区域的参数。它包含五个组件：完全限定域名、TTL、记录类别、记录类型和数据记录。资源记录的格式由请求评注 (RFC) 定义。资源记录中的数据取决于记录类型。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_542_0.png)

表中列出了各种 DNS 记录及其使用的格式。

| DNS 记录 | 描述 |
|---|---|
| SOA | Start Of Authority (SOA) 记录用于以字符串字段格式指定区域的信息。SOA 记录告诉服务器成为该区域的权威服务器。每个区域只包含一个 SOA 记录。SOA 记录的格式为：`@ IN SOA primary nameserver hostmaster email ( serial number time to refresh time to retry time to expire minimum TTL )` |
| NS | Name Server (NS) 记录用于定义特定区域的权威名称服务器。NS 记录的格式为 `IN NS nameserver`。名称服务器应该是 FQDN。它可以是主服务器或从服务器。 |
| A | Address (A) 记录用于将 IP 地址分配给名称。A 记录的格式为 `hostname IN A IP address`。IP 地址不应以句号 (.) 结尾。如果省略主机名，则 A 记录指向命名空间顶部的默认 IP 地址。 |
| PTR | Pointer (PTR) 记录用于反向名称解析映射。它用于反向映射区域文件中将 IP 地址映射到名称。PTR 记录的格式为 `last IP digit IN PTR FQDN of system`。`last IP digit` 指定 IP 地址中的最后一个数字，它应指向特定系统的域名。PTR 记录始终应以句号结尾。例如，`253 IN PTR srvA.example.com` |

