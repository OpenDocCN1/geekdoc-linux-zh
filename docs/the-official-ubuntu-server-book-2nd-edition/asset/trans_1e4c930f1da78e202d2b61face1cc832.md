

下面是 sar 命令的输出：

```
Linux 2.6.24-22-server (kickseed)    01/07/2009

08:05:01 PM  CPU   %user  %nice  %system  %iowait  %steal  %idle
08:15:01 PM  all   0.49   0.00   1.12     0.62     0.00    97.77
08:25:01 PM  all   0.49   0.00   2.15     1.21     0.00    96.16
Average:     all   0.49   0.00   1.63     0.91     0.00    96.96
```

如果你想从今天之外的某一天提取数据，只需使用 -f 选项后跟存储在 /var/log/sysstat 下的特定统计文件的完整路径。例如，要从当月第六天的统计数据中提取数据，我会输入

```
$ sar -f /var/log/sysstat/sa06
```

你可以使用其他任何 sar 选项来提取特定类型的统计数据，就像平常一样。

## Ganglia

当你想要查看数小时或数天前的系统情况时，本地监控非常有用，但缺点是你必须登录到每台主机并提取这些统计数据。此外，有时在有图表或其他可视化时，更容易判断系统的健康状况。有许多工具可以为服务器网络聚合统计数据，但其中最简单、最轻量的工具之一叫做 Ganglia。

Ganglia (http://ganglia.info) 被设计用于监控集群，并提供了一个很棒的轻量级守护进程 gmond，在每台主机上运行并通过多播 IP 地址将其统计数据广播给同一集群中的其他主机。我在这里说“集群”，但你并不需要拥有集群服务器才能使用 Ganglia。对于本章的其余部分，你可以将集群简单地视为按提供相同类型服务的方式对服务器进行逻辑分组的方式。由于特定集群中的所有主机都监听并与相同的多播地址通信，因此它们都可以感知彼此的健康状况。

除了监控守护进程 gmond 之外，Ganglia 还提供了一个名为 gmetad 的服务器，可以指向不同的集群，并将其数据聚合到本地 RRD 文件中。RRD 是小型统计数据库的常见格式，许多工具可以使用这些文件生成图表。Ganglia 本身提供了一个漂亮的基于 PHP 的 Web 前端，可以安装在你的 gmetad 主机上，它将为你提供访问各种统计图表的权限，这些图表可针对整个集群聚合，或深入到单个主机。

## 在所有主机上安装 ganglia-monitor

第一步是在你希望 Ganglia 监控的所有机器上安装 ganglia-monitor 包，该包提供了 gmond：

```
$ sudo apt-get install ganglia-monitor
```

gmond 程序期望不同的集群要么在不同的多播 IP 上通信，要么至少在不同的端口上通信。所有 gmond 配置都通过 /etc/ganglia/gmond.conf 文件完成。默认情况下 /etc/ganglia/gmond.conf 已设置为在多播 IP 239.2.11.71 和端口 8649 上通信。如果你只想为所有主机创建一个大型集群，你需要做的唯一配置更改是在 /etc/ganglia/gmond.conf 文件的 cluster 部分添加 name = "clustername"。在我的示例中，我将集群命名为 Ubuntu Cluster，因此我的部分如下所示：

```
cluster {
    name = "Ubuntu Cluster"
    owner = "unspecified"
    latlong = "unspecified"
    url = "unspecified"
}
```

将其添加到 gmond.conf 的底部并重启 ganglia-monitor 服务（sudo /etc/init.d/ganglia-monitor restart）。默认的 gmond.conf 充满了注释和示例选项，你可以设置这些选项。其中大多数选项允许你用位置、纬度和经度等可选信息标记特定集群。如果你确实决定运行多个集群，则需要更改 gmond 将要通信的多播频道或多播端口。你可以根据网络的简便性为每个集群更改其中一个或两个。一些管理员可能希望保持端口不变而更改 IP，以便其本地防火墙配置更简单。其他人可能希望保持 IP 不变而仅更改端口，以便他们可以将所有 Ganglia 流量保持在同一个多播 IP 上。在任何情况下，需要更改的选项都是 `udp_send_channel` 部分中的 `mcast_join` 和 `port`。以下是这两个选项均设置为默认值的一个示例：

```
```text
udp_send_channel {
  mcast_join = 239.2.11.71
  port = 8649
  ttl = 1
}
```
```

一旦你以想要的方式为集群配置了 gmond.conf，就将其部署到该集群中的所有剩余服务器，并在所有服务器上重启 ganglia-monitor init 脚本。如果你启用了任何防火墙，请确保它们允许来自多播 IP 的流量，并且还允许 TCP 和 UDP 端口 8649（或你设置的特定端口）上的流量。一旦 gmond 设置正确，你可以登录到特定主机并 telnet 到 localhost 的端口 8649，你应该会得到大量 XML 输出：

```
```xml
$ telnet localhost 8649
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
<?xml version="1.0" encoding="ISO-8859-1" standalone="yes"?>
<!DOCTYPE GANGLIA_XML>
<GANGLIA_XML VERSION="3.1.2" SOURCE="gmond">
  <CLUSTER NAME="unspecified" LOCALTIME="..." OWNER="unspecified" LATLONG="unspecified" URL="unspecified">
    <HOST NAME="..." IP="..." REPORTED="..." TN="..." TMAX="..." DMAX="..." LOCATION="...">
      <METRIC NAME="swap_free" VAL="88316" TYPE="uint32" UNITS="KB" TN="77" TMAX="180" DMAX="0" SLOPE="both" SOURCE="gmond"/>
      <METRIC NAME="os_name" VAL="Linux" TYPE="string" UNITS="" TN="612" TMAX="1200" DMAX="0" SLOPE="zero" SOURCE="gmond"/>
      <METRIC NAME="pkts_out" VAL="0.19" TYPE="float" UNITS="packets/sec" TN="93" TMAX="300" DMAX="0" SLOPE="both" SOURCE="gmond"/>
    </HOST>
  </CLUSTER>
</GANGLIA_XML>
```
```

