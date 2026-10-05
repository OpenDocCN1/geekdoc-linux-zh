

# 第 6 章 BIND 9 配置参考

在 `view` 语句中定义的区域仅对匹配该视图的客户端可见。通过在多个视图中定义同名称的区域，可以为不同的客户端提供不同的数据，例如拆分 DNS 设置中的“内部”客户端和“外部”客户端。

`options` 语句中的许多选项也可以在 `view` 语句中使用，这些选项仅在解析该视图的查询时生效。当没有提供特定视图的值时，将使用 `options` 语句中的值作为默认值。此外，可以在 `view` 语句中指定区域选项（zone options）；这些特定的视图默认值优于 `options` 语句中的值。

视图是特定于类的。如果没有指定类，则假设为类 IN。请注意，所有非 IN 类的视图必须包含一个提示区域（hint zone），因为只有 IN 类具有编译进去的默认提示。

如果配置文件中没有 `view` 语句，则会自动创建一个匹配任何客户端的默认视图，在配置文件顶层指定的任何 `zone` 语句都将被视为此默认视图的一部分。如果存在任何显式的 `view` 语句，则所有的 `zone` 语句必须发生在 `view` 语句内部。

以下是一个使用 `view` 语句实现的拆分 DNS 设置示例。

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

## 6.2.21. zone 语句语法

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

## 6.2.22. zone 语句定义与用法

### 6.2.22.1. 区域类型

| 类型 | 说明 |
| :--- | :--- |
| master | 服务器拥有该区域数据的主副本，并能够为其提供权威回答。 |
| slave | 从属区域（slave zone）是主区域的副本。masters 列表指定了一个或多个主服务器的 IP 地址，从区域联系这些服务器以更新其区域副本。默认情况下，传输从服务器的 53 端口进行；可以通过在 IP 地址列表之前指定端口号或按服务器更改所有服务器的端口。对主服务器的验证也可以通过每个服务器特定的 TSIG 密钥完成。如果指定了文件，则每当区域更改时，副本将写入此文件，并在重启时从该文件重新加载。建议使用文件，因为通常可以加快启动并消除延迟。（在每台服务器有数十或数千个区域的情况下，最好对区域名称使用两级命名方案。例如，区域 example.com 的一个从属服务器可能会将区域内容放在一个名为 ex/example.com 的文件中，其中 ex/ 只是区域名称的前两个字母。） |
| stub | 存根区域（stub zone）与从属区域类似，区别在于它只复制主服务器的 NS 记录，而不是整个区域。这意味着在某些情况下，用户只需在父区域的主服务器上配置存根即可。BIND 9 绝不允许以这种方式允许不同区域的区域数据。因此，如果 BIND 9 主管一个父区域，且配置了存根区域，那么所有的属服务器也需要配置存根区域。例如，使用 RFC2157 地址的私有网络可以使用存根区域来让 10.in-addr.arpa 使用一组内部服务器。 |
| forward | “forward”是一种基于区域配置转发的方法。类型为 forward 的区域可以包含 forward 和/或 forwarders 语句，这适用于该区域内的查询。如果没有 forwarders 语句或给出一个空的 forwarders 列表，则不对该区域进行转发，从而消除了 options 中任何转发的影响。如果你想使用这种类型的区域来更改全局转发的行为（即，“首先到”、“仅到”或反之，但使用相同的服务器），你需要指定全局 forwarders。 |

区域名称后面可以跟随一个类。如果没有指定类，则假设为类 IN（代表 Internet）。这在大多数情况下都是正确的。 |

hesiod 类命名于 MIT Athena 项目的一项信息服务。它用于共享各种系统数据库的信息，如用户、组、打印机等。关键字 HS 是 hesiod 的同义词。 |

另一个 MIT 的开发成果是 CHAOSnet，它是 20 世纪 70 年代中期的一种 LAN 协议。它的区域数据可以使用 CHAOS 类指定。 |

## 6.2.22.3. 区域选项

- allow-notify: 请参见第 6.2.14.3 节中的 allow-notify 说明。
- allow-query: 请参见第 6.2.14.3 节中的 allow-query 说明。
- allow-transfer: 请参见第 6.2.14.3 节中的 allow-transfer 说明。
- allow-update: 指定哪些主机允许向主区域提交动态 DNS 更新。默认是拒绝所有主机的更新。
- update-policy: 指定“简单安全更新”策略。请参见第 6.2.22.4 节。

初始的根服务器集使用“提示区域”（hint zone）指定。服务器启动时，它使用根提示找到一个根服务器并获取最新的根服务器列表。如果没有为类 IN 指定提示区域，服务器将使用编译好的默认根服务器提示。IN 类以外的类没有内置默认值。

