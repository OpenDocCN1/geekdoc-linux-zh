
## BIND 配置选项

`-u` 指定在绑定到 53 端口后切换到哪个 UID（例如使用一个名为 `'named'` 且没有登录权限的用户，类似于 `'nobody'`）。

`-g` 指定在绑定到 53 端口后切换到哪个 GID（例如使用一个名为 `'named'` 的组，类似于 `'nobody'`）。

`-t`

运行 chrooted 版本的 bind 更简单的方法是下载 `bind-chroot` 软件包（大多数发行版都作为 contrib 软件包提供）并安装它。安装后，你需要一个名为 `named` 的用户和组（这是 bind 服务器要切换的 UID/GID），只需使用 `groupadd` 和 `useradd` 即可。某些软件包使用 `holelog` 将信息记录到 `/var/log/messages`（就像 bind 通常做的那样），如果不可用，你需要安装它，这很麻烦。为了给 bind 添加此配置文件，通常会配置得很安全（即你无法向 bind 查询版本信息）。

bind 的另一个方面是它包含了关于你的网络的信息。当某人向 DNS 服务器查询信息时，他们通常会对某项信息发出一个很小的请求，例如：`www.sefried.org` 的 IP 地址是什么？存在域名服务器，DNS 服务器会收集 `sefried.org` 的所有信息并将其抓取，然后将其提供给其他服务器（在辅助 DNS 服务器的情况下）。这具有潜在的危险性，因为任何人都可以调用并请求。Bind 版本 4 并没有多少安全性，你可以限制许可的审查服务器，但细粒度不足，无以产生实用价值。这在 Bind 8 中发生了变化，那里有全局设置，且大部分这些设置也可以应用于单个域名。你可以轻松地限制传输和查询、记录查询、设置最大数据大小等。记住，在限制区域时，必须保护**所有**名称服务器（主服务器和辅助服务器），因为你可以像主服务器一样轻松从辅助服务器传输区域。

这里是一个相对安全的 `named.conf` 文件（取自 `ftp.tux.org` 的 `bind-chroot` 软件包）：

```
options {
    // 以下路径对于此 chroot 是必要的
    directory "/var/named";
    dump-file "/var/tmp/named_dump.db"; // _PATH_DUMPFILE
    pid-file "/var/run/named.pid"; // _PATH_PIDFILE
    statistics-file "/var/tmp/named.stats"; // _PATH_STATS
    memstatistics-file "/var/tmp/named.memstats"; // _PATH_MEMSTATS
    // 必要 chroot 路径结束
    check-names master warn; /* default. */
    datasize 20M;
}
```

```
zone "localhost" {
    type master;
    file "master/localhost";
    check-names fail;
    allow-update { none };
    allow-transfer { any };
}
```

```
zone "0.0.127-in.addr.arpa" {
    type master;
    file "master/127.0.0";
    allow-update { none };
    allow-transfer { any };
}
```

```
// 来自 localhost 外，拒绝并记录对我们版本数的查询
zone "bind" chaos {
    type master;
    file "master/bind";
    allow-query (localhost);
}
```

```
zone "." {
    type hint;
    file "named.zone";
}
```

```
zone "example.org" {
    type master;
    file "zones/example.org";
    allow-transfer {
        10.2.1.1;
        10.3.1.1;
    };
}
```

Bind 运行在 53 端口，同时使用 `udp` 和 `tcp`。`udp` 用于正常的域名查询（它轻量且快速快），`tcp` 用于区域传输和大型查询（例如 `dig www.microsoft.com`）。这种 `tcp` 防火墙相对安全，并且会停止任何区域传输，偶尔的 DNS 查询可能无法工作。最好使用 `named.conf` 来控制传输。

```
ipfwadm -I -a accept -P tcp -s 10.0.0.0/8 -D 0.0.0.0/0 53
ipfwadm -I -a accept -P tcp -s some.trusted.host -D 0.0.0.0/0 53
ipfwadm -I -a deny -P tcp -s 0.0.0.0/0 -D 0.0.0.0/0 53
```

或者

```
ipchains -A input -p tcp -j ACCEPT -s 10.0.0.0/8 -d 0.0.0.0/0 53
ipchains -A input -p tcp -j ACCEPT -s some.trusted.host -d 0.0.0.0/0 53
ipchains -A input -p tcp -j DENY -s 0.0.0.0/0 -d 0.0.0.0/0 53
```

```
ipfwadm -I -a deny -P tcp -S 0.0.0.0/0 -D 0.0.0.0/0 119
```

或者

```
ipchains -A input -p tcp -j ACCEPT -s 10.0.0.0/8 -d 0.0.0.0/0 119
ipchains -A input -p tcp -j ACCEPT -s some.trusted.host -d 0.0.0.0/0 119
ipchains -A input -p tcp -j DENY -s 0.0.0.0/0 -d 0.0.0.0/0 119
```

## DNews

`http://netwinsite.com/dnews.htm`

## DHCPD

DHCPD 是所有网络管理员都应该使用的工具。它允许你向请求网络设置/等信息的客户端提供服务，这意味着网络连接所需的客户端设置只需保持默认值并开启机器即可。它还允许你轻松地重新配置客户端（例如从 10.0.1.0 移动到 10.0.2.0，或使用一组新的 DNS 服务器）。从长期来看（以及短期内也是如此），DHCP 将为你节省大量工作、金钱和精力。我在家里运行它，只有 8 个客户端，发现生活变得简单多得多。DHCPD 由 ISC 维护，地址为：`http://www.isc.org/dhcp.html`。

我强烈建议你运行 DHCPD 2.x（3x 处于 alpha 阶段），它有很多新功能，而且易于设置和使用。不过，该程序的绝对版本往往有点神经质，请注意它是 beta 软件。务必不要将 DHCPD 暴露在互联网上。DHCP 流量应该只在本地网段上运行，可能会被转发到另一个网段的 DHCP 服务器，但你在互联网上看到的唯一 DHCP 流量将是攻击/DoS（它们可能会恢复你所有的 IP，让你的客户端孤立无援）。如果你要在互联网上转发 DHCP 流量，**千万不要**。出于多种原因，这是一个一个坏主意（主要是性能/可靠性，也包括安全性）。

我建议 DHCP 服务器仅作为一个 DHCP 服务器，锁定在某个地方（如果你依赖 DHCP 运行网络，而 DHCP 服务器故障，你的网络将面临严重问题），允许它快速运行，如果你需要跨越子网（如果你有多个服务器，其中只有一个服务器物理连接了 DHCP 服务器），请使用 DHCP 中继（NT 没有内置功能，Linux 的 DHCP 软件具有此能力，等）。NT 和 DHCP 之间也存在已知问题，NT RAS 有一个糟糕的习惯，会疯狂地吸取 IP 地址（我见过一个 NT 服务器抢占了 64 个地址并无限期保留），因为它正尝试为将拨入/拨出的客户端预留 RAS IP。要么关闭 NT 的 RAS，要么将其放在它单独的子网中，它发送给 DHCP 服务器的 MAC 地址非常奇怪（并且在前几个字节中拼写出 RAS），并且很容易进行映射。

DHCPD 包含 2 个可执行文件：

- `dhcpd` - DHCP 服务器

- `dhrelay` - 一个 DHCP 中继程序（用于将请求中继到中央 DHCP 服务器，因为 DHCP 是基于广播的，而广播通常不会（也不应该）跨越路由器/以太卡。）

DHCPD 需要 2 个库文件：

- `/lib/dhcp-linux.so.2`

- `/lib/libc.so.6`

一个配置文件：

- `/etc/dhcpd.conf` - 配置信息、启动文件位置等。

以及其他一些杂项文件：

- `/etc/dhcpd.leases` - 活动租约列表

- 一个启动文件，你可以仅对随附的那个进行修改
