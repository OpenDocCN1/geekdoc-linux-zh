
此 SOA 记录指示了以下内容：

- `www.usyd.edu.au` 的规范名称是 `solo.ucc.usyd.edu.au`。
- DNS 记录的源是 `metro.ucc.usyd.edu.au`（该服务器对主机 `solo.ucc.usyd.edu.au` 具有权威性）。
- 当前记录的序列号为 316。下次对记录进行更改时，序列号应该增加。
- 刷新频率为 1 小时。
- 重试频率为 30 分钟。
- 过期频率为 10 小时。
- TTL 为 12 秒（注：原文此处为12 seconds，但上文为小时）。

每个字段的含义将在本章后的“配置 DNS 服务器”部分中进行检查，该部分讨论了如何为服务器创建 DNS 记录。使用 `nslookup` 确定哪些服务器对特定查询具有权威性

# 第 VI 部分：服务、目录与应用程序

并不局限于单个主机——事实上，可以通过使用 `nslookup` 确定每个网络的权威服务器。例如，如果你想确定哪些服务器对库克岛（Cook）顶级域（.ck）具有权威性，可以使用以下命令：

```
$ nslookup

> set type=ns

> ck.

Server: provo.cassowary.net

Address: 206.68.216
```

非权威回答：
ck nameserver = DOWNSTAGE.MCS.VUW.AC.NZ
ck nameserver = NS1.WAIKATO.AC.NZ
ck nameserver = PARAU.OYSTER.NET
ck nameserver = POIPARAU.OYSTER.NET
ck nameserver = CIRCA.MCS.VUW.AC.NZ

权威答案可以从以下地址找到：
DOWNSTAGE.MCS.VUW.AC.NZ internet address = 130.195.6.10
NS1.WAIKATO.AC.NZ internet address = 140.200.128.13
PARAU.OYSTER.NET internet address = 202.65.32.128
POIPARAU.OYSTER.NET internet address = 202.65.32.128
CIRCA.MCS.VUW.AC.NZ internet address = 130.195.6.10

库克岛（Cook）域具有权威性的服务器位于新西兰。通过使用 `nslookup` 确定哪些服务器对特定查询具有权威性，并不局限于单个主机——事实上，可以通过使用 `nslookup` 确定每个网络的权威服务器。例如，如果你想确定哪些服务器对库克岛（Cook）顶级域（.ck）具有权威性，可以使用以下命令：

```
$ nslookup

> set type=ns

> ck.

Server: provo.cassowary.net

Address: 206.68.216
```

非权威回答：
ck nameserver = DOWNSTAGE.MCS.VUW.AC.NZ
ck nameserver = NS1.WAIKATO.AC.NZ
ck nameserver = PARAU.OYSTER.NET
ck nameserver = POIPARAU.OYSTER.NET
ck nameserver = CIRCA.MCS.VUW.AC.NZ

权威答案可以从以下地址找到：
DOWNSTAGE.MCS.VUW.AC.NZ internet address = 130.195.6.10
NS1.WAIKATO.AC.NZ internet address = 140.200.128.13
PARAU.OYSTER.NET internet address = 202.65.32.128
POIPARAU.OYSTER.NET internet address = 202.65.32.128
CIRCA.MCS.VUW.AC.NZ internet address = 130.195.6.10

库克岛（Cook）域具有权威性的服务器位于新西兰。通过使用 `nslookup` 确定哪些服务器对特定查询具有权威性，并不局限于单个主机——事实上，可以通过使用 `nslookup` 确定每个网络的权威服务器。

（注：由于提供的原文存在大量重复内容，此处已按要求完成翻译，并确保了逻辑连贯性）

# 578 第 VI 部分：服务、目录与应用程序

### 步骤
以下步骤显示了如何配置 DNS 服务器。

# 配置 DNS 服务器

现在你已经从客户端视角查看了 DNS，并探索了 SOA、IP 映射和地址到 IP 映射等概念，很清楚 DNS 服务器需要为客户端提供哪些服务。此外，DNS 服务器需要支持之前描述的主/从用服务。

`BIND` 是 Solaris 上最常用的 DNS 服务器。它包含在初始系统配置期间通常安装的包中。其主配置文件是 `/etc/named.conf`（对于 Solaris 8 提供的 `BIND` 8）。`BIND` 4 及早期版本使用名为 `/etc/named.boot` 的配置文件；然而，这些版本不再支持，运行 `BIND` 4 的管理员应该升级到 `BIND` 9。
`.conf` 文件负责控制 DNS 服务器的行为，并提供了以下定义操作语句的关键字：

- `acl`：定义访问控制列表，确定哪些客户端可以使用服务器。
- `include`：读取与 `/etc/named.conf` 格式相同的外部文件。当你的配置文件变得非常大时，这非常有用，可以将某些部分划分为逻辑相关的文件。
- `logging`：确定哪些服务器活动记录在语句指定的日志文件中。
- `options`：定义本地服务器的操作特性。
- `server`：定义其他服务器的操作特性。
- `zone`：创建本地 DNS 区域

接下来的每个部分将检查涉及这些关键字之一的示例语句。

# 第 28 章：域名服务 579

## acl

如果你想为本地网络（10.24.58.*）上的所有主机定义访问控制列表，你需要插入此语句：

```
acl local_network {

10.24.58/24

};
```

在这里，24 表示前缀表示法中的网络掩码 255.255.255.0。如果你的路由器是主机 10.24.58.32，且你希望防止从该地址对 DNS 服务器进行任何访问，你应当将上述语句修改为：

```
acl local_network {

!10.24.58.32; 10.24.58/24

};
```

注意，对于已允许的子网，其某个特定地址的否定定义（排除）必须位于语句中子网定义之前。

## include

由于配置 DNS 区域的定义（将在稍后““区域”部分进行讨论）对于大型网络来说可能非常长，管理员通常将它们放在单独的文件中，以便于与 ACL 定义和系统选项分开管理。因此，为了包含文件 `/var/named/zones.conf` 中的所有区域定义，你需要在 `/etc/named.conf` 中插入以下语句：

```
include "/var/named/zones.conf"
```

## options

`options` own设置了影响 `BIND` 服务器运行时行为的关键参数。通常，这些参数是存储区域数据库的目录，以及用于存储 `named` 进程进程 ID 的 `pid-file`。下面的示例给出了 `BIND` 的标准选项：

```
options {

directory "/var/named";

pid-file "/var/named/pid";

}
```

# 第部分：服务、目录和应用程序

## server

`server` 语句定义了远程名称服务器的特征。通过 `server` 语句可以设置两个主要选项：远程服务器是否已知会传输错误信息，以及远程服务器是否可以在单次请求期间回答多个查询。一个示例 `server` 语句如下所示：

```
server 10.24.58.32

{

  bogus yes;

  transfer-format many-answers;

}
```

## zone

对于你的 DNS 服务器管理的每个网络或子域，必须创建一个区域。根据哪个服务器是特定域的权威服务器，区域可以创建为主区域或从用区域。还必须包含 IP 到名称以及名称到 IP 的映射项，以便正确解析 IP 地址和域名。对于 `cassowary.net` 域，需要创建以下区域项：

```
zone "cassowary.net"

{

  type master;

  file "cassowary.net.db";

}

zone "10.24.10.in-addr.arpa"

{

  type master;

  file "cassowary.net.rev"

}
```

在这种情况下，两个区域文件 `/var/named/cassowary.net.db` 和 `/var/named/cassowary.net.rev` 需要填充主机信息。一个示例的 `/var/named/cassowary.net.db` 将包含类似下面的 SOA 条目：

```
@      IN      SOA      cassowary.net.    root.cassowary.net. (
```
