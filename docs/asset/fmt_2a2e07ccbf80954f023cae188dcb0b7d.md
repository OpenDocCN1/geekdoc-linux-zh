
不要列出你不接受邮件的域名！Sendmail 认为它是任何列出域名的最终决定者，如果邮件无法本地投递，它将向发送者返回错误消息。在此处使用远程域名不会打扰任何人除了你的用户。

## 用户映射

现在 Sendmail 将接受该域的邮件，请告诉系统将域名地址发送到哪里。默认情况下，Sendmail 查找与邮件地址名称相同的账户。我的机器接收 `blackhelicopters.org` 和 `absolutefreebsd.com` 的邮件。默认情况下，Sendmail 将 `mwlucas@absolutefreebsd.com` 的邮件投送给本地用户 `mwlucas`，将 `mwlucas@blackhelicopters.org` 的邮件投送给本地用户 `mwlucas`。也许这是不同的人；理论上，用户 `mwlucas@blackhelicopters.org` 可能是 W. Lucas，与本人没有关系。我不想要他的邮箱，他也无法忍受我的邮箱。你无法阻止不同域名存在重名的用户邮箱名。解决方案是使用 Sendmail 并在虚拟用户表 `/etc/mail/virtusertable` 中建立账户映射。以下是一些示例条目：

| 邮件地址 | 本地用户/动作 |
| :--- | :--- |
| `stenchmaster@blackhelicopters.org` | `chris` |
| `postmaster@blackhelicopters.org` | `mwlucas` |
| `mwlucas@blackhelicopters.org` | `mwlucas` |
| `silence@blackhelicopters.org` | `error:nouser spambait address` |
| `@blackhelicopters.org` | `error:nouser no such user` |

第一条目将左侧特定的电子邮件地址映射到右侧的特定用户。发送到 `stenchmaster@blackhelicopters.org` 的邮件将投递到本地账户 `chris`。接两个条目将域名中的电子邮件地址路由到本地系统上的用户账户。第四条目稍微有趣一点，因为它向发送者返回错误。我希望系统对任何向 `silence@blackhelicopters.org` 发送邮件的人返回“no such user”（无此类用户）错误。当我必须为一个我知道会给我发垃圾邮件的人填写在线表单时，我会使用这个地址。我会激活几分钟来获取愚蠢的注册邮件，激活账户，然后再次屏蔽该地址。最后，最后一个条目是整个域名的通用规则。通过指定不带用户名的 `@blackhelicopters.org`，我告诉 Sendmail 将此规则应用于所有没有特定规则的地址。发送到此列表之外地址的邮件将收到“no such user”错误。

曾经，许多系统管理员为他们的域名使用全收（catch-all）邮箱地址，并动态创建电子邮件地址。“你想跟我聊天吗？这是你在我域名下的个人邮箱。”然而，现在垃圾邮件发送者会进行字典攻击，因此，指向真实人员账户的全收地址是拦截大量垃圾邮件的极佳方法。

## 字典攻击

字典攻击是指入侵者逐个尝试所有可能的名称。垃圾邮件发送者会通过尝试域名下所有可能的电子邮件地址来执行字典攻击。通过发送邮件到 `aardvard@yourdomain.com`、`aardv@yourdomain.com`、`aaron@yourdomain.com` 等，一直到字典末尾，垃圾邮件发送者希望某些垃圾邮件在发送出去之前能遇到真实的接收者。`/usr/share/dict/words` 中的列表包含 235,882 个单词；如果你的邮件服务器接受这些单词中的每一个作为你域名的有效邮箱地址并将其重定向到你的个人账户，你将别无选择只能删除邮箱，并在攻击期间没有人向你发送任何内容。

> ^3 当然，在现实生活中他们确实指向同一个人。但你明白我的意思了。

为你的其他虚拟域名创建类似的条目。要让 `mwlucas@absolutefreebsd.com` 和 `mwlucas@blackhelicopters.org` 指向不同的账户，只需在 `virtusertable` 中创建单独的映射：

| 邮件地址 | 本地用户 |
| :--- | :--- |
| `mwlucas@absolutefreebsd.com` | `michael` |
| `mwlucas@blackhelicopters.org` | `mwlucas` |

我建议按字母顺序列出你的域名，以在你在一台机器上拥有数千个域名时减少混乱。

与其他 Sendmail 配置文件一样，`sendmail(8)` 通过你必须保持更新的数据库访问 `virtusertable`。对 `virtusertable` 的更改在你不通过进入 `/etc/mail` 运行 `makemap` 更新数据库之前不会生效，就像你更新其他 Sendmail 数据库一样。

现在，只需为域名发布指向你邮件服务器的 MX 记录，你的电子邮件虚拟域名就准备就绪。

## 修改 sendmail.cf

还记得那个糟糕的配置文件 `/etc/mail/sendmail.cf` 吗？是的，你需要更改它。不要直接编辑 `sendmail.cf`，Sendmail 实际上包含了从其他配置文件构建此文件的工具。是的，按标准标准来看这很奇怪，但在 Sendmail 创建时它是尖端的。我向你保证它很年轻，人们称之为“酷炫老派”。

FreeBSD 包含两个 `.cf` 文件：`sendmail.cf` 和 `submit.cf`。`sendmail.cf` 文件配置 Sendmail 将邮件传输到其他系统以及运行中的入站 Sendmail 进程。Sendmail 仅在提交配置中使用 `submit.cf`，并且仅用于处理本地未发送邮件队列。`submit.cf` 实际上简单得多，如果你愿意在两个独立文件中工作：`freebsd.mc` 和 `submit.mc`。

`m4(1)` 命令从这些文件中读取指令，而定义是 `m4` 宏处理器的配置文件。存储在 `/usr/share/sendmail/` 中的指令实际上构建了 `.cf` 文件。你可以在 `.mc` 文件中定义 Sendmail 所需的行为，并使用 `m4` 从它们构建 Sendmail 配置文件。例如，让我们看看 `freebsd.mc`。

虽然文件以注释标记开头，但一旦开始实际配置，井号（`#`）就不再被使用；相反，`dnl` 用于注释任何你想让 `m4(1)` 忽略的内容。该文件中的某些行可能是显而易见的：

```
FEATURE(`access_db', `hash -o -TcmMPF /etc/mail/access')
...
FEATURE(`mailertable', `hash -o /etc/mail/mailertable')
FEATURE(`virtusertable', `hash -o /etc/mail/virtusertable')
```

## 垃圾邮件、蠕虫和病毒

黑名单？组织会因为该区块内一个或两个小网络的行为就把大块 IP 空间加入黑名单吗？如果是这样，该黑名单将阻止你接收来自这些 IP 块的邮件。这对你来说可能不是问题，但在为别人的邮件选择黑名单之前，你需要考虑所有这些因素。

在写本文时，我首选的反垃圾邮件工具是 Spamhaus（http://www.spamhaus.org/）。Spamhaus 创建于 1999 年，为低流量邮件服务器提供免费服务，为高流量站点提供廉价服务。ZEN 黑名单包括要被垃圾邮件发送者屏蔽的 IP 地址、分配给终端用户（拨号上网、DSL、电缆等）的地址（这些用户不应直接发送邮件），以及僵尸网络中的地址。这些地址中的任何一个都可能成为垃圾邮件、病毒甚至更糟东西的来源，通过拒绝来自这些地址的所有邮件，你可以大幅减少你的垃圾邮件负载。如果你使用 SSL 进行中继访问为客户提供主机服务（如下一节所述），ZEN 可能会阻止这些用户发送邮件。使用 SBL 而不是 ZEN。我们将在本节中使用 Spamhaus ZEN 服务作为我们的示例黑名单，但你可以使用任何你喜欢的黑名单。

默认的 `sendmail.mc` 包含一个示例黑名单条目：

```
dnl FEATURE(`dnsbl', `blacklist.example.com', `"550 Mail from " $&{client_addr} " refused - see http://example.com/"')
```

http://www.mail-abuse.org 默认黑名单对所有用户（甚至是低流量用户）都是付费服务，但它提供了黑名单配置的模板。检查你的黑名单以获取必要的主机信息，然后在以下添加规则，全部在单行内：

```
FEATURE(`dnsbl', `zen.spamhaus.org', `"550 Mail from " $&{client_addr} " refused - see http://www.spamhaus.org/zen/"')
```

我们将告诉基于 DNS 的功能，并检查域名 `zen.spamhaus.org` 的条目。我们还提供了自定义的拒绝信息，包括客户端的 IP 地址和指向信息的链接。

重新构建 `sendmail.cf`，重启 sendmail 以使黑名单生效，并观察你的邮件日志消息。被黑名单拦截的邮件出现在 `/var/log/maillog` 中，格式如下：

```
Jun 16 12:10:13 weildemaster sm-mta[40174]: ruleset=check_relay, arg1=82-46-225-100.cable.ubr04.duund.blueonder.co.uk, arg2=127.0.0.4, relay=82-46-225-100.cable.ubr04.blueonder.co.uk, reject=550 5.7.1 Mail from 86.26.225.100 refused - see http://www.spamhaus.org/zen/
```

这是你不想浪费任何时间处理的一类垃圾邮件。虽然黑名单并不完美，但它们可以大幅减少你的垃圾邮件负载。另一个强大的工具是灰名单，我们接下来将看到。

# 灰名单

黑名单提供了针对已知垃圾源的单方面保护。白名单记录了已知良好的邮件源。这两个陈述中的关键词都是“已知”。停止未知威胁比停止已知威胁要困难得多。灰名单提供了一个很好的折中方案，让你能够拒绝坏邮件并接受好邮件，同时帮助你将每个人归入这些类别之一。

大多数垃圾邮件源都尝试向许多收件者发送尽可能多的邮件。为了做到，它们使用了精简版的 SMTP 协议。特别是，大多数僵尸网络不会尝试多次发送邮件。真实的邮件服务器会尝试长达五天来发送合法邮件，而灰名单利用了真实邮件服务器与僵尸网络之间的这种差异，接受前者并拒绝后者。

垃圾邮件发送者会适应是真的，有些僵尸网络已经开始在几小时后重新发送邮件。好消息是，灰名单为黑名单维护者提供了识别新垃圾源的机会，并将源 IP 加入他们的黑名单，以利用他们的工作。

对灰名单的一个大意见是它会减慢合法邮件的传输。这在某种程度上是事实。邮件管理员可以将良好的 IP 地址和域名添加到白名单中，这是一个从不灰名单的邮件源列表。这样，来自你的客户和重要业务伙伴的邮件将立即通过。

你可以找到针对许多 MTA 的许多不同的灰名单实现。在我看来，最强大且实用的是 Bob Beck 的 `spamd(8)`。这个灰名单系统使用 PF 过滤器并可以做很多事情来减少垃圾邮件，但配置起来相对复杂。如果你的邮件服务器上运行 PF，你应该研究 `spamd(8)`。在这里，我们使用 `milter-greylist` (`/usr/ports/mail/milter-greylist`)，它更简单，但提供了几乎相当（但没那么惊艳）的结果。

> 我最喜欢的 PF/spamd 是流量整形，它让进入的垃圾邮件发送者突然降低到相当于 900 波调制解调器的速度。PF/spamd 可以让僵尸网络主机忙几天，同时几乎不消耗你的系统资源。最重要的是，当垃圾邮件试图向你发送邮件时，它并没有发送成千上万封垃圾邮件。这是在我了解它多年后仍让我微笑的极少数特征之一。

# 配置 milter-greylist

安装 `milter-greylist` 后，查看配置文件 `/usr/local/etc/greylist.conf`。这是一个标准的 Unix 风格配置文件，包含变量赋值，用井号表示注释。使用该配置文件指定超时时间、探测邮件更改器、白名单地址和收件人以及许多其他功能。我们在这里只讨论普通系统所需的特性。务必阅读 `greylist.conf(5)` 以获取灰名单的完整细节。`milter-greylist` 非常成熟，它可能支持你的特殊情况。

## 基础程序设置

在 `greylist.conf` 的顶部，你会发现一组基础程序设置。你可能不需要更改这些。

```
pidfile "/var/run/milter-greylist.pid"
socket "/var/milter-greylist/milter-greylist.sock"
dumpfile "/var/milter-greylist/greylist.db"
user null
```

`pidfile` 记录运行的 `milter-greylist(8)` 进程 ID。`socket` 是运行的 `sendmail` 守护进程通信的 Unix 套接字。`dumpfile` 是已识别邮件的数据库。当 `milter-greylist` 识别出新的垃圾邮件时，将其加入该数据库。最后，指定非特权用户运行 `milter-greylist` 守护进程。

## 访问控制列表

我不希望被灰名单处理的用户会被专门列入白名单，但所有其他邮件都将进行灰名单处理：

```
acl whitelist "my network"
acl whitelist "good domains"
acl whitelist "broken mta"
acl whitelist "spam lovers"
acl greylist default
```

第一条目允许来自 `my network` 列表中定义的 IP 地址的邮件。第二条允许来自 `good domains` 列表中列出的域名的所有邮件。第三条允许来自 `broken mta` 列表中定义的 IP 地址的所有邮件。第四条目指定了不会经历灰名单处理的用户——也就是说，他们可以立即接收所有邮件。最后一条对所有其他邮件进行灰名单处理，要求所有发送者在接受其提供的邮件之前证明它们是正规的邮件服务器。

## 灰名单时机

默认情况下，`milter-greylist` 有 30 分钟的重试要求。虽然垃圾机器人尝试在几分钟内重新传输垃圾邮件，但极少机器人会等待 30 分钟。随着计算机性能的提高，垃圾机器的行为会发生变化，如果看到后代重传的时间窗口越来越长，我不会感到惊讶。你需要调整临时失败的持续时间。在 greylist acl 中使用 `delay` 关键字来设置。你可以使用 `d`、`h` 和 `m` 分别代表天、小时和分钟。在这里我将挑战时长设置为两小时，在 2007 年是一个荒谬的长时间，但对于一两年后来说相当合理：

```
acl greylist default delay 2h
```

一旦邮件发送者通过了灰名单挑战，`milter-greylist` 会缓存发送者的身份三天，然后再次对其进行挑战。在此期间，来自该发送者的入站邮件不会被延迟。你可能还需要根据环境更改此超时时间。使用 `autowhite` 关键字来设置。在这里，我们将 `milter-greylist` 设置为允许发送者在 30 天内无需进一步挑战即可发送邮件：

```
acl greylist default autowhite 30d
```

原则上，灰名单挑战的时机很大程度上取决于你的环境。你可能会发现，五分钟的延迟足以满足你的反垃圾邮件需求，而不会过度延迟邮件；而其他人可能需要几小时的延迟才能可以接受地清理垃圾邮件。

## 将 milter-greylist 挂载到 Sendmail

`milter-greylist` 在 Sendmail 之外运行。如何让 Sendmail 与 `milter-greylist` 通信？关键在于 Sendmail 的 Milter 接口，它允许外部程序挂接到 Sendmail 并提供额外功能。

当你从 ports 安装 `milter-greylist` 时，你会看到关于如何挂载 Sendmail 并重建 `sendmail.cf` 的指令。通常，你向 `<hostname>.mc` 的末尾添加行并重建 `sendmail.cf`。例如，在编写此时，milter-greylist port 告诉我在我的邮件服务器的 `.mc` 文件中添加以下内容：

```
dnl MILTER MACROS
define(`confMILTER_MACROS_CONNECT', `j, {if_addr}')
define(`confMILTER_MACROS_HELO', `{verify}, {cert_subject}')
define(`confMILTER_MACROS_ENVFROM', `i, {auth_authen}')
define(`confMILTER_MACROS_ENVRCPT', `greylist')

INPUT_MAIL_FILTER(`greylist', `S=/var/milter-greylist/milter-greylist.sock, F=T, T=S:30s')
```
