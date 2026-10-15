
# BIND 9 管理员参考手册

## 第 1 章 引言

互联网域名系统（DNS）由用于层级方式指定互联网实体名称的语法、用于授权名称管理权限的规则，以及将名称映射到互联网地址的系统实现组成。DNS 数据维护在一组分布式层级数据库中。

### 1.1. 文档范围

伯利互联网域名（BIND）为许多操作系统实现了一个域名服务器。这为系统管理员提供了有关安装维护以及互联网软件联盟（ISC）BIND 第 9 版本软件包的基本信息。本手册版本对应于 BIND 第 9 版本。

### 1.2. 文档组织

在本文档中，第 1 章 介绍了以层级方式指定互联网实体名称的语法，第 2 章 介绍了用于授权名称管理权限的规则，第 3 章 介绍了将名称映射到互联网地址的系统实现。第 4 章和 5 章 描述了在各种环境下运行 BIND。第 6 章 介绍了区域文件，第 7 章 包含了安全注意事项，第 8 章 包含了故障排除。正文之后是附录，它们包含了有用的信息。

### 1.3. 文档规范

在本文档中，我们使用了以下规范：

- **粗体** 用于定义术语
- *斜体* 用于强调或标题
- `内联代码` 用于代码片段
- [链接文本](URL) 用于引用

对于代码块，我们使用以下格式：

```
代码内容
```

对于表格，我们使用以下格式：

| 表头 | 表头 |
| --- | --- |
| 内容 | 内容 |

对于列表，我们使用以下格式：

- 无序列表项
1. 有序列表

区域。为了让 DNS 能够容服务器和网络故障，大多数区域有两个或多个权威服务器。

权威服务器的响应在数据包中设置了“权威回答”（AA）位。这使得在使用 `dig`（第 3.4.1.1 节）等工具调试 DNS 配置时能够轻松识别它们。

### 1.4.4.1. 主服务器 (Primary Master)

维护区域数据主副本的权威服务器被称为*主主服务器*，或简称为*主服务器*。它从某些人工编辑的本地文件，或者可能是由人工编辑的其他本地文件机械生成的文件中加载区域内容。该文件被称为*区域文件*。

### 1.4.4.2. 从服务器 (Slave Servers)

其他权威服务器，即*从服务器*（也称为*从服务器*），通过称为*区域传输*的复制过程从另一台服务器加载区域内容。通常数据是从主服务器传输的，但也可以从另一个从服务器传输。换句话说，从服务器本身也可以作为其下级从服务器的主服务器。

### 1.4.4.3. 隐藏服务器 (Stealth Servers)

通常，该区域的所有权威服务器都列在父区域的 NS 记录中。这些 NS 记录构成了父区域对该区域的*委托*。权威服务器也列在区域文件本身，位于区域的*顶层或顶点*（apex）。你可以在区域的顶层 NS 记录中列出不在父区域 NS 委托中的服务器，但你不能在父区域委托中列出不在区域顶层存在的服务器。

*隐藏服务器*是对某个区域具有权威性但未列在该区域 NS 记录中的服务器。隐藏服务器可用于保留区域的本地副本，以加速对区域记录的访问，或确保即使该区域的所有“官方”服务器不可用，该区域仍然可用。

主服务器本身即是隐藏服务器的配置通常被称为“隐藏主”配置。使用这种配置的场景是主服务器位于防火墙之后，因此无法与外部世界直接通信。



### 1.4.5. 缓存名称服务器 (Caching Name Servers)

大多数操作系统提供的解析器库是“存根解析器”（stub resolvers），这意味着它们无法通过直接调用权威服务器来自己执行完整的 DNS 解析过程。相反，它们依赖本地名称服务器代表它们执行解析。这样的服务器被称为递归名称服务器（recursive name server）；它为本地客户端执行递归查找。

为了提高性能，递归服务器会缓存它们执行的查找结果。由于递归和缓存过程紧密相连，“递归服务器”和“缓存服务器”术语通常被同义使用。

记录在缓存名称服务器缓存中保留的时间由与每个资源关联的生存时间（`TTL`）字段控制。

### 1.4.5.1. 转发 (Forwarding)

即使是名称服务器也不一定会自己执行递归查找。相反，它可以将其无法从缓存中满足的某些或全部查询转发到另一个名称服务器，这通常被称为转发器（forwarder）。

可能有一个或多个转发器，会按顺序对其进行查询，直到列表耗尽或找到答案。当你不希望站点的所有服务器都与互联网服务器直接交互时，通常会使用转发。一个典型的场景涉及一些内部 DNS 服务器和一个互联网防火墙。无法通过防火墙传递数据包的服务器将请求转发到可以执行此的服务器，由该服务器代表内部服务器查询互联网 DNS 服务器。使用转发功能的额外益处是，中央机器建立了一个更完整的信息缓存，所有客户端都可以从中受益。

### 1.4.6. 多重角色的名称服务器

`BIND` 名称服务器可以同时担任某些区域的主服务器、其他区域的从服务器，以及一组本地客户端的缓存（递归）服务器。

然而，由于权威名称服务和缓存/递归名称服务的功能在逻辑上是分离的，因此将它们运行在单独的服务器上是有益的。仅提供权威名称服务的服务器（仅权威服务器）可以在禁用递归的情况下运行，从而提高可靠性和安全性。对于任何区域都没有权威性且为本地客户端提供递归服务的服务器（仅缓存服务器）不需要从整个互联网访问，可以放置在防火墙内部。

## 第 2 章 BIND 资源需求

### 2.1. 硬件要求

DNS 的硬件需求传统上相当小。对于许多安装来说，退役活跃岗位的服务器作为 DNS 服务器的表现依然出色。

然而，`BIND` 9 的 DNSSEC 和 IPv6 特性证明是相当消耗 CPU 的，大量使用这些特性的组织可能希望为这些应用程序考虑更大的系统。`BIND` 9 现在已完全支持多线程，允许在需要它的的安装中充分利用多处理器系统。

### 2.2. CPU 要求

`BIND` 9 的 CPU 要求从提供不带缓存的静态区域服务的 `i486` 级机器，到如果你打算处理许多动态更新和 DNSSEC 签名区域、每秒提供数千次查询的企业级机器。

### 2.3. 内存要求

服务器内存足够大以容纳缓存和离磁盘的区域。可以使用 `max-cache-size` 选项来限制缓存使用的内存量，但以减少缓存命中和导致更多 DNS 流量为代价。拥有足够的内存将所有区域加载到内存中仍然是一个良好的做法。

### 2.4. 名称服务器密集型问题

对于名称服务器密集型环境，可以使用两种替代配置。第一种是客户端查询主服务器，主服务器有足够的内存构建大型缓存。第二种替代方案是独立设置从级名称服务器。在这种配置下，单个机器不需要那么多内存。

### 2.5. 支持的操作系统

`ISC BIND` 9 编译并运行在以下操作系统：

- `IBM AIX` 4.3
- `Compaq Digital/Tru64 UNIX` 4.0
- `Compaq Digital/Tru64 UNIX` 5 (带 IPv6)
- `HP HP-UX` 11
- `IRIX 64`
- `Sun Solaris` 2.6, 7, 8
- `NetBSD` 1.5 (带 `threads` 0.17)
- `FreeBSD` 3.4-STABLE, 3.5, 4.0, 4.1
- `Red Hat Linux` 6.0, 6.1, 6.2, 7.0

## 第 3 章 名称服务器配置

在本节中，我们提供了一些建议配置以及使用指南。我们还讨论了合理选项设置的主题。

### 3.1. 示例配置

### 3.1.1. 仅缓存名称服务器

以下示例配置适用于拒绝外部客户端使用的仅缓存服务器。

```
// 我们希望允许查询的两个子网。
acl "corpnets" ( 192.168.4.0/24; 192.168.7.0/24 );
options {
    directory "/etc/namedb"; // 工作目录
    pid-file "named.pid"; // 将 pid 文件放在工作目录
    allow-query { "corpnets"; }
}
// 根服务器提示
zone ". { type hint; file "root.hint"; };
// 为环回地址 127.0.0.1 提供反向映射
zone "0.0.0.127.in-addr.arpa" {
    type master;
    file "localhost.rev";
    notify no;
}
```

### 3.1.2. 仅权威名称服务器

此示例配置适用于作为 `example.com` 主服务器以及作为子域 `eng.example.com` 从服务器的仅权威服务器。

```
options {
    directory "/etc/namedb"; // 工作目录
    pid-file "named.pid"; // 将 pid 文件放在工作目录
    allow-query { any; }; // 这是默认值
    recursion no; // 不提供递归服务
}
```

### 3.2. 负载均衡

基础的负载均衡可以通过在 DNS 中为名称使用多个 `A` 记录来实现。

例如，如果你有三个网络地址分别为 `10.0.0.1`、`10.0.0.2` 和 `10.0.0.3` 的 `WWW` 服务器，设置如下的一组记录意味着客户端将在三分之一的时间连接到某一台机器：

| 名称 | TTL | 类 | 类型 | 资源记录 (RR) 数据 |
|---|---|---|---|---|
| www | 600 | IN | A | 10.0.0.1 |
| | 600 | IN | A | 10.0.0.2 |
| | 600 | IN | A | 10.0.0.3 |

当解析器查询这些记录时，`BIND` 将轮询它们并以不同的顺序对查询做出响应。在上面的示例中，客户端将随机接收到按 1, 2; 3; 2, 1; 以及 3, 1, 2 顺序的记录。大多数客户端将使用返回的第一条记录并丢弃其余。

关于请求排序的更多细节，请检查 `options` 语句中的 `rrset-order`，参见 **RRset 排序 (RRset Ordering)**。该子语句在 `BIND` 9 中不支持，仅支持所描述的排序方案。

### 3.3. 通知 (Notify)

DNS Notify 是一种机制，允许主名称服务器通知其从服务器区域数据的更改。在响应来自主服务器的 `NOTIFY` 之后，从服务器将检查其区域版本是否为当前版本，如果不是，则启动传输。

DNS Notify 在 `RFC 1996` 中有完整的文档。请参见区域选项 `also-notify` 的描述，见第 6.2.14.6 节。有关 `notify` 的更多信息，请参阅第 6.2.14.1 节。

### 3.4. 名称服务器操作

### 3.4.1. 用于名称服务器守护进程的工具

系统管理员有几种必不可少的诊断、管理和监控工具，用于控制和调试名称服务器守护进程。我们在此节中描述了其中几种。

#### 3.4.1.1. 诊断工具

```
dig
```

域名信息抓取器 (`dig`) 是一个命令行工具，可用于从域名系统服务器收集信息。`Dig` 有两种模式：用于单次查询的简单交互模式，以及对列表中的每条查询行执行查询的批量模式。所有查询选项都可以从命令行访问。

```
dig [@server] domain
[query-type][query-class][+query-option][-dig-option]%comment]
```

`dig` 的通常用法形式为：

```
dig @server domain query-type query-class
```

欲需更多信息以及可用命令和选项列表，请参见 `dig` 的手册页（man page）。

#### host

`host` 工具通过命令行界面提供简单的 DNS 查询，用于查找互联网主机名。默认情况下，该工具在主机名和互联网地址之间进行转换，但其功能通过使用选项得到了扩展。

```
host [-acdRTvw] [-c class] [-N ndots] [-t type] [-W timeout] [-R retries] hostname [server]
```

欲需更多信息以及可用命令和选项列表，请参见 `host` 的手册页。

#### nslookup

`nslookup` 是一个用于查询互联网名称服务器的程序。`nslookup` 有两种模式：交互式和非交互式。交互模式允许用户查询名称服务器有关各种主机的信息或打印主机列表。非交互模式仅用于打印主机或域的名称和所请求的信息。

```
nslookup [option...] [server]
```

当未提供参数（将使用默认名称服务器）或当第一个参数为连字符（'-'）且第二个参数为要查找的主机或互联网地址时，会进入交互模式。由于其界面晦涩且行为经常不一致，我们不建议使用 `nslookup`。请改用 `dig`。

### 3.4.2. 管理工具

管理工具在服务器的维护中起着不可或缺的作用。

#### named-checkconf

`named-checkconf` 程序检查 `named.conf` 文件的语法。

```
named-checkconf [-directory] [filename]
```

#### named-checkzone

`named-checkzone` 程序检查主文件的语法和一致性。

```
named-checkzone [-dq] [-c class] zone [filename]
```

远程名称守护进程 (`rndc`) 程序允许系统管理员控制服务器的运行。如果你在不带任何选项的情况下运行 `rndc`，它将显示如下用法信息：

```
rndc [-c config] [-s server] [-p port] [-y key] command [command...]
```

`command` 是以下内容之一：

- `reload`: 重新加载配置文件和区域。
  ```
  rndc reload [class [view]]
  ```
- `reload zone`: 重新加载指定的区域。
  ```
  rndc reload zone [class [view]]
  ```
- `refresh zone`: 为指定的区域安排维护任务。
- `reconfig`: 重新加载配置文件并加载新区域，但如果现有文件已更改，则不重新加载。当区域数量较多时，这比完全重载更快，因为避免了检查区域修改时间的需要。
- `stats`: 将服务器统计数据写入统计文件。
- `querylog`: 切换查询日志。也可以通过在 `named.conf` 的 `logging` 部分显式地将 `queries` 类别指向 `channel` 来启用查询日志。
- `dumpdb`: 将服务器缓存转储到转储文件。
- `stop`: 停止服务器，确保通过动态更新或 `IXFR` 进行的最新更改首先保存到更新区域的主文件中。
- `halt`: 立即停止服务器。通过动态更新或 `IXFR` 进行的最新更改不会保存到主文件中，但当服务器重启时将从日志文件中向前回滚。
- `trace`: 将服务器调试级别增加一。
- `trace level`: 将服务器的调试级别设置为显式值。
- `notrace`: 将服务器的调试级别设置为 0。
- `flush`: 刷新服务器缓存。
- `status`: 显示服务器状态。

在 `BIND` 9.2 中，`rndc` 支持 `BIND` 8 工具的所有命令，但 `rndc start` 除外，后者在 `rndc` 的通道模式中是不支持的。需要一个配置文件，因为与服务器的所有通信都是使用基于共享密钥的数字签名进行验证的，除了使用配置文件外没有其他方法提供该密钥。`rndc` 配置文件的默认位置是 `/etc/rndc.conf`，但可以使用 `-c` 选项指定替代位置。如果找不到配置文件，`rndc` 也会在 `/etc/rndc.key` 中查找（当 `BIND` 配置时定义的）。

```
);
```

并且它有一个与 `rndc_key` 相同的键值语句。

运行 `rndc-confgen` 程序将方便地为你创建一个 `rndc.conf` 文件，并同时显示你需要添加到 `named.conf` 中的相应控制语句。或者，你也可以运行 `rndc-confgen -a` 来设置 `rndc.key` 文件，而完全不需要修改 `named.conf`。

### 3.4.2. 信号

某些 UNIX 信号会导致命名服务器执行特定的操作，如下表所示。这些信号可以使用 `kill` 命令发送。

| 信号 | 描述 |
|---|---|
| SIGHUP | 导致服务器读取 `named.conf` 并重新加载数据库。 |
| SIGTERM | 导致服务器清理并退出。 |
| SIGINT | 导致服务器清理并退出。 |

## 第 4 章 高级概念

### 4.1. 动态更新

动态更新（Dynamic update）是指在特定条件下，添加、修改或删除主区文件中的记录或 `RRset` 的能力术语。动态更新在 `RFC 2136` 中有详细描述。

动态更新通过在区域语句中包含 `allow-update` 或 `update-policy` 子句来按区域启用的。

安全区域（使用 DNSSEC 的区域）的更新遵循 `RFC 3007`：受更新影响的 `SIG` 和 `NXT` 记录将由服务器使用在线区域密钥自动生成。更新授权基于事务签名和显式服务器策略。

#### 4.1.1. 日志文件

所有对使用动态更新区域的更改都存储在区域的日志文件（journal file）中。该文件由服务器在发生第一次动态更新时自动创建，并在相应的区域文件名后添加 `.jni` 扩展名。日志文件为二进制格式，不应手动编辑。

服务器还会偶尔（“dump”）将更新区域的完整内容转储到其区域文件中。这不会在每次动态更新后立即执行，因为当大区域频繁更新时，这样做速度会太慢。相反，转储会延迟 15 分钟，允许进行额外的更新发生。

当服务器在关闭或崩溃后重启时，它将重放日志文件，将上次区域更新之后发生的所有更新合并到区域中。

传入的增量区域传输的更改也以类似的方式记录日志。

动态区域的区域文件通常无法通过手动编辑，因为它们无法保证包含最新的动态更改——这些更改仅位于日志文件中。确保动态区域的区域文件是最新的唯一方法是运行 `rndc`。

如果你必须动态地更改区域，以下步骤将有效：使用 `rndc` 关闭服务器（仅发送信号或使用 `rndc halt` 是不够的）。等待服务器退出，删除区域的 `.jni` 文件，编辑区域文件，然后重启服务器。删除 `.jni` 文件是必要的，因为手动编辑的内容不会出现在日志中，导致其与区域文件的内容不一致。

### 4.2. 增量区域传输 (IXFR)

增量区域传输 (`IXFR`) 协议是从服务器仅传输更改数据的方法，而无需传输整个区域。`IXFR` 协议在 `RFC 1995` 中记录。请参见建议标准（Proposed Standards）。

当作为主服务器时，`BIND` 9 支持那些具有必要的更改历史信息的区域的 `IXFR`。这些包括由动态更新维护的主区域，以及通过 `IXFR` 获取数据的从区域，但不包括手动维护的主区域或通过完整区域传输 (`AXFR`) 获取的区域。

当作为从服务器时，`BIND` 9 将尝试使用 `IXFR`，除非被显式禁用。有关禁用 `IXFR` 的更多信息，请参见服务器语句中 `request-ixfr` 子句的描述。

### 4.3. Split DNS

为内部和外部资源设置不同的 DNS 视图或可见性，通常称为拆分 DNS（Split DNS）设置。组织想要以这种方式设置其 DNS 有几个原因。

设置 DNS 系统的常见原因是从互联网上的“外部”客户端隐藏“内部”DNS 信息。关于这是否真的有用存在一些争议。内部信息会以许多方式泄露（例如，通过邮件头），而大多数精明的“攻击者”可以使用其他方法找到他们需要的信息。

另一个设置拆分 DNS 系统的常见原因是允许位于过滤器后面或 `RFC 1918` 空间（如 `RFC 1918` 文档的保留 IP 空间）的内部网络在互联网上解析 DNS。拆分 DNS 还可以允许邮件进入内部网络。

以下是一个 DNS 设置示例：

假设有一名为 `Example, Inc.` (`example.com`) 的公司，其公司服务器具有带有互联网协议 (`IP`) 空间的内部网络以及一个供公众使用的外部非军事化区 (`DMZ`)，或网络的“外部”部分。

`Example, Inc.` 希望其内部客户端能够解析外部主机名，并与外部人员交换邮件。该公司还希望其内部解析器能够访问某些仅限内部的区域，这些区域在内部网络外部完全不可用。

为了实现这一点，公司将设置两组名称服务器。一组位于内部网络（在保留的 `IP` 空间内），另一组位于堡垒机上，这些是位于 `DMZ` 的、与网络双端都通信的“代理”主机。

内部服务器将配置为将所有查询转发到 `DMZ` 中的服务器，但对 `site1.internal`、`site2.internal`、`site1.example.com` 和 `site2.example.com` 的查询除外。

这些内部服务器将拥有完整的记录集。

#### 内部 DNS 服务器配置



```
acl internals { 172.16.72.0/24; 192.168.1.0/24; };
acl externals { bastion-ips-go-here; };
options {
  ...
  forward only;
  forwarders { // 转发到外部
    servers {
    bastion-ips-go-here;
    };
    allow-transfer { none; }; // 示例 allow
    transfer (no one)
    allow-query { internals; externals; }; // 限制查询访问
    allow-recursion { internals; }; // 限制递归
  ...
};
zone "site.example.com" { // 示例主区域
  type master;
  file "m/sitel.example.com";
  forwarders { }; // 执行正常的迭代
  tion (do not forward)
  allow-query { internals; externals; };
  allow-transfer { internals; };
};
// resolu-
zone "site2.example.com" {
  type slave;
  file "s/site2.example.com";
  masters { 172.16.72.3; };
  forwarders { };
  allow-query { internals; externals; };
  allow-transfer { internals; };
};
zone "site.internal" {
  type master;
  file "m/sitel.internal";
forwarders { };
allow-query { internals; };
allow-transfer { internals; }

zone "site2.internal" {
type slave;
file "s/site2.internal";
masters { 172.16.72.3; };
forwarders { };
allow-query { internals; }
allow-transfer { internals; }
```

外部（堡垒机）DNS 服务器配置：

```
acl internals { 172.16.72.0/24; 192.168.1.0/24; };
 externals { bastion-ips-go-here; };
```

```
options {
...
allow-transfer { none; }; // 示例 allow
transfer (no one)
allow-query { internals; externals; }; // 限制查询访问
allow-recursion { internals; externals; }; // 限制递归
};
```

```
zone "sitel.example.com" { // 示例从用区域
type master;
file "m/sitel.foo.com";
allow-query { any; };
allow-transfer { internals; externals; }
};
```

```
zone "site2.example.com" {
type slave;
file "s/site2.foo.com";
masters { another_bastion_host_maybe; };
allow-query { any; };
allow-transfer { internals; externals; }
};
```

# 第 4 章. 高级概念

在堡垒机（s）上的`resolv.conf`（或等效文件）中：

```
search ...
nameserver 172.16.72.2
nameserver 172.16.72.3
nameserver 172.16.72.4
```

### 4.4. TSIG

这是一份关于在`BIND`中设置基于事务签名（`TSIG`）事务安全性的简短指南。它描述了配置文件的更改，以及不同功能所需的更改，包括创建事务密钥的过程以及在`BIND`中使用事务签名的方法。

`BIND`主要支持用于服务器通信的`TSIG`。这包括区域传输、通知（`notify`）和递归查询消息。较新版本的`BIND 8`解析器对`TSIG`的支持有限。

`TSIG`在动态更新中可能最有用。动态区域的主服务器应该使用访问控制来控制更新，但基于`IP`的访问控制是重要的。基于密钥的访问控制要优得多，请参见建议标准（`Proposed Standards`）。`nupdate`程序通过`-k`和`-y`命令选项支持`TSIG`。

### 4.4.1. 为每对主机生成共享密钥

生成一个要在`host1`和`host2`之间共享的密钥。选择一个任意的密钥名称：`"host1-host2."`。密钥名称在两台主机上必须相同。

#### 4.4.1.1. 自动生成

以下命令将生成一个描述的 128 位（16 字节）`HMAC-MD5`密钥。更长的密钥更好，但用`MD5`更容易处理。注意，最大密钥长度为 512 位；密钥比产生 128 位所需的要长。

```
dnssec-keygen -a hmac-md5 -b 128 -n HOST host1-host2.
```

密钥位于文件`Khost1-host2.+.157+00000.private`中。不直接使用此文件，但可以从文件中提取`"Key:"`随后的`base64`编码字符串并用作共享密钥：

`Key:` `La/E5cG90+0sl1jq0a2da==`

字符串`"La/E5cG90+0sl1jq0a2da=="`可以用作共享密钥。

#### 4.4.1.2. 手动生成

共享密钥仅仅是经过`base64`编码的随机位序列。大多数`ASCII`字符串都是有效的`base64`（假设长度是 4 的倍数且仅使用有效字符），因此可以手动生成共享密钥。

此外，可以将已知字符串通过`mmencode`或类似的程序运行以生成`base64`编码数据。

### 4.4.2. 将共享密钥复制到两台机器

这超出了传输的范围。应该使用安全的传输机制。这可以是安全`FTP`、`ssh`、电话等。

### 4.4.3. 通知服务器密钥的存在

假设`host1`和`host2`都是服务器。在每台服务器的`named.conf`文件中添加以下内容：

```
key host1-host2. {
  algorithm hmac-md5;
  secret "LaESCJG90+0sljqq0a2jdA==";
}
```

算法`hmac-md5`是`BIND`支持的唯一算法。`secret`是上面生成的。由于这是一个密钥，建议`named.conf`不要对全局可读，或者将`key`指令添加到一个对全局不可读且被`named.conf`包含的文件中。

至此，密钥已被识别。这意味着如果服务器接收到由此密钥签名的消息，它可以验证签名。如果签名成功，响应将由相同的密钥签名。

### 4.4.4. 指示服务器使用密钥

由于密钥在两个主机之间共享，必须指示服务器何时使用密钥。在`host1`的`named.conf`文件中添加以下内容，如果`host2`的`IP`地址为`10.1.2.3`：

```
server 10.1.2.3 {
  keys { host1-host2. };
}
```

可以存在多个密钥，但只使用第一个。该指令不包含密钥，因此全局公开。

如果`host1`向该地址发送消息，该消息将使用指定的密钥签名；`host1`将期望响应由相同的密钥签名。

在`host2`的配置文件（带有`host1`的地址）中必须存在类似的语句，以便`host2`签名。

### 4.4.5. `TSIG`密钥访问控制

```
acl internals { 172.16.72.0/24; 192.168.1.0/24; };
 externals { bastion-ips-go-here; };
```

### 4.4.6. 错误

`TSIG`的处理可能会导致多种错误。如果`TSIG`感知服务器接收到未知密钥，将返回`FORMERR`。如果`TSIG`感知服务器接收到无效签名，将返回`BADSIG`。如果`TSIG`感知服务器接收到时间超出允许范围的消息，将返回`BADTIME`。在任何这些情况下，`rcode`均被设置为`NOTAUTH`。

## 第 4 章 高级概念

还必须与父区域和/或子区域的管理员通信，以传输密钥和签名。父区域必须指示一个区域的安全状态，以便支持`DNSSEC`的解析器能够信任其数据。

为了让其他服务器信任此区域中的数据，它们必须是静态地配置此区域的区域密钥，或者配置`DNS`树中该区域之上任何区域的密钥。

### 4.7.1. 生成密钥

`dnskeygen`程序用于生成密钥。

一个安全的区域必须包含一个或多个区域密钥。区域密钥将对区域中的所有记录进行签名，且区域密钥的名称必须与区域相同，类型为`ZONE`，并用于身份验证。建议区域密钥使用`IETF`设计为“强制实施”的加密算法；目前这些算法包括`RSA1`（在`BIND 9.2`中不支持）和`DSA`。

以下命令将为`child.example`区域生成一个 768 位的`DSA`密钥：

```
dnsseckey -a DSA -b 768 -n ZONE.example.
```

将产生两个输出文件：`Rchild.example,+00312345.key`和`Rchild.example,+00312345.private`（其中`12345`是密钥标记示例）。密钥文件名包含了密钥名称（`child.example.`）、算法（`3`是`DSA`，`1`是`RSA`等）以及密钥标记（本例中为`12345`）。私钥（在`.private`文件中）用于生成签名，公钥（在`.key`文件中）用于签名验证。

要生成另一个具有相同属性（但标记不同）的密钥，请重复该命令。

应使用`INCLUDE`语句将公钥插入到区域文件中，包括`.key`文件。

### 4.7.2. 创建密钥集

`dnsmakekeysyset`程序用于从一个或多个密钥创建一个密钥集（`keyset`）。

密钥生成后，必须构建一个密钥集传输给父区域的管理员，以便父区域可以使用其自身的区域密钥对密钥进行签名，并正确指示此区域的安全状态。构建密钥集时，必须指定要包含的密钥列表以及集合的`TTL`，也可以指定父区域签名的预期有效期。

插入密钥集的密钥列表还可能包含位于区域顶部的非区域密钥。`dnssec-makekeyset`也用于区域中的其他名称。

以下命令生成一个包含上述密钥另一个密钥的密钥集，其`TTL`为`3600`，从现在开始的签名有效期为 10 天。

```
dnssec-makekeyset -t 3600 -e +864000 Kchild.example.+003+12345 Kchild.example.+003+23456
```

产生一个输出文件：`keyset-child.example..`。该文件应传输给父区域进行签名。它包含了密钥，以及由区域密钥本身生成的对密钥集的的签名，这些签名用于证明私钥的所有权并确保预期的有效期。

### 4.7.3. 对子密钥集签名

`dnssec-signkey`程序用于对子区域的密钥集进行签名。如果`child.example`有任何安全的委托（例如`grand.child.example`），子区域管理员应接收每个安全子区域的密钥集文件。这些密钥必须由此区域的密钥进行签名。

以下命令使用区域密钥对子密钥集进行签名：

```
dnssec-signkey keyset-grand.child.example. Kchild.example.+003+12345 Kchild.example.+003+23456
```

产生一个输出文件：`signedkey-grand.child.example..`。该文件应既传回子区域又要保留。它包含了来自密钥集文件的所有密钥（子区域密钥）以及由此区域密钥生成的签名。

### 4.7.4. 对区域签名

`dnssec-signzone`程序用于对区域进行签名。将存在对应于安全子区域的任何`signedkey`文件，以及父区域生成的此区域的签名文件（如果有）。区域签名器将为该区域生成`NXT`和`SIG`记录，还将合并父区域的区域密钥签名并在所有委托点指示安全状态。

以下命令对区域进行签名，假设它位于名为`zone.child.example.`的文件中。默认情况下，所有具有私钥的区域密钥都将被用于签名。

```
dnssec-signzone -o child.example zone.child.example
```

产生一个输出文件：`zone.child.example.signed`。该文件应被`named.conf`引用为该区域的输入文件。

### 4.7.5. 配置服务器

与`BIND 8`不同，`BIND 9`在加载时不验证数据，因此权威区域的区域密钥不需要在配置文件中指定。

任何安全根的公钥必须存在于文件的`trusted-keys`语句中，如本文后文所述。

### 4.8. `BIND 9`对`IPv6`的支持

`BIND 9`完全支持所有定义的`IPv6`名称到地址和地址到名称的查找。它将在支持`IPv6`的系统上使用`IPv6`地址进行查询。

对于正向查找，`BIND 9`同时支持`A`和`AAAA`记录。`AAAA`记录的使用已被弃用，但对于主机同时拥有`AAAA`和`A6`记录仍然有用，以保持与仅支持`AAAA`查询的存根解析器的实现向后兼容，因为跟踪`A6`链比执行`AAAA`查询更困难。

对于`IPv6`反向查找，`BIND 9`支持`ipv6.arpa`域使用的新的“位字符串”（`bitstring`）格式，以及在`ipv6`域使用的较旧的“半字节”（`nibble`）格式。`BIND 9`包含一个轻量级解析器，新应用程序可以选择避免跟踪`A6`链位字符串标签的复杂性，见第 5 章。

有关`IPv6`地址格式和结构的概述，请参见第 3 节。

### 4.8.1. 使用`AAAA`记录进行地址查找

`AAAA`记录与`IPv4`记录并行。它在一个记录中指定整个地址。

```
$ORIGIN example.com.

host AAAA fffe:8050:201:80::
```

虽然它们的使用已被弃用，但它们对于支持旧的`IPv6`很有用。不应在不需要的地方添加它们。

### 4.8.2. 使用`A6`记录进行地址查找

`A6`记录比`AAAA`记录更灵活。它在记录中指定整个地址。由于跟踪位字符串标签的链链比执行`AAAA`查询更困难，新应用程序可能选择避免跟踪`A6`链位字符串的复杂性。例如：

```
$ORIGIN example.com.

host AAAA fffe:8050:201:80::
```

### 4.8.3. 使用半字节格式进行地址到名称查找

虽然使用半字节格式查找名称已被弃用，但为了与现有的`IPv6`应用向后兼容，它仍然可用。

在半字节格式下查找时，地址组件简单的反转，就像`IPv4`一样，并附加`ip6.int.`。例如，以下内容为`:3fffe:8050:201:860::1`的主机提供反向查找：

```
$ORIGIN 0.6.8.1.1.0.2.0.5.0.8.f.3.ip6.int.

1.0.0.0.0.0.0.0.2.4.0.0 1400
```

### 4.8.4. 使用位字符串格式进行地址到名称查找

位字符串标签可以在任何位边界开始和结束，而不是在半字节格式的 4 位倍数处。它们还使用`ipv6.arpa`而不是`ip6.int`。

使用位字符串重现之前的示例：

```
$ORIGIN [x3fffe805020021860/64].ip6.arpa.

[x004200000000001/64] 14400 IN PTR host.example.com.
```

### 4.8.5. 使用`DNS`委托`IPv6`反向地址

在`IPv6`中，同一个主机可能具有来自多个网络提供者的多个地址。由于地址的后缀通常保持不变，`DNAME`可以减少需要维护的反向映射区域文件的数量。

例如，考虑一个具有两个供应商（`example.net`和`example2.net`）以及两个`IPv6`地址的主机。由于主机选择自己的 64 位主机地址部分，只有提供者地址是发生变化的。

| host | IN | A6 | 64 | ::1234:5678:1212:5675 cust1.example.net. |
| | IN | A6 | 64 | ::1234:5678:1212:5675 subnet5.example.net. |
| $ORIGIN example.net. | IN | A6 | 48 | 0:0:0:0:::ipv6net.example.net. |
| cust1 | IN | A6 | 0 | aa:bb:cccc: |
| $ORIGIN example2.net. | IN | A6 | 48 | 0:0:0:1::ipv6net.example2.net. |
| ipv6net | IN | A6 | 0 | 6666:5555:54:: |

这设置了正向查询。为了处理反向查询，`example.net`服务商将拥有：

```
$ORIGIN [x0aabbcccc/48].ip6.arpa.

[dddd/16] IN DNAME ipv6-rev.example.com.
```

而`example2.net`将拥有：

```
$ORIGIN [x66665555000/48].ip6.arpa.

[x0001/16] IN DNAME ipv6-rev.example.com.
```

`example.com`只需要一个区域来处理这两种反向映射：

```
$ORIGIN ipv6-rev.example.com.



`[x1234567812125675/64] PTR host.example.com.`

# 第 5 章 BIND 9 轻量级解析器

## 5.1. 轻量级解析器库

传统上，应用程序与存根解析器（stub resolver）库链接，该库向本地缓存名称服务器发送递归 `DNS` 查询。

`IPv6` 为解析过程引入了新的复杂性，例如遵循 `A6` 链和 `DNAME` 记录，以及同时查找 `IPv4` 和 `IPv6` 地址。这些功能在传统的存根解析器中很难或无法实现。

相反，`BIND` 为轻量级解析器库和运行在本地主机上的解析器守护进程提供解析服务。它们使用简单的基于 `UDP` 的协议进行通信，即“轻量级解析器协议”，该协议与完整的 `DNS` 协议不同且更为简单。

## 5.2. 运行解析器守护进程

要使用轻量级解析器接口，系统必须运行解析器守护进程 `lwres`。

默认情况下，使用轻量级解析器库的应用程序将向端口 `921` 的 `IPv4` 回环地址（`127.0.0.1`）发送 `UDP` 请求。该地址可以通过 `/etc/resolv.conf` 中的 `lwserver` 行进行覆盖。守护进程将尝试回答问题“host foo.example.com 的地址是什么？”以及“IPv4 地址 10.1.2.3 的名称是什么？”

该进程目前只查找 `DNS`，但未来可能会使用其他源，如 `/etc/hosts`、`NIS` 等。

`lwres` 守护进程本质上是一个缓存名称服务器，使用轻量级解析器协议而不是 `DNS` 协议来请求。由于它需要在每个主机上运行，因此被设计为不需要或仅需要极少配置。除非另有配置，否则它使用 `/etc/resolv.conf` 中 `nameserver` 行列出的名称服务器作为转发器，但在未指定的情况下也能自主解析。

`lwres` 守护进程也可以配置一个 `named.conf` 风格的文件，默认位于 `/etc/lwres.conf`。也可以通过 `named.conf` 中的 `lwres` 语句配置名称服务器作为轻量级解析器守护进程。

# 第 6 章 BIND 9 配置参考

`BIND 9` 的配置与 `BIND 8.x` 大体相似；然而，有一些新的配置区域，例如视图（`views`）。`BIND 8.x` 配置文件在 `BIND 9` 中只需少许修改即可工作，但应对更复杂的配置进行审查，以检查是否可以使用 `BIND 9` 中的新功能更高效地实现。

`BIND 4` 可以使用脚本 `contrib/named-bootconf/named-bootconf.sh` 转换为新格式。

## 6.1. 配置文件元素

以下是整个 `bind` 配置中使用的元素列表：

| 元素 | 说明 |
| :--- | :--- |
| `acl_name` | 由 `acl` 语句定义的 `address_match_list` 的名称。 |
| `address_match_list` | 一个或多个 `ip_addr`、`ip_prefix`、`key_id` 或 `acl_name` 元素的列表，见第 6.1.1 节。 |
| `domain_name` | 用作 `DNS` 名称的引号字符串，例如 `"test.domain"`。 |
| `dotted_decimal` | 一个或多个由点（`'.'`）隔开的 `0` 到 `255` 之间的整数，例如 `23.45.67` 或 `89.123.45.67`。 |
| `ip4_addr` | 以点分表示法且恰好包含四个元素的 `IPv4` 地址。 |
| `ip6_addr` | 一个 `IPv6` 地址，例如 `fe80::200:ff83:fe01:9742`。 |
| `ip_addr` | `ip4_addr` 或 `ip6_addr`。 |
| `ip_port` | `IP` 端口号。限制为 `0` 到 `65535`，低于 `1024` 的值限制为 `root` 拥有进程。在某些情况下，可以使用星号字符作为占位符进行选择。 |
| `ip_prefix` | 一个 `IP` 前缀。以 `ip_addr` 表示，后面跟着斜杠（`/`）和掩码位数。例如 `127.0.0/8` 掩码为 `255.0.0`。 |
| `key_id` | 由 `key` 语句定义的标识。 |
| `key_list` | 多个 `key_id` 列表，用分号分隔。 |
| `number` | 一个非负 `64` 位无符号整数（`0` 到 `18446744073709551615`）。使用 `unlimited` 表示最大值。 |
| `path_name` | 用作路径的引号字符串，例如 `zones/master.`。 |
| `size_spec` | 一个数字、单词 `unlimited` 或单词 `default`。 |
| `yes_or_no` | 是 `yes` 或 `no`。也接受 `true` 和 `false`，以及数字 `1` 和 `0`。 |

### 6.1.1. 地址列表

#### 6.1.1.1. 语法



`address_match_list = address_match_element ;`

`[ address_match_element ]`

`address_match_element = [ ! ] ( ip_address [/length] | key_id | acl_name | ( address_match_list ) )`

### 6.1.1.2. 定义与使用

地址匹配列表（match lists）主要用于确定各种服务器操作的访问控制。它们还用于定义查询名称服务器的优先级，并设置服务器监听的地址。构成地址列表的元素可以是以下任何一种：

- 一个 IP 地址（IPv4 或 IPv6）
- 前缀表示法的 IP
- 由 `key` 语句定义的键 ID
- 之前通过 `acl` 语句定义的地址列表名称
- 用大括号括的嵌套匹配列表

当给定的 IP 地址或前缀与地址匹配列表进行比较时，按顺序遍历列表直到找到匹配元素。匹配的解释取决于该列表是用于访问控制、定义监听端口还是拓扑，以及该元素是否被否定。

当用于访问控制时，非否定列表允许访问，而否定的匹配拒绝访问。如果没有匹配，则拒绝访问。`allow-notify`、`allow-query`、`allow-transfer`、`update-notify` 和 `blacklist` 都使用地址匹配列表。同样，`listen-on` 选项将导致服务器不在任何匹配列表的机器地址上接受查询。

当用于 `topology` 子句时，非否定匹配根据其在列表中的位置返回距离（匹配越靠近列表开头，其与服务器之间的距离就越短）。否定的匹配将被分配最大距离。如果没有匹配，则地址将获得一个比任何非否定列表元素都远的距离，且比任何取反元素更近的距离。

由于算法的优先匹配特性，列表中定义另一个元素子集的元素应该位于更宽泛元素之前，无论其中一个是否被取反。例如，在 `1.2.3/24; ! 1.2.3.13;` 中，`1.2.3.13` 元素是完全没用的，除非算法会将对 `1.2.3.13` 的查找匹配到 `1.2.3/24` 元素。使用 `! 1.2.3.13; ! 1.2.3/24;` 可以解决这个问题，让 `1.2.3.13` 被取反拦截，而所有其他 `1.2.3.*` 主机都能通过。

## 6.1.2. 注释语法

`BIND 9` 的注释允许注释出现在 `BIND` 配置文件中空白可能出现的任何地方。为了迎各种类型的程序员，注释可以使用 C、C++ 或 shell/perl 结构来编写。

### 6.1.2.1. 语法

```
* 这是一个像 C 一样的 BIND 注释 */

// 这是一个像 C++ 一样的 BIND 注释

# 这是一个像常用 UNIX shell 和 perl 一样的 BIND 注释
```

### 6.1.2.2. 定义与用法

注释可以出现在 `BIND` 配置文件中空白可能出现的任何地方。
C 风格注释以两个字符 `/*`（斜杠、星号）开始，以 `*/`（星号、斜杠）结束。由于它们由这些字符完全界定，因此可以只注释一行的部分内容，也可以跨多行。

C 风格注释不能嵌套。例如，以下内容无效，因为整个注释在 `/*` 处结束：

```
* 这是注释的开始。

这仍然是注释的一部分。

/* 这是一个错误的嵌套注释尝试。 */

这不再属于任何注释了。 */
```

C++ 风格注释以两个字符 `//`（斜杠、斜杠）开始，并持续到物理行的末尾。它们不能跨越多个物理行；要让一个逻辑注释跨越多行，每行都必须使用 `//` 对。

例如：

```
// 这是注释的开始。下一行

// 是一个新注释，尽管它在逻辑上

// 是上一个注释的一部分。
```

Shell 风格（或如果你喜欢，是 perl 风格）注释以字符 `#`（井号）开始，并像 C++ 注释一样持续到物理行的末尾。

例如：

```
# 这是注释的开始。下一行

# 是一个新注释，尽管它在逻辑上

# 是上一个注释的一部分。
```

> 警告
> 警告：你不能像在区域文件（zone file）中那样使用分号（`;`）字符来开始注释。分号表示配置语句的结束。

## 6.2. 配置文件语法

一个 `B 9` 配置由语句和注释组成。语句和注释是可以在不包含在大括号内的情况下出现的唯一元素。许多语句包含一个子语句块，这些子语句也以分号终止。

支持以下语句：

| 语句 | 描述 |
| :--- | :--- |
| `acl` | 定义一个命名的 IP 地址匹配列表，用于访问控制和其他用途。 |
| `controls` | 声明供 `rndc` 工具程序使用的控制通道。 |
| `include` | 包含文件。 |
| `key` | 指定用于使用 TSIG 进行身份验证和授权的密钥信息。 |
| `logging` | 指定服务器日志的内容以及日志消息发送到的位置。 |
| `options` | 控制全局服务器配置选项和其他语句的默认值。 |
| `server` | 基于每个服务器设置某些配置选项。 |
| `trusted-keys` | 定义 DNSSEC 密钥。 |
| `view` | 定义一个视图（view）。 |
| `zone` | 定义一个区域（zone）。 |

`logging` 和 `options` 语句可以定义一次。

### 6.2.1. `acl` 语法

```
acl name {

  list list

};
```

### 6.2.2. `acl` 定义与用法

`acl` 语句定义一个命名的 IP 地址匹配列表，用于访问控制和其他用途。
注意：`acl` 语句只能定义一次。

| 列表 | 描述 |
| :--- | :--- |
| `any` | 匹配所有主机。 |
| `none` | 不匹配任何。 |
| `localhost` | 匹配回环地址。 |

### 6.2.3. `controls` 语法

```
controls {

  inet port {

    allow list;

    keys list;

  };

}
```

### 6.2.4. `controls` 定义与用法

`controls` 语句声明供 `rndc` 工具程序使用的控制通道。
`inet` 语句在指定的端口上监听。`inet` 端口可以是 IPv4 或 IPv6 地址。使用 `*` 端口表示监听所有接口。`allow` 子句允许根据匹配列表进行访问。`keys` 子句允许通过密钥列表对消息进行签名。

要禁用控制通道，可以使用空的 `controls` 语句：`controls { };`

### 6.2.8. `key` 语句的定义与用法

`key` 语句定义了用于 TSIG 的共享秘密密钥，详见第 4.4 节。

`key` 语句可以出现在配置文件的顶层，也可以出现在 `view`（视图）语句内部。定义在顶层中的密钥可以在所有视图中使用。打算用于 `controls`（控制）语句（见第 6.2.4 节）的密钥必须在顶层定义。

`key_id`（也称为密钥名称）是一个唯一标识密钥的域名名。它可以用于“`server`”语句，使发送到服务器的请求使用此密钥进行签名；或者用于地址匹配列表（address match lists），以验证传入的请求是否已使用该名称、算法和密钥进行了签名。

`algorithm_id` 是一个指定安全/身份验证算法的字符串。目前 TSIG 认证支持的算法是 `hmac-md5`。`secret_string` 是算法使用的密钥，被视为一个 base64 编码字符串。

### 6.2.9. `logging` 语句的语法

```
logging {

  channel channel_name {

    file path name

    [ versions ( number | unlimited ) ]

    [ size size spec ]

    syslog syslog_facility

    stderr

    null);

    [ severity (critical | error | warning | notice | 

      info | debug [ level ] | dynamic ); ]

    [ print-category yes or no; ]

    [ print-severity yes or no; ]

    [ print-time yes or no; ]

  }

  [ category category_name {

    channel_name ; [ ... ]

  };

}
```

### 6.2.10. `logging` 语句的定义与用法

`logging` 语句为命名服务器配置多种日志选项。其 `channel`（通道）部分将输出方法、格式选项和级别与一个名称关联，然后可以配合 `category`（类别）部分来选择如何记录不同类的消息。

仅使用 `logging` 语句即可定义任意数量通道和类别。如果没有 `logging` 语句，日志配置将如下：

```
logging {

  category "unmatched" { "null"; };

  category "default" { "default_syslog"; "default_debug"; };

}
```

在 `BIND 9` 中，日志配置只有在整个配置文件解析完成后才会建立。在 `BIND 8` 中，一旦解析到 `logging` 语句就会建立。当服务器启动时，所有关于配置文件语法错误的日志消息都将进入默认通道，或者如果指定了 `-g` 选项，则进入标准错误（`stderr`）。

#### 6.2.10.1. `channel` 子句

所有日志输出都指向一个或多个通道；你可以根据需要创建任意多个通道。

每个通道定义必须包含一个目标子句（destination clause），说明为该通道选择的消息发送到文件、特定的 `syslog` 设施、标准错误还是被丢弃。你可以可选地限制通道接受的严重性级别（默认为 `info`），以及是否包含命名的时间戳、类别名称和/或严重性级别（默认是不包含任何内容）。

`null` 目标子句会导致发送到该通道的所有消息被丢弃；在这种情况下，该通道的其他选项将毫无意义。

`file` 目标子句将通道重定向到磁盘文件。它可以限制文件允许增长的大小，以及每次打开文件时将保存多少版本的备份。

如果你使用了 `versions` `log` `file` 选项，`named` 将在打开文件时通过重命名来保留相应数量的备份版本。例如，如果你选择保留 3 个旧版本的 `lamers.log`，那么 `lamers.log.1` 将重命名为 `lamers.log.2`，`lamers.log.0` 重命名为 `lamers.log.1`，而 `lamers.log` 重命名为 `lamers.log.0`。你可以指定 `unlimited` 来限制版本数量。如果日志文件关联了 `size` 选项，则只有当打开的文件超过指定大小时才会进行重命名。默认不保留备份版本；任何现有的日志文件仅会被追加。

如果文件没有 `versions` 选项，则除非某些带外机制移除或截断日志使其小于最大大小，否则不会有更多数据写入日志。默认行为是不限制文件大小。

文件的 `size` 选项用于限制日志增长。如果文件超过了该大小，除非关联了 `versions` 选项，否则 `named` 将停止写入该文件。如果保留了备份版本，文件将如上述描述那样进行滚动并开始一个新文件。

`size` 和 `versions` 选项的示例用法：

```
channel "an_example_channel" {

    file "example.log" versions 3 20m;

    print-time yes;

    print-category yes;

}
```

`syslog` 子句将通道重定向到系统日志。其参数是 `syslog` 页面中描述的 `syslog` 设施。`syslog` 如何处理发送给它的消息见 `syslog.conf` 页面。如果你的系统使用的旧版本 `syslog` 导致 `open()` 仅接受两个参数，则此子句将被静默忽略。

`severity` 子句的作用类似于 `syslog` 的“优先级（priorities）”，只不过当你直接写入文件而不是使用 `syslog` 时，也可以使用它们。不符合给定严重性级别的消息将不会被通道选择；较高严重性级别的消息将被接受。

如果你正在使用 `syslog`，则 `syslog.conf` 中的优先级将透传。例如，将通道和级别定义为 `daemon` 和 `debug` 且仅通过 `syslog` 记录 `daemon` 消息，会导致 `info` 和 `notice` 消息被丢弃。如果情况反过来，即 `named` 消息仅为 `warning` 或更高级别，则 `syslog` 将打印所有消息。

`stderr` 子句将通道重定向到标准错误。这在服务器作为前台进程运行时调试配置时非常有用。当全局调试级别大于 0 时，服务器处于调试模式并提供详细的调试信息。提供特定严重性许多别的通道，例如：

```
channel "specific_level" {

    file "foo";

    severity debug 3;

}
```

将在调试模式下获得级别 3 或以下的调试输出，无论全局调试级别如何。`dynamic` 严重性的通道使用全局调试级别来确定打印哪些消息。

如果开启了 `print-time`，将记录日期时间。对于 `syslog` 通道可以指定 `print-time`，但这没有意义，因为 `syslog` 也会打印日期时间。如果请求了 `print-category`，将记录消息的类别。如果开启了 `print-severity`，将记录消息的严重性级别。`print-` 选项可以任意组合，并将始终按以下顺序打印：时间、类别、严重性。这里是开启所有三个 `print` 选项的示例：

```
28-Feb-2000 15:05:32.863 general: notice: running
```

定义了四个用于 `named` 默认日志的通道如下。其细节见 6.2.10.2 节。

```
channel "default_syslog" {

    syslog daemon;\                   发送到 syslog 的 daemon 设施

    severity info;\                 // 仅发送 info 及其更高优先级信息

}
```

```
channel "default_debug" {

    file "named.run";            // 写入工作目录下的 named.run

                                // 注意：如果启动服务器时带有 '-d' 选项

                                // 则使用 stderr 代替 "named.run"

    severity dynamic;\            // 当前调试级别

}
```

```
channel "default_stderr" {

    stderr;                        // 写入 stderr

    severity info;\                 // 仅发送 info 及其更高优先级信息

}
```

```
channel "null" {

    null;                          // 丢弃发送到此通道的所有内容

}
```

`default_debug` 具有特殊属性，当服务器调试级别不为零时它会产生输出。它通常写入名为 `named.run` 的文件。

# 第 6 章 `BIND 9` 配置参考

出于安全考虑，当使用 `"-u"` 命令行选项时，`named.run` 文件的只有在 `named` 切换到新 `UID` 后才会创建，以及 `named` 启动且仍以 `root` 身份运行时生成的任何调试输出。如果你需要捕获这些输出，必须使用 `"-g"` 选项运行服务器并将标准错误重定向到文件。

一旦定义了通道（`channel`），就无法重新定义。因此，你可以直接更改内置通道，但可以通过将通道指向你定义的通道来修改默认日志。

### 6.2.10.2. 类别短语 (Phrase)

有很多类别，因此你可以将日志发送到任何地方，而不会看到你不想要的日志。如果你没有为某个类别指定通道列表，则该类的日志消息将被发送到默认类别。如果你没有指定默认类别，将使用以下“`default`”：

```
category "default" { "default_syslog"; "default_debug"; };
```

例如，如果你想将安全事件记录到文件中，但同时也保留默认行为。你可以指定以下内容：

```
channel "my_security_channel" {

    file "my_security_file";

    severity info;

}

category "security" {

    my_security_channel;

    default_syslog;

    default_debug;

}
```

要丢弃类别中的所有消息，请指定空通道（`null`）：

```
category "xfer-out" { "null"; }

category "notify" { "null"; };
```



以下是可用的类别及其包含的日志信息类型简述。未来的 BIND 版本可能会添加更多类别。

| category | 描述 |
| :--- | :--- |
| `default` | 默认类别定义了那些未定义特定配置的类别的日志选项。 |
| `general` | 通用类别。许多事务仍未归类到特定类别中，它们都会汇到这里。 |
| `database` | 与名称服务器内部用于存储和缓存数据的数据库相关的消息。 |
| `security` | 请求的允许与拒绝。 |
| `config` | 配置文件的解析和处理。 |
| `resolver` | DNS 解析，例如缓存名称服务器代表客户端执行的递归查询。 |
| `xfer-in` | 服务器接收的区域传输（Zone transfers）。 |
| `xfer-out` | 服务器正在发送的区域传输。 |
| `notify` | `NOTIFY` 协议。 |
| `client` | 客户端请求的处理。 |
| `unmatched` | `named` 无法确定其类别或没有匹配视图（`view`）的消息。`client` 类别也会记录一条单行摘要。此类别最好发送到文件或 `stderr`，默认情况下它被发送到空通道。 |
| `network` | 网络操作。 |
| `update` | 动态更新。 |
| `queries` | 查询。使用 `queries` 类别将启用查询日志。 |
| `dispatch` | 将传入的数据包分发到待处理的服务器模块。 |
| `dnssec` | `DNSSEC` 和 `TSIG` 协议处理。 |
| `lame-servers` | 故障服务器（Lame servers）。这些是远程服务器配置错误，`BIND 9` 在解析过程中尝试查询这些服务器时发现。 |

### 6.2.11. lwres 语句语法

这是 `named.conf` 文件中 `lwres` 语句的语法：

```
lwres {

[ listen-on { ip_addr [port ip_port]; [ ip_addr [port ip_port]; ... ] }; ]; ];

[ view_name; ];

[ search domain_name; [ domain_name; ... ] }; ]; ]; [];

[ ndots number; ];

}
```

### 6.12.2 lwres 语句定义与用法

`lwres` 配置名称服务器同时也作为一个轻量级解析服务器运行，请见第 5.2 节。可能存在多个 `lwres` 语句用于配置具有不同属性的轻量级解析服务器。
`listen-on` 语句指定了该轻量级守护进程实例可以接受请求的地址列表（和端口）。如果没有指定端口，则使用端口 `921`。如果省略了此语句，请求将在 `127.0.0.1` 端口 `921` 上被接受。
`view` 语句将此轻量级解析器守护进程实例绑定到 DNS 命名空间中的一个视图中，其响应的构建方式将与匹配此视图的普通 DNS 查询相同。如果省略了此语句，将使用默认视图；如果没有默认视图，则会触发错误。
`search` 语句等同于 `/etc/resolv.conf` 中的 `search` 语句。它提供了一个域名列表，这些域名会被附加到查询中的相对名称之后。
`ndots` 语句等同于 `/etc/resolv.conf` 中的 `ndots` 语句。它指示了相对域名名中在附加路径元素之前，应导致精确匹配查找的最少点（dots）数。

### 6.12.3. options 语句语法

这是 `named.conf` 文件中 `options` 语句的语法：

```
options {

[ version version_string; ];

[ directory path_name; ];

[ named-xfer path_name; ];

[ tkey-domain domainname; ];

[ tkey-dhkey key_name key_tag; ];

[ dump-file path_name; ];

[ memstatistics-file path_name; ];

[ pid-file path_name; ]

[ statistics-file path_name; ];

[ zone-statistics yes_or_no; ];

[ auth-nxdomain yes_or_no; ];

[ deallocate-on-exit yes_or_no; ]

[ dialup_option; ]

[ fake-query

[ fake-query yes_or_no; ]

[ has-old-clients yes_or_no; ]

[ host-statistics yes_or_no; ]

[ minimal-responses yes_or_no; ]

[ multiple-cnames yes_or_no; ]

[ notify yes_or_no; ]

[ recursion yes_or_no; ]

[ rfc2308-type yes_or_no; ]

[ use-id-pool yes_or_no; ]

[ maintain-ixfr-base yes_or_no; ]

[ forward ( | first ) ];

[ - ];

warders { [ addr [port]; [ addr [port]; ... ] ; } ];

[ allow-query-

; ]

[ also-notify { ip_addr {ip_port} ; [ ip_addr {ip_port}; ... ] ; } ]

[ max-ifxr-log-size number; ]

[ coresize size_spec ; ]

[ datasize size_spec ; ]

[ files size_spec ; ]

[ stacksize size_spec ; ]

[ cleaning-interval number; ]

[ heartbeat-interval number; ]

[ interface-interval number; ]

[ statistics-interval number; ]

[ topology { address_matchlist }; ]

[ sortlist { address_matchlist }; ]

[ rrset-order { order_spec ; [ order_spec ; ...]; } ]

[ max-ttl number; ]

[ max-cache-ttl number; ]

[ sig-validity-interval number ; ]

[ min-roots number; ]

[ use-ifxr yes_or_no; ]

[ provide-ifxr yes_or_no; ]

[ request-ifxr yes_or_no; ]

[ treat-cr-space yes_or_no; ]

[ min-refresh-time number ; ]

[ max-refresh-time number; ]

[ min-retry-time number ; ]

[ max-retry-time number; ]

[ port ip_port; ]

[ additional-from-auth yes_or_no ; ]

[ additional-from-cache yes_or_no ; ]

[ random-device path_name ; ]

[ max-cache-size size_spec ; ]

[ match-mapped-addresses yes_or_no; ]

;
}
```



# 第 6 章 BIND 9 配置参考

### version
服务器通过查询 CHAOS 类中的 `name version.bind` 报告的版本。默认值是此服务器的实际版本号。

### directory
服务器的工作目录。配置文件中的任何非绝对路径名将被视为相对于此目录的相对路径。大多数服务器输出文件（例如 `named.run`）的默认位置是此目录。如果未指定目录，工作目录默认为 `.`，即启动服务器时所在的目录。指定的目录应该是绝对路径。

### named-xfer
此选项已废弃。在 BIND 8 中，它被用于指定 `named-xfer` 程序的路径。在 BIND 9 中，不再需要独立的 `named-xfer` 程序；其功能已内置在名称服务器中。

### tkey-domain
附加到使用 TKEY 生成的所有共享密钥名称后的域名。当客户端请求 TKEY 交换时，它可能也可能不指定密钥所需的名称。如果存在，共享密钥的名称将为“客户端部分+tkey-domain”。否则，共享密钥的名称将为“随机十六进制数字+tkey-domain”。在大多数情况下，该域名应该是服务器的域名。

### tkey-dhkey
服务器使用 TKEY 的 Diffie-Hellman 模式与客户端生成共享密钥所需的 Diffie-Hellman 密钥。服务器必须能够从工作目录加载公私密钥文件。在大多数情况下，密钥名称应该是服务器的主机名。

### dump-file
当通过 `rndcdumpdb` 指令时，服务器将数据库导出的文件路径。如果未指定，默认值为 `named_dump.db`。

### statistics-file
服务器退出时写入内存使用统计信息的文件路径。如果未指定，默认值为 `named.memstats`。

> Note：在 BIND 9 中尚未实现。

### pid-file
服务器写入其进程 ID（PID）的文件路径。如果未指定，默认值为 `/var/run/named.pid`。该 pid 文件用于那些想要向运行中的名称服务器发送信号的程序。

### statistics-file
当通过 `rndc stats` 指令时，服务器追加统计信息的文件路径。如果未指定，默认为服务器当前目录下的 `named.stats`。文件格式见第 6.2.14.15 节描述。

### port
服务器用于接收和发送 DNS 协议流量的 UDP/TCP 端口号。默认值为 53。此选项主要用于服务器测试：使用非 53 端口的服务器将无法与全局 DNS 通信。

### random-device
服务器使用的熵源。熵主要用于 DNSSEC 操作，例如 TKEY 事务和签名区域的动态更新。此选项指定了读取熵的设备（或文件）。如果这是一个文件，当文件内容耗尽时，需要熵的操作将失败。如果未指定，在存在时则默认值为 `/dev/random`（或等效设备），若不存在则为无。`random-device` 选项在启动时的初始配置加载期间生效，并在随后的重载中被忽略。

## 6.2.14.1. 布尔型选项

### auth-nxdomain
如果为 `yes`，则在 NXDOMAIN 响应上始终设置 AA 位，即使服务器实际上并不具有权威性。默认值为 `no`；这是与 BIND 8 相比的更改。如果你正在使用非常旧的 DNS 软件，可能需要将其设置为 `yes`。

### deallocate-on-exit
此选项在 BIND 8 中用于启用退出时检查内存泄漏。BIND 9 忽略此选项并始终执行检查。

### dialup
如果为 `yes`，服务器将所有区域处理为正在通过按需拨号的跨拨号链路进行区域传输，该拨号链路由源自此服务器的流量建立。这会根据区域类型产生不同的影响，并集中区域维护工作，使其在短时间间隔内发生（每隔心跳间隔发生一次，并希望在单次通话中完成）。它还会抑制一些正常的区域维护流量。默认值为 `no`。

`dialup` 选项也可以在 `view` 和 `zone` 语句中指定，在这种情况下它将覆盖全局 `dialup` 选项。

如果该区域是主区域，服务器将向所有从机发送 `NOTIFY` 请求。这将触发从机中的区域序列号检查（如果从机支持 NOTIFY），允许从机在连接激活状态时验证区域。

如果该区域是从区域或存根区域（stub zone），则服务器将抑制常规“区域已更新”（刷新）查询，仅在心跳间隔过期时执行这些查询，并添加 NOTIFY 请求。

可以使用 `notify` 实现更精细的控制，它只发送 NOTIFY 消息；`notify-passive` 发送 NOTIFY 消息并抑制正常的刷新查询；`refresh` 在心跳间隔过期时抑制正常的刷新处理和刷新查询；`passive` 则仅禁用正常的刷新处理。

### fake-iquery
在 BIND 8 中，此选项用于启用模拟已弃用的 DNS 查询类型 `INQUERY`。BIND 9 绝不进行 `INQUERY` 模拟。

### fetch-glue
此选项已废弃。在 BIND 8 中，`fetch-glue yes` 会导致服务器在构建响应的附加数据部分时，尝试获取它不拥有的资源记录。这现在被认为是一个坏主意，且 BIND 9 绝不这样做。

### has-old-clients
此选项在 BIND 8 中的实现有误，被 BIND 9 忽略。要实现 `has-old-clients yes` 的预期效果，请改用两个独立的选项 `options-xdomain yes` 和 `rfc2308-type no`。

### host-statistics
在 BIND 8 中，此选项启用对与名称服务器交互的每个主机的统计。在 BIND 9 中未实现。

### maintain-ixfr-base
此选项已废弃。它在 BIND 8 中被用于确定是否为增量区域传输（IXFR）保留事务日志。BIND 9 尽可能地维护事务日志。如果你需要禁用传出的区域传输，请使用 `provide-ixfr no`。

### minimal-responses
如果为 `yes`，则在生成响应时，服务器仅在需要时（例如授权、否定应答）向权威部分和附加数据部分添加记录。这可能会提高服务器的性能。默认值为 `no`。

### multiple-cnames
此选项在 BIND 8 中用于允许一个域名违反 DNS 标准允许存在多个 CNAME 记录。BIND 9.2 在主文件和动态更新中严格执行 CNAME 规则。

### notify
如果为 `yes`，则当服务器具有权威性的区域发生变化时，会发送 DNS NOTIFY 消息，详见第 3.3 节。消息将发送到该区域 NS 记录中列出的服务器（除 SOA NAME 字段中标识的主服务器外），以及发送到 `also-notify` 选项中列出的任何服务器。

如果明确，通知仅发送到使用 `also-notify` 显式列出的服务器。如果为 `no`，则不发送通知。

`notify` 选项也可以在 `zone` 语句中指定，在这种情况下它将覆盖 `options notify` 语句。只有当该选项导致从机崩溃时，才有必要关闭它。

### recursion
如果为 `yes`，且 DNS 查询请求递归，则服务器将尝试完成回答查询所需的所有工作。如果关闭了递归且服务器不知道答案，它将返回引用响应（referral）。默认值为 `yes`。请注意，设置 `recursion no` 并不会阻止客户端从服务器缓存中获取数据；它只是防止新数据作为客户端查询的结果而被缓存。缓存仍可能作为服务器内部操作（例如 NOTIFY 地址查找）的结果而发生。另，请参阅上文的 `fetch-glue`。

### rfc2308-type1
将此设置为 `yes` 将导致服务器在否定应答时同 SOA 记录一起发送 NS 记录。默认值为 `no`。

> Note：在 BIND 9 中尚未实现。

### use-id-pool
此选项已废弃。BIND 9 始终从池中分配查询 ID。

### zone-statistics
如果设置为 `yes`，服务器将默认收集服务器上所有区域的统计数据。可以使用 `rndc stats` 访问这些统计数据，它将将其转储到 `statistics-file` 列出的文件中。请参见第 6.2.14、15 节。

### use-ixfr
此选项已废弃。如果您需要禁用到特定服务器或服务器的 IXFR，请查看第 6.2.16 节中 `provide-ixfr` 选项的信息。参见第 4.2 节。

### provide-ixfr
参见第 6.2.16 节中 `provide-ixfr` 的描述

### request-ixfr
参见第 6.2.16 节中 `request-ixfr` 的描述

### treat-cr-as-space
此选项用于 BIND 8，用于让服务器将回车符（"r"）视为与空格或制表符相同，以便加载在 NT 或 DOS 机器上生成的 UNIX 系统区域文件。在 BIND 9 中，UNIX 的"\n"和 NT/DOS 的"\r\n"换行符均接受，该选项被忽略。

### additional-from-cache
这些选项控制权威服务器在回答具有额外数据的查询，或遵循 CNAME 和 DDNAME 链时的行为。

当这两个选项都设置为 `yes`（默认值）且查询是从权威数据回答的（配置了服务器）时，响应的额外数据部分将从缓存中填充。在某些情况下，这是不可取的，例如对缓存的正确性的担忧，或者在从区域被第三方修改的服务器中。避免搜索这些额外数据将加快服务器操作，但可能会导致额外的权威查询。例如，如果查询请求 `foo.example.com` 的 MX 记录，并且发现了记录“MX 10 mail.example.net”，通常 `mail.example.net` 的地址记录（A 和 AAAA）也将提供，如果已知的话。将这些选项设置为 no。这些选项用于权威仅服务器或权威仅视图。在不指定递归 no 的情况下，这会导致服务器忽略这些选项并记录警告消息。

指定 additional-from-cache 实际上不仅禁用了查找数据时的缓存，还用于查找答案。这通常是存在缓存数据正确性问题的权威仅服务器的期望行为。

当服务器被递归查询一个不是权威顶点的名称时，由于额外数据来自缓存，服务器通常会带有根服务器或某些父节点的引用。如果指定了 additional-from-cache，服务器将无法提供引用，而是将用 REFUSED 回答查询。除非解析过程不需要引用，否则这不会引起任何问题。

### match-mapped-addresses
如果设置为 yes，则 IPv4 映射地址将匹配任何地址列表。启用此选项对于启用了 IPv6 的系统很有用，可以解决映射地址导致 TCP 连接被始终接受的内核缺陷。出于其他目的使用此选项是不被建议的。

### 6.2.14.2. Forwarding
转发设施可用于在服务器上创建站点范围缓存，减少到外部名称服务器的流量。它也可以用于无法访问 Internet 但希望查询外部的服务器。转发发生在服务器不是权威且缓存中没有答案的查询上。

### forward
此选项仅在 forwarders 列表不空时有意义。值为 `first`（默认值）会导致服务器首先查询转发器，如果转发器没有回答，服务器将自行查找答案。如果指定 `only`，服务器将仅查询转发器。

### forwarders
指定用于转发的 IP 地址。默认是空列表（不转发）。

转发也可以按域名配置，允许特定域名使用不同的转发器，或具有不同的 `forward only/first` 行为，或完全不转发，参见第 6.2.21 节。

### 6.2.14.3. Access Control
根据请求系统的 IP 地址限制对服务器的访问。参见第 6.1.1 节关于如何指定 IP 地址列表的细节。

#### allow-notify
除了区域主节点外，`zone` 语句中也可以指定 `allow-notify`，在这种情况下它会覆盖 `options allow-notify` 语句。它仅对于从区域有意义。如果没有指定，默认是仅来自从主的消息。

#### allow-query
指定哪些主机允许提问普通问题。`zone` 语句中也可以指定 `allow-query`，在这种情况下它会覆盖 `options allow-query` 语句。如果没有指定，默认是允许所有主机的查询。

#### allow-recursion
指定哪些主机允许通过此服务器进行递归查询。如果没有指定，默认是允许所有主机的递归查询。注意，禁止某个主机的递归查询并阻止该主机检索服务器缓存中的数据。

#### allow-v6-synthesis
指定哪些主机接收第 6.2.14.13 节所述的 IPv6 查询合成响应。

#### allow-transfer
指定哪些主机允许从服务器接收区域传输。`zone` 语句中也可以指定 `allow-transfer`，在这种情况下它会覆盖 `options allow-transfer` 语句。如果没有指定，默认是允许向所有主机传输。

#### blackhole
指定服务器不会接受用于查询的地址列表。来自这些地址的查询将不会响应。默认是 `none`。

### 6.2.14.4. Interfaces
可以使用 `listen-on` 选项指定服务器回答的接口和端口。`listen-on` 接受一个可选端口和一个 *address_match_list*。服务器将在匹配列表允许的所有接口上监听。如果没有指定端口，将使用端口 53。

允许使用多个 `listen-on` 语句。例如：

```
listen-on { 5.6.7.8; }

listen-on port 1234 { !1.2.3.4; 1.2/16 };
```

将为 IP 地址 5.6.7.8 开启端口 53 名称服务器，为机器上不是 1.2.3.4 的地址开启端口 1234 名称服务器。

如果没有 `no listen-on-v6`，服务器将在所有接口上监听端口 53。

`listen-on-v6` 选项用于指定服务器监听使用 IPv6 传入查询的端口。服务器不会像 IPv4 那样为每个 IPv6 接口地址绑定单独的套字。相反，它在 IPv6 通配符地址上监听。因此，`listen-on-v6` 参数允许的值只有

```
{ any; }
```

和

```
{ none; }
```

可以使用多个 `listen-on-v6` 来监听多个端口：

```
listen-on-v6 port 53 { any; }

listen-on-v6 port 1234 { any; };
```

要让服务器不监听任何 IPv6 地址，请使用

```
listen-on-v6 { none; };
```

如果没有指定 `listen-on-v6` 语句，服务器将不监听任何 IPv6 地址。

### 6.2.14.5. Query Address
如果服务器不知道问题的答案，它将查询其他名称服务器。`query-source` 指定了用于此类查询的地址和端口。对于通过 IPv6 发送的查询，有一个单独

`query-source-v6` 选项。如果地址为 * 或省略，则将使用通配符 IP 地址 (INADDR_ANY)。如果端口为 * 或省略，则将使用随机的未特权端口。默认值为：

```
query-source address * port *
query-source-v6 address * port *
```



注意：`query-source` 选项中指定的地址同时用于 UDP 和 TCP 查询，但端口仅适用于 UDP 查询。TCP 查询始终使用随机的未特权端口。

### 6.2.14.6. 区域传输 (Zone Transfers)

`BIND` 拥有相应的机制来促进区域传输，并对传输给系统造成的负载进行限制。以下选项适用于区域传输。

#### also-notify

定义一个名称服务器的 IP 地址列表，每当加载新的区域副本时，除了区域 NS 记录中列出的服务器外，还会向这些服务器发送 NOTIFY 消息。这有助于确保区域副本快速在隐藏服务器上收敛。如果在区域语句（`zone` statement）中提供了 `also-notify` 列表，它将覆盖 `options-also-notify` 语句。当区域语句被设置为 `no` 时，全局 `also-notify` 列表中的 IP 地址将不会为该区域发送 NOTIFY 消息。默认为空列表（无全局通知列表）。

#### max-transfer-time-in

运行时间超过此分钟数的入站区域传输将被终止。默认值为 120 分钟（2 小时）。

#### max-transfer-idle-in

在这些分钟内没有进展的入站区域传输将被终止。默认值为 60 分钟（1 小时）。

#### max-transfer-time-out

运行时间超过此分钟数的出站区域传输将被终止。默认值为 120 分钟（2 小时）。

#### max-transfer-idle-out

在这些分钟内没有进展的出站区域传输将被终止。默认值为 60 分钟（1 小时）。

#### serial-query-rate

从服务器会定期查询主服务器，以查找区域序列号是否发生变化。每次此类查询都会使用少量的从服务器网络带宽。为了限制使用的带宽量，`BIND` 9 限制了发送查询的速率。`serial-query-rate` 选项的值是一个整数，表示每秒发送查询的最大数量。默认值为 20。

#### serial-queries

在 `BIND` 8 中，`serial-queries` 选项设置了任何时刻允许处理的并发序列号查询的最大数量。`BIND` 9 不限制未处理查询的数量，并忽略 `serial-queries` 选项。相反，它通过定义 `serial-query-rate` 选项来限制发送查询的速率。

#### transfer-format

区域传输可以使用两种格式发送：单回答（`one-answer`）和多回答（`many-answers`）。`transfer-format` 选项用于主服务器以定义其发送的格式。`one-answer` 为每个传输的资源记录使用一个 DNS 消息。`many-answers` 将尽可能多的资源记录打包进一个消息中。`many-answers` 效率更高，但仅由较新的从服务器支持，例如 `BIND` 9、8.x 以及打过补丁的 `BIND` 4.9.5。默认值为 `many-answers`。可以通过 `server` 语句按服务器为基来覆盖 `transfer-format`。

#### transfers-in

可以并发运行的入站区域传输的最大数量。默认值为 10。增加 `transfers-in` 可能会加快从区域的收敛，但可能会增加本地系统的负载。

#### transfers-out

可以并发运行的出站区域传输的最大数量。超过限制的区域传输请求将被拒绝。默认值为 10。

#### transfers-per-ns

从给定的远程名称服务器并发传输的入站区域传输的最大数量。默认值为 2。增加 `transfers-per-ns` 可能会加快从区域的收敛，但可能会增加远程名称服务器的负载。可以通过 `server` 语句中的 `transfers` 短语按服务器为基来覆盖 `transfers-per-ns`。

## 第 6 章，BIND 9 配置参考

#### transfer-source

`transfer-source` 决定了将使用哪个本地地址绑定到用于获取入站传输区域的 IPv4 TCP 连接。它还决定了用于刷新查询和转发动态更新的源 IPv4 地址以及可选的 UDP 端口。如果未设置，它默认为系统控制的值，该值通常是“最接近”远程端的接口地址。如果为被传输的区域指定了 `allow-transfer` 选项，则该地址必须出现在远程端的选项中。此语句设置了所有区域的 `transfer-source`，但可以通过在配置文件的 `view` 或 `zone` 块中包含 `transfer-source` 语句，按视图 或区域为基来覆盖。

#### transfer-source-v6

与 `transfer-source` 相同，只是区域传输是使用 IPv6 执行的。

#### notify-source

`notify-source` 决定了使用哪个本地地址以及可选的 UDP 端口来发送 NOTIFY 消息。该地址必须出现在从服务器的 `masters` zone 子句或 `allow-notify` 子句中。此语句设置了所有区域的 `notify-source`，但可以通过在配置文件的 `zone` 或 `view` 块中包含 `notify-source` 语句，按区域 / 视图为基来覆盖。

#### notify-source-v6

与 `notify-source` 类似，但适用于发送到 IPv6 地址的 notify 消息。

## 6.2.14.7 操作系统资源限制

可以限制服务器对许多系统资源的使用。在指定资源限制时允许使用比例值。可以使用 `107374184` 代替 `unlimited` 来指定 GB 的限制。或者最大可用数量。默认使用服务器启动时的限制。详见描述。以下选项为名称服务器进程设置系统资源限制。某些操作系统不支持部分或任何限制。如果使用了不支持的限制，系统将发出警告。

#### coresize

核心转储的最大大小。默认值为 `default`。

#### datasize

服务器可能使用的数据内存量。默认值为 `default`。这是内存使用的硬限制。如果服务器尝试分配超过此限制的内存，分配将失败，这可能导致服务器无法执行 DNS 服务。因此，此选项对于限制服务器使用的内存非常有用，但默认值太小。如果想限制服务器使用的内存，请使用 `max-cache-size` 和 `recursive-clients` 选项。

#### files

服务器并发打开的文件的最大数量。默认值为 `unlimited`。

#### stacksize

服务器可能使用的栈内存量。默认值为 `default`。

## 6.2.14.8 服务器资源限制

以下选项通过服务器内部执行资源消耗限制，而不是通过操作系统。

#### max-ifr-log-size

此选项已过时；为了兼容 `BIND` 8，会被接受但忽略。

#### recursive-clients

服务器代表客户端执行的并发递归查询的最大数量。默认值为 1000。由于每个递归客户端使用相当多的内存（大约 20 千字节），在内存有限的主机上可以减少 `recursive-clients` 选项的值。

#### tcp-clients

服务器接受的并发 TCP 连接的最大数量。默认值为 100。

#### max-cache-size

用于服务器缓存的最大内存，单位为字节。当缓存中的数据量达到此限制时，服务器将使记录提前过期以防止超过限制。在具有多个视图的服务器中，该限制独立适用于每个视图的缓存。

默认值为无限制，这意味着只有当记录的 TTL 过期时，才会从缓存中清除。

## 6.2.14.9. 定期任务间隔

#### cleaning-interval

服务器每隔 `cleaning-interval` 分钟将从缓存中移除过期的资源记录。默认为 60 分钟。如果设置为 0，则不会进行定期清理。

#### heartbeat-interval

当此间隔过期时，服务器将对所有标记为拨号（`dialup`）的区域执行区域维护任务。默认为 60 分钟。合理值为 1 天（1440 分钟）。如果设置为 0，则不会对这些区域进行区域维护。

#### interface-interval

服务器每隔 `interface-interval` 分钟扫描一次网络接口列表。默认为 60 分钟。如果设置为 0，则仅在加载配置文件时进行扫描。扫描后，将在任何新接口上启动监听器（前提是它们被允许 `listen-on` 配置）。已消失的接口上的监听器将被清理。

#### statistics-interval

每隔 `statistics-interval` 分钟记录一次命名服务器统计信息。默认值为 60。如果设置为 0，则不记录任何统计信息。

> 注意：在 `BIND` 9 中尚未实现。

### 6.2.14.10. 拓扑

在其他条件相同的情况下，当服务器从命名服务器列表中选择一个命名服务器进行查询时，它倾向于选择在拓扑上距离自己最近的一个。`topology` 语句接受 `address_match_list` 并以特殊方式解释它。每个顶层元素被分配一个距离。非否定元素根据其在列表中的位置获得距离，匹配项越接近列表开头，它与服务器之间的距离就越短。取反匹配将被分配距离服务器的最大距离。如果没有匹配，该地址将获得一个比列表中任何非否定元素都远、但比任何取反元素都近的距离。例如，

```
topology {
  10/8;
  !1.2.3/24;
  { 1.2/16; 3/8; }
}
```
将最优先选择网络 10 服务器，其次是网络 1.2.0.0（子网掩码 255.255.0.0）和网络 3 上的主机，网络 1.2.3（子网掩码 255.255.255.0）上的主机优先级最低。

默认拓扑为

```
topology ( localhost; localnets; );
```

> 注意：`BIND` 9 中未实现 `topology` 选项。

### 6.2.14.11. sortlist 语句

对 DNS 查询的响应可能由多个资源记录（RR）组成，形成一个资源记录集（RRset）。服务器通常以不确定的顺序返回 RRset（但请参阅第 6.2.14.12 节中的 `rrset-order` 语句）。客户端解析器代码应根据情况重新排列 RRs，即优先使用本地网络上的任何地址而非其他地址。然而，并非所有的解析器都这样做，或者其配置不正确。当客户端使用本地服务器时，排序在服务器端根据客户端的地址进行。这只需要配置命名服务器，而不需要配置所有客户端。

`sortlist`（见下文）接受一个 `address_match_list`，并在 `topology` 语句（第 6.2.14.10 节）上对其特定解释。`sortlist` 中的每个顶层语句必须是一个具有一个或两个元素的显式 `address_match_list`。顶层列表的第一个元素（可能是 IP 地址、IP 前缀、ACL 名称或嵌套的 `address_match_list`）将与查询源地址进行检查，直到找到匹配项。

一旦匹配了查询源地址，如果顶层语句仅包含一个元素，则使用匹配源地址的实际原始元素来选择响应中的地址，并移动到响应的开头。如果语句是两个元素的列表，则第二个元素被处理为与 `topology` 语句中的 `address_match_list` 相同。每个顶层元素被分配一个距离，响应中距离最小的地址将被移动到响应的开头。

## 第 6 章 BIND 9 配置参考

在以下示例中，来自来自主机本身任何地址的任何查询将获得优先选择任何本地连接网络上地址的响应。其次优选的是 `192.168.1/24` 网络上的地址，之后是 `192.168.2/24` 或 `192.168.3/24` 网络，这两个网络之间没有显示优劣之。来自 `192.168.1/24` 网络主机的查询将优先选择该网络上的其他地址，而非 `192.168.2/24` 和 `192.168.3/24` 网络。来自 `192.168.4/24` 或 `192.168.5/24` 网络主机的查询将优先选择其直接连接网络上的其他地址。

```
sortlist {
    localhost;
    localnets;
        192.168.1/24;
        { 192.168.2/24; 192.168.3/24; }; // 如果本地主机
    192.168.1/24; // 则首先在
    { 192.168.2/24; 192.168.3/24; }; // 后续网络
    192.168.2/24;
    { 192.168.1/24; 192.168.3/24; }; // 如果在 C 类
    192.168.2/24; // 则使用 .1, .2 或 .
    { 192.168.1/24; 192.168.3/24; }; // 则使用 .2, .3
    192.168.3/24;
    { 192.168.4/24; 192.168.5/24; }; // 如果在 C 类
    f-fer that net
    ; // 如果 .4 或 .5, pre-
};
```
以下示例将为本地主机和直接连接网络上的主机提供合理的行为。这与 `BIND` 4.9 中的地址排序行为相似。发送给本地主机查询的响应将有利于任何直接连接的网络。发送给直接连接网络上其他主机查询的响应将优先选择同一网络上的地址。对其他查询的响应将不会排序。

```
sortlist {
    {localhost; localnets};
    {localnets};
};
```

### 6.2.14.12. RRset 排序

当回答中返回多个记录时，配置放置在响应中的记录顺序可能是很有用的。`rrset-order` 语句允许配置记录的顺序。

```
rrset-order [ class ] [ type ] [ domain ] order
```
允许对 RRset 进行排序。`rrset-order` 的定义如下：

| | |
|---|---|
| `fixed` | 响应以固定顺序返回。 |
| `random` | 响应以随机顺序返回。 |
| `cyclic` | 响应以循环顺序返回。 |

例如：

```
rrset-order class IN "example.com" random; cyclic;
```



无论哪种成功，都由 `BIND 9` 随机选择 `rrset-order` 决定。如果出现多个 `rrset-order` 语句，将采用最后一个。

> 注意：在 `BIND 9` 中实现 `rrset-order` 语句。`BIND` 随机选择选择一个，，，绕绕 `RRset` 结尾。

### 2.14.13. 合成 IPv6 响应

许多解析器支持使用 `RFC1886` 的 `AAAA` 记录进行 `IPv6` 查询，并在 `ip6.int` 域中使用二进制标签进行反向查询，但 `BIND 9` 不支持 `RFC2874`-style 查询。

对于那些希望继续使用轻量级解析器而不是切换到 `BIND 9` 的用户，`BIND 9` 提供了一种方法，可以将 `RFC1886`-style lookups 转换为 `RFC2874`-style lookups。

此功能默认禁用，可以通过 `all-v6-synthesis { address_match_list }` 子添加到 `options` 或 `view` 语句中启用。启用后，递归 `AAAA` 查询将导致首先尝试 `AAAA` 查询，如果失败，则进行查找。无论哪一个成功，结果都以合成 `AAAA` 记录的形式返回。同样，`ip6.int` 中的递归 `PTR` 查询将导致在 `ip6.arp` 中查找二进制标签，如果失败，则查询 `ip6.int`。结果将以 `ip6.int` 中的合成 `PTR` 记录返回。

合成记录的 `TTL` 为零。目前不支持对合成响应进行 `DNSSEC` 验证；因此，包含合成 `RR` 的响应不会设置 `AD` 标志。

> 注意：`all-v6-synthesis` 仅对提供递归服务的客户端执行。

## 6.24.14. 调优

`lame-ttl`

设置缓存失效服务器指示的秒数。`0` 禁用缓存。（不建议。）默认为 `600`（`10` 分钟）。最大值为 `1800`（`30` 分钟）。

`max-nache-ttl`

为了减少网络流量并提高性能，服务器存储负缓存。`max-nache-ttl` 用于设置这些答案在服务器中的最大保留时间（秒）。默认 `max-nache-ttl` 为 `10800` 秒（`3` 小时）。`max-nache-ttl` 不能超过 `7` 天，如果值更大，将被静默截断为 `7` 天。

`max-cache-ttl`

`max-cache-ttl` 设置服务器缓存普通（积极）答案的最长时间。默认为一周（`7` 天）。

`min-roots`

接受根服务器请求所需的根服务器最小数量。默认为 `2`。

注意：`BIND9` 尚未实现。

### 6.24.15. `sig-validity-interval`

指定由于动态更新（第 4.1 节）自动生成的 `DNSSEC` 签名在未来的过期天数。默认值为 `30` 天。签名的起始时间（inception time）无条件地设置为当前时间的前一小时，以允许有限的时钟偏移。

- `min-refresh-time`
- `max-refresh-time`
- `min-retry-time`

这些选项控制服务器在刷新区域（查询 `SOA` 变化）或重试失败的传输时的行为。通常使用区域的 `SOA` 值，但这些值是由主服务器设置的，服务器管理员对这些内容的控制权很小。

这些选项允许管理员按区域、按视图（`view`）或全局设置最小和最大刷新及重试时间。这些选项适用于从区域（slave zones）和根区域（stub zones），并将 `SOA` 刷新和重试时间限制在指定的值。

### 6.24.16. 统计文件

`BIND 9` 生成的统计文件与 `BIND 8` 生成的相似，但并不相同。

统计转储以 `++ Statistics Dump ++++ (97398949)` 行开始，括号中的数字是 `Unix` 风格的时间戳，以自 `1970` 年 `1` 月 `1` 日起的秒数。该行之后是一系列行，包含计数器类型、计数器值、可选的区域名称以及可选的视图名称。未列出视图和区域的行是整个服务器的全局统计数据。带有区域和视图名称的行对应给定的视图和区域（默认视图省略视图名称）。统计转储以 `— Statistics Dump — (97398949)` 行结束，该数字与起始行的数字相同。

维护了以下统计计数器：

| 计数器 | 说明 |
| :--- | :--- |
| `success` | 向服务器或区域进行的成功查询数。成功查询定义为返回除引导响应（referral response）外的 `NOERROR` 响应的查询。 |
| `referral` | 产生引导响应（referral responses）的查询数。 |
| `nxrset` | 产生无数据 `NOERROR` 响应的查询数。 |
| `nxdomain` | 产生 `NXDOMAIN` 响应的查询数。 |
| `recursion` | 导致服务器执行递归以查找最终答案的查询数。 |
| `failure` | 产生除上述之外失败响应的查询数。 |

### 6.24.17. `server` 语句语法

```
server ip_addr {

  [ bogus yes_or_no ; ]

  [ provide-ifxr yes_or_no ; ]

  [ request-ifxr yes_or_no ; ]

  [ edns yes_or_no ; ]

  [ transfers number ; ]

  [ transfer-format ( one-answer | many-answers ) ; ; ]

  [ keys { string ; { string ; {...} } } ; ; ]

}
```

### 6.24.18. `server` 语句定义与用法

`server` 语句定义了与远程名称服务器相关的特征。`server` 语句可以出现在配置文件的顶层，也可以`view`语句内部。如果`view`语句包含一个或多个`server`语句，则只有这些适用于该视图，任何顶层语句将被忽略。如果`view`不包含`server`语句，则任何顶层`server`语句将作为默认值。

如果你发现远程服务器正在提供错误数据，将其标记为 `bogus`（虚假的）将防止对其进行进一步查询。`bogus` 的默认值为 `no`。

`provide-ifxr` 子句决定了作为主服务器的本地服务器在给定的远程服务器（从区域）请求时，是否会通过增量区域传输进行响应。如果设置为 `yes`，只要可能，将提供增量传输。如果设置为 `no`，到远程服务器的所有传输都将是非增量的。如果未设置，则使用视图或全局块中 `provide-ifxr` 选项的值作为默认值。

`request-ifxr` 子句决定了作为从区域的本地服务器是否向给定的远程服务器（主服务器）请求增量区域。如果没有设置，则使用视图或全局块中 `request-ifxr` 选项的值作为默认值。

不支持 `IXFR` 的 `IXFR` 请求会自动回退到 `AXFR`。因此，没有必要手动列出支持 `IXFR` 和不支持 `IXFR` 的服务器；应该始终使用全局默认值 `yes`。`provide-ifxr` 和 `request-ifxr` 子句的目的是即使在主、从区域都声称支持 `IXFR` 的情况下也能禁用 `IXFR`，例如如果其中一个服务器存在 `bug` 或者在使用 `IXFR` 时会损坏数据。默认值为 `yes`。

`edns` 子句决定了本地服务器在与远程服务器通信时是否尝试使用 `EDNS`。服务器支持两种区域传输方法。第一种 `one-answer` 为每个传输的资源使用一个 `DNS` 消息。`many-answers` 效率更高，但只有 `many-answers` 被理解。`BIND 9`、`BIND 8.x` 以及补丁版本支持。你可以为 `server` 指定使用这种方法。如果未指定 `transfer-format`，将使用 `options` 语句指定的 `transfer-format`。

`transfers` 用于限制来自远程服务器的并发区域传输数量。如果没有指定 `transfers`，将根据 `transfers-ns` 限制。

`keys` 子句用于识别由 `key` 语句定义的密钥，用于与服务器通信。`key` 语句必须位于 `server` 语句之前。当发送到远程服务器的请求将使用此处指定的密钥签名。来自远程服务器的请求不需要此密钥签名。

虽然 `keys` 子句允许多个密钥，但每个服务器仅支持单个密钥。

### 6.24.19. `trusted-keys` 语句语法

```
trusted-keys {

  string number number string;

  [ string number number string;]]
}
```

### 6.24.20. `trusted-keys` 语句定义与用法

`trusted-keys` 语句定义了 `DNSSEC` 安全根。`DNSSEC` 见第 4.7 节。当非权威区域的公钥已知但无法通过 `DNS` 安全获取时，定义安全根（它是根区域或其父区域未签名）。一旦密钥被配置为信任密钥，它将被视为已验证并证明是安全的。解析器对安全根下的所有 `DNS` 数据进行 `DNSSEC` 验证。

`trusted-keys` 语句可以包含多个密钥项，每项都包含密钥的域名、标志、协议、算法以及密钥数据的 `base64` 表示法。

### 6.24.21. `view` 语句语法

```
view view_name [class] {

    match-clients { address_match_list };

    match-destinations { address_match_list };

    match-recursive-only { yes_or_no };

    [ view_option, ... ]

    [ zone_statistics yes_or_no ]

    [ zone_statement; ... ]

};
```

### 6.24.22. `view` 语句定义与用法

`view` 语句是 `BIND 9` 的强大功能，允许名称服务器根据提问者回答不同的 `DNS` 查询。它对于拆分 `DNS` 设置而无需运行多个服务器特别有用。每个 `view` 语句定义了一个子集客户端看到的 `DNS` 命名空间视图。如果客户端的源 `IP` 地址匹配视图 `match-clients` 子句的 `address_match_list`，且其目的 `IP` 地址匹配视图 `match-destinations` 子句的 `address_match_list`，则该客户端匹配该视图。如果未指定，`match-clients` 和 `match-destinations` 默认匹配所有地址。`view` 语句的顺序具有重要意义——客户端请求将在其匹配的第一个 `view` 上下文中解析。

# 第 6 章 `BIND 9` 配置参考

在 `view` 语句中定义的区域仅对匹配该视图的客户端可见。通过在多个视图中定义同名称的区域，可以为不同的客户端提供不同的数据，例如拆分 `DNS` 设置中的“内部”客户端和“外部”客户端。

`options` 语句中的许多选项也可以在 `view` 语句中使用，这些选项仅在解析该视图的查询时生效。当没有提供特定视图的值时，将使用 `options` 语句中的值作为默认值。此外，可以在 `view` 语句中指定区域选项（`zone options`）；这些特定的视图默认值优于 `options` 语句中的值。

视图是特定于类的。如果没有指定类，则假设为类 `IN`。请注意，所有非 `IN` 类的视图必须包含一个提示区域（hint zone），因为只有 `IN` 类具有编译进去的默认提示。

如果配置文件中没有 `view` 语句，则会自动创建一个匹配任何客户端的默认视图，在配置文件顶层指定的任何 `zone` 语句都将被视为此默认视图的一部分。如果存在任何显式的 `view` 语句，则所有的 `zone` 语句必须发生在 `view` 语句内部。

以下是一个使用 `view` 语句实现的拆分 `DNS` 设置示例。

```
view "internal" {

    // 这应该匹配我们的内部网络。

    match-clients { 10.0.0.0/8 };

    // 仅为内部客户端提供递归服务。

    recursion yes;

    // 提供 example.com 区域的完整视图

    // 包含内部主机的地址。

    zone "example.com" {

        type master;

        file "example-internal.db";

    }

}

view "external" {

    match-clients { any };

    // 拒绝为外部客户端提供递归服务。

    recursion no;

    // 提供 example.com 区域的限制视图

    // 仅包含公开访问主机。

    zone "example.com" {

        type master;

        file "example-external.db";

    }

}
```

### 6.24.23. `zone` 语句语法

```
zone zone_name [class] {

  type ( master | slave | hint | stub | forward ) ;

  allow-notify { address_match_list } ;

  allow-query { address_match_list } ;

  allow-transfer { address_match_list } ;

  allow-update { address_match_list } ;

  update-policy { update_policy_rule [...] } ;

  allow-forwarding { address_match_list } ;

  also-notify { ip_addr [port_addr] ; [ ip_addr [port_addr] ... ] };

  check-names (fail|ignore) ;

  dialup dial_option ;

  file string ;

  forward (only first) ;

  forward-ers { ip_addr [port_addr] ; [ ip_addr [port_addr] ... ] };

  ifconfig-base string ;

  ifconfig-tmp-file string ;

  maintain-ifconfig yes_or_no ;

  masters [port_addr] ; [ ip_addr [port_addr]] ;

  max-ifconfig-log-size number ;

  max-transfer-idle number ;

  max-transfer-time number ;

  max-transfer-timeout number ;

  notify yes_or_no explicit ;

  pubkey number ;

  transfer-source { ip4addr | * } [port_addr] ;

  transfer-source-v6 { ip6addr | * } [port_addr] ;

  notify-source { ip4addr | * } [port_addr] ;

  notify-source-v6 { ip6addr | * } [port_addr] ;

  zone-statistics yes_or_no ;

  sig-valid-interval number ;

  database string ;

  min-refresh-time number ;

  max-refresh-time number ;

  min-retry-time number ;

  max-retry-time number ;

}
```



### 6.2.22. zone 语句定义与用法

#### 6.2.22.1. 区域类型

| 类型 | 说明 |
| :--- | :--- |
| `master` | 服务器拥有该区域数据的主副本，并能够为其提供权威回答。 |
| `slave` | 从属区域（slave zone）是主区域的副本。`masters` 列表指定了一个或多个主服务器的 IP 地址，从区域联系这些服务器以更新其区域副本。默认情况下，传输从服务器的 53 端口进行；可以通过在 IP 地址列表之前指定端口号或按服务器更改所有服务器的端口。对主服务器的验证也可以通过每个服务器特定的 `TSIG` 密钥完成。如果指定了文件，则每当区域更改时，副本将写入此文件，并在重启时从该文件重新加载。建议使用文件，因为通常可以加快启动并消除延迟。（在每台服务器有数十或数千个区域的情况下，最好对区域名称使用两级命名方案。例如，区域 `example.com` 的一个从属服务器可能会将区域内容放在一个名为 `ex/example.com` 的文件中，其中 `ex/` 只是区域名称的前两个字母。） |
| `stub` | 存根区域（stub zone）与从属区域类似，区别在于它只复制主服务器的 `NS` 记录，而不是整个区域。这意味着在某些情况下，用户只需在父区域的主服务器上配置存根即可。`BIND 9` 绝不允许以这种方式允许不同区域的区域数据。因此，如果 `BIND 9` 主管一个父区域，且配置了存根区域，那么所有的属服务器也需要配置存根区域。例如，使用 `RFC2157` 地址的私有网络可以使用存根区域来让 `10.in-addr.arpa` 使用一组内部服务器。 |
| `forward` | “forward”是一种基于区域配置转发的方法。类型为 `forward` 的区域可以包含 `forward` 和/或 `forwarders` 语句，这适用于该区域内的查询。如果没有 `forwarders` 语句或给出一个空的 `forwarders` 列表，则不对该区域进行转发，从而消除了 `options` 中任何转发的影响。如果你想使用这种类型的区域来更改全局转发的行为（即，“首先到”、“仅到”或反之，但使用相同的服务器），你需要指定全局 `forwarders`。 |

区域名称后面可以跟随一个类。如果没有指定类，则假设为类 `IN`（代表 Internet）。这在大多数情况下都是正确的。

`hesiod` 类命名于 MIT Athena 项目的一项信息服务。它用于共享各种系统数据库的信息，如用户、组、打印机等。关键字 `HS` 是 `hesiod` 的同义词。

另一个 MIT 的开发成果是 `CHAOSnet`，它是 20 世纪 70 年代中期的一种 LAN 协议。它的区域数据可以使用 `CHAOS` 类指定。

#### 6.2.22.3. 区域选项

- `allow-notify`: 请参见第 6.2.14.3 节中的 `allow-notify` 说明。
- `allow-query`: 请参见第 6.2.14.3 节中的 `allow-query` 说明。
- `allow-transfer`: 请参见第 6.2.14.3 节中的 `allow-transfer` 说明。
- `allow-update`: 指定哪些主机允许向主区域提交动态 DNS 更新。默认是拒绝所有主机的更新。
- `update-policy`: 指定“简单安全更新”策略。请参见第 6.2.22.4 节。

初始的根服务器集使用“提示区域”（hint zone）指定。服务器启动时，它使用根提示找到一个根服务器并获取最新的根服务器列表。如果没有为类 `IN` 指定提示区域，服务器将使用编译好的默认根服务器提示。`IN` 类以外的类没有内置默认值。

##### `allow-update-forwarding`

指定哪些主机允许向从区提交动态 DNS 更新，并将这些更新重定向到主区。默认值为 `{ none };`，这意味着不会执行任何更新转发。要启用更新转发，请指定 `allow-update-forwarding { any };`。指定除 `{ none; }` 或 `{ any; }` 以外的值通常是适得其反的，因为访问控制的责任应该由主服务器承担，而不是从服务器。

请注意，在从服务器上启用更新转发功能可能会导致依赖于不安全的 IP 地址访问控制的主服务器受到攻击；更多信息请参阅第 7.3 节。

##### `also-notify`

仅当此区域的 `notify` 激活时才有意义。接收 DNS NOTICE 的机器 set 由所有列出的名称服务器（主服务器除外）加上任何通过 `also-notify` 指定的 IP 地址组成。每个 `also-notify` 地址后面都可以指定一个端口，以便将通知消息发送到默认端口 53 以外的端口。`also-notify` 对于存根区（stub zones）没有意义。默认是空列表。

##### `check-names`

此选项在 `BIND 8` 中用于限制主文件中域名的字符集和或从网络接收的 DNS 响应的字符集。`BIND 9` 不限制域名的字符集，并且没有实现 `check-names` 选项。

##### `database`

指定用于存储区域数据使用的数据库类型。`database` 关键字后面的字符串被解释为由空白符分隔的单词列表。第一个单词标识数据库类型，任何后续单词将作为参数传递给数据库，并以特定于数据库类型的方式进行解释。

默认值为 `"rbt"`，即 `BIND 9` 原生的内存红黑树数据库。该数据库不接受参数。

如果向服务器中链接了额外的数据库驱动程序，则可以使用其他值。发行版中包含了一些示例驱动程序，但默认没有链接。

##### `dialup`

请参阅第 6.2.14 节中关于 `dialup` 的描述。

##### `forward`

仅当区域具有转发器列表时才有意义。`only` 值会导致查找在尝试转发器且未得到答复后失败，而 `first` 则允许尝试正常查找。

##### `forwarders`

用于覆盖全局转发器列表。如果在类型为 `forward` 的区域中未指定，则对该区域不进行转发；不使用全局选项。

##### `ixfr-base`

在 `BIND 8` 中用于指定动态更新和 `IXFR` 的事务日志（journal）文件名称。这是一个未文档的选项，通过附加 `.jn1` 来构建日志文件的名称。

##### `ixfr-tmp-file`

曾是 `BIND 8` 中的一个未文档的选项。`BIND 9` 忽略了它。

##### `max-transfer-time-in`

请参阅第 6.2.14.6 节中 `max-transfer-time-in` 的描述。

##### `max-transfer-idle-in`

请参阅第 6.2.14.6 节中 `max-transfer-idle-in` 的描述。

##### `max-transfer-time-out`

请参阅第 6.2.14.6 节中 `max-transfer-time-out` 的描述。

##### `max-transfer-idle-out`

请参阅第 6.2.14.6 节中 `max-transfer-idle-out` 的描述。

##### `notify`

请参阅第 6.2.14.1 节中 `notify` 的描述。

##### `pubkey`

在 `BIND 8` 中，此选项用于指定公区域密钥，以便在从磁盘加载 DNSSEC 签名区域时验证签名。`BIND 9` 在加载时不验证签名并忽略该选项。

##### `zone-statistics`

如果为 `yes`，服务器将保留此区域的统计信息，这些信息可以转储到服务器选项中定义的 `statistics-file`。

##### `sig-validity-interval`

请参阅第 6.2.14.14 节中 `sig-validity-interval` 的描述。

##### `transfer-source`

请参阅第 6.2.14.6 节中 `transfer-source` 的描述。

##### `transfer-source-v6`

请参阅第 6.2.14.6 节中 `transfer-source-v6` 的描述。

##### `notify-source`

请参阅第 6.2.14.6 节中 `notify-source` 的描述。

##### `notify-source-v6`

请参阅第 6.2.14.6 节中 `notify-source-v6` 的描述。

##### `min-refresh-time`
##### `max-retry-time`
##### `min-retry-time`
##### `max-retry-time`

请参阅第 6.2.14.14 节中的描述。

#### 6.2.22.4. 动态更新策略

`BIND 9` 支持两种授予客户端对区域执行动态更新权限的方法，分别通过 `allow-update` 和 `update-policy` 选项配置。

`allow-update` 类的工作方式与 `BIND` 之前的版本相同。它授予给定客户端更新区域内任何名称的任何记录的权限。

`update-policy` 子句是 `BIND 9` 中的新功能，允许对允许的更新进行更细粒度的控制。它指定了一组规则，每条规则授予或拒绝一个或多个身份更新一个或多个名称的权限。如果动态更新请求消息已签名（即它包含了 `TSIG` 或 `SIG(0)` 记录），则可以确定签名者的身份。

规则指定在 `update-policy` 中。规则格式如下：

```
allow|deny { identity } name [ [ ]
allow|deny { identity } name [ type ]
allow|deny { identity } name [ type ] [ time ]
allow|deny { identity } name [ type ] [ time ] [ interval ]
allow|deny { identity } name [ type ] [ time ] [ interval ] [ predicate ]
```



如果使用 `deny`，则忽略时间参数。如果使用 `allow`，则允许更新。

## 6.3 区域文件

### 6.3.1 资源记录类型及其使用场景

本节很大程度上借自 RFC 1034，描述了资源记录 (RR) 的概念以及何时使用。

#### 6.3.1.1 资源记录 (RR)

域名标识一个节点。每个节点有一组资源信息，可以是空的。

一组与特定名称相关的资源信息由多个 RR 组成。RR 的顺序不需要名称服务器、解析器或 DNS 的其他部分保留。为了优化，例如指定某个服务器首先尝试。

资源记录的组成部分：

| 字段 | 描述 |
| :--- | :--- |
| 所有者域名 | RR 所在的域名。 |
| 类型 | 一个 16 位编码值，指定资源记录中的类型。类型指向抽象资源。 |
| TTL | RR 的生存时间。该字段是以秒为单位的 32 位整数，解析器在缓存 RR 时主要使用。TTL 描述了 RR 在丢弃前可以缓存多久。 |
| 类 | 一个 16 位编码值，标识协议族或协议实例。 |
| RDATA | 描述资源的类型和有时取决于类的数据。 |

以下是有效的 RR 类型（列出的某些类型虽然未过期，但是实验性的 (x) 或历史性的 (h)，不再广泛使用）：

| 类型 | 描述 |
| :--- | :--- |
| `A` | 主机地址。 |
| `A6` | IPv6 地址。 |
| `AAAA` | 过时的 IPv6 地址格式 |
| `AFSDB` | (x) AFS 数据库服务器的位置。实验性。 |
| `CERT` | 持数字证书。 |
| `CNAME` | 指定别名的规范名称。 |
| `DNS` | 反向地址的委托。替换为另一个名称进行查找。在 RFC 2672 中。 |
| `GPOS` | 指定全局位置。被 `LOC` 代替。 |
| `HINFO` | 标识主机使用的 CPU 和操作系统。 |
| `ISDN` | (x) ISDN 地址的表示。实验性。 |
| `KEY` | 存储与域名关联的公钥。 |
| `KX` | 标识此域名的密钥交换者。 |
| `LOC` | (x) 用于存储 GPS 信息。参见 RFC 1876。实验性功能。 |
| `MX` | 识别该域的邮件交换服务器。详情请参见 RFC 974。 |
| `NAPTR` | 名称权威指针。 |
| `NSAP` | 网络服务访问点。 |
| `NS` | 域的权威名称服务器。 |
| `NXT` | 用于 DNSSEC，以安全地指示特定区间内具有所有者名称的 RR（资源记录）在区域内不存在，并指示现有名称存在哪些 RR 类型。详情参见 RFC 2535。 |
| `PTR` | 指向域名命名空间其他部分的指针。 |
| `PX` | 提供 RFC 822 与 X.400 之间的映射。 |
| `RP` | (x) 关于负责该域人员的信息。实验性功能。 |
| `RT` | (x) 针对没有直接广域网地址的主机提供的路由绑定。实验性功能。 |
| `SIG` | (“签名”）包含在安全 DNS 中经过认证的数据。详情参见 RFC 2535。 |
| `SOA` | 标识权威区域的起始。 |
| `SRV` | 关于已知网络服务的信息（取代了 `WKS`）。 |
| `TXT` | 文本记录。 |
| `WKS` | (h) 关于该域支持哪些已知网络服务（如 SMTP）的信息。历史记录，已被更新的 RR 替代。 |
| `X25` | (x) X.25 网络地址的表示。实验性功能。 |

以下类记录目前在 DNS 中是有效的：

| 类 | 描述 |
| :--- | :--- |
| `IN` | 互联网系统。 |
| | 有关其他旧版 RR 类的信息，请参见第 A.2.1 节。 |

RDATA 是描述资源的依赖于类型或类的数据：

| 类型 | 描述 |
| :--- | :--- |
| `A` | 对于 `IN` 类，一个 32 位 IP 地址。 |
| `A6` | 将域名映射到 IPv6 地址，并为前导“前缀”位提供间接支持。 |
| `CNAME` | 域名。 |
| `DNAME` | 为域名命名空间的整个子树提供备用命名，而不是单个节点。它导致查询名称的后缀被替换为 `DNAME` 记录 RDATA 中的名称。 |
| `MX` | 一个 16 位的偏好值（越低越好），后跟一个愿意作为所有域邮件交换的主机名。 |
| `NS` | 完全限定域名。 |
| `PTR` | 完全限定域名。 |
| `SOA` | |

所有者名称是隐式的，而不是 RR 的固有组成部分。例如，名称在内部为命名空间形成树结构或哈希表，并在节点上链联 RR。剩余的 RR 是固定头（类型、类、TTL），它们对所有 RR 都是一致的，以及一个符合所描述资源所需的变量（RDATA）。

TTL 的含义是 RR 在缓存中可以保留多久的时间限制。此限制不适用于区域中的权威数据；它也会通过区域的刷新策略进行超时。短 TTL 可用于最小化缓存，而零 TTL 则禁止缓存。从互联网性能的实际情况来看，这些方案的 TTL 数量级应以天为单位。如果可以预料到更改，可以在更改之前减小 TTL 以减少更改期间的不一致性，然后在更改后将其恢复到原来的值。

RR 的 RDATA 部分中的数据是以二进制字符串和域名的组合形式携带的。域名被框架为指向 DNS 中其他数据的“指针”。

#### 6.3.1.2 RR 的文本表达式

RR 在 DNS 协议数据包中以二进制形式表示，并且在存储在名称服务器或解析器中时，通常以高度编码的形式表示。RFC 1034 中提供的示例采用了类似于主文件使用的样式，用以显示 RR 的内容。在这种格式中，大多数 RR 显示在单行中，尽管可以使用括号进行续行。

行的开头给出 RR 的所有者。如果某行开头有空格，则假设该所有者与上一个 RR 相同。为了可读性，通常包含空行。

在所有者之后，我们列出 RR 的 TTL、类型和类。类和类型使用上述定义的助符，TTL 是类型字段之前的整数。为了避免解析时的歧义，类型和类的助符是互斥的，TTL 是整数，且类型助符始终在最后。为了清晰起见，示例中经常省略 `IN` 类和 TTL 值。

RR 的资源数据或 RDATA 部分通过对数据典型表示法的了解给出。

例如，我们可能会显示消息中携带的 RR 为：

```
ISI.EDU. MX 10 VENERA, ISI.EDU.
         MX 10 VAXA, ISI.EDU.
VENERA.ISI.EDU A 128.9.0.32
                 10.1.0.52
VAXA.ISI.EDU A 10.2.0.27
                128.9.0.33
```

MX RR 有一个 RDATA 部分，由一个 16 位数字数字后跟一个域名组成。地址 RR 使用标准的 IP 地址格式来包含一个 32 位的互联网地址。

此示例显示了六个 RR，三个域名中的每个域名都有两个。

类似地，我们可能会看到：

```
XX.LCS.MIT.EDU. IN A 10.0.0.44
CH A MIT.EDU. 2420
```

此示例显示了 `XX.LCS.MIT.EDU` 的两个地址，每个属于不同的类。

### 6.3.2. MX 记录讨论

如上所述，域名服务器将信息存储为一系列资源记录，每条记录都包含关于给定名称（通常是主机，但并非总是）的特定信息。跟踪 RR 的简单方法是将其作为类型化数据对，即与相关数据匹配的域名，并带有一些额外的类型信息，以帮助系统确定 RR 何时有效。

MX 记录用于控制邮件的投递。记录中指定的数据是优先级和域名。优先级控制尝试投递的顺序，越低越优先。如果两个优先级相同，则随机选择一个服务器。如果两者都未成功，邮件将回退到下一个优先级。负缓存的最大时间为 3 小时（3h）。

```
example.com. IN MX 10 mail.com
             IN MX 10 mail2.com
             IN MX 20 backup.org
mail.com IN A 10.0.0.1
mail2.com IN A 10.0.0.2
```

> **注意：** 示例中的 `$ORIGIN` 行用于为示例提供上下文——它们并不一定出现在实际用法中。它们在这里仅用于指示示例是相对于列出的起始点的。

### 6.3.3. 设置 TTL

RR 字段的生存时间（TTL）是一个 32 位整数，以秒为单位表示，主要供解析器在缓存 RR 时使用。TTL 描述了 RR 在被丢弃之前可以缓存多久。区域文件中目前使用以下三种类型的 TTL。

| 类型 | 描述 |
| :--- | :--- |
| `SOA` | `SOA` 的最后一个字段是负 TTL。它控制其他服务器缓存来自你提供的 `NXDOMAIN` 响应多久。 |
| | 负缓存的最大时间为 3 小时（3h）。 |
| `TTL` | 区域文件顶部的 `$TTL` 指令（在 `SOA` 之前）为每个没有特定 TTL 的 RR 提供默认 TTL。 |

每个 RR 都可以将 TTL 作为 RR 的第二个字段，这将控制其保持多久。所有这些 TTL 默认单位均为秒，但可以显式指定单位，例如 `1h30m`。

### 6.3.4. IPv4 中的反向映射

反向域名解析（即从 IP 地址到名称的翻译）通过 `in-addr.arpa` 域和 `PTR` 记录实现。`in-addr.arpa` 域中的项目按从最低到最高位的顺序排列，从左到右读取。这与 IP 地址通常写入顺序相反。因此，IP 地址为 `10.1.2.3` 的机器对应的 `in-addr.arpa` 名称为 `3.2.1.10`。该名称应该有一个 `PTR` 资源记录，其数据字段为机器名称，或者如果机器有多个名称，可以是多个 `PTR` 记录。例如，在 `[example]` 域中：

```
$ORIGIN 2.1.10.in-addr.arpa
3 IN PTR foo.example.com
```

> **注意：** 示例中的 `$ORIGIN` 行用于为示例提供上下文——它们并不一定出现在实际用法中。它们在这里仅用于指示示例是相对于列出的起始点的。

### 6.3.5. 其他区域文件指令

主文件格式最初定义在 RFC 1035 中并得到了扩展。虽然主文件格式本身与类无关，但主文件中所有的记录必须属于同一类。主文件包括 `$ORIGIN`、`$INCLUDE` 和 `$TTL`。

#### 6.3.5.1. $ORIGIN 指令

语法：`$ORIGIN domain-name [ comment ]`

`$ORIGIN` 设置了将附加到任何未限定记录的域名名。当一个区域首次被读取时，会有一个隐式的 `$ORIGIN <zone-name>`。如果 `$ORIGIN` 参数指定的域名不是绝对的，则会将当前的 `$ORIGIN` 附加到 `$ORIGIN` 参数中指定的域名之后。

```
$ORIGIN example.com.

WWW CNAME MAIN-SERVER
```

等同于

```
WWW.EXAMPLE.COM. CNAME MAIN-SERVER.EXAMPLE.COM.
```

#### 6.3.5.2. $INCLUDE 指令

语法：`$INCLUDE filename [ origin][ comment ]`

读取并处理文件 `filename`，就像它被包含在当前位置的文件中一样。如果指定了 `origin`，则处理文件时会将 `$ORIGIN` 设置为该值，否则使用当前的 `$ORIGIN`。
一旦文件被读取，源和当前域名名将恢复到执行 `$INCLUDE` 之前的值。

> 注意：RFC 1035 规定在 `$INCLUDE` 之后应该恢复当前的源（origin），但对于是否也应该恢复当前域名名未说明。BIND 9 恢复了这两者。这可以被解释为对 RFC 1035 的偏离、一项特性或两者兼有。

#### 6.3.5.3. $TTL 指令

语法：`$TTL default-ttl [ comment ]`

为后续未定义 TTL 的记录设置默认的生存时间（TTL）。有效的 TTL 范围是 0-2147483647 秒。

`$TTL` 定义在 RFC 2308 中。

#### 6.3.6. BIND 主文件扩展：$GENERATE 指令

语法：`$GENERATE range lhs type rhs [ comment ]`

`$GENERATE` 用于创建一系列的资源记录，这些记录之间的区别仅在于一个迭代器。`$GENERATE` 可以轻松地生成记录集，以支持 RFC 2317 中描述的子 /24 反向委托（reverse delegations）：无类分类 `IN-ADDR.ARPA` 描述。

```
$ORIGIN 0.0.192.IN-ADDR.ARPA.

$GENERATE 1-2 NS SERVER1.EXAMPLE.

$GENERATE 1-127 $CNAME .0
```

等同于

```
0.0.192.IN-ADDR.ARPA. NS SERVER1.EXAMPLE.

0.0.192.IN-ADDR.ARPA NS SERVER2.EXAMPLE.

1.0.0.192.IN-ADDR.ARPA CNAME 1.0.0.192.IN-ADDR.ARPA

2.0.0.192.IN-ADDR.ARPA CNAME 2.0.0.192.IN-ADDR.ARPA

...

127.0.0.192.IN-ADDR.ARPA CNAME 127.0.0.192.IN-ADDR.ARPA
```

| 参数 | 描述 |
| :--- | :--- |
| `range` | 这可以有两种形式：`start-stop` 或 `start-stop/step`。如果第一种形式被设置为 1，则 `start`、`stop` 和 `step` 的所有必须都是正数。 |
| `lhs` | `lhs` 描述了要创建的资源记录的所有者名称。`lhs` 中的任何单个 `$` 符号都会被迭代器值替换。若要在输出中获得一个 `\$`，需要使用反斜杠 `\` 转义 `$`，例如 `\$` 后可选地跟随修饰符，这些修饰符更改相对于迭代器的偏移、字段宽度基基。修饰符通过 `[offset,width,base]` 引入，例如 `[-2,3,d]` 会从当前值减去 20，并以 3 位零填充十进制字段输出结果。可选输出格式有十进制（`d`）、八进制（`o`）和十六进制（`x` 或大写的 `X`）。如果 `lhs` 不是绝对的，则会将当前的 `$ORIGIN` 附加到该名称上。为了兼容早期版本，`$$` 仍被识别为输出中的文字 `$`。 |
| `type` | 目前支持的类型只有 `PTR`、`CNAME`、`A`、`AAAA` 和 `NS`。其处理方式与 `lhs` 类似。 |
| `rhs` | `rhs` 是一个域名。其处理方式与 `lhs` 类似。 |

`$GENERATE` 指令是 BIND 的扩展，不是标准区域文件格式的一部分。

## 第 7 章节：BIND 9 安全考虑

### 7.1. 访问控制列表

访问控制列表（ACLs）是地址列表，你可以设置并为其取别名，以便以后在 `allow-notify`、`allow-query`、`blackhole`、`allow-transfer` 等处使用。
使用 ACLs 允许你控制谁可以访问你的名称服务器，而无需用巨大的 IP 地址列表弄乱配置。使用 ACLs 并控制对服务器的访问是一个好主意。限制外部对你服务器的访问可以防止伪欺和 DoS 攻击。以下是如何正确应用 ACLs 的示例：

```
// 设置一个名为 "bogusnets" 的 ACL，它将阻止 RFC1918 空间

acl bogus-nets { 0.0.0.0/8; 10.0.0.0/8; 172.16.0.0/12; 192.168.0.0/16; 127.0.0.0/8; }

// 设置一个名为 our-nets 的 ACL。将此替换为真实的 IP 数字

acl our-nets ( x.x.x.x/24; x.x.x.x/21 );

options {

allow-query { our-nets };

allow-recursion { our-nets };

...

blackhole { bogusnets; };

}

zone "example.com" {

type master;

file "example.com";

allow-query { any };

};
```

这允许从外部对服务器进行递归查询，除非之前禁用了递归。有关如何使用 ACLs 保护你的服务器的更多信息，请参阅 **AUSCERT** 的公告，地址：`http://auscert.org/pub/advisory/dns_dos`

### 7.2. chroot 和 setuid（用于 UNIX 服务器）

在 UNIX 服务器上，可以通过指定 `-t` 选项在 `chroot` 环境中运行 BIND。这可以通过将 BIND 放置在“沙箱”中来帮助提高安全性，从而限制服务器被攻破时的损害。UNIX 版本 BIND 的另一个有用功能是可以作为非特权用户（`-u`）运行守护进程。我们建议在 `chroot` 时作为非特权用户运行。以下是一个在 `chroot` 沙箱 `/var/named` 中加载 BIND 并运行 `named` setuid 的命令行示例：

```
/usr/local/bin/named -u -t /var/named
```



### 7.2.1. chroot 环境

为了让 `chroot()` 在特定目录（例如 `/var/named`）中正常工作，你需要设置一个包含 BIND 运行所需一切的环境。从 BIND 的角度来看，`/var/named` 是文件系统的根。你需要调整 `pid-file` 等选项的值来适应这一点。与 BIND 的早期版本不同，你不需要编译 `named` 的静态共享库。但是，取决于你的操作系统，你可能需要设置像 `/dev/zero` 等项。

### 7.2.2. 使用 setuid

在运行非特权用户之前，使用 `touch` 工具（更改访问修改时间）或 `chown` 工具（更改所有者和组）对你需要 `named` 写入的文件。

### 7.3. 动态更新安全

动态更新的访问应该被严格限制。在早期版本中，这种方法是基于请求更新的主机 IP 地址，这很容易被伪造。由于这些原因，我们强烈建议通过事务签名（TSIG）对更新进行验证。也就是说，`allow-update` 选项应该列出 TSIG 名称，而不是 IP 地址。或者，可以使用新的 `update-policy` 选项。某些站点将所有动态更新数据放在子域中并将子域委托给独立的区域。这样，包含关键数据的顶级区域就不需要任何动态更新。

# 第 8 章节：故障排除

### 8.1. 常见问题

#### 8.1.1. 它无法工作；我如何发现哪里错了？

解决安装和配置问题的最佳方案是预先设置日志措施。日志文件提供了用于发现问题以及如何修复的提示和信息。

### 8.2. 递增和更改序列号

区域序列号只是数字——与日期无关。许多人将其设置为一个代表日期的数字，通常格式为 `YYYMMDD`。许多人为了测试 `Y2K` 合规性将其设置为 2000 年看看是否有效。然后他们尝试恢复旧的序列号。这将导致问题，因为序列号用于指示区域已更新。如果从服务器上的序列号小于主服务器上的序列号，从服务器将尝试更新其副本。

解决此问题是将该数字加上 `2147483647` (`2^31-1`)，重新加载区域并确保所有从都更新到新的区域序列号，将其重置为你想要的数字，然后重新加载区域。

如需讨论支持安排，请联系 `info@isc.org` (`mailto:info@isc.org`) 或访问 `ISC` 网页 `http://www.isc.org/services/support/` 了解更多信息。

## 附录 A 附录

### A.1 致谢

#### A.1.1. DNS 和 BIND 简史

尽管域名系统的“官方”起源于 1984 年 `RFC 920` 的发布，但新系统的核心内容在 1983 年的 `RFC 882` 和 `883` 中已被描述。从 1984 年到 1987 年，`ARPANet`（今日互联网的前身）成为了一个实验平台，用于在快速扩张的运行网络环境中开发新的命名/寻址方案。1987 年编写并发布了新的 `RFC`，它们修改了原始文档，以纳入基于工作模型的改进。`RFC 1034`《域名 - 概念与设施》和 `RFC 1035`《域名 - 实现与规范》被相继发布，并成为所有 DNS 实现的基础。

第一个名为“Jeeves”的域名服务器由 `Paul Mockapetris` 在 1983-84 年于南加州大学信息科学研究所（`US-ISI`）和 `SRI` 国际网络中心（`SRI-NC`）的 `DEC Tops-20` 机器上编写。不久后，加利福尼亚大学伯克利分校的一组研究生在美国国防高级研究计划署（`DARPA`）的资助下，编写了用于大学的互联网域名（`BIND`）软件包。`BIND 4.8.3` 之前的版本由加州大学伯克利的计算机科学组（`CSRG`）维护，`Douglas Terry`、`Mark Painter`、`David Ripple` 和周春组成了最初的 `BIND` 项目团队。在来自数字设备公司借调至 `CSRG` 的员工 `Ralph Campbell` 和 `Kevin Dunlap` 对软件包完成额外工作后，他们在 1985 年到 1987 年间维护了 2 年 `BIND`。许多其他人也对 `BIND` 的开发做出了贡献：`Doug Kingston`、`Craig Partridge`、`Smart Carl-Mitchell`、`Mike Jim Bloom` 和 `Mike Schwartz`。`BIND` 的后续维护由 `Mike Karels` 和 `O. K.` 负责。

数字设备公司（现为 `Compaq` 公司）发布了 `BIND 4.9.1` 版本。当时担任 `DEC` 员工的 `Paul Viese` 成为 `BIND` 的主要维护者。`Phil Alquist`、`Robert Elz`、`Jan Barrett`、`Paul Albitz`、`Bryan Beecher`、`Andrew Part`、`Andrew Cherenson`、`Tom Limcinelli`、`Berthold Alffrath`、`Faisal Baaran`、`Anant Kumar`、`Art Hardin`、`Win Treese`、`Don Lewis`、`Christophe Wolffugel` 等人的协助。

`BIND 4.9.2` 版本由 `Wix Enterprises` 赞助。`Paul Viese` 成为 `BIND` 的首席架构师/程序员。

`4.9.3` 及之后的版本由互联网软件联盟开发和维护，并由 `ISC` 赞助者的支持。作为共同架构师/程序员，`Bob Halley` 和 `Paul Vicxie` 在 1997 年 5 月发布了第一个生产就绪的 `BIND 8` 版本。如今，`BIND` 开发工作得益于几家公司的赞助以及许多个人不懈的努力。

## A.2. 历史 DNS 信息

### A.2.1 资源记录的分类

#### A.2.1.1. HS = hesiod

`[hesiod]` 类是由 `MIT Athena` 项目开发的一种信息服务。它用于共享各种系统数据库的信息，如用户、组、打印机等。关键字 `hs` 是 `hesiod` 的同义词。

#### A.2.1.2. CH = chaos

`chaos` 类用于指定由 `MIT` 开发的 70 年代中期开发的 `LAN` 协议 `CHAOSnet` 的区域数据。

## A.3. 通用 DNS 参考信息

### A.3.1 IPv6 地址 (A6)

`IPv6` 地址是用于接口及一组接口的 128 位标识符，引入 DNS 是为了实现可扩展的互联网路由。地址有三种类型：*单播*（`Unicast`），单个接口的标识符；*任任播*（`Anycast`），一组接口的标识符；以及*组播*（`Multicast`），一组接口的标识符。在这里我们描述全局单播地址方案。有关更多信息，请参阅 `RFC 2374`。

可聚合的全局单播地址格式如下：

| 3 | 13 | 8 | 24 | 16 | 64 bits |
|---|---|---|---|---|---|
| FP | TLA | RES | NLA ID | SLA ID | Interface ID |
| ID | <--- Public Topology ---> | | <-Site Topology-> | <--- Interface Identifier ---> |

其中

| FP | = 格式前缀 (001) |
| TLA ID | = 顶级聚合标识符 |
| RES | = 留作后用 |
| NLA ID | = 下一级聚合标识符 |
| SLA ID | = 站点级聚合标识符 |
| INTERFACE ID |  标识符 |

`公共拓扑`（`Public Topology`）由上游提供商或 `ISP` 提供，大致对应于地址范围的 `IPv4` 网络部分。`站点拓扑`（`Site Topology`）是你对该空间进行子网划分的地方，就像将一个 `IPv4/16` 网络划分为 `/24` 子网一样。`接口标识符`（`Interface Identifier`）是给定网络上单个接口的地址。（在 `IPv6` 中，地址属于接口而非机器）。
`IPv6` 的子网划分能力比 `IPv4` 灵活得多：现在可以在边界上进行子网划分，且与无分类域间路由（`CIDR`）相同。
`A6` 全局单播地址的公共拓扑内部结构包括：

| 3 | 8 | 24 |
|---|---|---|---|
| FP | TLA ID | RES | NLA ID |

`3` 位 `FP`（格式前缀）`001` 表示这是一个全局单播地址。其他类型地址的 `FP` 长度可能不同。
`13` 位 `TLA`（顶级聚合器）提供了你的顶级骨干网运营商的前缀。

`8` 位预留位。

`24` 位用于下一级聚合器。这允许拥有 `TLA` 的组织将其 `IP` 空间的部分分发给客户组织，以便客户随后通过填充更多 `NLA` 位来进一步划分网络，并向其客户分发 `IPv6` 前缀，以此此类推。

站点拓扑部分没有特定的结构。组织可以按照自己想要的方式分配这些位。

接口标识符在相应网络上必须是唯一的。在以太网网络中，确保这一点的一种方法是将地址设置为硬件地址的前三个字节“`FFFF`”，然后是硬件地址的最后三个字节。第一个字节的最低有效位应取反。地址以冒号隔开的 32 位块形式写入，块的前导导零可以省略，例如：

```
3fe:8050:201:9:a00:fe61:2b32
```

`IPv6` 地址规范可能包含长字符串的零，因此架构师包含了一种用于指定它们的简写。双冒号（`::`）表示符合条件的最长零字符串。

## A.4. 参考文献（建议阅读）

### A.4.1 请求征求（RFC）

互联网协议族的规范文档作为请求征求（`RFC`）系列的一部分发布，标准本身由互联网工程任务组（`IETF`）和互联网小组（`IESG`）定义。`RFC` 可通过 `FTP` 获取：`ftp://www.isi.edu/in-notes/RFC`（其中 `xxx` 是 `RFC` 号）。

## Bibliography

### 标准

- `[RFC2974]` `C. Partridge`, 邮件与域名系统，1986 年。
- `[RFC1034]` `P.V. Mockapetris`, 域名 - 概念与设施，1987 年。
- `[RFC1035]` `P.V. Mockapetris`, 域名 - 实现与规范，1987 年。

### 拟标准

- `[RFC2181]` `R. El` 和 `R. Bush`, DNS 规范的澄清，1997 年。
- `[RFC2308]` `M. Andrews`, DNS 查询负缓存，1998 年。
- `[RFC1995]` `M. Ohta`, DNS 增量传输，1996 年。
- `[RFC1996]` `P. Pixie`、`S. Thomson`、`Y. Rekhter` 和 `J. Bound`, 域名系统中的动态更新，1997 年。
- `[RFC2845]` `P. Pixie`、`O. Gudmundsson`、`D. Eastlake, 3rd` 和 `B. Wellington`, DNS 密钥事务认证 (TSIG)，2000 年。

### 开发中的拟标准

- `[RFC1886]` `S. Thomson` 和 `C. Huitema`, 支持 IPv6 的 DNS 扩展，1995 年。
- `[RFC20655]` `D. Eastlake, 3rd` 和 `C. Kaufman`, 域名系统安全扩展，1997 年。
- `[RFC2137]` `D. Eastlake, 3rd`, 安全域名动态更新，1997 年。

### 关于 DNS 实现的其他重要 RFC

- `[RFC1535]` `E. Gavron`, 一个安全问题以及对广泛使用的 DNS 软件的建议修正，1993 年。
- `[RFC1536]` `A. Kumar`、`P. Postel`、`C. Neuman`、`P. Danzig` 和 `S. Miller`, 常见的 DNS 实现错误和建议修复，1993 年。
- `[RFC1982]` `R. El` 和 `R. Bush`, 序列号算术，1996 年。

# 资源记录类型

- `[RFC1183]` `C.F. Everhart`, `L. A. Mamakos`, `R. Ullmann`, and `P. Mockapetris`, 新 DNS RR 定义，1990年10月。
- `[RFC1706]` `B. Manning` and `R. Colella`, DNS NSAP 资源记录，1994年10月。
- `[RFC2168]` `R. Daniel` and `M. Mealling`, 使用域名名系统解析统一资源标识符，1997年1月。
- `[RFC1876]` `C. Davis`, `P. Pixie`, and `I. Dickinson`, 在域名系统中表达位置信息的方法，1996年1月。
- `[RFC2052]` `A. Gulbrandsen` and `P. Pixie`, 用于指定服务位置的 DNS RR，1996年10月。
- `[RFC2163]` `A. Allochchio`, 使用 Internet DNS 分发 MIXER 一致全局地址映射，1998年1月。
- `[RFC2230]` `R. Atkinson`, DNS 密钥交换委托记录，1997年10月。

# DNS 与互联网

- `[RFC1101]` `P. V. Mockapetris`, 网络名称及类型的 DNS 编码，1989年4月。
- `[RFC1123]` `Braden`, 互联网主机主机 - 应用与支持，1989年10月。
- `[RFC1591]` `J. Postel`, 域名系统结构与委托，1994年3月。
- `[RFC2317]` `H. Eidnes`, `G. de Groot`, and `P. Pixie`, 无类 IN-ADDR.ARPA 委托，1998年3月。

# DNS 操作

- `[RFC1537]` `B. Beertema`, 常见的 DNS 数据文件配置错误，1993年10月。
- `[RFC1912]` `D. Barr`, 常见的 DNS 运行与配置错误，1996年2月。
- `[RFC2010]` `B. Manning` and `P. Vixie`, 根服务器的运行标准，1996年10月。
- `[RFC2219]` `M. Hamilton` and `R. Wright`, 使用 DNS 别名用于网络服务，1997年10月。

# 其他 DNS 相关的 RFC

- `[RFC1464]` `R. Rosenbaum`, 使用域名系统存储任意字符串属性，1993年5月。
- `[RFC1713]` `O. Romao`, DNS 调试工具，1994年11月。
- `[RFC1794]` `T. Brisco`, DNS 对负载均衡的支持，1995年4月。
- `[RFC2240]` `O. Vaughan`, 域名分配的法律依据，1997年11月。
- `[RFC2345]` `J. Klensens`, `T. Wolf`, and `G. Oglesby`, 域名与公司名检索，1998年5月。
- `[RFC2352]` `O. Vaughan`, 使用法律名称作为域名的惯例，1998年5月。

# 过时且未实现的性 RR

- `[RFC1712]` `C. Farrell`, `M. Schulze`, `S. Pleitner`, and `D. Baldoni`, 地理位置的 DNS 编码，1994年11月。

## A.4.2. 互联网草案

互联网草案（`IDs`）是互联网工程任务组（`ETF`）的粗草工作文档。从本质上说，它们是处于开发阶段的 `RFC`。警告实现者不要将 `ID` 视为存档，除非附有“正在进行的工作”的免责声明，否则不应在任何正式文件中引用或引述 `ID`。除非经过作者更新，否则 `ID` 在删除后有效期仅为六个月。

## A.4.3. 关于 BIND 的其他文档

## 参考文献

`Paul Albitz` and `Cricket Liu`, `DNS 与 BIND`, 1998.
