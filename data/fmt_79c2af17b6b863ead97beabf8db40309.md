
`ifconfig_fxp1_alias4="inet 64.41.132.165 netmask 255.255.255.255"`

`ifconfig_fxp1_alias5="inet 64.41.132.166 netmask 255.255.255.255"`

## 使用 `/etc/hosts` 文件将名称映射到 IP 地址

我们需要一种方法将主机名映射到 IP 地址。通常，这是通过 DNS 完成的，但我们尚未设置 DNS。在此期间，我们可以使用 `/etc/hosts` 文件为我们已知的主机（例如本地网络上的主机）提供映射。

`/etc/hosts` 允许你构建一个表，其中每个条目列出一个 IP 地址、其最常用（或“官方”）的主机名，以及任何别名（映射到同一 IP 地址的额外名称）。这些项目中的每一项都由空格或制表符分隔。在发起任何 DNS 查询之前都会先查询此表，因此 `/etc/hosts` 既充当 DNS 的备份（如果 DNS 不可用），也充当覆盖机制（如果 DNS 未提供正确信息）。别名甚至可以作为首选主机的快捷方式，以便你无需记住那些主机的名称，这与 shell 别名类似（我们在第 11 章“自定义 Shell”的“Shell 初始化文件”部分讨论过 shell 别名）。

以下是来自 `/etc/hosts` 的几行示例：

```
64.41.131.132          ns          ns.somewhere.com     lion.somewhere.com

64.41.131.133          www2        www2.somewhere.com

64.41.132.165          www3        www3.somewhere.com

114.235.123.11         www.foobar.com fred
```

有了这个表，你可以通过名称连接到列出的主机——无论是第二列中的“官方”名称还是第三列中列出的任何别名——即使无法连接到任何 DNS 服务器也是如此。

## 使用 `ping` 测试网络连接

在完成网络配置（无论是通过 `sysinstall` 还是通过 `/etc/netstart`）之后，你可以使用 `ping` 来确保设置是正确的。`ping` 程序是一个简单的基于 ICMP 的工具，它检查来自指定主机的回显，并报告每个数据包到达主机并返回所需的往返时间。

`ping` 的使用非常简单。你可以针对 IP 地址或主机名（或 `/etc/hosts` 别名）运行它，它会一直运行，直到你按 Ctrl+C 中断它：

```
# ping fred

PING fred (114.235.123.11): 56 data bytes

64 bytes from 114.235.123.11: icmp_seq=0 ttl=243 time=485.344 ms

64 bytes from 114.235.123.11: icmp_seq=1 ttl=243 time=351.589 ms

^C

--- fred ping statistics ---

2 packets transmitted, 2 packets received, 0% packet loss

round-trip min/avg/max/stddev = 351.589/418.466/485.344/66.877 ms
```

这是一个健康的 TCP/IP 配置，因为指定的主机对 ping 进行了响应。然而，如果主机不可达，ICMP 数据包将超时并报告连接失败。如果发生这种情况，说明你的配置有问题（或者，远程主机可能确实宕机了，因此请务必尝试多个目标主机）。以下显示了一次未能到达目标的 ping 尝试：

```
# ping 64.41.131.133

PING 64.41.131.133 (64.41.131.133): 56 data bytes

ping: sendto: Host is down

ping: sendto: Host is down

ping: sendto: Host is down

ping: sendto: Host is down

^C

--- 64.41.131.133 ping statistics ---

10 packets transmitted, 0 packets received, 100% packet loss
```

## 使用 `/etc/resolv.conf` 文件配置 DNS

要使用真正的 DNS，你需要访问至少一个域名服务器。这台服务器位于何处并不重要——大多数域名服务器都配置为允许来自互联网任何地方的查询，对发起查询的人员没有限制。然而，这种做法正在减少，在大多数情况下，你希望仅使用由你的 ISP 或企业网络管理员提供的域名服务器地址。

域名服务器在 `/etc/resolv.conf` 文件中指定，示例如下：

```
search somewhere.com

nameserver 64.41.131.132

nameserver 207.78.98.20

nameserver 64.40.111.102
```

`nameserver` 关键字指定域名服务器的 IP 地址；你可以拥有任意数量的此类条目，列出的顺序即为查询它们的顺序。如果一个服务器超时，则会查询下一个服务器。不过，许多应用程序对 DNS 查询有内部超时机制，这些查询会被传递给操作系统处理，因此，排在第三个或第四个位置之后的服务器可能不会带来太多额外好处。

`search` 关键字指定搜索域——即附加到非完全限定主机名后的字符串。例如，如果你执行 `nslookup www`，解析器会附加搜索域并针对 `www.somewhere.com` 执行实际查询。你可以在同一行中列出多个搜索路径：

```
search somewhere.com foobar.com cs1ab.ivy.edu
```
