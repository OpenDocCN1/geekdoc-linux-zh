
| | `ATTORNEY` | 顶级域名 |

| | `BEER` | `Grand Hollow, LLC` |

| | `BIZ` | `Atomic LLC` |

| | `BUILDERS` | `Wild LLC` |

| | `CHRISTMAS` | `Holly Fields, LLC` |

| | `COM` | 商业组织 |

| | `COOP` | 合作协会 |

| | `EDU` | 受国家认可的高等教育机构 |

| `GOV` | 美国政府 |

| | `INFO` | 任何人 |

| `INT` | 政府间的条约 |

| `MIL` | 美国军事 |

| `MUSEUM` | 电话服务提供商 (`ISPs`) |

| `NAME` | 非商业社区 |

| `NET` | 可注册的 |

| `ORG` | `Road Registry, Inc.` |

| `ZIP` | `Outer Falls, LLC` |

| `ZONE` | 澳大利亚 |

| `AU` | 德国 |

| `DE` | 芬兰 |

| `FI` | 日本 |

| `JP` | 英国 |

| `UK` | 美国 |

| `US` | `Deutschland` |

`![](img/2a18e06cd9c395e41f26ecba1fd_313.png)` **图 11.6** 互联网层次结构。

### 网络与互联

你可以使用 `ifconfig` 命令查看和设置网络接口，包括 IP 地址、`localhost`、子网掩码、广播地址和传输单元（`MTU`）。然而，该命令在大多数 Linux 系统中不再维护，被现代的 `ip` 命令取代。它可以用于安装后配置网络参数及其当前设置。在本节中，我们展示了用于查看各种接口的 `ip` 命令示例，以及用于检查和设置网络参数的 `ip` 命令示例。子网掩码（也称为 `subnet mask`）是 `TCP/IP` 用于识别主机是在远程网络还是本地子网的一个位。广播用于主机向子网上的所有主机或远程发送数据报。`TCP/IP` 网络中的 `MTU` 是 IP 数据报（包）的大小，是由用于连接其他主机的链路层决定的。以下是 `ip` 命令的一个示例，显示你登录到一个具有 `localhost` 接口以及网络接口 `enp0`、`enp1` 和 `enp2` 的主机，每个接口都有 `IPv4` 和 `IPv6` 地址。

```
$ ip addr show
1: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noque state UNKNOWN group default
    len 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00

    inet 127.0.0.1/8 scope host
        valid_lft preferred_lft forever
    inet6 ::1/64 scope host
        valid_lft preferred_lft forever
2: enp2:<BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc no state UP group default
    len 1000
    link/ether 00:18:30:ce:be:6e brd ff:ff:ff:ff:ff
    inet 202.147.169.195/24 brd 202.147.169.223 global enp2s
        valid_lft preferred_lft forever
    inet6 fe80::c67ab:4f1a:21fa:f0f5/64 scope link
        valid_lft preferred_lft forever
```

# 284

# Linux

```
valid_1ft forever preferred_1ft forever
3: enol:<BROADCAST,MULTICAST,LOWER_UP> mtu 1500 qdisc pfifo_fast UP
group default qlen 1000
link/64:51:06:49:70:46 brd:ff:ff:ff:ff:ff
inet 172.16.0.1/16 brd 172.165.255 global enol
valid_1ft forever preferred_1ft forever
inet6 fe80::e323:bbf4:9833:ceb0/64 scope link
valid_1ft forever preferred_1ft forever
```

你可以使用 `ip` 命令来显示有关特定接口的信息。例如，`ip show enol` 命令会显示相关接口的信息。系统管理员可以启用或禁用这些接口或其任何参数，正如第 17 章所讨论的。本章将进一步讨论输出内容以及获取和设置网络参数的各种选项。

`ip` 命令在 Linux Mint 中通常位于 `/bin` 和 `/sbin` 目录。如果你收到 `ip command not found` 的错误消息，你应该将相关目录包含在搜索路径中重新执行命令。你可以运行 `cat /etc/hosts` 命令来显示网络上主机的域名和 IP 地址。

你可以使用 `host` 命令对作为命令行参数传递的主机名进行 DNS 查询。在接下来，我们使用 `host` 命令显示名称的 IP 地址，反之亦然。例如，显示 `iasteate.berkeley`、`facebook.com` 以及与 IPv6 地址对应的域名。`host iasteate` 命令的输出显示了 `iasteate.Iowa State University` 的 IPv4 和 IPv6 地址。它还显示了爱荷华州立大学有十台机器处理电子邮件。第二个命令的输出显示 IPv6 地址属于 `thumb.iasteate`。第四个和第六个命令的输出显示了 `stanford.edu` 和 `facebook.com` 的 IPv4 和 IPv6 地址，以及域名服务器无法将 IP 地址 `198.175.93.39` 映射，这意味着该名称不存在。

```
$ host iasteate
iasteate.has has address 129.186.235.2
iasteate.has has IPv6 2610:130:101:113::
iasteate.mail is handled by 10 mailin.iasteate.com.
$ host 2610:130:101:113::
2.0.0.0.0.0.0.0.0.3.1.1.0.0.3.1.0.0.1.6.2.ip6.arpa
name redirect.its.iasteate.com.
$ redirect.its.iasteate.com
irect.its.iasteate.com has address 129.186.235.2
irect.its.iasteate.com has IPv6 2610:130:101:113::
$ stanford.edu
stanford.edu has address 177.61.267.215
stanford.edu has IPv6 address 2670:fed6:0925a::ab43:d7c8
stanford.mail is handled by 10 mxa-00000d3.gsl.pphosted.com.
stanford.mail is handled by 10 mkb-00000d3.gsl.pphosted.com.
$ host 2607:f140:082::110
0.1.0.0.0.0.0.0.0.2.8.0.0.0.0.0.0.0.0.4.1.f.7.0.6.2.ip6.arpa
name calweky-farm-prod.ist.berkeley.com.
$ host facebook.com
facebook.com has address 157.240.20.35
facebook.com has IPv6 address 2a02:2880:f1c8:8183:facebook:b00c:0:2de
facebook.com is handled by 10 msgin.vvv.facebook.com.
$ host 52.6.169.253
host 33.96.175.198-in-addr.arpa. not found: 3(NXDOMAIN)
253.169.52-in-addr.arpa domain name pointer ec2-52-6-169-253.compute-1.
amamazonaws.com.
```

## 网络与互联

在 Linux 系统上，你可以使用 `nslookup` 命令进行 DNS 查询。以下是命令的示例运行。

```
$ nslookup google.com
Server: 127.0.0.1
Address: 127.0.0.1#53

Nonauthoritative answer:
Name: google.com
Address: 216.58.208.78
```

同样，你可以使用 `dig` 命令在 Linux 上进行 DNS 查询。
