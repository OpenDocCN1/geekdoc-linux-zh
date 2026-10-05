

# Linux TCP/IP 

inet_peer_maxttl tcp_keepalive_time tcp_synackretries
inet_peer_minttl tcp_low_latency tcp_syncookies
inet_peer_threshold tcp_max_orphans tcp_syn_retries
ip_default_ttl tcp_max_sstresh tcp_timestamps
ip_dynaddr tcp_max_syn_backlog
ip_forward tcp_max_tw_buckets udp
tcp_mem udp_rmem_min
tcp_moderate_rcvbuf udp_wmem_min
tcp_mtu_probing

neigh/
route/

许多名称中包含 rate（速率）和 max（最大）的变量用于防止默认服务攻击。`conf` 子目录下的变量是按接口设置的。它包含了所有默认配置的子目录以及每个接口（包括回环接口）的子目录。每个子目录都包含相同一组文件。

```bash
$ubuntu$ cd conf/default; ls -F
accept_redirect disable_policy promote_secondaries
accept_source_route disabled_xmrf proxy_arp
arp_accept force_igmp_version rp_file
arp_announce forwarding secure_retries arp_filter log_martians send_retries
arp_ignore mc_forwarding shared_media
boot_relay medium_id tag
```

如果你更改了 `conf/eth0` 子目录中的变量，那么该更改将仅适用于该接口。如果你更改了 `conf/all` 目录，你可能期望它能为所有现有接口应用对应的值，但事实并非如此。每个变量都有自己的规则来替换来自 `all` 的更改。某些值会与当前值进行 OR（或）运算，某些进行 AND（与）运算，其他则取最大值 MAX 或最小值。据我们所知，内核源码之外没有关于此过程的文档，因此保持整个默认设置可能是最好的。只需对单个接口的修改提供理由即可。

如果你更改了 `conf/default` 目录中的变量，新值将传播到稍后配置的所有接口。另一方面，将默认值作为未引用的信息保留也是好的；如果你想撤销其他更改，它们可以作为一个很好的健全性检查。

`/proc/sys/ipv4/` 目录也包含每个接口的子目录。每个子目录中的文件控制该接口的 ARP 表管理和 IPv6 邻居发现。以下是带有 gc（垃圾回收）的列表，它们决定了 ARP 条目的超时和丢弃。

```bash
$ubuntu$ cd conf/default; ls -F
anycast_delay gc_stat_time proxy_delay
app_solicit gc_thresh1 proxy_qlen
base_receive_time gc_thresh2 retrans_time
base_receive_ms gc_thresh3 retrans_time_ms
delay_first_probe_time locktime ucast_solicit
g_interval mcast_solicit un_qlen
```

# 第 14 章 TCP/IP 网络

要查看变量的值，请使用 `cat`；要设置它，请使用 `echo` 并重定向到相应的文件名。例如，命令

```bash
ubuntu$ cat icmp_echo_ignore_broadcasts
0
```

显示该变量的值为 0，意味着广播打印不会被忽略。要将其设置为 1（避免在遭受 Smurf 类型拒绝服务攻击时重试失败），请运行



```bash
ubuntu$ sudo sh -c "echo 1 > icmp_echo_ignore_broadcasts"
```

从 `/proc/sys/net` 目录执行。

通常你在调整这些变量时登录的是正在调优的网络，所以请小心！你可能会搞得很糟糕，导致需要从控制台重启才能恢复，如果系统恰好位于阿拉斯加州的 Point Barrow 且现在是 1 月，这可能会非常不便。在考虑调整生产机器之前，先在你的桌面系统上测试调整这些变量。

要永久更改这些任何参数（或更准确地说，在每次系统启动时重置它们），请将相应的变量添加到 `/sysctl`。`sysctl` 文件的格式是 `变量=值`，而不是你在从 shell 中手动更改变量时运行的 `echo value > variable`。变量名是相对于 `/proc/sys/` 的路径，如果你愿意，也可以使用点代替斜杠。例如，`/etc/sysctl.conf` 文件中的以下任意任意行

```
net.ipv4.forward=0
net/ipv4/ip_forward=0
```

将关闭此主机上的 IP 转发。

`/proc` 下的某些内容比其他部分有更好的文档。最好的方法是查看手册第 7 节相关协议的主页。例如

你也可以查看内核发行版中的 `/ip-sysctl.txt` 文件以获取一些良好的注释。如果你没有安装内核，只需谷歌搜索 `ip-sysctl.txt` 即可找到文档。

# 安全相关的内核变量

表 14.9 显示了 Linux 在处理非常敏感的网络问题时的默认行为。有关这些行为影响的简要描述，请参见第 472 页。我们建议你验证这些变量的值，以便你不挂载广播列表、不进行路由重定向且不接受。

* 18. 如果你以 `sudo echo 1 > icmp_echo_ignore_broadcasts` 的形式输入此命令，你只会产生一个“拒绝访问”的消息——你的 shell 在运行 `sudo` 之前就会尝试打开输出文件。你希望 `sudo` 应用于 `echo` 命令和重定向。因此，你必须创建一个 root 子 shell 来执行整个命令。

# Linux NAT 数据包过滤

源路由数据包。这些应该是经过源路由的。

## 表 14.9 Linux 中的默认安全相关行为

| 特性 | 主机 | 控制 |
| :--- | :--- | :--- |
| IP 转发 | 关闭 | /proc/ipv4/ip_forward |
| ICMP 重定向 | 开启 | /proc/ipv4/accept_redirects |
| 源路由 | 变化 | /proc/ipv4/accept_source_route |
| 广播 | 忽略 | /proc/ipv4/icmp_echo_ignore_broadcasts |

## Linux NAT 和过滤

Linux 传统上实现了网络地址转换 (NAT)，称为端口地址转换 (PAT)。在早期的 Linux 版本中是不可能的，但现代内核支持它。NAT 的功能有详细介绍。

要让 NAT 工作，必须启用连接跟踪模块。内核模块为：

```bash
ubuntu$ modprobe ip_conntrack
ubuntu$ modprobe ip_nat
ubuntu$ modprobe ipt_tables
ubuntu$ modprobe iptable_filter_conntrack
```

# Solaris 配置

## 14.13 Solaris 网络

 Solaris 提供了丰富的启动脚本。在一个展会上，我们曾获得过一个每天都有一个系统管理员问题的日历。1 月 1 日的问题是名称切换。尽管如此，让我们来看看 Solaris 网络配置。

## Solaris 基础网络配置

 Solaris 将一些网络配置文件存放在 `/etc`，另一些放在 `/etc/inet`。许多通过符号链接重复，实际文件位于 `/etc/inet`，而链接位于 `/etc`。要设置主机名，将其输入 `/etc/nodename` 文件。更改将在重启机器后生效。某些使用短主机名；另一些使用完全域名。

`/etc/defaultdomain` 文件命名暗示可能用于指定 DNS 域，但它标识的是 NIS 或 NIS+ 域。DNS 域像通常一样指定在 `/etc/resolv.conf` 中。

 Solaris 使用 `/etc/nsswitch.conf` 来设置 `/etc/hosts`、NIS、NIS+ 和 DNS 的配置顺序。我们建议查看 hosts 文件，以便启动。nsswitch.conf 中的行可以是

```
hosts: dns
```

如果主机通过 DHCP 获取 DNS 服务器地址，这就是默认配置。

 Solaris 网络可以以传统模式运行，也可以以“网络自动魔法”（NWAM）模式运行，由 nwamd 守护进程管理网络。NWAM 模式适用于工作站，但它的配置有限且仅允许一个网络接口处于活动。下面的讨论假设使用传统模式。

要查看激活的网络模式，运行 `svcs svc/network/physical`。应该有两个配置行，一个对应 NWAM，另一个对应传统的。

关于名称切换的信息请参见第 739 页。

