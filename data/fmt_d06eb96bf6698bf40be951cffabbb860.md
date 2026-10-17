
zone "1.1.10.IN-ADDR.ARPA" {

  type master;

  file "db.10.1.1";

}

zone "2.1.10.IN-ADDR.ARPA" {

  type master;

  file "db.10.1.2";

}

zone "3.1.10.IN-ADDR.ARPA" {

  type master;

  file "db.10.1.3";

}

zone "186.17.15.IN-ADDR.ARPA" {

  type master;

  file "db.15.17.186";

}

zone "." {

  type hint;

  file "db.cache";

}

`(wtec712-rtr) named.data- 1s`

```
boot.cacheonly db.10.1.2 db.15.17.186 named.boot
conf.cacheonly db.10.1.3 db.baseball named.conf
db.10.1.1 db.127.0.0 db.cache params-file
```

如你所见，`hosts_to_named` 创建了带有反向查找（IP 地址到名称）的 `db` 文件，其父级域名为 `baseball-hp.com`。我们网络中的每个节点都将具有完全限定域名短写 `name.baseball.hp.com`。

+ 5. 由于许多安装仍然在主机名中使用下划线，我强烈建议你通过修改 `hosts_to_named` 生成的 `named.conf` 文件中的 `check-names` 列表来允许此操作。例如，你可能想要更改这些行：

```
options {
check-names response fail // 不要更改此行
check-names slave warn
```

```
options {
check-names response ignore // 将 "fail" 改为 "ignore"
check-names slave ignore // 将 "warn" 改为 "ignore"
check-names master ignore // 添加这一整行
```

6. 在 `db.cache` 中填入根名称服务器的地址。如果你是直接连接到互联网，并通过查询网卡（NIC）上的名称服务器，可以从站点 `ftp://internet.net/domain/named.cache` 获取更新后的列表。

接下来，下载后将该文件复制到 `db.cache`。如果你没有直接连接到互联网，而是需要通过防火墙查询根名称服务器，请将防火墙设置为根名称服务器，并按照指定根名称服务器的方式将你的 `db.cache` 条目指向防火墙。正确配置 `db.cache` 非常重要，否则像邮件和名称解析等服务将受到影响。这里有一个示例：

```
; 填入根服务器的名称和地址
;
; . 99999999 IN NS root.server.
; root.server. 99999999 IN A ??..???
;
; 99999999 IN NS firewall.baseball.hp.com.
firewall.baseball.hp.com. 99999999 IN A 15.17.186.99
```

在这种情况下，`firewall.baseball.hp.com.` 是我的防火墙，由于我的名称服务器无法直接查询根名称服务器，`db.cache` 指向我的防火墙。

+ 7. 如果你打算有一个不与互联网进行任何方式通信的主主名称服务器，那么你需要通过执行几项操作将你的名称服务器设置为根服务器。可以在 `hosts_to_named` 的 `params` 文件中使用 `-r` 选项，或者进行以下更改：

在你的 `named.conf` 文件中，将：

```
zone ". {
type hint;
file "db.cache";
```

更改为：

```
zone ". {
type master;
file "db.root";
```

根名称服务器数据库 `db.root` 将包含：

```
. IN SOA baseball.hp.com. root.baseball.hp.com. (
       1         ; 序列
       10800      ; 每 3 小时刷新一次
       3600       ; 每小时重试一次
     60480     ; 一周后过期
     86400 )    ; 最小 TTL 为 1 天
IN NS baseball.hp.com.
baseball.hp.com. IN A 15.50.73.92
```

我们所做的是设置了一个带有一个记录的内部根名称服务器 `db.root`。下一个考虑是将对于你不具有权威性的域名的查询发送到哪里。如果你的域名是 `baseball.hp.com`，而有人询问 `google.com`，会发生什么？嗯，如果你配置了没有转发器（forwarders）的根名称服务器，答案是什么都没有。查询将因“host not found”（未找到主机）而失败。如果你不希望内部系统查询互联网域名，这可能是一件好事。安全和网络拥塞通常是原因。然而，如果你想解析互联网名称和地址呢？简单，在你的 `/etc/named.conf` 中配置一个 `forwards` 语句，指向防火墙或任何直接与根名称服务器通信的系统，如下所示：

```
options {
check-names response ignore; // 将 fail 改为 ignore
check-names slave ignore              // 将 warn 改为 ignore
check-names master ignore             
forwards { firewall_ip_address; }; // 转发到防火墙
}
```

## 第 12 章 网络

启动名称服务器后，你可以使用 `sig_named` 来执行各种功能。在你修改了任何 `db` 文件或 `/etc/named.boot` 之后，你需要告诉 `named` 刷新其数据库。你可以使用以下两个命令之一来实现这一点：

```bash
# sig_named restart
# kill -HUP /var/run/named.pid
```

这将重新加载数据库，你可以通过查看下面的 `/var/adm/syslog/syslog.log` 末尾来验证：

```
Oct 12 08:49:13 m3107ced named[8074]: primary zone "0.0.127.IN-AD-DRPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "baseball.hp.com" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "1.1.10.IN-AD-DRPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "2.1.10.IN-AD-DRPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "3.1.10.IN-AD-DRPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "1.168.192.IN-AD-DRPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "2.168.192.IN-AD-DRPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: primary zone "3.168.192.IN-AD-DRPA" loaded (serial 1)
Oct 12 08:49:13 m3107ced named[8074]: Ready to answer queries.
```

如你所示，`named` 加载了我们的每一个数据库（或区域），并准备好回答查询。

- 11. 同时通过名称和 IP 地址测试查询。

## 在 HP-UX 11.0 和 11i 上使用 BIND 8.1.2 设置 DNS 服务器
