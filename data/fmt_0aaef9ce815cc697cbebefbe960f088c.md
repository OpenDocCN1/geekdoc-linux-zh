
`MAIL_HUB` 和 `SMART_HOST` 行将入站和出站邮件导向 `smtp.sendmail.com`。DNS 中的 `MX` 记录应当协作，并将该主机的优先级列得高于单独机器（`MX` 记录中的数字越小优先级越高）。转发文件的路径被设置为为空，别名文件也设为空；所有别名扩展都在主机器上完成。这里指定了 `nocananify` 功能以节省时间，DNS 查询在主机器上进行。

### sendmail.com 的主机器

`sendmail.com` 的主机器可能是受攻击最频繁的 `sendmail` 安装之一。它必须尽力处理垃圾邮件，对人们提出的所有新邮件程序攻击保持安全，并保护其背后的机器。以下是它的配置文件：

```
divert(-1)
##### smi-master, katroo.mc, version 8.9.3
divert(0)
VERSIONID(@#)katroo.mc 2.1 (sendmail) 10/19/98)
OSTYPE('solaris2')
DOMAIN('generic')
MASQUERADE_AS(sendmail.com')
MASQUERADE_DOMAIN(sendmail.com')
undefined('BITNET_RELAY')
undefined('UUCP_RELAY')
define('CONFCHECK_ALIASES', 'True')
define(confCOPY_ERRORS_TO, 'Postmaster')
define(confEBINDIR, '/usr/lib')
define(confREFER_MODE, 'm')
define(confHOST_STATUS_DIRECTORY, '.hotstat')
define(confNO_RCP_ACTION, '')
define('MAIL_HUB', 'smtp.sendmail.com')
FEATURE('anonify)
define('SMART_HOST', 'smtp.sendmail.com')
define('conFORWARD_PATH', ' ')
MAILER(local)
MAILER(smtp)
```

# 第 19 章 电子邮件 595

请注意，通常出现在 `.mc` 文件开头的 `divert` 语句和注释在此处缺失。只有当在配置文件开头使用 shell 风格的 `(#)` 注释时，这些注释才是必要的。

此站点运行 `sendmail 8.9.3`，并使用了一些（8.10 以前的）配置行结构。其邮件负载导致许多性能参数远高于其默认值。

```
VERSIONID(@#)xor.mc.3 (trent) 3/29/99)
OSTYPE(@sunos.4)
```

```
define(PRIVACY_FLAGS, 'noexpn,norvry')
def(MESSAGE_TIMEOUT, '5d/72h')
def(MAILER_PATH, '/usr/bin/mail/local')

#### 为了性能和高负载负载这些值
def(conFMCL_CACHE_SIZE, '16')
def(conFMCL_CACHE_TIMEOUT, '10m')
def(CHECK_ALIASES, False)
def(DOMAIN_NAME, 'xor.com')
def(MAX_MESSAGE_SIZE, '5000000')
def(QUEUE_LA, 'Port-NNN')
def(REFUSE_LA, '30')
```

```
FEATURE(always_add_domain)
FEATURE(use_cw_file)
FEATURE(virtertable)
GENERIC_DOMAIN(xor.com)
FEATURE(generictstable)
FEATURE(masquerade_envelope)
FEATURE(redirect)
FEATURE(access_db, 'hash -o /etc/mail/access/')
```

```
MAILER(local)
MAILER(smtp)

LOCAL_RULESETS
##### 垃圾邮件和病毒检查规则已删除；见第593页
```

正如你从这些示例的多样性所示，设置配置文件没有唯一的正确方法。`sendmail` 包含了许多用于路由邮件和处理头部的结构。在某种程度上，选择取决于个人偏好，或者取决于复制该文件的个人是如何做的。

## 19.10 SENDMAIL 中的垃圾邮件相关功能

`Spam` 是垃圾邮件的术语，也称为未请求的商业性电子邮件。它已成为一个严重的问题，主要是因为发送者（至少在美国）不是按字节计费，而是为连接支付固定费用。或者，如果他们不按字节计费，他们发送一封有成千上万接收者的邮件，并通过另一台机器转发。另一台机器支付了昂贵的按字节成本，而垃圾邮件发送者只需支付一份费用。在许多国家，终端用户按接收的字节付费，并对为了接收垃圾邮件而付费感到愤怒。

垃圾邮件似乎主要是一个美国的问题。美国的营销文化发现了一个金矿并继续开发它。

美国的 `ISP` 已开始感受到垃圾邮件的影响，因为他们的支持热线必须处理越来越多源自客户的垃圾邮件滥用案例。科罗拉州的一家拥有约 150 个下游 `T1` 客户（许多是 `ISP`）的 `ISP` 需要一个兼职人员专门负责处理垃圾邮件投诉。

从营销人员的角度来看，垃圾邮件的效果很好。响应率高、成本低，且投递即时。一份包含 3000 万电子邮件地址的列表成本约为 40 美元。

许多垃圾邮件发送者试图通过这种建议来骚扰无辜的人：如果你想从邮件列表中被删除，请回复一封写有“remove”的邮件。虽然他们可能会删除你，但你只是向他们证实了他们拥有一个有效的、最近的电子邮件地址；这一事实可能会让你出现在其他列表中。垃圾邮件发送者还喜欢篡改他们的邮件头部，试图伪装邮件的发件人以及起源邮件的机器。

最近，将电子邮件地址提供给垃圾邮件发送者的人开始使用某种形式的字典攻击来获取未知地址。从常用名称列表开始，扫描软件添加不同的首字母，希望能命中有效的电子邮件地址。为了检查这些地址，软件会连接到例如 50 个 `ISP` 的邮件服务器，并对数百万地址中的每一个地址执行 `VRFY` 查询。

这种探测对你的邮件服务器及其投递客户合法邮件的能力有巨大影响。`sendmail` 可以通过使用 `PrivacyOption goaway` 来处理这种情况，该功能从第610 页开始介绍。但如果 `VRFY` 被拦截，他们会尝试 `EXPN`，如果两者都被拦截，他们会尝试 `RCPT`。他们可以尝试数百万个地址而可能永远不发送单封邮件——尽管这会让你的邮件服务器一直忙碌。

`sendmail` 添加了一些很好的功能来帮助控制垃圾邮件，并处理偶尔携带的邮件病毒。遗憾的是，大多数 `ISP` 必须通过所有邮件，因此这些功能对于客户策略来说可能过于严苛（或者，也许它们并不如此）。然而，这些功能在用户端可以产生很好的效果。

有四种垃圾邮件控制功能：

- 控制中继的规则，即离站用户使用你的邮件服务器向另一个离站用户发送邮件。垃圾邮件发送者经常利用中继来试图掩盖邮件的真实来源，从而避免其 `ISP` 的检测。它还让他们可以使用你的计算资源而节省他们自己的资源。这是致命的。
- 访问数据库，允许通过地址过滤邮件，而不是让电子邮件防火墙来完成工作。
- 黑名单，包含已知的垃圾邮件。
- 头部检查，这是一项允许过滤的强大功能。

我们将在接下来的章节中详细描述这些功能。

# 第19章 电子邮件 599

`promiscuous_relay` 功能允许从任何站点中继到任何其他站点。这是通往 Paul Pixie 黑名单列表的单程票。请勿使用此功能。

`relay_based_on_MX` 功能是有害的，因为你无法控制哪些站点被允许将其 `MX` 记录指向你。通常情况下，只有将 `MX` 记录指向你邮件服务器的主机是你自己，但没有什么能阻止其他站点更改其 `MX` 记录指向你。垃圾邮件发送者通常没有更改 `MX` 记录的能力，但某些阴暗的站点完全可以做到。

`loose_relay_check` 功能允许垃圾邮件发送者使用的“99% 黑客攻击”形式的地址格式。

`relay_local_from` 功能信任邮件信封上的发送者地址，并中继看起来源自本地地址的邮件。当然，邮件的信封和头信息都是轻易伪造的，而垃圾邮件发送者是伪造专家。

如果你考虑以某种形式开启中继，请查阅 `sendmail` 文档 `/README` 以确保你不会无意中成为垃圾邮件发送者的朋友。当你变成那样时，请让中继检查站点之一验证你是否无意中创建了开放中继——尝试 `orbs.org` 或 `abuse`。

在某些配置错误的情况下，你的主机可能会被说服解析滥用 `UUCP` 地址系统的奇怪地址。为了万无一失，如果你没有 `UUCP`（或 `BITNET` 或 `DECNet`）连接，你可以使用：

```
FEATURE('noucp')
undefined('UUCP_RELAY')
undefined('BITNET_RELAY')
undefined('DECNET_RELAY')
```

为了防止这种情况，对于这些行的良好做法是将它们放在你的 `DOMAIN` 文件中。
