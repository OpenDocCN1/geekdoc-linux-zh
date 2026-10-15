
# 智能中继主机（可以为空）

DS

# 不允许出现在本地用户名中的操作符（即网络指示符）

CO %

# 仅包含点的类（用于识别标准名称）

C.

# 仅包含左括号的类（用于识别域名字面量）

C[

# access_db 接收类

C(Accept)OK RELAY

C(Res)OKR

# 允许中继的主机 ($=R)

FR-o `/etc/mail/relay-domains`

这里是 `sendmail.mc` 文件的引用作为对比：

```text
define(`SMART_HOST', `smtp.provider.provider')
define(`CONF_USER_ID', `8:122') dnl
define(`UOCP_RELAY') dnl
define(`BITNET_RELAY') dnl
define(`CAFOUTO_REBUILD') dnl
define(`CONFTO_CONNECT', `1m') dnl
define(`CONTRY_NULL_MX_LIST',true) dnl
```

你可以看出为什么该文件被描述为晦涩的。

复杂的邮件服务器设置不在本书的涵盖范围之内；关于此主题的更多信息，我们推荐 Costales 和 Allman 编写的《Sendmail, 3rd Edition》，这是一本关于 Sendmail 配置的 1200 页全面巨著。然而，以下五个章节将介绍常用选项。

## 配置伪装（Masquerading）

有时你可能希望 Sendmail 伪装成你系统实际主机名以外的主机。如果你拨号连接互联网且 ISP 为你处理所有邮件，就会出现这种情况。在这种情况下，你希望 Sendmail 伪装成你 ISP 的域名。例如：

```text
MASQUERADE_AS(`samplenet.org') dnl
```

## 使用智能主机（Smart Hosts）

如果你没有持续的互联网连接，你可能希望 Sendmail 将你的消息发送到 ISP 的邮件服务器并由其为你处理。在没有持续互联网连接的情况下，你可能会发现很难向某些位置交付消息（例如邮件服务不稳定且频繁的地区）。在这种情况下，你可以配置 Sendmail 通过传递给另一个服务器作为智能主机，而不是直接尝试交付。你可以在 `sendmail.mc` 文件中使用如下行来启用智能主机：

```text
define(`SMART_HOST', `samplenet.org')
```

此行告诉 Sendmail 将收到的任何邮件传递给服务器 `smtp.samplenet.org` 而直接交付。如果你的 ISP 像许多其他一样阻止任何邮件中继，智能主机将无法工作，因为中继经常被用于传播垃圾邮件。

## 设置投递间隔

如前所述，Sendmail 通常在接收到消息后立即尝试交付，并在间隔后再次尝试。如果你只有周期性的互联网连接（使用拨号连接），你可能希望 Sendmail 将所有消息留在队列中，并在特定的时间或提示时交付。你可以通过向 `sendmail.mc` 添加下几行来配置 Sendmail 这样做：

```text
define(`IVERY_MODE', `d')
```

此行导致 Sendmail 仅按计划的间隔尝试交付邮件（默认为 20 到 30 分钟之间）。然而，如果你长时间离线，这种延迟可能是不够的。在这种情况下，你可以使用以下命令调用 Sendmail，例如：

```bash
# sendmail -q3m
```

此行告诉 Sendmail 在启动时处理队列，并在你手动让它这样做时再次处理。如果你希望 Sendmail 在处理队列之前等待特定的提示，可以使用如下命令：

```bash
# sendmail -bd -q
```

> 提示：如果你通过调制调器联网，`/etc/ppp` 中有一个名为 `pppd.linkup` 的配置文件。当 PPP 守护进程启动时，该文件中的任何命令都会自动运行。当你拨号连接互联网时，你可以将 `sendmail -q` 添加到此文件中，以便自动处理你的邮件队列。

## 构建 sendmail.cf 文件

有很多书籍可以探索 Sendmail 配置的深度，但《Sendmail Installation and Operation Guide》是权威参考。也可以 Google 搜索找到配置指南；许多人在不同的配置中使用 Sendmail。幸运的是，Fedora 提供了一个开箱即用的默认 Sendmail 配置，只要你的网络配置正确且不需要 ISP 类的 Sendmail 配置。

在对 `sendmail.mc` 进行所有更改后，你必须重建 `sendmail.cf` 文件。首先，备份你的旧文件：

```bash
# cp /etc/mail/sendmail.cf /etc/mail/sendmail.cf.old
```

你必须通过 m4 处理器运行 `sendmail.mc` 以生成可配置文件。使用如下命令来实现此：

```bash
# m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```
