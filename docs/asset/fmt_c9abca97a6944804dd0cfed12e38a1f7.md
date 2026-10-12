
假设办公室局域网内有几个系统以及公共的 Web、FTP 和邮件服务器。到互联网的单一连接经过 NAT（第 11 部分），因此它被本地系统和服务器共享。直接连接互联网的系统是路由器、防火墙和服务器。这种场景利用了 `named.conf` 中的 `View` 子句，并支持本地和公共用户的二级名称服务器。虽然公共用户需要访问作为支持服务器域名的 DNS 服务器，但他们不需要 DNS 服务器支持递归查询。对公共用户不支持递归查询限制了 DNS 服务器和互联网连接的负载。出于安全考虑，公共用户不能访问服务器以外的本地系统信息。本地用户应该能够访问本地系统信息，并能够递归地使用 DNS。

![](img/1e024b9f135a8b3cebc6731238212d84_937_0.png)

图 24-11 分裂域 DNS 服务器

图 24-11 显示服务器对局域网和互联网的查询响应不同。

`system-config-firewall`（第 893 页）或 `iptables` 工具（第 895 页）控制内部和外部系统上的哪些用户访问哪些端口。DNS 控制哪些系统被发布给哪些用户。

`named.conf` 文件有四个子句：一个 `Options` 子句、两个 `Views` 子句和一个 `Logging` 子句。`Options` 子句指定区域位于 `/var/named` 目录。`View` 子句指定解析器可以访问的特征和区域，这取决于解析器的地址。一个区域用于局域网/本地用户；另一个用于互联网/公共用户。`Logging` 子句为默认消息设置 `misc2.log` 文件；你必须如前所述创建 `/var/log/bind` 目录。

有多种方法可以指定哪些客户端查看 `view`。以下 `named.conf` 文件使用了 `match-clients` 语句：

```
$ cat /etc/named.conf
options {
    directory "/var/named";
}; //end options
```

```
view "local" IN {
// start local view
match-clients { 127.0.0.1; 192.168.0.0/24 };
recursion YES;
}
```

```
zone "zach.net" {
    master;
    file "local.net";
    notify YES;
}
```

```
zone "0.168.192.in-addr.arpa" IN {
  type master;
  file "named.local";
  notify YES;
}
```

```
zone "." IN {
  type hint;
  file "named.ca";
} // end local view
```

```
view "public" IN {
  match-clients {"any"};
  recursion NO;
} // start public view
```

```
zone "zach.net" IN {
  type master;
  file "public.net";
  notify YES;
}
```

```
zone "0.168.192.in-addr.arpa" IN {
  type master;
  file "named.public";
  notify YES;
}
```

```
zone "." IN {
  type hint;
  file "named.ca";
} // end public view
```

```
logging {
  channel "misc" {
    file "/var/log/bind/misc2.log" versions 2 size 1m;
    print-time YES;
    print-severity YES;
    print-category YES;
  }
  category default {
    "misc"
  }
} // end logging
```

`named.conf` 中 `View` 子句的顺序至关重要，因为呈现给客户端的视图是客户端匹配的第一个视图。之前的 `named.conf` 包含两个 `View` 子句：一个用于本地用户，一个用于公共用户，按此顺序排列。本地用户定义为位于 `192.168.0.0/24` 子网或 `localhost(127.0.0.1)` 的用户；公共用户定义为任何用户。如果你反转了 `View` 子句的顺序，所有用户（包括本地用户）都将获得为公共设计的视图，没有任何用户能看到本地视图。

# 设置不同类型的 DNS 服务器 887

`Options` 子句中的许多语句都可以在 `View` 子句中使用，它们会覆盖（全局）`Options` 子句中的相同语句。`recursion`（递归）语句可以出现在 `Options` 子句中，同样它它也会出现在每个 `View` 类中。`named.conf` 文件设置了一个服务器，为本地运行的查询提供递归回答，为面向公的查询提供迭代回答。这种设置为本地用户提供了快速、完整的回答，在限制分配给其他用户的网络和处理器带宽的同时，继续为本地服务器提供权威性服务。

为了让 `named.conf` 易于理解和维护，不同 `View` 子句中的区域可以具有相同的名称，但属于不同的区域。示例中的本地和公共 `View` 子句都有名为 `zach.net` 的区域：公共的 `zach.net` 区域文件名为 `public.net`，本地的名为 `local.net`。

`Logging` 子句描述见第 881 页。

定义 `zach.net` 的区域文件与之前的示例中的类似；公共文件是本地文件的子集。两个文件中 SOA 记录之后都跟着一个 TXT、两个 NS 和两个 MX 资源记录。接下来是三个 CNAME 记录，它们将指向 `www.zach.net`、`ftp.zach.net` 和 `mail.zach.net` 的查询重定向到 `ns.zach.net` 系统。接下来的四个资源记录指定了 `ns.zach.net` 类的两个名称服务器地址和两个邮件服务器。

最后四个资源记录出现在本地 `zach.net` 区域中，而不是公共区域中；它们是针对本地系统的 (A) 资源记录。与其在每个系统的 `/etc/hosts` 中保留这些信息，不如将其保存在 DNS 服务器上，那里可以方便地更新。当你使用 DNS 代替 `/etc/hosts` 时，必须相应更改 `/etc/nsswitch.conf`（第 494 页）中的 hosts 行。

```
$ cat local.net
; zach.net zone file
```

| $TTL 3D SOA ns.zach.net. mgs@sobell.com. ; serial |

| :--- | :--- |

| 201011118 | refresh |

| 8H | retry |

| 4W | expire |

| 1D ) | minimum |

| IN TXT "Sobell Associates Inc." | 名称服务器地址（未限定） |

| IN NS ns | 名称服务器地址 |

| IN NS ns.speedy.net. | 名称服务器地址（已限定） |

| IN MX 10 mail | 邮件交换（主/未限定） |

| IN MX 20 mail.max.net. | 邮件交换（备/已限定） |

# 888 章 BIND：跟踪域名名和地址

| IN TXT "Sobell Associates Inc." | 名称服务器地址（未限定） |

| IN NS ns | 名称服务器地址 |

| IN NS ns.speedy.net. | 名称服务器地址（已限定） |

| IN MX 10 mail | 邮件交换（主/未限定） |

| IN MX 20 mail.max.net. | 邮件交换（备/已限定） |

| IN A ns | 192.168.0.1 |

| IN A mail | 192.168.0.2 |

| IN CNAME www | mail |

| IN CNAME ftp | mail |

| IN A ns | 192.168.0.5 |

| IN A grape | 192.168.0.3 |

| IN A potato | 192.168.0.4 |

| IN A peach | 192.168.0.6 |

`zach.net` 区域文件的公共版本如下：
