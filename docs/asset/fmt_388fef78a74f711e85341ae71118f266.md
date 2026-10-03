
## 示例：俄罗斯域名服务器发送域名请求

在这些规则之后，以下是一个俄罗斯域名服务器向我们的网络发送域名请求时的发生示例：

```
$ sudo tcpcdump -lttfi pf0 port domain
tcpdump: WARNING: snaplen raised from 16 to 160
tcpdump: listening on pf0, link-type PFLOG
Sep 30 24:27:41.260190 212.5.66.14.53 > 194.54.107.53: [domain]
Sep 30 24:27:41.260253 212.5.66.14.53 > 194.54.107.53: [domain]
Sep 30 24:27:41.260267 212.5.66.14.53 > 194.54.107.53: [domain]
...
```

出于调试和监控目的，连接中的第一个数据包提供了足够的信息。然而，有时你可能想记录所有匹配规则的数据包。要做到这一点，请在你想要监控的规则中使用 `(all)` 选项。对我们的最小规则集进行此更改后，我们得到了如下：

```
block (all)

log (pass) quick trip out to port spp keep host
```

### 日志冗余说明

此选项会让日志变得冗余。为了说明 `log (all)` 生成了多少额外数据，我们将使用以下规则集片段，它允许域名查找和网络时间同步：

```
udp_services = "{ domain, ntp }"

pass log (all) inet proto udp to port $udp_services
```
