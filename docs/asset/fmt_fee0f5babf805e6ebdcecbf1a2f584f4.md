
而且 `ns.linux.bogus` 的地址是 `127.0.0.2`。看起来不错。

## 4.3 结语

当然，这个域名是完全虚假的，它包含的所有地址也是如此，而且遗憾的是，这可能稍微有点令人困惑。关于真实域名的真实示例，请参下一节。

## 5 真实域名示例

在这里我们列出一些真实的区域文件（zone files）

用户建议我在解释中包含一个运行中域名的示例，因为我之前对运行域名与虚假示例之间区别的说明不太清楚。

这个示例有一点需要：不要进入你的名称服务器！它仅供阅读参考。如果你想实验这个虚假示例，我是在获得 `LAND-5` `David Bullock` 的许可后使用此示例的。这些文件创建于 1996 年 9 月 24 日，现在查询 `LAND-5` 的名称服务器，结果可能与你看到的有所不同。另外，记住：删除开头的空格 `;`-

### 5.1 /etc/named.boot (或 /var/named/named.boot)

在这里我们找到了两个反向区域的主行：`127.0.0` 网段，以及 `LAND-5` 的 `206.6.177` 子网。以及 `land-5` 正向区域 `land-5.com` 的主行。请注意，他没有像我在这个 HOWTO 中那样将文件放在 `pz` 目录中，而是将它们放在一个名为 `zone` 的目录中。

```
; Boot file for LAND-5 name server

;

directory /var/named

; type                               source file or host

cache                                     root.cache

primary          0.0.127.in-addr.arpa  zone/127.0.0

primary          177.66.206.in-addr.arpa  zone/206.6.177

primary          land-5.com                 zone/land-5.com
```

### 5.2 /var/named/root.cache

记住这个文件是动态的，这里列出的是旧的。你最好使用现在通过 `dig` 生成的文件。

```
<<>> Dig 2.1 <<>>

;; res options init recur defnam dnscr

;; got answer:

:>>HEADER<< opcode: QUERY, status: NOERROR, id: 6

;; flags: qr rd da Ques: 1, Ans: 9, Auth: 0, Add: 9

;; QUESTIONS:

  , type = NS, class = IN
```

```
; ANSWERS:

518357 NS H.ROOT-SERVERS.NET

518357 NS B.ROOT-SERVERS.NET

518357 NS C.ROOT-SERVERS.NET

518357 NS D.ROOT-SERVERS.NET

518357 NS E.ROOT-SERVERS.NET

518357 NS I.ROOT-SERVERS.NET

518357 NS F.ROOT-SERVERS.NET

518357 NS G.ROOT-SERVERS.NET

518357 NS A.ROOT-SERVERS.NET
```

```
; ADDITIONAL RECORDS:

H.ROOT-SERVERS.NET 165593 A 128.63.253

B.ROOT-SERVERS.NET 165593 A 128.9.0.107

C.ROOT-SERVERS.NET 222766 A 192.33.4.12

D.ROOT-SERVERS.NET 165593 A 128.8.10.90

E.ROOT-SERVERS.NET 165593 A 192.203.230.10

I.ROOT-SERVERS.NET 165593 A 192.36.148.17

F.ROOT-SERVERS.NET 299616 A 192.5.5.241

G.ROOT-SERVERS.NET 165593 A 192.112.36.4

A.ROOT-SERVERS.NET 165593 A 198.41.0.4
```

```
; Total query time: 20 msec

;; FROM: land-5 to SERVER: default ---- 127.0.0.1

;; WHEN: Fri Sep 20 10:11:22 1996

;; MSG SIZE sent: 17 rcvd: 312
```

### 5.3 /var/named/zone/127.0.0

只有基础内容、强制性的 `SOA` 记录，以及一个将 `127.0.0.1` 映射到 `localhost` 的记录。两者都是必须的。文件中不应该有更多内容了。除非名称主机发生变化，否则它可能需要更新。

```
@ IN land-5.com. root,land-5.com.

    19960203 : Serial

    28800 : Refresh

    7200 : Retry

    60480 : Expire
```

### 5.4 /var/named/zone/land-5.com

在这里可以看到 `SOA` 记录、需要的 `NS` 记录。我们可以看到它有一个 `ns2.psi.net` 备用服务器。我们还可以看到有一个名为 `land-5` 的主主机来处理所有服务。从 `SOA` 记录来看，`root@land-5.com` 是另一个联系地址。序列号格式如下：记住序列号必须单调递增，这里只有在明天你才能再次编辑文件。考虑使用两个数字。

| Type | Class | Value |
| :--- | :--- | :--- |
| `NS` | `IN` | `land-5.com.` |
| `NS` | `IN` | `ns2.psi.net.` |
| `MX` | `IN` | `10 land-5.com.` |
| `A` | `IN` | `127.0.0.1` |
| `A` | `IN` | `206.6.177.1` |
| `CNAME` | `IN` | `land-5.com.` |
| `CNAME` | `IN` | `land-5.com.` |
| `CNAME` | `IN` | `land-5.com.` |
| `CNAME` | `IN` | `land-5.com.` |
| `CNAME` | `IN` | `land-5.com.` |
| `A` | `IN` | `206.6.177.3` |
| `CNAME` | `IN` | `funn.land-5.com` |
| `TXT` | `IN` | `"LAND-5 Corporation"` |
| `A` | `IN` | `206.6.177.200` |
| `MX` | `IN` | `10 land-5.com.` ; Primary Host |
| `A` | `IN` | `206.6.177.201` |
| `MX` | `IN` | `10 land-5.com.` ; Primary Host |
| `A` | `IN` | `206.6.177.202` |

### 5. 真实域名示例

```
ws_177203      MX      10 land-5.com. ; Primary Host

ws_177203      A       206.6.177.203

ws_177204      MX      10 land-5.com. ; Primary Host

ws_177204      A       206.6.177.204

ws_177205      MX      10 land-5.com. ; Primary Host

ws_177205      A       206.6.177.205

               ; {Many repetitive definitions - SNIP}

ws_177250      A       206.6.177.250

ws_177250      MX      10 land-5.com. ; Primary Host

ws_177251      A       206.6.177.251

ws_177252      MX      10 land-5.com. ; Primary Host

ws_177252      A       206.6.177.252

ws_177253      MX      10 land-5.com. ; Primary Host

ws_177253      A       206.6.177.253

ws_177254      MX      10 land-5.com. ; Primary Host

ws_177254      A       206.6.177.254

                               10 land-5.com. ; Primary Host
```
