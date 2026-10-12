
```bash
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

通过 `-D` 命令向 `client_addr` 变量赋值。

`client_addr` 变量通常包含发起邮件连接的系统的 IP 地址。由于这是一个 `-bt` 测试，没有邮件连接，因此我们使用 `-D` 命令在 `client_addr` 变量中放置一个值。接下来，规则集 `Basic_check_relay` 在没有输入地址的情况下使用，这就是为什么焦点字符没有包含任何地址值的原因。`Basic_check_relay` 规则不处理输入地址；它处理在 `client_addr` 中找到的地址。第一个测试返回 `OK`，显示本地地址 `172.168.12.12` 是接受的邮件源。接下来，地址 `192.168.72.37` 被存储在 `client_addr` 中并再次运行规则集 `Basic_check_relay`。该地址在 `dnsbl.foobirds.org` 中被找到。

虽然启用 `dnsbl` 很简单，但它并不是一个完美的解决方案，因为你无法选择 RBL 中列出的哪些站点被拒绝。这是一个“全或无”的方案。事实上，这使得它的操作像开关灯一样简单。这意味着，你可能因为某个友好站点的管理员忘记关闭中继，就会被阻止接收来自该站点的电子邮件。出于这个原因，某些组织决定构建自己的基于 DNS 的黑洞列表。

## 第 11 章 停止垃圾邮件

... 错误信息是：

```
$: "550 Mail from " * 192 . 168 . 72 . 37
refused by blackhole site dnsbl.foobirds.org*
```

### 创建反垃圾邮件访问数据库

访问数据库中条目的格式是容易的部分。决定具体要在数据库中放入什么则更困难。互联网上有一些组织收集关于垃圾邮件者的信息，这可能帮助你构建反垃圾邮件访问数据库。可以开始的几个站点有 `maps.viz.com`、`spam.abuse.net/spam/` 和 `www.mids.org/nospam`。这些站点是定位已知垃圾邮件者信息的起点。

当然，除了从在线垃圾邮件者列表中提取数据外，你还可以使用你喜欢的编辑器直接向访问数据库输入自己的条目。我发现这是简单的方法，对于响应我个人的垃圾邮件问题来说也最灵活。

如果你喜欢 `X Windows` 工具，你甚至可以使用 `linuxnuxconf` 来构建访问数据库。图 11.1 显示了使用 `linuxnuxconf` 创建的反垃圾邮件过滤器。

#### 图 11.1 使用 linuxnuxconf 创建访问数据库

![](img/9639113aa446fb8976cb3d377f7aafdd_334_0.png)

在窗口左侧，从 `linuxconf` `Anti-Spam Filters` 菜单中选择其中一项。共有四种可能的选择：

-   **设置拒绝的发送者**（`Setting Rejected Senders`）：`Setting Rejected Senders` 选择创建一个垃圾邮件过滤器。该选择打开 `Mail Rejected From` 选项卡。点击 `Add` 打开图 11.1 所示的选项卡。`Rejected Message` 选项卡是你定义垃圾规则的地方，包括邮件的来源以及发送给该来源的错误信息。图 11.1 显示来自 `we11junk.com` 的邮件将被拒绝，并带有错误信息“550 Junk is not accepted.”。这是 `linuxconf` 菜单中唯一能阻止邮件的选项。其他三个邮件过滤选择用于放宽邮件中继限制，以便你创建服务器。

-   **为 IP 设置“中继”**（`Setting ‘Relay’ for IP`）：使用此选择定义服务器应该中继邮件的主机或网络。通过 IP 识别主机或网络。这将为指定的主机启用邮件中继功能。

-   **为名称设置“中继”**（`Setting ‘Relay’ for name`）：使用此选择定义服务器应该中继邮件的主机或域名。通过名称识别主机或网络。

-   **设置中继到主机**（`Setting Relay to Hosts`）：此选择识别服务器应该中继邮件的远程主机。一种可能的用途是识别你的系统通过之中继的外部邮件服务器——例如你的公司邮件服务器。

当你点击 `Act/Changes` 按钮（代表激活更改）时，`linuxconf` 工具将为你构建访问数据库文件。`linuxconf` 会创建文本文件和实际的数据库。

如果你像我一样使用文本编辑器构建访问列表，那么你还必须手动构建数据库。使用 `Sendmail` 自带的 `makeup` 命令将文本文件转换为数据库。你还需要让 `Sendmail` 知道你有一个想要使用的访问数据库。使用 `access_db` 功能来完成此。关于构建访问数据库和配置 `Sendmail` 使用它的的详细信息，请参阅第 6 章。

访问数据库在选择地址方面为你提供的精细粒度控制，以及当地址匹配成功时你可以选择的各种操作，意味着访问数据库是大多数站点拦截垃圾邮件者的正确工具。但如果你需要对过程有更深层的控制，可以定义自己的 `Sendmail` 重写规则来处理邮件地址。

### 使用反垃圾邮件重写规则

大多数管理员将 `Sendmail` 重写规则视为修改源自本地系统用户邮件程序中出站邮件地址的方法。反垃圾邮件规则集允许你处理传入邮件的地址和标头。`Sendmail` 为你的个人规则提供了三个反垃圾邮件规则集。这些是：

-   `Local_check_relay`：这是一个规则集，你可以在其中定义处理正在中继邮件的规则。

-   `Local_check_rcpt`：这是一个规则集，你可以在其中定义根据收件地址处理邮件的规则。

-   `Local_check_mail`：这是一个规则集，你可以在其中定义根据发件者地址处理邮件的规则。

假设你一直在通过一个仅包含用户名的 `From:` 地址接收作为本地邮件的垃圾邮件。此外，假设你已经配置了邮件服务器，使得本地邮件的 `From:` 地址始终包含主机名。你可以使用 `Local_check_mail` 来如列表 11.4 所示检查发件者地址。

#### 列表 11.4 一个简单的反垃圾邮件规则集

```sendmail
SLocal_check_mail
# Check for user@host
RS$ $+ @$ #OK
RS$ #error: 55: Invalid From address
```

列表 11.4 的第一行是一个 `S` 命令，定义了将传入地址与 `Local_check_mail` 规则集进行规则。`R` 命令匹配模式 `$ $+ @$`，寻找一个或多个标记 (`$`)、一个字面量符号 (`@`) 和一个或多个标记。任何 `user@host` 格式的地址都匹配此模式。格式显示，如果地址匹配模式，则退出 (`$`) 并向调用规则集返回邮件程序名 `#OK`。邮件程序名 `#OK` 是一个虚拟用户，表示该地址是有效的。

第二个 `R` 命令匹配所有未能匹配第一个规则的地址。对于所有这些地址，规则返回邮件程序名 `#error` 和错误信息的文本。`#error` 邮件程序是一个特殊的邮件程序，它会将邮件连同错误信息返回给发件者。此的替代方案是使用 `#discard` 掩码，它会静地丢弃邮件。大多数管理员倾向于返回错误信息。

> 注意：列表 11.4 中的规则集只是一个教学示例，设计为易于解释且长度适中。它太简单了，无法有效处理地址和各种本地地址格式。

### 处理输入邮件标头

除了定义你的规则集外，你还可以从标头定义调用规则集，以检查系统接收到的标头格式。有时垃圾邮件者会使用格式不正确的标头来指示邮件是垃圾邮件。假设你受到某人的干扰，对方忘记创建一个看起来有效的 `Message-Id:` 标头。你可以使用如列表 11.5 所示的代码。

#### 列表 11.5 检查标头内容

```sendmail
LOCAL_RULESETS
Message-Id: $>check_MID_header

Scheck_MID_header
R$+ @ $\$OK
R$* $: 550: Invalid Header
```

`_RULESETS` 部分包含一个针对 `sendmail.cf` 文件的 `H` 命令。与我们在第 7 章中看到的 `sendmail.cf` 命令不同，它是被用来检查标头的。
