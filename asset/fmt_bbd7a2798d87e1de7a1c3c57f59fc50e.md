
SMTP 是基础电子邮件协议。SMTP 全称为简单邮件传输协议（simple mail transfer protocol），基于 TCP/IP 协议族。这是 `sendmail` 很好理解的语言，两个相关 `sendmail` 程序之间的节点通信实际上是对话的交换。

图 20.2 显示了标识为 `ms1.mydomain` 和 `ms3.yourdomain` 的两个主机之间这种通信（或者准确地说是对话）的简化表示。这两个主机直接通信。本地 `sendmail` 正在将本地主机上的本地用户 `me` 发出的电子邮件发送到远程主机上的用户 `you`（电子邮件地址为 `<you@ms3.yourdomain>`）。本地 `sendmail` 在传输邮件之前会传递发送者和收件人信息；地址信息构成信封，它与邮件头分开传递。信封中最多可以列出一个收件人，尽管同一封邮件……任何将“多地址”电子邮件拆分为多个“单地址”信封的操作都必须在地址解析时进行；SMTP 仅假设只有一个收件人。

![](img/849eeed37051e04ac7ecd9d56adb0ba2_472_0.png)

图 20.2：SMTP 的简化表示。

为了更深入地查看 SMTP 协议，后面是另一个使用 `*sendmail*` 详细模式的示例。详细模式列出了发送者和收件人主机上两个 `*sendmail*` 程序之间的完整对话。在这个示例中，邮件消息由发送者 `<bil@patsy.mys.scps.edu>` 发送给收件人 `<mis@apollo.ph.mys.scps.edu>`：邮件文本位于名为 `"indata.mail"` 的文件中。再次，两个主机直接通信（在电子递递中没有中继邮件主机）。

```
/usr/lib/sendmail -v mis@apollo.ph.mys.scps.edu < indata.mail
mis@apollo.ph.mys.scps.edu. Connecting to apollo.ph.mys.scps.edu via ether...
trying 146.98.8.3... connected.
220 apollo.ph.mys.scps.edu HP Sendmail (1.38.193.4/16.2) ready at Tue, 5 Jul 1998 17:06:13—0400
>>> HELLO patsy.mys.scps.edu
250 apollo.ph.mys.scps.edu Hello patsy.mys.scps.edu, pleased to meet you
>>> MAIL FROM:<bil@patsy>... Sender ok
250 <mis@apollo.ph.mys.scps.edu> Rec ok
>>> RCPT TO:<mis@apollo.ph.mys.scps.edu> Recipient ok
250
>>> DATA
354 Enter mail, with ". on a line by itself
>>>.
250 OK
>>> QUIT
221 apollo.ph.mys.scps.edu closing connection
mis@apollo.ph.mys.scps.edu Sent
```

以数字开头的行和以 `>>` 字符开头的行成了 SMTP 对话。以字符开头的行显示发送者主机在说什么；收件人主机的回复以数字为开头显示。

- 前两行是发送者主机上的消息，描述了 `sendmail` 正在执行的操作：

```
apollo.ph.myschool.scps.edu... Connecting to apollo.ph.myschool.scps.edu via ether... Trying 146.98.8.31... connected.
第一行显示了邮件发送给谁，以及主机 apollo.ph.myschool.scps.edu 是否在网络上。第二行显示了收件人主机的 IP 地址（在这种情况下，IP 地址是通过 DNS 获取的）。
```

- 一旦发送者的 `sendmail` 连接到收件人主机，它就会等待另一方发起进一步对话。收件人通过发送数字 `220` 后跟其域名进行回复（这是唯一要求的信息）；程序名称（通常是，但不总是，`sendmail`）；以及程序版本。它还声明已就绪并给出了本地日期时间。

```
220 apollo.ph.myschool.scps.edu HP Sendmail (1.38.193.4/162) ready at Tue, 5 Jul 1998 06:13 -0400
```

- 接下来，发送者的 `sendmail` 发送消息 `HELO`（这并不是拼写错误）；收件人回复 `250` 并确认发送者的主机名可接受：

```
>> HELO patsy.myschool.scps.edu
250 hello patsy.myschool.scps.edu, pleased to meet you
```

- 如果到目前为止一切顺利，发送者的 `sendmail` 从邮件消息信封中发送发件人名称（该主机上的用户）；收件人的 `sendmail` 接受发送者名称并回复以以数字 `250` 开头的消息：

```
>> From:<bj@pasty>
250 <bj@pasty>... Sender ok
```

- 接下来，发送者的 `sendmail` 从邮件消息信封中发送收件人名称（远程主机上的用户）；收件人的 `sendmail` 接受（在这种情况下）或拒绝此消息（那时它将回复错误 `"User unknown"`）。回复以数字 `250` 开头：

```
>> RCPT To:<mis@apollo.ph.myschool.scps.edu>
250 <mis@apollo.ph.myschool.scps.edu... Recipient ok
```

- 发送信封信息后，发送者的 `sendmail` 尝试发送电子邮件数据（头部和正文合并）：

```
>> DATA
354 Mail end
```

`DATA` 消息基本上是告诉收件人准备接收数据；数据不会显示，仅使用单独成行的一点点来标记邮件消息的结束——这是 SMTP 协议的惯例。为了防止邮件中可能包含单点的任何行被误解，发送者的 `sendmail` 在任何以点开头的行开头插入一个额外的点；收件人的 `sendmail` 会移除这些额外的点。

- 电子邮件成功发送后，将由收件人的 `sendmail` 确认。发送者的 `sendmail` 发送 `QUIT` 表示所有操作已完成，收件人的 `sendmail` 确认正在关闭连接：

- `250 Ok`

- `>>> QUIT`

- `221 apollo.ph.myschool.scps closing connection`

- 最后一行简单地确认邮件消息已成功送达：

- `misapollo.ph.myschool.scps.edu... Sent`

## 20.1.2 MTA 程序 sendmail

UNIX 邮件系统的核心是 MTA 程序 `sendmail`；因此，整体文本的大部分内容与 `sendmail` 有关，具体与 `sendmail` 管理有关。

### 20.1.2.1 sendmail 守护进程

`sendmail` 守护进程在每个旨在完全支持电子邮件的主机上持续运行。`sendmail` 守护进程监听 `25` 端口并处理传入的电子邮件。该守护进程在系统启动期间从任何 `rc` 初始化脚本被调用，通常执行以下命令或类似的命令序列：

```
if [ -f /usr/lib/sendmail -a -f /etc/sendmail.cf ]; then
  cd /var/spool/queue; rm -f nf *
  /usr/lib/sendmail -bd -ql; echo -n "sendmail"
fi
```

`rc` 脚本首先检查 `sendmail` 程序及其配置文件 `/etc/sendmail.cf` 是否存在。如果两个都存在，则检查邮件队列目录并清除发现的任何可能的 `nf` 或锁定文件；系统在处理邮件队列时可能关机，因此可能无意中留下了未处理的文件。它们必须在系统启动期间被删除，以便为重新处理这些文件以及新文件留出空间。

接下来，脚本使用两个命令行选项启动 `sendmail`。`-bd` 选项告诉 `sendmail` 作为守护进程运行，持续监听 `25` 端口以接收电子邮件。`-q` 选项决定了处理邮件队列的频率；对于大多数系统，`1h`（一小时）是一个很好的选择。对于大型邮件列表（邮件服务器），更频繁的邮件队列处理可能更；`30` 分钟 `-q30m` 或 `15` 分钟 `-q15m` 是更好的选择。此时间仅针对邮件队列；在 `25` 端口接收的电子邮件会立即处理，只有在递送失败时才会进入邮件队列重新处理。

`sendmail` 守护进程在系统活动期间一直运行。然而，当它变得太忙时，`sendmail` 守护进程将产生另一个或多个守护进程来帮助处理电子邮件。每个守护进程在完成任务后都会退出，父守护进程即使在空闲也会继续运行。

### 20.1.2.2 sendmail 命令

`sendmail` 实际上是一个多功能且强大的 UNIX 命令，可以随时从命令行执行。守护进程选项 `-bd` 只是许多可能选项之一。`sendmail` 也可以被调用来完成单个任务，就像任何其他 UNIX 命令一样；这是通常对 `sendmail` 的测试和调试进行理解。

为了更好地理解 `sendmail`，下面总结了其主要程序特性：

- `sendmail` 向一个或多个个人员发送消息，并根据需要通过网络路由消息。`sendmail` 会根据需要进行互联网转发，以将消息投递到正确的位置。

- `sendmail` 并不是设计用于用户界面；其他 MUA（邮件用户代理）程序提供了友好的前端。`sendmail` 仅用于投递格式化的消息。在没有标志的情况下，`sendmail` 从其标准输入读取到 `EOF`（文件结束符）或带有单点的行，并将找到的信件（消息）副本发送到目标地址。它根据地址的语法和内容决定发送消息的方式。

- 在发送方侧，收件者地址会在本地别名（`aliases`）中查找（或通过 `NIS`），并进行适当的别名处理。此外，如果收件者的主目录下存在 `.forward` 文件，`sendmail` 会将每条消息的副本转发到该文件包含的收件者列表。在地址中使用反斜杠 `\` 可以防止对齐。通常，发送者不会包含在别名展开中（例如，如果 `john` 加入了组，而组在展开中包含 `john`，则邮件不会转发给 `john`）。

- `sendmail` 可以将邮件直接路由到网络中的其他已知主机。直接投递邮件的主机列表取决于 `sendmail` 的配置，也可以由某些相关文件维护。

- `sendmail` 命令的格式为：

```
/usr/lib/sendmail { option }
```

其中选项如下：

| 选项 | 操作 |
|---|---|
| `-bd` | 作为守护进程运行，等待 SMTP 连接。 |
| `-bi` | 初始化别名数据库。 |
| `-bm` | 以通常方式投递邮件（默认）。 |
| `-bp` | 打印邮件队列摘要并列出当前在队列中的所有邮件。 |
| `-bt` | 在地址测试模式下运行。此模式读取地址和解析步骤，用于调试配置解析规则。 |
| `-bv` | 仅验证名称 —不收集或投递消息。验证模式通常用于验证用户或邮件列表。 |
| `-bz` | 创建配置冻结文件。 |
| `-n` | 不进行别名处理。 |
| `-hv` | 设置跳数为 N。每处理一次邮件，跳数就会增加一次；当达到限制时，邮件将带错误信息返回。 |
| `-q [time]` | 按给定间隔处理队列中保存的消息。如果省略时间，则处理一次队列。时间以标记数字的形式给出，其中 `s` 是秒，`m` 是分钟，`h` 是小时，`d` 是天，`w` 是周。例如，`-q130m` 或 `-q90m` 将超时时间设置为一小时三十分。 |
| `-t` | 为收件者读取消息。发送给人的 `"To:"`、`"Cc:"` 和 `"Bcc:"` 行将留空，`"Bcc:"` 行在传输前会被删除，列表中的任何地址都将被抑制。 |
| `-v` | 详细模式，将宣布别名展开；显示 SMTP 对话等。 |

- 下面由以下文件支持 `sendmail`，这意味着 `sendmail` 会查找查找并使用以下文件：

| 路径 | 描述 |
|---|---|
| `/etc/aliases` | 别名名称的 ASCII 数据（或者为 `/etc/mail/aliases`） |
| `/etc/sendmail.cf` | 配置文件 |
| `/etc/sendmail.fc` | 冻结的配置文件 v |
| `/etc/sendmail.st` | 收集的统计数据 |
| `/usr/lib/mailhosts` | 可以直接发送邮件的主机列表 |
| `/usr/bin/sendmail.hf` | 帮助文件 |
| `/var/spool/queue/` | 临时文件和队列邮件 |
| `$HOME/.forward` | 转发消息的收件者列表（基于用户） |
| `/usr/bin/mail` | 投递本地邮件 |
| `/usr/bin/mailx` | 递本地邮件（可选） |

注意：除了 `/etc/sendmail.cf` 外，实际路径均在 `/etc/sendmail.cf` 中指定；此处显示的路径仅为近似。对于新的 `sendmail` 版本，配置文件移动到了 `/etcetc/sendmail.cf`。

`sendmail` 对传入邮件的处理（无论它是来自本地 MUA 程序还是远程 `sendmail`）都基于列出的文件。虽然这些文件的重要性各异，但最重要的文件是 `sendmail` 配置文件 `/etc/sendmail.cf` —— 稍将详细讨论该文件。然而，其他一些文件如全局邮件别名文件、个人邮件转发文件、冻结的 `sendmail` 配置文件以及投递程序、邮件发送器也值得关注。让我们从它们开始。

## 20.1.2.3 其他 sendmail组成部分

为了完全应对如此艰巨的任务，`sendmail` 依赖于其他相关程序和文件，下文进行了简要总结。

### 20.1.2.3.1 全局别名

全局别名文件 `/etc/aliases`（有时链接到 `/etc/mail/aliases`）在系统级别提供了：

- 个人本地用户的替代名称（昵称）

- 转发到其他主机的邮件

- 邮件列表

`/etc/aliases` 中条目的基本格式为：

```
alias: recipient[, recipient, ...]
```

其中

`alias:` 邮件投递的目标名称

`recipient:` 另一个本地用户名、另一个别名的名称，或包含用户和主机的完整地址。

（注：此处原文存在大量重复的格式说明，已按要求保留结构逻辑并翻译核心含义）

（此处省略重复的格式定义部分，保持逻辑一致）

## 20.1.2.3.3 邮件投递程序 — Mailers

`sendmail` 是 MTA（邮件传输代理）程序，它本身并不处理邮件投递；除非邮件需要通过 TCP/IP 网络投递到另一个远程主机。相反，`sendmail` 会调用其他程序执行投递；这些程序被称为投递代理，或简单称为 `Mailers`。这如图 20.3 所示。

![](img/849eeed37051e04ac7ecd95adb0ba_478_0.png)

图 20.3: Sendmail 与 mailers 的关系。

`Mailer` 的定义包含在 `sendmail` 配置文件中。然而，选择 `mailer` 的标准并不是 `mailer` 定义的一部分；`sendmail` 仅决定何时使用某个 `mailer`，并向其提供必要的投递数据。

另一方面，`mailer` 的定义为 `sendmail` 提供了知道如何调用 `mailer` 所需的信息。`sendmail` 包含了投递程序的名称和位置，但完整信息包含一些额外的参数。通常，`sendmail` 配置数据的语法与其他 UNIX 配置数据大不同，我们稍后将详细讨论。目前，让我们关注在 `sendmail` 配置文件中指定的“M 配置条目”：

```
M=mailer-name P=mailer-path F=mailer-flags S=send-rules R=receive-rules A=mailer-arguments
```

其中：

`M` 标识一个 `mailer` 定义配置条目，`sendmail` 通过该符号名称识别对应的投递代理。符号名称位于 `M` 之后，没有空格。

`P=` 指定执行邮件投递的邮件程序的完整路径。对于由 `sendmail` 自身通过 TCP/IP 网络执行的电子邮件转发，此字段应为 `[TCP]` 或 `[IPC]`。

**`F=`** 指定某些标志，用于提供更多关于邮件器（`mailer`）定义的定义。每个标志单独占一行，且是布尔值——通过存在或不存在来表示真假。

**`S=`** 指定在重写发送者地址时使用的规则（这将在后文中进行解释）。

**`R=`** 指定在重写收件人地址时使用的规则（这将在后文中进行解释）。

**`A=`** 指定提供给每个对应邮件程序的命令行参数。对于两个强制性的邮件器，没有限制：即 `local` 和 `prog`；邮件器的名称是任意的。但无论它们是否被使用或需要，都必须定义。它们允许向本地用户（`mailer local`）或本地程序（`mailer prog`）投递电子邮件。如果没有它们，`sendmail` 将无法启动并打印相应的错误消息。显然，为了让 `sendmail` 正常运行，必须定义其他邮件器，但 `sendmail` 程序并不严格要求它们。

## 20.1.2.3.4 sendmail 配置文件

这是 `sendmail` 配置的核心所在；配置文件完全定义了 `sendmail` 的行为——所有内容都在其中指定。`sendmail` 配置文件为 `/etc/sendmail.cf`（有时为 `/usr/lib/sendmail.cf` 以及近期的 `/etc/mail/sendmail.cf`）。`sendmail.cf` 有三个主要功能：

1. 定义环境。

2. 将地址重写为适用于后续处理的正确语法。

3. 将地址映射为投递电子邮件所需的指令。

为了执行所有这些功能，配置文件需要许多不同的配置条目：

- **Macro**（宏）定义和选项定义环境。

- **Rewrite**（重写）规则将电子邮件地址从一种格式转换为另一种格式。

- **Mailer**（邮件器）定义指定投递电子邮件所需的程序。
