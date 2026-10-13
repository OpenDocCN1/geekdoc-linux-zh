
建立代理缓存内网基础设施的真正原因是管理控制。安全是一个大问题。一种方法是设置指向互联网的防火墙网关，使其仅在代理缓存之间路由流量。代理缓存可以做出智能路由决策。例如，Sun 在欧洲和美国都有连接到互联网。如果用户访问欧洲的网际站点，访问将通过本地连接进行路由。当访问美国的站点时，可以进行选择。路由可以通过 Sun 的私有网络连接到位于美国的网关，也可以直接连接到欧洲的互联网然后通往美国。第二种方案减少了昂贵的跨大西洋私有链路的负载，但如果欧洲连接中断，可以使用第一种方案作为备用。

## 58 资源管理

受限路由强制每个想要访问互联网的终端用户必须通过代理缓存进行。缓存根据 URL 和客户端 IP 地址（这通常足够识别终端用户）对每次访问进行路由和过滤逻辑处理。如果公司策略是“仅在工作时间内为业务用途提供互联网访问”，那么就可以识别出用非业务流量堵塞网络的员工。可能让员工知道他们的活动被记录并可以被追溯就足够了。发布一份工作期间访问次数最多的站点分析报告供大家查看，将起到警醒的作用。可以添加过滤以拒绝访问流行但不受欢迎的站点。

点在于，你拥有的昂贵广域网容量有限。终端用户倾向于耗尽你提供的所有容量。使用温和的同伴压力来保持使用高效且合理，可以从根本上提高网络实际运行的性能。

`Solaris Bandwidth Manager` 软件可以在环境中有效使用，根据所需的 URL、域名或协议混合情况实施策略。例如，如果到互联网股票报价服务器的流量挤占了公司内网广范围内更重要的流量，`Solaris Bandwidth Manager` 软件可以将对该站点的访问限制为总量的指定百分比。代理缓存控制与带宽结合是优化广域网和互联网网关带宽的一种强大且灵活的方法。

## 集群代理缓存架构

Apache 和 Netscape™ 代理缓存是传统 Web 服务器的扩展。它们被单独使用，尽管可以在分级缓存层次中使用，但缓存之间没有优化。另一种方案是集群缓存。Harvest 缓存是最初的开发产品，现在已成为商业产品。Squid 缓存是一个免费的衍生品，也是某些商业产品的基础。Squid 用于顶级的缓存安装，为非常大的互联网服务提供商提供跨区域的流量缓存。

集群缓存使用交换协议 `ICP` 相互通信，并形成显式的兄弟节点和父节点层次结构。如果负载会使单台机器崩溃，或者如果高可用性很重要，则将多个系统配置为兄弟节点。每个兄弟节点在缓存中存储数据，同时也使用 `ICP` 搜索其他兄弟节点的缓存。结果是：有效缓存大小是所有兄弟节点的总和，命中率得到提高，并且客户端访问哪个兄弟节点都没有关系。父子关系也形成了比单独层次更高效的结构，因为基于 `ICP` 的连接比单独的 HTTP 传输更高效。`ICP` 连接保持开启状态，传输的延迟更低。

在集群缓存架构中使用带宽管理，为缓存间协议赋予高优先级，以便在缓存产生大量网络流量时，缓存查询的响应时间不受影响。

## 虚拟 Web 托管

大量的个人和企业注册了自己的个人域名，并希望域名在互联网上激活并带有主页。在很多情况下，这些名称几乎活动，但它们被分配了固定的 IP 地址，并且某处的 Web 服务器必须对该地址做出响应。在 Solaris 环境中，可以在单个网络接口上配置多个 IP 地址。默认限制是每个接口 256 个虚拟地址，但已被扩展到每个接口 8000 个地址，并可能更高。使用 `ifconfig` 命令为接口分配 IP 地址，并在接口名称后加跟冒号来指定虚拟接口。使用 `ndd` 命令查询或设置虚拟地址的最大数量。

```
ifconfig -a
lo0: inet 127.0.0.1 flags=UP,BROADCAST,POINT,MULTICAST mtu 1684
inet 127.0.0.1 netmask 255.255.255
hme0: inet 192.168.1.10 flags=UP,BROADCAST,POINT,MULTICAST mtu 1684
inet 192.168.1.10 netmask 255.255.255.0
hme1: inet 192.168.1.11 flags=UP,BROADCAST,POINT,MULTICAST mtu 1684
inet 192.168.1.11 netmask 255.255.255.0
hme2: inet 192.168.1.12 flags=UP,BROADCAST,POINT,MULTICAST mtu 1684
inet 192.168.1.12 netmask 255.255.255.0
```

```
ndd -get /dev/ip_addrs_per_if
256
```

虚拟地址数量的限制在于在所有地址上运行 `ifconfig` 的时间。当配置了数千个虚拟地址时，重启时间会受到影响，这在高可用性场景下是一个重大问题。Solaris 2.6 操作系统环境经过优化以加速这一过程。

![](img/52144374747884a32fdddbed4e8cd9d7_93_0.png)

图 4-23 合整合 Web 服务器的资源管理

在图 4-23 中，Web 服务器被分配了 20 个份额（shares），这意味着如果数据库对处理器提出了过高需求，将保证至少获得 20% 的处理器资源。此外，如果 Web 服务器中的 `cgi-bin` 进程因内存泄漏而失控，整个系统不会耗尽交换空间；只有 Web 服务器受到影响。

## 在单个 Web 服务器内管理资源

通常需要使用资源管理来控制单个 Web 服务器内部的行为。例如，一个 Web 服务器可能被多个用户共享，每个用户都有自己的 CGI-BIN 程序。一个 CGI-BIN 程序中的错误可能会导致整个 Web 服务器运行变慢，或者在内存泄漏的情况下，甚至可能导致 Web 服务器崩溃。为了防止这种情况的发生，请使用进程级限制（per-process limits）。

| Web 服务器 | `/usr/lib/httpd` |
|---|---|

| `cpu.shares=20 shares` | Web Server, `httpd` |
| `memory=50 Mbytes` | 虚拟内存限制为 5 Mbytes |
| `process.memory=5 Mbytes` | `/cgi-bin/form.pl` |
| | CGI-BIN perf 程序限制为 5 Mbytes 虚拟内存 |
| | `/cgi-bin/lookup.sh` |
| | Shell 程序限制为 5 Mbytes 虚拟内存 |

图 4-24 单个 Web 服务器的资源管理

## 多个虚拟 Web 服务器的资源管理

单机通常托管多个虚拟 Web 服务器。在这种情况下，存在多个 `httpd` Web 服务器进程的实例，利用 SRM 软件进行资源控制的机会要得多。

你可以通过在 Web 服务器配置文件中设置参数，将每个 Web 服务器作为不同的 UNIX 用户 ID 。这有效地将每个 Web 服务器连接到 SRM 层次结构中不同的 Inode 上。例如，Solaris Web 服务器在配置文件 `/etc/http/httpd.conf` 中具有以下参数，如图 4-25 所示：

```
# Server parameters
server {
  server_root "/var/http/"
  server_user "webserver1"
  mime_file "/etc/http/mime.types"
  mime_default_type text/plain
  acl_enable "yes"
  acl_file "/etc/http/access.acl"
  acl_delegate_depth 3
  cache_enable "yes"
  cache_small_file_cache_size 8 # megabytes
  cache_large_file_cache_size 256 # megabytes
  cache_max_file_size 1 # megabytes
  cache_verification_time 10 # seconds
  comment "Sun WebServer Default Configuration"
}

# The following are the server wide aliases
map /cgi-bin/ /var/http/cgi-bin/ cgi
map /sws-icons/ /var/http/demo/sws-icons/ cgi
map /admin/ /usr/http/admin/

# To enable viewing of server stats via command line,
# uncomment the following line
map /sws-stats dummy stats
}
```

图 4-25 Solaris Web 服务器参数文件

通过将每个 Web 服务器配置为不同的 UNIX 用户 ID 运行，你可以为每个 Web 服务器设置不同的限制。这对于控制和核算托管许多 Web 服务器的机器上的资源使用特别有用。你可以利用大部分或所有的 SRM 资源控制和限制：

### 份额 [cpu.shares]

CPU 份额可以按比例为不同的 Web 服务器 分配资源。
