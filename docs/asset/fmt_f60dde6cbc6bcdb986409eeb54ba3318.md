
其中 `domain.com` 是你站点的域名，`nameserver` 之后的 IP 地址是你通信的 DNS 服务器地址。你可以有多多三个 `nameserver` 条目，系统会尝试每一个，直到其中一个返回响应。

# DNS 之前 - /etc/hosts

为你的站点配置 DNS 时，你需要熟悉以下工具：

- `named`
- 解析器库
- `nslookup`
- `traceroute`

`named` 是需要在 DNS 服务器上运行以处理查询的守护进程。如果它不能运行，职责是将请求转发到可以运行的服务器。除了查询外，`named` 还负责执行区域传输。区域传输是更改 DNS 信息在互联网上传播的方法。

# 配置 DNS 客户端：/etc/resolv.conf

网络中的每台机器都是 DNS 客户端。为了知道要使用哪个 DNS 服务器，你需要配置 `/etc/resolv.conf` 文件。该文件看起来应该是这样：

```
search domain.com

nameserver 192.168.42.1
```

其中 `domain.com` 是你站点的域名，`nameserver` 之后的 IP 地址是你通信的 DNS 服务器地址。你可以有多多三个 `nameserver` 条目，系统会尝试每一个，直到其中一个返回响应。

# 至少，你需要拥有以下条目：

- 本地 `localhost`
- 你的 NIS 服务器
- 任何挂载 NFS 的系统
- 主机本身

| IP Address | Hostname | Alias |
|---|---|---|
| 127.0.0.1 | localhost | |
| 192.168.42.7 | vestax | www |
| 192.168.42.8 | mailhub | mailhub.domain.com |
| 192.168.42.6 | technics | |

最左列是要解析的 IP 地址。下一列是主机名。随后的列都是该主机的别名。在第二行示例中，地址 `192.168.42.7` 是 `vestax` 的。`vestax` 的另一个名字是 `www`。

# 硬件连接与设备

`resolver` 库允许客户端程序执行 DNS 查询。该库被内置在 Linux 的标准库中。

`nslookup` 是一个从命令行调用的实用程序，用于确保查询的解析器和 DNS 服务器都已正确配置。`nslookup` 通过将主机名解析为 IP 地址，或将 IP 地址解析为域名来实现此。要使用 `nslookup`，只需将你想要解析的地址作为参数提供给 `nslookup`——例如：

```
nslookup r.domain.com
```

结果应该如下所示：

```
[root@root ~ # nslookup rame.domain.com

Server: numark.domain.com

Address: 192.168.42.1

Non-authoritative answer:

Name: rame.domain.com

Address: 192.168.42.8
```

`traceroute` 允许你确定数据包跨越你的网络和其他网络传输路径。这对于调试网络连接非常有用，特别是当故障排除位于他人的网络时。

使用 ICMP 协议（与 `ping` 相同），`traceroute` 会到达目标主机路径上的每台机器，并显示每个站点的相应名称和 IP 地址。每个名称旁边是到达目的地的三次往返花费的毫秒数。

要执行 `traceroute`，使用目标主机名或 IP 地址作为参数——例如，`traceroute www.hyperreal.org`

将返回如下的内容：

```
traceroute to hyperreal.org (204.62.130.147) 30 hops, 40 bytes packets

1  fe80::cr2.global.net (204.258.146.77) 0.829 ms 0.764 ms 0.519 ms

2  pos6::cr2.global.net (206.251.0.30) 1.930 ms 1.889 ms 1.887 ms

3  fe0-br2.global.net (206.251.5.2) 2.760 ms 2.779 ms 2.517 ms

4  sl-tk-17H0/3.sprinkler.net (142.228.144.9) 5.117 ms 6.160 ms 6.109 ms

5  sl-tk-14H0/3.sprinkler.net (142.228.144.9) 5.453 ms 5.985 ms 6.157 ms

6  sl-wired2-S0-T1.sprinkler.net (142.228.144.138) 10.987 ms 25.130 ms 11.831 ms

7  fs72-s0.wired.net (205.227.220.62) 30.453 ms 15.808 ms 21.220 ms

8  taz.hyperreal.org (204.62.130.147) 16.745 ms 13.018 ms
```

如果你以字符（如 `*`）代替主机名启动，那么该机器可能由于各种原因不可用（网络故障和防火墙拦截是最常见的）。请务必注意从一个站点到另一个站点所需的时间。如果你觉得连接变得异常缓慢，可能只是中间的某一个连接变慢了。

`traceroute` 也是衡量站点连通性的良好方法。如果你正在评估一个 ISP，可以尝试从其处进行 `traceroute`。

# TCP/IP 网络管理
第 13 章

## 配置 DNS 服务器

如前所述，DNS 有三种类型：主、从和缓存。

主 DNS 是这三种中最具权威性的。当 DNS 服务器是某个域名的主服务器时，它拥有该站点内所有主机的最新记录。

从 DNS 没有像主服务器那样权威。通常，离线 DNS 服务器被配置为从服务器，因此它们接收更新的速度没有主服务器快。从实际角度来看，它们具有权威性。

缓存 DNS 不是权威的。当第一次向缓存服务器发出查询时，查询会被转发到权威服务器。如果该服务器对查询域名具有权威性，结果将返回缓存服务器。缓存服务器将其保存在本地缓存中并继续返回该答案，直到目过期。

所有 DNS 服务器都应该配置为缓存功能。

根据你的站点配置，你可能不需要自己的名称服务器。例如，如果你连接到现有的网络，可能已经有一个供你使用的名称服务器。相反，如果你正在设置一个新的部门，你可能想为本地机器设置一个缓存服务器，以减轻你站点主服务器的负载。

![](img/421e47878893966b6e8fcf1c1c76141_287_0.png)

> 提示
如果你计划使用 PPP 连接，你绝对应该设置自己的缓存 DNS 服务器。这将减少 PPP 连接的负载。

# /etc/named.boot 文件

这是 `named` 启动时读取的文件。`named.boot` 文件中的每行都以关键字或分号（表示该注释）开头。该文件的格式如下：

- `;` 注释以分号开始
- `directory directory_name`
- `cache filename`
- `primary domain filename`
- `secondary domain ip_addr filename`
- `forwards ip_addr [...]`

`directory` 关键字告诉 `named` 配置中提到的文件名在系统中的位置。

`cache` 关键字让 `named` 执行缓存功能。`cache` 行末尾列出的文件包含了互联网上所有根 DNS 服务器的列表。这些根服务器用于预热 name 的缓存。你可以从根服务器获取最新的列表。

## 硬件连接与设备

第三部分

第四个值表示次级服务器，这些服务器缓存了该条目，如果无法联系到主服务器进行更新，则应在指定的秒数后丢弃该值。对于此项，一到两周是一个合适的值。

最后一个值是 `minimum` 条目，它告诉缓存服务器在无法联系到主 DNS 服务器时，在过期某个条目之前应该等待多久。对于该条目，五到七天是一个不错的范围。

不要忘记在第五个值之后放置一个右括号。

## NS–名称服务器

NS 记录指定了给定域名的权威名称服务器。该内容的示例行如下：

```
IN NS ns1.domain.com.

IN NS ns2.domain.com.
```

请注意，如果名称服务器的域名适用于当前的 SOA 记录，则你不需要在 DNS 记录中指定名称字段。

在此示例中，域名 `domain.com` 有两个名称服务器：`ns1.domain.com` 和 `ns2.domain.com`。这些是完全限定的主机名，因此它们需要句点后缀。如果没有句点，`named` 将它们的值评估为 `ns1.domain.com.domain.com`，这并不是你想要的结果。

## A–地址记录

地址记录用于提供从主机名到 IP 地址的翻译。对于所有希望具有已知主机名的机器，都应该有一个 A 记录。使用 A 记录的示例条目如下：

```
toybox IN A 192.168.42.59
```
