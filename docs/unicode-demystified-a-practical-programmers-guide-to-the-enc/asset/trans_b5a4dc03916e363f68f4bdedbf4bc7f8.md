

# 第 9 章 网络与互联网

traceroute 工具可以帮助你解决路由配置问题和路由路径故障。当你无法访问某个主机时，可以使用 traceroute 查看数据包的流向、到达了多远以及延迟是多少。

接下来的示例是从本地计算机到 www.linux.org 路由的 traceroute 输出。第一行告诉你路由的 IP 地址、将跟踪的最大跳数（hops）以及将使用的的数据包大小。每个带有数字的行都包含中间目的地的名称和 IP 地址，随后是数据包到该目的地往返一次所需的时间。traceroute 工具每个目的地显示三个数据包；因此每行有三个时间值。第 1 行显示了数据包发送到本地网关时的统计数据（小于 3 ms）。第 4-6 行显示它在到达圣何塞之前在山景（加利福尼亚州）之间跳转。在第 13 跳和第 14 跳之间，数据包跨越了美国（从旧金山到东部某地）。到第 18 跳时，数据包已找到 www.linux.org。当 traceroute 工具未收到响应时会显示星号（*）。每个星号表示它等待了三秒。

```
$ /usr/sbin/traceroute www.linux.org (198.182.196.253), 30 hops, 38 packets
1 gw.local.com. (204.94.139.265) 2.904 ms 2.425 ms 2.783 ms
2 coavad-gw2.meer.net (209.157.140.1) 19.727 ms 23.287 ms 24.783 ms
3 gw-mw1.meer.net (140.174.164.1) 18.795 ms 24.973 ms 19.207 ms
4 d1-4-2.002.us.ver.net (206.184.210.241) 54.948 ms 40.182 ms d1-10-0-0-200.a03.
   mtwca01.us.ver.net (206.86.25.183) 59.091 ms 39.485 ms
5 p1-1-0-a09.mtwca01.us.ver.net (209.157.181.166) 78.688 ms 66.266 ms 44.405 ms 49.362 ms
6 p1-12-0-a09.msj053.us.ver.net (209.157.181.166) 32.424 ms 93.337 ms 54.946 ms
7 sj003.us.ver.net (129.250.381) 38.952 ms 63.611 ms 43.496 ms 49.925 ms
8 mae-west1.US.CRL.NET (136.113.109) 48.532 ms 66.296 ms 38.999 ms
9 t3-3-0.us.crl.net (165.113.252) 139.808 ms 78.579 ms 68.699 ms
10 E0-CRL-SFO-02-E0X00.US.NET (165.113.252) 43.023 ms 51.910 ms 42.967 ms
11 sfo2-vta1.us.crl.net (205.134.254) 155.351 ms 154.606 ms 178.632 ms
12 mae-east-02.iix.ai.net (142.192.177.201) 202.852 ms 201.811 ms 204.560 ms
13 oc12-3-0.meer-east.iix.ai.net (205.134.161.2) 155.667 ms 219.16 ms
14 border-ai.inlogic.com (205.134.175.254) 214.622 ms * 190.423 ms
15 router.inlogic.com (198.182.196.224) 235.427 ms 228.856 ms 16 *
17 linux.org (198.182.196.253) 207.964 ms 178.683 ms 179.483 ms
```

# host 和通用：

host 工具通过主机名查找 IP 地址。它比 nslookup 更简单。例如，显示如何通过一个 IP 地址查找域名：

```
$ host 140.174.164.2
2.174.170.4 pointer=meer.net.
```

# 网络工具

dig 工具查询 DNS 服务器关于域的信息。dig 是功能强大的工具，具有许多功能，比 host 更复杂。以下 dig 使用关键字获取 any：

```
$ dig any update
;; DIG 9.1.3 >> update
;; global options: print
;; Got answer:
;; HEADER: opcode: QUERY, id: 30224; flags: qr ra; QUERY: 1; AUTHORITY: 7
;; QUESTION SECTION
update.edu. ANY

;; ANSWER SECTION
update.edu. 74567 NS dns.update.edu.
update.edu. 74567 NS dns.eng.edu.
update.edu. 74567 NS dns.acesag.update.edu.
update.edu. 74567 NS nr01.netmtgt.update.edu.
update.edu. 83413 SOA dns.update.edu. 2000106 3600 900 25920 86400
update.edu. 83438 MX 10 ducs6v.update.edu.
update.edu. 83438 MX 10 dserv3c.update.edu.
update.edu. 83438 MX 10 dserv6b.update.edu.
update.edu. 83438 MX 20 dserv3b.update.edu.
update.edu. 83438 MX 20 dserv3b.update.edu.

;; AUTHORITY SECTION
update.edu. 74567 NS dns.update.edu.
update.edu. 74567 NS dns.eng.edu.
update.edu. 74567 NS dns.acesag.update.edu.
update.edu. 74567 NS nr01.netmtgt.update.edu.

;; ADDITIONAL SECTION
dns.update.edu. 2867 IN A 192.168.2.10
dns.eng.update.edu. 68182 IN A 192.168.1.10
dns.acesag.update.edu. 132867 IN A 192.168.4.50
dns.update.edu. 160958 IN A 192.168.41.3
nr01.netmtgt.update.edu. 74567 IN A 192.168.251
ucs6v.update.edu. 83438 IN A 192.168.2.27
dserv3c.update.edu. 83438 IN A 192.168.2.148

;; Query time: 29 msec
;; SERVER: 140.174.162.4#53(140.174.162.4)
;; WHEN: Thu Feb 28 15:54:33 2002
;; MSG SIZE rcvd: 499
```

dig 工具显示了大量信息。

- Authority Section（权威部分）指定了主域名服务器，Additional Section（附加部分）指定了对应 Authority 部分名称的 IP 地址。
- SERVER 行（位于末）指定了本地系统使用的 DNS 服务器的名称和 IP 地址：这是 dig 获取信息的地方。
- 第二列指定了以秒为单位的 TTL（页 149）。
- 第三列的 IN 是查询类别，表示互联网类查询。
- 第四列的 SOA、MX、NS 或 A 指定了行包含的信息类型（DNS 查询类型）：
    - NS（名称服务器）记录指定了 upstate.edu 使用的名称服务器。只有在查询域时 NS 记录才有意义。
    - MX（邮件交换器）记录指定了你正在查询的域的邮件服务器。the. 域有多个邮件服务器。较低的偏好值是邮件优先级。the. 域有多个邮件服务器。
    - 给定域的 SOA（区域授权）。
    - 控制域的 TTL。
    - 控制另一个服务器何时刷新（refresh）。
    - 控制另一个服务器何时超时。
    - A（记录）指定了最后一列中的 IP 地址。

