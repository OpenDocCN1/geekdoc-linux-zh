
```
        file /tmp/named.log; # 消息发送的位置

        print-time yes; # 打印时间戳

        print-category yes; # 是否打印消息类别？

    }

    category config { custom }; # 配置文件

    category notify { custom }; # NOTIFY 消息

    category dnssec { custom }; # TSIG 消息

    category general { custom }; # 杂项

    category security { custom }; # 安全消息

    category xfer-out { custom }; # 区域传输

    category lame-servers { custom };

}
```

> 注意
> 保留并频繁检查日志尤为重要，因为语法错误经常会导致 BIND 拒绝一个区域且不对其回答查询，导致你的服务器变成“跛脚服务器”（意味着它对本应负责的区域不再具有权威性）。

# 解析器配置

在运行 BIND 之前的最后一步是设置本地解析器软件。这涉及配置 `/etc/hosts`、`/etc/resolv.conf` 和 `/etc/nsswitch.conf` 文件。

为了避免无意义的网络流量，大多数 UNIX 解析器仍然使用名为 `/etc/hosts` 的类似 hosts 的文本文件来存储常用主机的名称和地址。该文件中的每行包含一个 IP 地址和该主机的名称列表。对于任何你能够独立于 DNS 进行解析的主机，请在该文件中添加条目。如果在 `/etc/hosts` 中找到了该条目，解析器就无需联系 DNS 服务器即可解析名称，从而减少了网络流量。

`/etc/resolv.conf` 指定了首选名称服务器的地址以及一个域名列表，不限定的名称将相对于这些域名进行解析。你使用如 `nameserver 1.2.3.4` 的行指定名称服务器（其中 `1.2.3.4` 是名称服务器的地址）。你可以使用多个 `nameserver` 行（通常最多三个）。你可以使用 `search` 行指定一个用于搜索不限定名称的域名列表。

如 `example.com.net` 的搜索行会导致解析器尝试解析不限定名称 `xyz`，首先尝试作为 `xyz.example.com`，如果失败，则尝试 `xyz.example.net`。不要在搜索列表中使用过多域名，因为这会降低解析速度。

`/etc/nsswitch.conf` 中的 `hosts: dns` 行会导致解析器在名称查找过程中在使用 DNS 之前先咨询 `/etc/hosts`。这允许你通过对 `/etc/hosts` 进行临时更改来覆盖 DNS，这在网络测试期间特别有用。（旧版本的解析器可能需要使用 `/etc/host.conf` 文件中的旧版 hosts 文件和 `bind` 行。）

# 运行 named 名称服务器守护进程

最后，你现在可以通过 `/etc/rc.d/init/named start` 启动 `named`。你应该能在 syslog 中看到与下面相似的消息（或根据你设置的日志配置）。执行此操作的一种方法是使用 `tail` 命令监控日志文件；它会将文件中的更改在屏幕上滚动。

```
# tail -f /var/log/messages
```

October 9 23:48:33 titan named[2605]: starting BIND 9.2.0 -u named
October 9 23:48:33 titan named[2605]: using 1 CPU
October 9 23:48:33 titan named[2608]: loading configuration from '/etc/named.conf'
October 9 23:48:33 titan named[2608]: listening on IPv6 interfaces found
October 9 23:48:33 titan named[2608]: listening on IPv4 interface lo, 127.0.0.1#53
October 9 23:48:33 titan named[2608]: named startup succeeded
October 9 23:48:33 titan named[2608]: listening on IPv4 interface eth0, 192.168.2.68#53
October 9 23:48:33 titan named[2608]: command channel listening on 127.0.0.1#953
October 9 23:48:33 titan named[2608]: zone 0.0.127.in-addr.arpa/IN: loaded serial 197022700
October 9 23:48:33 titan named[2608]: zone localhost/IN: loaded serial 42
October 9 23:48:33 titan named[2608]: running

你可以使用 `rndc` 与此 `named` 实例进行交互。运行 `rndc` 参数会显示可用命令列表，包括重载区域、转储统计数据、切换日志、停止服务器的能力。（不幸的是，`rndc` 尚未实现与早期 BIND 版本发布的所有命令）。

你现在应该能够解析 `example.com` 了。如果出现问题，请阅读“故障排除 DNS”部分进行诊断和修复。

# 为真实域名提供 DNS

首先，我们必须引入区域（注意接下来的五个记录都使用了 `@`，代表 `example.com`）：

```
zone "example.com" {
    type master;
    file "example.com";
};
```

区域文件如下：

```
@       SOA ns1.example.com. admin.example.com. (20010901 24h 7h 1w 3600h)
NS      ns1.example.com.
NS      ns2.example.com.
A       192.0.2.1
A       192.0.2.96
MX 5     mx1.example.com.
MX 10    mx2.example.com.
A       192.0.2.2
A       192.0.2.3
A       192.0.2.4
A       192.0.2.5
A       192.0.2.6
```

`SOA` 记录与之前看到的类似。两个 `NS` 记录将 `ns1.example.com`（我们自己的服务器，`192.0.2.1`）和 `ns2.example.com`（我们朋友的服务器，`192.0.2.96`）定义为 `example.com` 的权威名称服务器。

MX 记录指定每个区域的邮件服务器。MX RR 有两个参数：优先级数字和主机名。在投递给 `example.com` 的邮件时，列出的 MX 按优先级从小到大的顺序尝试。在这种情况下，`mx1.example.com`（我们自己的机器，`192.0.2.2`）优先级最低并会被尝试。如果向 `mx1` 投递失败（无论原因），将尝试下一个列出的 MX `mx2.example.com`（我们朋友的服务器）。

`A` 记录表示 `example.com` 的地址为 `192.0.2.1`，接下来的几行指定了区域内其他主机的地址：我们的名称服务器 `ns1` 和 `ns2`，邮件服务器 `mx1` 和 `mx2`，两个 Web 服务器以及两个工作站。

接下来，我们添加 `NS` 记录将 `foo.example.com` 域权限委托给 `dns1` 和 `dns2.foo.com`。这些 `A` 记录被称为“胶记录”（glue records），它们允许解析器找到权威名称服务器的地址以便继续查询。（如果我们使用 `dig`，`dns1` 和 `dns2` 的 `NS` 记录如下：

```
; 委托
foo NS dns1.foo.com.
foo NS dns2.foo.com.
dns1.foo A 192.0.2.96
dns2.foo A 192.0.2.1
```

（列在响应的 AUTHORITY 部分中，而 ADDITIONAL 部分将包含它们的地址。）

注意 dns2.foo.example.com 是 192.0.2.1，这是我们自己的名称服务器。我们正作为 foo.example.com 区域的从服务器，并必须相应配置 `named`。我们在 `named.conf` 中引入该区域作为从区域，并指定主名称服务器的地址：

```
zone "foo.example.com" {
    type slave;
    file "foo.example.com";
    masters {
        192.0.2.96;
    }
}
```
