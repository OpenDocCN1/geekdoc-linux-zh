
| `$TTL` `@` `IN` `SOA` `ns.sam.net.` `mgs@scobell.com.` `( 2010110501 : serial 8H : refresh 24H : retry 4W : expire 1D : minimum )` |

| | `TXT` `IN` `A` `IN` `"Sobhell Associates Inc."` |

| `NS` `ns` : 域名服务器地址（未限定） |

| `NS` `ns.max.net.` : 域名服务器地址（限定） |

| `MX` `10` `mail` : 邮件交换（主） |

| `MX` `20` `mail.max.net.` : 邮件交换（从） |

| `localhost` `IN` `A` `127.0.0.1` |

| `www` `IN` `ns` |

| `ftp` `IN` `CNAME` `ns` |

| `gw` `IN` `A` `192.168.0.1` `"Router"` |

| `ns` `IN` `A` `192.168.0.6` |

| `MX` `10` `mail` |

| `MX` `20` `mail.max.net.` |

| `mark` `IN` `A` `192.168.0.3` |

| `MX` `10` `mail` |

| `MX` `20` `mail.max.net.` |

| `TXT` `"MCS"` |

| `mail` `IN` `A` `192.168.0.4` |

| `MX` `10` `mail` |

| `MX` `20` `mail.max.net.` |

某些资源记录在 `Name` 字段中具有 `type`；没有名称的记录继承自上一个资源记录的名称。同样，资源记录可能有一个继承值，跟在 `SOA` 记录之后的五条资源记录从 `@`（或区域名）继承自 `SOA` 记录。这些记录属于整个区域。在前一个示例中，第一条 `TXT` 记录继承自 `SOA` 记录；它是 `sam.net` 区域的 `TXT` 记录（使用命令 `host -t sam.net` 显示 `TXT` 记录）。这些资源记录之后是区域内的资源记录。例如，`Name` 字段设置为 `mark` 的 `MX` 记录是 `sam.net` 域的记录。

# 854 第 24 章 DNS/BIND：跟踪域名和地址

`localhost` 的 `A` 记录后面有两个 `CNAME` 资源记录，指定 `www(sam.net)` 和 `ftp(sam.net)` 为 `ns.sam.net` 的别名。例如，连接到 `ftp.sam.net` 的用户将连接到 `192.168.0.6`。`gw`、`ns` 和 `mail` 是 `sam.net` 区域内的资源记录。

日志文件：在重启 `named` 之前，创建日志目录并赋予所示权限和所有权。如果 `named` 位于 jail 中，请在 `/var/lib/named/` 创建目录。

```
$ sudo mkdir /var/log/bind
$ sudo chown bind:bind /var/log/bind
$ ls -ld /var/log/bind
drwxr-xr-x 2 bind bind 4096 Aug 20 14:26 /var/log/bind
```

```
# /var/log/syslog
Apr 26 18:05:19 named[2219]: 9.7.0 -u bind -t /var/lib/named
Apr 26 18:05:19 named[2219]: found 1 CPU, using 1 worker thread
Apr 26 18:05:19 named[2219]: loading configuration from '/etc/bind/named.conf'
Apr 26 18:05:19 named[2219]: listening on IPv4 interface lo, 127.0.0.1:53
Apr 26 18:05:19 named[2219]: listening on IPv4 interface eth0, 192.168.0.10:53
Apr 26 18:05:19 named[2219]: command channel listening on 127.0.0.1:53
Apr 26 18:05:19 named[2219]: command channel listening on :53
```

```
# /var/log/bind/misc.log
```

`misc.log` 文件可能显示 `syslog` 文件中未出现的错误：

```
01:05:19.932 info: zone 0.168.192.in-addr.arpa/IN: loaded serial 2010110501
01:05:19.933 info: zone sam.net/IN: loaded serial 2010110501
01:05:19.933 notice: running
```

## 从服务器

要设置从服务器，从主服务器将 `/etc/bind/named.conf` 复制到从服务器，将 `type` 语句替换为 `type slave` 并添加 `masters {1.2.3.4; }` 指令。移除从服务器未作为从服务器的任何区域，如果从服务器不响应递归查询，则包括根目录 (.)。如有必要，按照上一节末尾说明为日志文件创建 `/var/log/bind` 目录。

从服务器从主主服务器或另一个从服务器查询信息。`notify` 语句指定了你希望当主服务器上的信息更改时，主服务器是否通知从服务器。设置（全局）

## 设置不同类型的 DNS 服务器 855

`Options` 子句中的 `notify` 值或 `Zone` 子句中的 `notify` 值，这会覆盖给定区域的全局设置。格式为：

`notify YES | NO | EXPLICIT`

`YES` 使主服务器通知 `NS` 资源记录以及 `also-notify` 语句中列出的所有从服务器。当你将 `notify` 设置为 `EXPLICIT` 时，服务器仅通知 `also-notify` 语句列出的从服务器。`NO` 关闭通知。

如果你在主服务器上设置 `notify YES`，每当你更改区域中 `SOA` 记录的序列号时，从服务器上的区域文件都会更新。你必须手动将更改分发 `/etc/bind/named.conf` 和包含的文件。

## 分 Split解析服务器

假设你想要建立一个局域网 (`LAN`)，为内部系统的本地用户提供所有系统和服务（这些系统可能位于防火墙后），但仅为互联网（公共）用户提供某些公共服务（如 Web、FTP 和邮件）。分 `DNS` 服务器（也称为 `DMZ DNS`）通过区别对待来自内部系统的查询和来自公共系统的查询来处理这种情况。

### View 子句

`BIND 9` 在 `named.conf` 中引入了 `View`。`View` 子句促进了分区域 `DNS` 服务器的实现。每个视图为一组客户端提供不同的 `DNS` 命名空间视角。如果没有 `View` 子句，`named.conf` 中指定的所有区域都是默认视图的一部分。

# 第 24 章 DNS/BIND：追踪域名和地址

![](img/f67bdb23d5a8cb457175c8ce91ec36c2_895_0.png)

图 24-6 分割地线 DNS 服务器

`**named.conf**` 文件包含四个子句：一个 `Options` 子句、两个 `View` 子句和一个 `Logging` 子句。`Options` 子句指定了区域文件位于 `/etc/bind` 目录。`View` 子句指定了解析器可以访问的特性和区域，这些取决于解析器的地址。其中一个区域用于局域网（LAN）/本地用户；另一个用于互联网/公网用户。`Logging` 子句设置了用于默认消息的 `m2.log` 文件。

有多种方法可以指定哪些客户端可以看到某个视图（view）。下面的 `**named.conf**` 文件使用了 `match-clients` 语句：

```
$ @etc/bind/named.conf
options {
    directory "/etc/bind"
}; //end options

view "local" IN {
    match-clients { 127.0.0.1; 192.168.0.0/24 };
    recurion YES;

    zone "zach.net" IN {
        type master;
        file "local.net"
        notify YES;
    }

    zone "0.168.192.in-addr.arpa" IN {
        type master;
        file "named.local"
        notify YES;
    }

    zone "." IN {
        type hint;
        file "named.ca";
    }
    // end local view
}
```

## 设置不同类型的 DNS 服务器
