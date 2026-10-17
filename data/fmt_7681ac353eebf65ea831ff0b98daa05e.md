
你可以通过紧跟在 `-G` 选项后的命令行参数来微调几个与灰名单相关的参数。

## 为什么灰名单之所以有效

为了让核心服务（如 SMTP 邮件传输）具有容错能力，人们投入了大量的设计和开发努力。在实际上，这意味着像 SMTP 这样的服务的“尽力而为”（best effort）已经尽可能接近消息投递的完美记录。这就是为什么我们可以依靠灰名单来最终从正确的服务器接收邮件。

互联网邮件传输的当前标准定义在 RFC 5321 中。以下是第 4.5.4.1 节“发送策略”的几个节选：

> “在典型系统中，编写消息的程序具有某种方法来请求对新发出的邮件进行立即关注，而无法立即传输的邮件必须排队并由发送者定期检索……”
>
> “发送者在一次尝试失败后，必须延迟重试特定目标。通常情况下，重试间隔应该至少为 30 分钟；然而，当 SMTP 客户端能够确定未投递的原因时，更复杂且多变的策略将是有益的。”
>
> “重试将持续到消息传输成功或服务器放弃为止；放弃时间通常需要设置为 4-5 天。”

投递邮件是一个协作的、尽力而为的过程，RFC 明确指出，如果你正尝试向目前无法接收的报告发送邮件，那么你的责任（一项要求）是稍后重试，给接收服务器一个从其问题中恢复的机会。

灰名单的巧妙之处在于它是一个方便的“缓兵”。当我们声称遇到了临时的本地问题时，该问题实际上等同于“管理员告诉不要和陌生人交谈”。带有有效消息的发送者会再次调用，但垃圾邮件发送者不会等待重试，因为这增加了他们投递消息的成本。这就是为什么灰名单仍然有效，而且由于它是基于对标准的严格遵守，¹ 误报（false positives）非常罕见。

¹ RFC 5321 的相关部分与 RFC 2821（后者已废弃）的相关部分相同。从这些中我们感到非常失望，IETF 没有澄清这些文本片段，而它们现在正沿着标准轨道向前。我的反应（实际上，这是一段吐槽）见于 `http://bsdly.blogspot.com/2008/10/ietf-failed-to-account-for-greylisting.html`。

² 相关的 RFC 主要是 RFC 1123 和 RFC 5321，它们使早期的 RFC 2821 废弃。记住，临时拒绝是 SMTP 的容错特性。

冒号分隔的列表 `2:4:864` 代表 passtime、greyxep 和 whiteexp 的值：

- `passtime` 表示 spam 认为重试前合理时间的最小分钟数。默认是 25 分钟，但在这里我们使用
- `greyxep` 是条目在从灰名单移除保留的小时。
- `whiteexp` 决定白名单保留的小时。`greyxep` 和 `whiteexp` 的默认值分别为 4 小时和 864 小时（一个月）。

## 灰名单的实践

实施灰名单的站点用户和管理员认为灰名单可以显著降低他们任何内容过滤的负载。我们将通过日志文件查看灰名单的状况。如果你使用 `-v` 命令行选项进行详细日志，你的日志将包含 IP 地址之外的更多项目。在详细日志的情况下，典型的日志如下：

```
Oct 2 19:53:21 delilah spam[26905]: 65.210.185.131: connected (1/1), lists: spews1

Oct 2 19:55:04 delilah spam[26905]: 83.213.115: connected (2/1)

Oct 2 19:55:05 delilah spam[26905]: 83.213.115: (GREY) <gilbert@keyholes.net> -> <wkit8zpu.fs@datadok.com>

Oct 2 19:55:05 delilah spam[26905]: 83.213.115: disconnected after 0 seconds.

Oct 2 19:55:05 delilah spam[26905]: 83.213.115: connected (2/1)

Oct 2 19:55:06 delilah spam[26905]: 83.213.115: (GREY) <gilbert@keyholes.net> -> <wkit8zpu.fs@datadok.com>

Oct 2 19:55:06 delilah spam[26905]: 83.213.115: disconnected after 1 seconds.

Oct 2 19:57:07 delilah spam[26905]: 65.210.185.131: (BLACK) -bounce-3c7E0A4/branch1.summer-bargain.com -> <datadok.com>

Oct 2 19:58:50 delilah spam[26905]: 65.210.185.131: From: Insurance Savings <notify@branch1.summer-bargain.com>

Oct 2 19:58:50 delilah spam[26905]: 65.210.185.131: To: adm@datadok.net Subject: SAVING MONEY on Auto Insurance

Oct 2 20:00:05 delilah spam[26905]: 65.210.185.131: disconnected after 4 seconds. lists: spews1

Oct 2 20:03:48 delilah spam[26905]: 222.240.6.118: connected (1/0)

Oct 2 20:03:48 delilah spam[26905]: 222.240.6.118: disconnected after 0 seconds.

Oct 2 20:06:51 delilah spam[26905]: 24.711.110.12: connected (1/1), lists: spews1

Oct 2 20:07:00 delilah spam[26905]: 221.196.37.249: connected (2/1)

Oct 2 20:07:12 delilah spam[26905]: 221.196.37.249: disconnected after 21 seconds. lists: spews1
```

第一行是来自 spews1 黑名单机器的连接开始。接下来的六行显示了来自另一台机器的两次尝试的完整记录，每次都是作为第二个活动连接的。这第二台机器尚未在该黑列表中，因此被列入灰名单。在灰名单机器尝试投递的消息中，有一个相当奇怪的投递地址（`wokit982psu@datalok.no`）。这里的技巧将在第 109 页的“灰名单陷阱”中介绍。地址之前的（GREY 和 BLACK）表示灰名单或黑名单状态。黑名单主机有更多活动，稍后我们看到在 404 秒（6 分 44 秒）后，黑名单主机在未完成投递的情况下就放弃了。

其余行显示了几个非常短的连接，包括一个来自单独黑名单机器的连接。然而，这次机器快速连接以查看 SMTP 对话开始时的任何 (BLACK) 标记，但我们在最后看到了对列表（spews1）的引用。大约 400 秒大约是灰名单垃圾邮件发送者挂起的时间（根据来自各个网站的数据以及完成 EHLO 对话所需的时间（以每秒 1 字节的速率）。然而，在查看日志时，你会发现一些挂起更长的垃圾邮件发送者。例如，在我们的网关数据中，有一条日志如下：

```
Dec 11 23:57:24 delilah spam[32048]: 69.640.26: connected (1/1), lists: spamhaus spews1 spews2

Dec 12 00:30:08 delilah spam[32048]: 69.640.26: disconnected after 1964 lists: spamhaus spews1 spews2
```

## 跟踪你的真实连接：spamlog

在后台，很少被提到且几乎没有文档记录的是 spam 最重要的辅助程序之一：spamlog 白名单更新器。它在后台运行，记录到你邮件服务器的连接以保持白名单更新。其想法是确保你通信的主机之间发送的邮件经过最少的麻烦。

> **注意**
>
> 如果你一直按照讨论进行到这里，spamlog 可能已经自动启动了。然而，如果你最初的 spam 配置没有包含灰名单，spamlog 可能没有启动，你可能会遇到奇怪的症状，例如灰名单和白名单没有正确更新。在启用灰名单后重启 spam 应该也能确保 spamlog 已加载并可用。

为了正常履行工作，`spamlogd` 需要记录进出你邮件服务器的 SMTP 连接，正就像我们在第 5 章的示例速率设置中所做的那样：

```
emailserver = "192.0.2.225"

pass log proto tcp to $emailserver port $email

pass log proto tcp from $emailserver port smtp
```

在 OpenBSD 4.1 及更高版本（以及对应版本）中，你可以创建多个 pfig 接口并指定规则的位置。以下是将 `spamlogd` 需要读取的数据与其余 PF 日志分离的方法：

1. 使用 `ifconfig pfiglog create` 创建一个独立的 pfiglog 接口，或创建一个仅包含 `up` 一行的 `hostname.pfiglog` 文件。
2. 将规则更改为如下：

```
pass log (pfiglog) proto tcp to $emailserver port $email

pass log (pfiglog) proto tcp from $emailserver port smtp
```

3. 在 `spamlogd` 的启动参数中添加 `-1 pfiglog`。

这将 spamd 相关的日志与其他部分隔离开。（关于日志请参阅第 9 章）

一旦上述规则生效，`spamlogd` 将允许接收你发送的邮件的 IP 地址进入白名单。这不能保证回复会立即通过，但在大多数配置中，它可以显著提高速度。

# 灰名单陷阱

我们知道垃圾邮件发送者很少使用完全符合标准的 SMTP 实现来发送信息，这就是为什么灰名单有效。我们也知道垃圾邮件发送者很少检查他们提供给劫持机器的地址是否可以投递。结合这些事实，如果你看到一个被灰名单化的机器尝试向你域名中的无效地址发送信息，那么该信息很有可能是垃圾邮件或恶意软件。

这种认识导致了垃圾邮件防护的下一个进化步骤——一种被称为“灰名单陷阱”的技术。当一个灰名单主机尝试向我们域名中的已知坏地址投递邮件时，该主机会被添加到名为 `spam-greytrap` 的维护黑名单中。`spam-greylist` 列表成员将受到与其他黑名单成员相同的每秒 1 字节的蜜罐惩罚。

`spam` 中实现的灰名单陷阱既简单又优雅。作为起点，你主要需要运行在灰名单模式下的 `spam`。另一个关键组件是你的服务器处理的域名中的地址列表，但仅包含你确定会收发合法邮件的地址。列表中的地址数量并不重要，但必须至少有一个，而上限主要取决于你想添加多少个地址。

接下来，你使用 `spamd` 通过灰名单陷阱功能来填充你的列表，然后坐在一旁观察。首先，发送者尝试向你灰名单陷阱列表上的地址发送邮件，对于任何你之前没有交换过邮件的发送者，仅仅会被灰名单化。如果同一台机器再次尝试（无论是使用无效地址还是灰名单陷阱列表中的另一个地址），就会触发陷阱，违规者将被放入 `spamd-greytrap` 并持续 24 小时。在接下来的 24 小时内，任何来自该陷阱的 SMTP 流量都将断断续续以每秒 1 字节的速度传输。

24 小时的时间不足以对合法流量造成严重干扰，因为真实的 SMTP 实现会持续尝试投递几天。该技术的经验表明，它很少产生误报。24 小时后继续发送垃圾邮件的机器很快就会再次回到蜜罐。

要设置你的陷阱，请使用 `spamd` 的 `-t` 选项。在我的案例中，之前“灰名单实践”中提到的那个奇怪地址就是包含在内的理想候选者：

```
$ sudo spamd -a wkitp982pu.fsf@dat.nok
```

我实际输入的命令是 `$ sudo spamd -T -a "cwkitp982pu.fsf@datadnok"`。在 OpenBSD 4.1 和更新后的版本中，`spamd` 不需要括号或引号，但它也能接受。

你可以根据需要添加尽可能多的地址。我倾向于通过查看灰名单和邮件服务器日志，寻找尝试投递到我域名中不存在的地址的失败报告，以此为我的本地垃圾邮件地址列表寻找新条目（是的，这听起来确实很疯狂）。

> 确保你添加到陷阱列表的地址是无效的且将保持无效。发现你把一个有效地址设为了垃圾邮件陷阱（即使是暂时的），没有什么比这令人尴尬了。

下面的日志片段显示了发送垃圾邮件的信息在第一次接触时被灰名单化，然后笨拙地返回投递到我添加到陷阱的地址，结果在几分钟内进入了 `spam-greytrap` 黑名单。我们知道在接下来的 20 小时内它会在那里：

```
Nov 6 09:50:25 delillah[23576]: 210.214.12.57: connected (1/0)

Nov 6 09:50:32 delillah[23576]: 210.214.12.57: connected (2/0)

Nov 6 09:50:40 delillah[23576]: (GREY) 210.214.12.57: <gilbert@keyholes.net> -> <wkitp982pu.fsf@datadnok>

Nov 6 09:50:40 delillah[23576]: 210.214.12.57: disconnected after 15 seconds.

Nov 6 09:50:42 delillah[23576]: 210.214.12.57: connected (2/0)

Nov 6 09:50:45 delillah[2357]: (GREY) 210.214.12.57: bounce-3C7E04B3@branch1.bargainz.com -> <admataped.no>

Nov 6 09:50:45 delillah[2357]: 210.214.12.57: disconnected after 13 seconds.

Nov 6 09:50:50 delillah[2356]: 210.214.12.57: connected (2/0)

Nov 6 09:51:00 delillah[2356]: (GREY) 210.214.12.57: <gilbert@keyholes.net> -> <kitip982pu.fs@fedataped.no>

Nov 6 09:51:00 delillah[2356]: 210.214.12.57: disconnected after 18 seconds.

Nov 6 09:51:02 delillah[2356]: 210.214.12.57: disconnected after 12 seconds.

Nov 6 09:51:08 delillah[2356]: 210.214.12.57: connected (2/0)

Nov 6 09:51:18 delillah[2356]: (GREY) 210.214.12.57: <gilbert@keyholes.net> -> <kitip982pu.fs@fedataped.no>

Nov 6 09:51:18 delillah[2356]: 210.214.12.57: disconnected after 16 seconds.

Nov 6 09:51:18 delillah[2357]: (GREY) 210.214.12.57: bounce-3C7E04B3@branch1.bargainz.com -> <admataped.no>

Nov 6 09:51:20 delillah[2356]: 210.214.12.57: connected (1/1), lists: spam-greytrap

Nov 6 09:51:23 delillah[2356]: 210.214.12.57: connected (2/2), lists: spam-greytrap

Nov 6 09:55:33 delillah[2357]: (BLACK) 210.214.12.57: <gilbert@keyholes.net> -> <kitip982pu.fs@fedataped.no>

Nov 6 09:55:34 delillah[2356]: (BLACK) 210.214.12.57: bounce-3C7E04B3@branch1.bargainz.com -> <admataped.no>
```

> 顺带一提，看起来垃圾邮件发送者甚至换了另一台机器发送，但“发件人”和“收件人”地址保持不变。他仍在尝试向一个从未投递成功的地址发送邮件，这一事实表明这个发送者并不查看他的列表。

### 使用 spamdb 管理列表

有时你可能查看或检查黑名单、白名单和灰名单的内容。这些记录位于 `/var/lib/spamdb`，管理员管理这些列表的主要接口是 `spamdb`。

早期版本的 `spamdb` 仅提供向数据库添加白名单条目或更新现有条目的选项（`spamdb -d nn.mm.nn.mm`）。你可以根据使用列表的缺陷或灰名单算法的影响删除白名单。最新版本的 `spamdb` 提供了更有趣的功能来支持灰名单。

### 更新列表

如果你在不带任何参数的情况下运行 `spamdb`，它会列出你的 spamdb 数据库内容，并允许你添加或删除 spamdb 地址和陷阱条目。你也可以动态添加白名单条目。

如果你想将一个主机添加到白名单，而不将其添加到永久 `nospam` 文件并重新加载规则集，你可以这样从命令行操作：

```
$ spamdb -a 213.187.179.198
```
