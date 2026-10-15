
这意味着本地 `cassowary.net` 域的主 DNS 服务器是 `provo.cassowary.net` (`206.68.216.16`)。该服务器随后连接到对 `paulwaters.com` 具有权威性的 `dns19.hostave.com`，该服务器对 `paulwaters.com` 域及其主机 (`paulwatters.com`)、别名 (`www.paulwaters.com`) 以及所需的 IP 地址具有权威。如果我们反转过程，改为在命令行上提供 IP 地址 `209.67.50.23`，我们将对该地址执行反向查找，这将解析到域名 `paulwaters.com`。

## 练习 26-2 使用 nslookup

使用 `nslookup` 确定 `www.sun.com` 的 IP 地址。

如果你想验证你的 DNS 服务器是否返回了正确的 IP 地址，或者你想自己验证一个地址，以交互模式运行 `nslookup` 允许你设置用于所有查询的 DNS 服务器名称。如果我们想解析悉尼大学 Web 服务器的域名，可以使用以下命令：

```
$ nslookup www.usyd.edu.au
```

# Sun 认证 Solaris 9.0 系统和网络管理员合一考试指南
466

然而，我们可以通过将我们的 DNS 服务器设置为 `ucc.usyd.edu.au` 域的权威 DNS 服务器，来验证该 IP 地址确实是正确的：

```
$ nslookup
Default Server: provo.cassowary.net
Address: 206.68.216.16
```

在这里，我们输入对目标域权威的 DNS 服务器名称：

```
> server metro.ucc.su.oz.au
Default Server: metro.ucc.su.oz.au
Address: 129.78.64.22
```

接下来，我们输入要解析的主机名：

```
> www.usyd.edu.au
Server: metro.ucc.su.oz.au
Address: 129.78.64.22
```

返回了正确的 IP 地址：

```
Name: solo.ucc.usyd.edu.au
Address: 129.78.64.24
Aliases: www.usyd.edu.au
```

如果你想确定 `www.usyd.edu.au` DNS 记录的一些关键特征，例如对该主机权威的 DNS 服务器以及负责该主机的管理员地址，可以通过 `nslookup` 获取起始授权（SOA）记录：

```
$ nslookup
Default Server: provo.cassowary.net
Address: 206.68.216.16
```

```
> server metro.ucc.su.oz.au
Default Server: metro.ucc.su.oz.au
Address: 129.78.64.22
> set qa
> www.usyd.edu.au
Server: metro.ucc.su.oz.au
Address: 129.78.64.22
```

```
www.usyd.edu.au canonical name = solo.ucc.usyd.edu.au
ucc.usyd.edu.au
  origin = metro.ucc.usyd.edu.au
  mail addr = root.metro.usyd.edu.au
  serial = 316
  refresh = 3600 (1 hour)
  retry = 1800 (30 mins)
  expire = 36000 (10 hours)
  minimum ttl = 43200 (12 hours)
```

此 SOA 记录指示以下内容：

- `www.usyd.edu.au` 的规范名称是 `solo.ucc.usyd.edu.au`。

# 第 26 章：DNS
467

- DNS 记录的源（origin）是 `metro.ucc.usyd.edu.au`（该服务器对主机 `solo.ucc.usyd.edu.au` 权威）。
- 当前记录的序列号（serial）为 `316`。下次记录发生变化时，序列号应该递增。
- 刷新率（refresh）为 1 小时。
- 重试率（retry）为 30 分钟。
- 过期率（expire）为 10 小时。
- TTL 为 12 小时。

> 考试提示：你应该能够识别 SOA 记录中不同的字段。

在为服务器创建 DNS 记录时，我们将检查每个字段的含义。使用 `nslookup` 确定哪些服务器对特定查询具有权威性不仅限于单个主机——事实上，通过使用 `nslookup` 可以确定整个网络的权威服务器。例如，如果我们想确定哪些服务器对库克群岛顶级域名（`.ck`）具有权威，我们将使用以下命令：

```
$ nslookup
> set type=ns
> ck.
Server: provo.cassowary.net
Address: 206.68.216.16
```

```
Non-authorative answer:
ck nameserver = DOWNSTAGE.MCS.VUM.AC.NZ
ck nameserver = NS1.WAIKATO.AC.NZ
ck nameserver = PARAU.OYSTER.NET.CK
ck nameserver = POIPARAU.OYSTER.NET.CK
ck nameserver = CIRCA.MCS.VUM.AC.NZ
```

```
Authoritative servers can be found from:
DOWNSTAGE.MCS.VUM.AC.NZ internet address = 130.195.6.10
NS1.WAIKATO.AC.NZ internet address = 140.200.128.13
PARAU.OYSTER.NET.CK internet address = 202.65.32.128
POIPARAU.OYSTER.NET.CK internet address = 202.65.32.127
CIRCA.MCS.VUM.AC.NZ internet address = 130.195.5.12
```

某些库克群岛顶级域名的权威服务器位于新西兰。这种地理上的分离似乎很奇怪，但如果你曾在拉罗托加岛（Rarotonga）经历过热带风暴，就有意义了——如果 `OYSTER.CK` 网络中断，主机名仍可以通过 `WAIKATO.AC.NZ` 的备份服务器解析。

还可以使用 `nslookup` 列出某个顶级域的所有网络：

```
$ nslookup
> set type=ns
```

495

# Sun 认证 Solaris 9.0 系统和网络管理员合一考试指南
468

伯克利互联网守护进程（BIND）是最常用的服务器。它的主配置文件 `/etc/named.conf` 负责控制服务器的行为并提供了以下关键字：

| 关键字 | 描述 |
| :--- | :--- |
| `acl` | 定义哪些客户端可以使用服务器的访问列表。 |
| `include` | 读取格式与 `/etc/named.conf` 相同的外部文件。当配置文件变得很大时，可以将部分拆分为文件。 |
| `logging` | 决定哪些活动记录在日志文件中。 |
| `options` | 定义本地属性。 |
| `server` | 定义其他服务器属性。 |
| `zone` | 创建本地 DNS 区域。 |

现在我们从客户端的角度检查了 DNS，并探索了 SOA、IP 映射等概念。让我们配置 DNS 服务器。

## acl

如果我们想为本地网络（`10.24.58.0/24`）的所有主机定义访问列表，我们将插入此语句：

```
acl local_network {
    10.24.58.0/24;
};
```

在这里，`24` 表示前缀法下的网络掩码 `255.255.255.0`。现在，如果我们是主机 `10.24.58.32`，并且想阻止从该地址访问 DNS 服务器，我们将之前的语句修改为：

```
acl local_network {
    10.24.58.32; 10.24.58.0/24;
};
```

注意，对于同时也允许的子网，特定地址的否定必须在语句中该子网定义之前。

## include

稍后，我们将检查如何配置 DNS 区域。由于这些定义对于大型网络可能非常长，管理员通常将它们放在单独的文件中，以便与 ACL 定义和选项分开管理。因此，为了包含 `/var/named/zones.conf` 文件中的所有区域定义，我们会在 `/etc/named.conf` 文件中插入以下语句：

```
include "/var/named/zones.conf"
```
