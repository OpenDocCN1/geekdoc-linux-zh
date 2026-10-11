
`request-ixfr yes`             # BIND 9 服务器语句

```
```

从 BIND 9.3 开始，`named` 现在可以向从服务器提供 IXFR，以传输手动进行的编辑。使用 `ixfr-differences` 选项启用此行为；见第 429 页。

IXFR 要求区域文件按标准顺序排序。`named` 为你处理这项杂务，但该要求使得 IXFR 变成了一种权衡。服务器使用了更多的内存和 CPU 来交换减少网络流量。

人们付出了大量努力以确保在 IXFR 期间服务器崩溃不会留下损坏数据的区域。向不支持支持的服务器发送 IXFR 请求会自动退回到标准的 AXFR 区域传输。

# 动态更新

DNS 系统的建立基于名称到地址的映射相对稳定且不频繁变化。然而，使用 DHCP 动态分配 IP 地址的站点在启动时不断打破这一规则。有两种经典的解决方案：向 DNS 数据库添加通用条目或不断编辑 DNS 文件。对于许多站点来说，两种方案都不令人理想。

第一种方案对于用过拨号 ISP 的人来说熟悉。DNS 配置如下：

```
dhcp-host1.domain. IN A  192.168.0.1

dhcp-host2.domain. IN A  192.168.0.2
```

## 15.14 更新区域文件

虽然这是一个简单的解决方案，但它意味着主机名与特定的 IP 地址永久绑定，计算机每当接收到新的 IP 地址时就会更改主机名。在这种环境下，基于主机名的日志记录或安全措施将变得非常困难。

BIND 近期版本中的动态更新（dynamic update）功能提供了一种替代方案。它允许 DHCP 守护进程通知 BIND 它所做的的地址分配，从而更新文件中 DNS 数据库的内容。动态更新可以添加、删除或修改资源记录。在进行动态更新时，系统会保留一个日志文件（`zoname.jnl`）以防止服务器崩溃的发生。

如果你不停止动态更新流，就无法手动编辑一个动态更新的区域。使用 `rndc rnd` 或 `rndc freeze zone` 可以解决这个问题。这些命令会将日志文件同步到磁盘上的主区域文件并删除日志文件。之后，你就可以手动编辑区域文件了。当然，区域文件的格式可能已经被 `named` 的“猴子”破坏——该文件看起来将像是由 `named` 为从服务器维护的样。

在区域被冻结期间，所有的动态更新尝试将被拒绝；使用与你冻结时相同的参数运行 `rndc rndaw` 以从磁盘重新加载区域文件并启用动态更新。

BIND 9 提供的 `nsupdate` 程序提供了一个用于动态更新的命令行界面。它以批处理模式运行，从键盘或文件读取命令。一个空行或发送信号标记输入结束，并将更改发送到服务器。两个空行表示输入结束。命令语言包含一种原始语句，用于表达诸如“如果 DNS 中不存在此主机名，则添加它”之类的结构。作为 `nsupdate` 动作的谓词，你可以要求一个名称存在或不存在，或者要求资源集（resource set）存在或不存在。

例如，这里是一个简单的 `nsupdate` 脚本，它添加了一个新主机，如果该别名不在区域中，则也会为现有主机添加一个别名。角括号是由 `nsupdate` 生成的，不是命令脚本的一部分。

```
$ nsupdate

> update add newhost.cs.colorado.edu 86400 A 128.233.243.16

> prereq nxdomain gypsy.cs.colorado.edu

> update add gypsy.cs.colorado.edu CNAME evi-laptop.cs.colorado.edu
```

DNS 的动态更新是令人不安的。它们可能会对你的系统数据提供不受控制的访问。不要尝试使用 IP 地址进行访问控制——它们太容易伪造了。带有共享密钥的 TSIG 认证更好；它是可用且易于配置的。BIND 9 支持两种：

```
$ nsupdate -k keydir:keyfile

$ nsupdate -y keyname:secretkey
```

## 第 15 章 – DNS：域名系统

由于密码直接写在命令行上，任何在正确时刻运行 `w` 或 `ps` 的人都能看到它。出于这个原因，优先使用 `-k` 形式。关于 TSIG 的更多详细信息，请参见从第 453 页开始的章节。

`named.conf` 中的 `allow-update` 或 `update-policy` 用于启用区域的动态更新。`allow-update` 允许根据 IP 或基于密钥的认证授予更新任何记录的权限。`update-policy` 是 BIND 9 的一个扩展，允许对主机名或记录类型的更新进行细粒度控制。它需要基于密钥的认证。两种区域均可选。

使用 `update-policy` 允许客户端更新它们的 A 或 PTR 记录但不更新 KEY 记录。你也可以使用 `update-policy` 允许主机仅更新自己的记录。这些参数允许你显式地表达名称，作为子域、通配符或作为关键字 `self`，后者为机器访问其自身的记录设置策略。资源记录通过类和类型来标识。`update-policy` 规则的语法为：

```
update-policy { grant deny } identity name type [ ];
```

`identity` 是授权更新所需的加密密钥的名称。`nametype` 有四种值之一：`name`、`subdomain`、`wildcard` 或 `self`。`name` 是要更新的区域，类型是可以更新的资源类型。如果没有指定任何类型，则除 SOA、NS、RSIG 和 SEC 之外的所有类型都可以被更新。这里有一个例子：

```
update-policy { grant dhcp-key dhcp.cs.colorado.edu A };
```

此配置允许任何知道密钥 `dhcp-key` 的人更新 `dhcp.cs.colorado.edu` 子域中的地址记录。该语句将出现在主服务器的 `named.conf` 文件中，位于 `zone` 区域语句下（针对 `dhcp.cs.colorado.edu`）。此外还需要一个密钥来定义 `dhcp-key`。

以下摘自科罗拉多大学计算机科学系 `named.conf` 文件的片段使用了 `update-policy`，允许管理班的学生更新自己的子域，但不会干扰 DNS 环境的其他部分。

```
// saclass.net in {

zone "saclass.net"

    type master;

    file "saclass.net";

    update-policy {

        grant factor_mroe. subdomain saclass.net;

        grant mojo_mroe. subdomain saclass.net;

        grant dawdle_mroe. subdomain saclass.net;

        grant pirate_mroe. subdomain saclass.net;

    }

// 还有更多

}
