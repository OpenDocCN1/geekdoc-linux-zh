
- 7. `ns.redhat.com` 将 `www.redhat.com` 的地址（Red Hat 为了负载均衡目的维护了两个 Web 服务器）返回给 `chivas`。

- 8. `Chivas` 将 `www.redhat.com` 的地址返回给 `cuernavaca`。

- 9. `Cuernavaca` 使用 `Netscape` 处理请求并与 `www.redhat.com` 交换信息。

图 9-3 显示了参与 DNS 工作的三方之间的关系。

你可以使用 `dig` 命令来演示这一过程。（你可以使用交互式 `dig` 或批处理模式下的 `dig` 来显示有关主机和域名的信息）。

运行以下命令：

```
dig www.redhat.com T_ANY
```

你应该能看到 Listing 9-1 中显示的信息。

![](img/75465a3c65cedf6b73d2aa7a566f6512_249_0.png)

图 9-3: 三个交互式 DNS 功能

## 第 9 章：构建域名服务器

### Listing 9-1: Dig 显示了关于 Red Hat Web 服务器的域信息

```
:: <<>> DIG 9.2.1 <<>> www.redhat.com

:: global options: printcmd

:: Got answer:

:: ->>HEADER<< opcode: QUERY, status: NOERROR, id: 15284

::; flags: qr ra; QUERY: 1, ANSWER: 2, AUTHORITIONAL: 3

:: QUESTION SECTION:

;www.redhat.com IN A

:: ANSWER SECTION:

www.redhat.com 600 IN A 216.148.218.197

www.redhat.com 600 IN A 216.148.218.195

:: AUTHORITY SECTION:

redhat.com 600 IN NS ns1.redhat.com.

redhat.com 600 IN NS ns2.redhat.com.

redhat.com 600 IN NS ns3.redhat.com.

:: ADDITIONAL SECTION:

s1.redhat.com 157562 IN A 66.178.233.210

s2.redhat.com 157562 IN A 66.77.185.41

s3.redhat.com 157562 IN A 63.240.14.66

:: Query time: 103 msec

:: SERVER: 192.168.1.254#53(192.168.1.254)

:: WHEN: Tue Sep 10 21:02:46 2002

:: MSG SIZE 166 rcvd: 166
```

查看 Listing 9-1 的末尾，在 `AUTHORITY SECTION`，你会发现 `dig` 咨询了“A”根服务器 `A.ROOT-SERVERS.NET`。根级名称服务器包含了 `redhat.com` 的名称服务器的地址。这些信息允许 `dig` 查询递归地从根服务器遍历到 `redhat.com` 的权威名称服务器，并最终找到了 `www.redhat.com` 的地址。

## 理解资源记录 (RR)

资源记录 (`RR`) 为权威名称服务器提供了基础。`RR` 定义了关于区域的基本信息，例如名称和邮件服务器。`RR` 还定义了 `IN`、`A` 和 `PTR` 记录。你可以在 `named.conf` 文件和区域文件中找到 `RR`。

## 使用起始授权 (SOA) 资源记录

以下摘自区域文件的片段显示了定义 DNS 服务器行为的一般参数；在此情况下，该区域是虚构的 `myomain.com`。

```
@ IN SOA myomain.com. root.mydomain.com. (
    2002091002 ; Serial
    10800 ; Refresh
    3600 ; Retry
    360000 ; Expire
    86400 ) Minimum
    IN NS ns.mydomain.com.
    IN MX 10 mail.mydomain.com.
```

`myomain.com` 区域文件中的此部分指定了 `myomain.com` 的起始授权 (`SOA`)。下列表描述了每个资源记录：

- `@`: 此符号意味着 `SOA` 与域相同。

- `IN`: `IN` 是一个提供 IP 地址的名称服务器类。当与 `A`、`PTR` 或 `CNAME` 记录结合使用时。

```
options {
  directory "/var/named";
}
```

- `acl`: 你可以定义访问控制列表（ACLs）来限制对 DNS 服务器的访问信息。访问控制列表有助于提高安全性并最小化管理成本。以下 `acl` 限制了对我们私有网络上机器的访问：

```
acl private : 192.168.1.0/24;
```

在这里，我们定义了标签——或变量 `private`，它对应于我们的私有网络。（注意 `/24` 是子网掩码 `255.255.255.0` 的简写。A 类和 B 类网络分别使用 `/8` 和 `/16` 的简写。）一旦定义，你就可以在配置文件的其他地方使用该标签来限制对其定义值的访问；在这种情况下，即私有网络。

- `zone name`: 该语句定义了区域定义。`zone` 语句定义了类型（主服务器 `master` 或从服务器 `secondary`/`slave`）、域名名称以及区域数据库文件名为。选项参数设置了选项，例如允许谁进行区域传输。以下示例定义了 `paunchy.net` 区域：

```
zone "paunchy.net" (
  type master;
  file paunchy.zone;
  allow-query ( any);
  allow-transfer ( 192.168.1.0/24 )
)
```

在这种情况下，该区域是主服务器。所有的映射信息都包含在 `paunchy.zone` 文件中；`paunchy.zone` 位于 `/var/named` 目录，该目录由 `options` 中的 `directory` 参数定义。我们允许任何人进行查询，尽管防火墙阻止了任何互联网用户进行解析。允许向我们私有网络上的任何机器进行传输，以便我们设置从服务器 DNS 服务器。

注意，如果我们在配置文件中定义了 `acl` 变量，可以用 `acl` 变量来替换显式的网络地址。例如，通过定义 `acl -acl private ( 192.168.1.0/24 );`，我们可以更改传输参数以允许传输。

![](img/75465a3c65cedf6b73d2aa7a566f6512_254_0.png)

区域映射文件 `paunchy.zone` 的名称是任意的，可以是任何名称。传统上，区域文件使用 `.db` 后缀——例如 `paunchy.db`——将它们描述为数据库。`zone` 这个词作为前缀或后缀使用的频率更频繁。我们使用 `.zone` 以保持与时俱进。

以下选项用于设置各种基于安全性的 DNS 服务器功能：

- `key`: 为 DNS 服务器设置加密密钥。

- `trusted keys`: 提供来自服务器信任的其它机器的密钥列表。

- `logging`: 在 DNS 服务器上设置日志记录。日志对于查看哪些机器正在访问 DNS 服务器并执行了区域传输非常重要。日志之所以重要，是因为它们提供了区域传输的审计轨迹，并提供验证你的密钥和访问列表是否按设计运行的方法。

一些主要参数如下：

- `allow-query`: 定义哪些机器可以查询本地 DNS 服务器。

- `allow-recursion`: 定义哪些 DNS 服务器可以递归地查询本地 DNS 服务器。

- `allow-transfer`: 定义哪些 DNS 服务器可以与本地 DNS 服务器执行区域传输。

- `forwards`: 列出本地 DNS 服务器可以转发查询的机器列表。

- `masters`: 对一个域具有权威性的从服务器列表。

- `slave`: 一个域的从服务器列表。

- `Comments` (注释): 注释由两个连续的斜杠 `//` 定义。注释用于记录 `named` 配置文件。

这里描述的选项用于确定 DNS 服务器将与哪些机器协作。指定哪些机器可以和不能与其交互，可以限制黑客获得的机会。使用这些选项可以显著增强 DNS 服务器的安全性。

## 介绍 `/var/named/` 配置文件

区域的位置在 `/etc/named.conf` 文件中任意定义。默认目录在 `options` 部分通过 `directory` 参数定义。`/var/named` 目录是 `named` 区域和其他其他配置文件的事实默认位置。我们的示例使用了该标准。

`bind` RPM 软件包默认不安装任何配置文件。我们正在根据 `bind` 软件包提供的示例构建我们的初始文件。这些文件如下：
