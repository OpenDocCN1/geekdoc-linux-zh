
> 如果发布了 sendmail 新版本且提供了等效的 Red Hat 包，可以从 http://www.sendmail.org/ 下载完整的源码发行。请记住，这将涉及对整个分发包进行配置和编译，这并不是初学者或胆小者的任务。

## 启动 sendmail

要启动 `sendmail`，你可以重启机器，或者直接执行命令 `/etc/init.d/sendmail` 来运行该服务。启动和停止 `sendmail` 的过程与其他服务器进程无异。之前的安装过程创建了 `/etc/init.d/sendmail` 文件，并使用 `chk-config` 命令在 `/etc/rc.d` 目录中创建适当的链接。

有关控制守护进程和服务器进程的 shell 脚本的详细信息，请查看第 12 章。

`www.united.com` 额外内容

`/etc/init.d/sendmail` shell 脚本接受四种命令行参数之一。如果带 `start` 参数调用，`sendmail` 脚本将启动守护进程，除非收到 `/etc/sysconfig/sendmail` 文件的指示，否则它将立即处理入站邮件，并每 60 分钟尝试递送队列邮件。此外，每次守护进程启动时，都会从 `/etc/mail` 目录下的纯文本配置文件创建多个数据库映射。如果使用 `stop` 作为命令行参数调用，邮件服务器将关闭，后续的入站消息将被忽略（保留在发送消息机器的传出队列中）。

如果提供的命令行参数为 `restart`，脚本将按顺序执行上述停止和启动程序。使用 `status` 作为参数将报告守护进程是否正在运行，如果正在运行，它会打印 PID。所有其他命令行参数都将导致错误并打印用法信息。

如果你的机器在加载 `sendmail` 时（在打印 Starting sendmail 消息后）似乎挂起了几分钟，说明机器的主机无法解析。要解决这个问题，请将机器的 IP 地址和主机名添加到 `/etc/hosts` 文件中。这种行为可能发生在 X 服务器尝试启动时。

如果 `sendmail` 以守护进程模式运行，入站消息将通过处理并存储在 `/var/spool/mail` 目录。该目录中的每个文件代表本地机器上的有效用户名（编译到程序或通过环境变量设置使用此目录作为用户的收件箱）。

传出消息在处理期间或必须排队递送时存储在 `/var/spool/queue` 目录中。这些文件名看起来很奇怪，但有一套一致的命名方案。前两个字符表示数据类型（见表 19-1），后续的所有字符是处理该消息的 `sendmail` 进程 PID 的唯一标识符。

### 表 19-1 /var/spool/queue 中的名前缀

| 文件名前缀 | 存储的数据 |
|---|---|
| df | 电子邮件的正文。 |
| qf | 包含邮件头和其他详细信息的控制文件。 |
| tf | 如果遇到递送错误，则创建的 qf 文件的副本。 |
| xf | 尝试消息时生成的任何错误消息。 |

## 其他程序

如 `sendmail` 安装输出所示，分发包中包含了其他可执行程序。这些程序见表 19-2。

### 表 19-2 相关的 sendmail 程序

| 程序 | 描述 |
|---|---|
| hoststat | 显示最近与本地机器 sendmail 守护进程通信的主机状态。等于 sendmail -bh，默认禁用。 |
| mailq | 显示队列中等待处理的消息摘要（等于 sendmail -bp）。 |
| mailstats | 显示消息计数和字节统计。 |
| makmap | 将纯文本文件（例如 /etc/mail/virtusertable）转换为哈希数据库文件（例如 /etc/mail/virtusertable.db）。 |
| newaliases | 将纯文本 /etc/aliases 文件转换为哈希数据库 /etc/aliases.db（等于 sendmail -bi）。 |
| praliases | 打印 /etc/aliases 中定义的所有别名。 |
| procmail | 未包含在 sendmail 包中，但用 sendmail 的 MDA（邮件投递代理）使用。 |
| purgest | 清空存储主机信息的目录。等于 sendmail -bH，默认禁用。 |
| rmail | 通过 UUCP 处理入站邮件。 |
| smrsh | 为运行 sendmail 程序实现的限制 shell。 |

## sendmail 执行的日志

`sendmail` 执行的日志量可以在 `sendmail.cf` 文件中配置，默认情况下，`syslog` 提供了良好的覆盖范围。

### 第 IV 部分 Red Hat Linux 和服务器设置

每当发送或接收消息时，`/var/log/maillog` 都会创建一个日志记录。以下是该文件的示例：

```
Jul 19 12:52:40 sendmail[444]: alias database rebuilt by root
Jul 19 12:52:40 sendmail[444]: /etc/aliases: 14 aliases, 10 bytes total
Jul 19 12:52:40 sendmail[460]: starting daemon (8.9.3)
Jul 19 12:54:34 sendmail[1120]: from=root, size=161,class=0,pri=3,msgid=<199007191254.OAA1120@my.com>, relay-root@localhost
Jul 19 12:54:35 sendmail[1127]: OAA1120:to=jkpat,claddr=root (0/0), delay=00:00,xdelay=00:00,mail-local,stat=Sent
```

日志将显示人们尝试不该做的事情。早期邮件中启用的 wiz 和 debug 命令被发现是一个巨大的安全问题。此外，`expn` 和 `vrfy` 命令（可以通过配置选项禁用）提供的信息比你分发的要多。

```
Jul 19 13:03:27 sendmail[699]: NOQUEUE: "wiz" command from localhost [127.0.0.1](127.0.0.1)
Jul 19 13:03:29 sendmail[699]: NOQUEUE: "debug" command from localhost [127.0.0.1](127.0.0.1)
Jul 19 13:03:37 sendmail[701]: NOQUEUE: localhost [127.0.0.1](127.0.0.1): expn oracle
Jul 19 13:03:43 sendmail[702]: NOQUEUE: localhost [127.0.0.1](127.0.0.1): vrfy oracle
```

## 配置 sendmail

如果你需要与系统管理员交谈，只需提到“`sendmail.cf` 文件”、“地址重写规则”或“邮件循环自身”，你就会立即被理解，被视为同道，并获得许多人的同情。

`sendmail.cf` 文件（或 `sendmail` 配置）因其晦涩的语法、几乎无法解读的规则集以及在混乱中进行管理的能力而闻名遐迩（且臭名昭著）。这种声誉是实实在归的，但在过去几年里，随着 `m4` 预处理器宏的出现，配置 `sendmail` 变得简单得多，这些将在在本节末尾进行讨论。更此外，`sendmail` RPM 包含的默认 `/etc/sendmail.cf` 文件可能无需修改即可工作，尽管应该进行少微调整。

# 第 19 章：设置邮件服务器

`/etc/sendmail.cf` 文件包含了用于引导 `sendmail` 守护进程的配置信息和可选值。整个文件的长度远超 1000 行，其中至少有一半内容在这里没有被讨论（如果你发现需要操作这些行，将会会非常棘手）。在接后的章节中展示了一些可能有用的行，并在相关的选项块之后插入了注释。

`sendmail.cf` 文件的通用格式是一个单条命令文件，后面紧跟一个参数（通常用单个字母表示，但不一定如此）。例如，选项以一个大写字母 `O`（代表 option）开头。如果需要某个值，则在最后指定。命令必须从行的第一列开始，因为开头的空白字符表示上一行的延续。此外，每行只能存在一个命令。表 19-3 描述了有效命令。以 `#` 开头的行被视为注释，且不被处理。

## 表 19-3：/etc/sendmail.cf 中的可用命令

| 命令 | 描述 |
| --- | --- |
| C | 定义一个“类宏”（class macro），这是一个可以包含多个值的变量。 |
| D | 定义一个宏（macro），它可能只包含一个值。 |
| E | 设置环境变量。 |
| F | 定义一个“文件类宏”（file class macro），其值从文件或管道获取。 |
| H | 选择标题行的格式。 |
| K | 声明一个键数据库文件。 |
| L | 允许根据系统平均负载进行处理限制。 |
| M | 定义一个 MDA（邮件投递代理）及其参数。 |
| 0 | 为选项分配值。 |
| P | 定义消息优先级级别。 |
| R | 组装重写规则。 |
| S | 开始一组重写规则。 |
| T | 将用户分类为“受信”。 |
| V | 定义配置文件的主版本。 |

设置一个可运行的 `sendmail.cf` 文件是让你的电子邮件服务运行的关键。接下来的章节将对该文件进行分解。如果你正在设置第一个电子邮件服务器，应该彻底阅读这些章节，以便理解 `sendmail` 的工作原理，以及你需要更改哪些内容来适应你的邮件配置。我们将首先讨论选项行，然后讨论 `m4` 预处理器、转发文件和别名文件。

`sendmail.cf` 文件中任何以井号（`#`）开头的行都是注释，不会被解释。通常，你可以取消注释并更改这些行来激活特定功能，正如后续章节所述。

## sendmail 组件文件

`sendmail.cf` 文件的第一部分包含了用于创建 `sendmail.cf` 文件的组件文件列表。它还包含了关于配置文件格式和版本的信息。以下是 `sendmail.cf` 头部示例：

```
