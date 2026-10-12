
```bash
# cat /var/log/messages
--
19:25:48 peach named[22416]: starting BIND 9.3.2 -u named -t /var/named/chroot
19:25:48 peach named[22416]: found 1 CPU, using 1 worker thread
19:25:48 peach named[22416]: loading configuration from '/etc/named.conf'
19:25:48 peach named[22416]: listening on IPv4 interface lo, 127.0.0.1#53
19:25:48 peach named[22416]: listening on IPv4 interface eth0, 192.168.0.10#53
19:25:48 peach named[22416]: command channel listening on 127.0.0.1#953
19:25:48 peach named[22416]: command channel listening on ::1#953
```

`misc.log` 文件可能会显示消息文件中未出现的错误：

```bash
# cat /var/log/bind/misc.log
19:25:48.077 general: info: zone 0.168.192.in-addr.arpa/IN: loaded serial 2005110501
19:25:48.079 general: info: zone sam.net/IN: loaded serial 200511051
19:25:48.097 general: notice: running
```

## 从服务器

要设置从服务器，请将 `/etc/named.conf` 文件从主服务器复制到从服务器，并将 `type master` 语句替换为 `type slave`。删除从服务器不会充当从服务器的任何区域，包括根（`.`）区域（如果从服务器不响应递归查询）。按照前一节末尾的说明创建 `/var/log/bind` 目录用于日志文件。

### notify 语句

从服务器从主服务器或另一个从服务器复制区域信息。`notify` 语句指定你是否希望主服务器在其信息更改时通知从服务器。在 `Options` 部分中设置 `notify` 的（全局）值，或者在 `Zone` 部分中设置它，这会覆盖特定区域的全局设置。其格式为

* `notify` *YES* | *NO* | *EXPLICIT*

*YES* 会使主服务器通知列表中列出该区域 NS 资源记录的所有从服务器，以及 `also-notify` 语句中列出的 IP 地址的服务器。当你将 `notify` 设置为 `EXPLICIT` 时，服务器仅通知 `also-notify` 语句中列出的服务器。*NO* 关闭通知。

当你启动 `named` 时，它会将区域文件复制到 `/var/named`。如果你在主服务器上指定 `notify` `YES`，则每次你更改区域中 SOA 资源记录的 `serial` 字段时，从服务器上的区域文件都会更新。你必须手动分发更改到 `/etc/named.conf` 文件。

## 分裂地平线服务器

假设你要设置一个局域网，该局域网为其内部系统上的本地用户提供所有系统和服务（这些系统可能位于防火墙之后），并且仅向互联网（公共）用户提供某些公共服务——例如 Web、FTP 和邮件。*分裂地平线*（也称为 *DMZ*）DNS 服务器通过以不同的方式处理来自内部系统和公共系统（互联网上的系统）的查询来处理这种情况。

BIND 9 在 `named.conf` 中引入了 `View` 部分。`View` 部分有助于实施分裂 DNS 服务器。每个 `view` 为一组客户端提供不同的 DNS 命名空间视图。当没有 `View` 部分时，`named.conf` 中指定的所有区域都是隐含默认 `view` 的一部分。

假设一个办公室在局域网上有多个系统以及公共的 Web、FTP、DNS 和邮件服务器。与互联网的单条连接通过 NAT（第 1095 页）共享给本地系统和服务器。网关系统——直接连接到互联网的那一个——是一个路由器、防火墙和服务器。此场景利用了 `named.conf` 中的 `View` 部分，并支持为本地用户和公共用户设置独立的辅助名称服务器。虽然公共用户需要访问支持服务器的域名权威 DNS 服务器，但他们不需要 DNS 服务器支持递归查询。不支持公共用户的递归查询可以限制 DNS 服务器和互联网连接的负载。出于安全原因，公共用户不得访问除服务器外本地系统的信息。本地用户应能访问有关本地系统的信息，并应能递归使用 DNS 服务器。

图 24-11（上一页）显示服务器对来自局域网和互联网的查询做出不同的响应。

`iptables` 工具（第 819 页）控制内部和外部系统的用户可以访问哪些系统上的哪些端口。DNS 控制向哪些用户广播哪些系统。

`named.conf` 文件有四个部分：`Options`、`View` 部分和 `Logging`。`Options` 部分指定区域文件位于 `/var/named` 目录中。`View` 部分指定解析器获得访问权的特征和区域，这取决于解析器的地址。一个区域供局域网/本地用户使用，另一个供互联网/公共用户使用。`Logging` 部分为默认消息设置 `misc2.log` 文件。

指定哪些客户端看到某个 `view` 有几种方法。以下 `named.conf` 文件使用 `match-clients` 语句：

```bash
$ cat /etc/named.conf
options {
  directory "/var/named";
}; // end options

view "local" IN {   // start local view
match-clients { 127.0.0.1; 192.168.0.0/24;};
recursion YES;

zone "zach.net" IN {
  type  master;
  file  "local.net";
  notify  YES;
};

zone "0.168.192.in-addr.arpa" IN {
  type  master;
  file  "named.local";
  notify  YES;
};

zone "." IN {
  type  hint;
  file  "named.ca";
};
}; // end local view

view "public" IN { // start public view
match-clients { "all"} ;
recursion NO;

zone "zach.net" IN {
type master;
file "public.net";
notify YES;
};

zone "0.168.192.in-addr.arpa" IN {
type master;
file "named.public";
notify YES;
};

zone "." IN {
type hint;
file "named.ca";
};

}; // end public view

logging{
channel "misc" {
file "/var/log/bind/misc2.log" versions 2 size 1m;
print-time YES;
print-severity YES;
print-category YES;
};
category default {
"misc";
};
}; //end logging
```

`named.conf` 中 `View` 部分的顺序至关重要：呈现给客户端的 `view` 是客户端匹配的第一个 `view`。前面的 `named.conf` 文件包含两个 `View` 部分：一个供本地用户使用，一个供公共用户使用，顺序如此。本地用户被定义为位于 `192.168.0.0/24` 子网或本地主机（`127.0.0.1`）上的用户；公共用户被定义为任何用户。如果你颠倒了 `View` 部分的顺序，所有用户——包括本地用户——都会获得 intended for 公共的 `view`，而没有任何用户看到本地 `view`。

`Options` 部分中的许多语句可以在 `View` 部分中使用，在那里它们会覆盖（全局）`Options` 部分中的语句。可以出现在 `Options` 部分中的 `Recursion` 语句出现在每个 `View` 部分中。此 `named.conf` 文件设置了一个服务器，为源自本地的查询提供递归答案，为公共查询提供迭代答案。此设置向本地用户提供快速、完整的答案，限制用于其他用户的网络和处理器带宽，同时仍为本地服务器提供权威名称服务。
