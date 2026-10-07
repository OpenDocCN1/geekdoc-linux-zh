
...了。如果你想使用 MAPS RBL 来拦截垃圾邮件，请在你的 Sendmail 配置中添加以下功能（`dnsbl`）：

# 功能(`dnsbl`)

启用此功能后，MAPS RBL 中列出的所有站点的邮件都将被拒绝。MAPS RBL 中列出了许多系统。MAPS 执行的是非常严格的策略。如果你没有正确配置 Send-mail，任何中继的站点（可能包括你的站点）都会被列入 RBL。RBL 是导致正确配置至关重要的原因之一。配置依赖错误会导致你的站点被加入黑洞列表（blackhole list）。如果一个站点停止中继，它将在一个月后从列表中移除。如果你的站点被加入 RBL，请按照 MAPS 网站上的说明申请将其移除。访问 maps.viz.com 网站获取更多关于 MAPS 系统的信息。

虽然启用 `dnsbl` 很简单，但它并不是一个完美的解决方案，因为你无法选择 RBL 中列出的哪些站点被拒绝。这是一个“全或无”的方案。事实上，这使得它的操作像开关灯一样简单。这意味着，你可能因为某个友好站点的管理员忘记关闭中继，就会被阻止接收来自该站点的电子邮件。出于这个原因，某些组织决定构建自己的基于 DNS 的黑洞列表。

`dnsbl` 功能接受两个参数。第一个是包含黑洞列表的域名名称。默认值为 `rbl.maps.viz.com`，这是 MAPS RBL 的所在地。将其指向你构建的自己的黑洞列表的域名。如果 DNS 管理员在 `dnsbl.foobirds.org` 中创建了此类列表，则以下命令将配置 Sendmail 使用它：

# 功能(`dnsbl`, `dnsbl.foobirds.org`)

为了这项工作，DNS 管理员需要在 DNS 服务器中放置正确的条目。黑洞条目仅仅是 DNS 记录。这些记录通过反转被黑名单系统的 IP 地址来为记录创建一个 DNS 名字字段，并使用地址 `127.0.0.2` 作为地址记录的数据字段。这种格式意味着主机是通过 IP 地址而不是名称被封锁的。例如，如果你想将 IP 地址为 192.168.72.37 的 `clueless.exploited.com` 列入黑名单，你需要在你的黑洞域名内为主主机 37.72.168.192 放置一个地址记录。来自 `dnsbl.foobirds.org` 区域文件的的一些示例黑洞条目如下：

- + 18.12.20.172.dnsbl.foobirds.org IN 127.0.0.2
- 16.31.31.172.dnsbl.foobirds.org IN 127.0.0.2
- 37.72.168.192.dns1.foobirds.org. IN A 127.0.0.2
- 9.200.168.192.dns1.foobirds.org. IN A 127.0.0.2

注意：要了解更多关于构建 DNS 区域文件信息，请参阅 Craig Hunt 编写的《Linux Server Administration》(Syybex, 2000)。

一旦创建了 DNS 区域并使用正确的 `dnsbl` 功能构建了 Sendmail 配置，就可以运行带有 `-bt` 的 sendmail 命令来测试新配置。列表 11.3 显示了 `dnsbl.foobirds.org` 域测试。

## 11.3 测试 dnsbl 功能

```
$ sendmail -bt Ctest-dnsbl.cf
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <address>
> .O<client_addr>172.168.12.1
> Basic_check_relay >
rewrite: ruleset 192 input: <>
rewrite: ruleset 192 returns: OK
> .O<client_addr>192.168.72.37
> Basic_check_relay >
rewrite: ruleset 192 input: <>
rewrite: ruleset 192 returns: $# error @ $ 5 . 7 . 1
  $: "550 Mail from " * 192 . 168 . 72 . 37
    refused by blackhole site dnsbl.foobirds.org*
```

>> "D"
`client_addr` 变量通常包含发起邮件连接的系统的 IP 地址。由于这是一个 `-bt` 测试，没有邮件连接，因此我们使用 `-D` 命令在 `client_addr` 变量中放置一个值。接下来，规则集 `Basic_check` 在没有输入输入地址的情况下使用的，这就是为什么焦点字符没有包含任何地址值的原因。`Basic_check_relay` 规则不处理输入地址；它处理在 `client_addr` 中找到地址。第一个测试返回 `OK`，显示本地地址 172.168.12.12 是接受的邮件源。接下来，地址 192.168.72.37 被存储在 `client_addr` 中并再次运行规则集 `Basic_check_relay`。该地址在 `dnsbl.foobirds.org` 中被找到。

虽然启用 `dnsbl` 很简单，但它并不是一个完美的解决方案，因为你无法选择 RBL 中列出的哪些站点被拒绝。这是一个“全或无”的方案。事实上，这使得它的操作像开关灯一样简单。这意味着，你可能因为某个友好站点的管理员忘记关闭中继，就会被阻止接收来自该站点的电子邮件。出于这个原因，某些组织决定构建自己的基于 DNS 的黑洞列表。

## 第 11 章停止垃圾邮件

... 错误信息是：
$$: "550 Mail from " * 192 . 168 . 72 . 37
    refused by blackhole site dnsbl.foobirds.org*
