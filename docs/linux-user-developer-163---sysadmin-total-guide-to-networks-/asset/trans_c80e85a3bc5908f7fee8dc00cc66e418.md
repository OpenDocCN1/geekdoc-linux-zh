

# 每期都包含……

- 针对 Linux 专者的编程指南
- 来自企业厂商的最新动态
- 创新的树莓派项目与建议
- 最佳 Linux 发行版和硬件测评

# 为什么你应该订阅……

- 5 英镑即可尝试 5 期*
- 节省 30% 费用——每 6 期支付 25.15 英镑
- 免费送货上门
- 永不错过任何期

# 订购日期
6月30日
此优惠请使用代码 SUMMER161

# 邮寄
将您填写好的表格寄至：
Linux User & Developer Subscriptions, 800 Guillat Avenue, Kent Science Park, Sittingbourne, Kent ME9 8GU

# 您的详情

| 头衔 | 名字 |
| :--- | :--- |
| 姓 | |
| 地址 | |
| 邮政编码 | 国家 |
| 电话号码 | |
| 手机号 | |
| 电子邮箱 | |

# 直接记账付款
英国直接记账付款
我将以 5 英镑的价格获得前 5 期，此后每 6 期支付 25.15 英镑

![](img/f4a034c4fbc20906a013558fa4e058a2_28_0.png)

| 致经理 | 银行详情 |
| :--- | :--- |
| 地址 | |
| | 5 | 0 | 1 | 8 | 8 | 4 |
| 引用编号 | |
| 邮政编码 | |
| 账号 | |
| 银行分行 | |
| 日期 | |

# 付款详情
您的专属价格，13 期

欧元 £70 英国(ROW) £80 美元 £80
我随附了一份 6 英镑的杂志（支付给 Imagine Publishing Ltd）

# 信用卡/借记卡

| Visa | Mastercard | Amex | Maestro |
| :--- | :--- | :--- | :--- |
| 卡号 | | | |
| 有效期号 | |（如果是 Maestro） | |
| 签名 | | | |
| 日期 | | | |

如果您不想通过电话*或电子邮件** 接收来自 Imagine Publishing Ltd 的任何促销材料，请勾选。

如果您不想通过电话*或电子邮件* 接收来自其他公司的任何促销材料，请勾选。

服务条款与条件
*此优惠适用于新的英国直接记账订阅者，以 5 英镑获得前 5 期。此类订阅后，每 6 期需支付 25.15 英镑。必须提供优惠代码 SUMMER161 以享受此订阅价格。新订阅将从下一可用期开始。可按要求提供直接记账担保的详情。此优惠于 2016 年 6 月 30 日过期。

# 教程过程

![](img/f4a034c4fbc20906a013558fa4e058a2_29_0.png)

# 使用服务器进程进行系统编程

Mihalis Tsoukalos
是一位 Unix 管理员、Unix 和 iOS 程序员、数据库管理员以及数学爱好者。他自 1993 年以来一直使用 Linux。

# 资源

- 文本编辑器
- GCC 编译器
- Go 编译器
- Perl 解释器

# 开发可以脱离终端并在后台作为守护进程（daemons）运行的服务器进程

服务器进程具有独特的特殊进程。进程最常见的特征是它们在后台运行，没有与之关联的控制终端。

像往常一样，大多数展示的代码将用 C 语言编写。不过，你也会看到 Python 和 Go 的示例，因为这些语言允许你利用现有的模块和库。在为生产系统开发服务器时，服务器的行为应该是完美的；因此，除非你计划在一个没有适当规划、文档和测试的环境环境中，否则我们不建议任何做法。

- 孤儿进程组
- 定义日志参数
- 处理信号
- 创建锁文件
- 执行实际工作

首先，进程通常调用 `fork()` 生成子进程并使用 `exit()` 终止父进程。然后，它们调用 `setsid()` 创建新会话，因为服务器应该脱离终端并在后台运行，不需要终端。

服务器会将它们的当前工作目录更改为根目录（root），以确保它们独立于文件系统结构。它们还会在自己的环境中定义 `PATH` 环境变量。正如你所看到的，它们通常会将自己的进程 ID 写入操作系统的 `/tmp` 中的一个文件中。它们使用系统的日志功能将各种类型的消息写入日志文件。接下来，它们会更改文件掩码以便与运行的系统进行交互。最后，它们使用 `umask()` 将创建掩码更改为已知状态。

# 你需要知道的

服务器进程的通用算法涉及若干特定步骤：

- 第一次 `fork()`
- 第二次 `fork()`
- 成为会话组

![](img/f4a034c4fbc20906a013558fa4e058a2_29_1.png)

可用教程文件：
files.co.uk

30

# 2. mtsouk@mail:~/docs/archive/working/SPServer.LUD163/code (ssh)

这里是我们要操作的
logging.c 脚本
我们将开始
操作

```
code ./logging
Created child with pid = 27051
code ps ax | grep 27051
27054 pts/0 S= 0:00 grep 27052
code ps ax | grep 27052
27050 pts/0 S= 0:14 ./logging
27006 pts/0 S= 0:00 grep 27052
27052 -rw-r--r-- mtsouk Jan 21 05:01 /tmp/logging
code kill -HUP /tmp/pid
code kill -HUP /tmp/pid
code kill -HUP /tmp/pid
code kill -HUP /tmp/pid
code kill -USR1 /tmp/pid
27070 pts/0 S= 0:00 grep 27052
code ./logging
Created child with pid = 27102

你可以想象，进程通常被设计为永久运行！停止进程的唯一方法是发送服务器进程 ID。出于安全考虑，root 用户不会监控进程，除非绝对必要。通常情况下如此。每个进程，以及守护进程，都属于一个特定的用户。然而，每个由 root 权限启动的进程都可以更改其所需的用户 ID。但是，如果程序忽略了 `SIGHUP` 信号，它在控制进程终止后仍然可以在孤儿进程组中运行。它无法再次访问控制终端。这是第二次 `fork()` 调用的结果，取决于你使用的进程数量。你可能需要避免此进程，如果它已被其他进程使用。

# 开发服务器进程

你开发的进程在此时不会异常，它将像一个正常的进程一样在后台运行。simple 文件包含了必要的代码，以便从终端变得可用，并建立一个新会话，这在你的进程结束时可能会问题。此外，你应该知道，当进程组变成孤儿时，系统会自动其发送 `SIGHUP` 信号，这通常会导致

> /sample
Created child with pid = 1561
Created child with pid = 1562
$ ps -o ppid,ppid,command | grep simple
PID PGID COMMAND
1561 1 1562 ./sample
$ ps ax | grep -v

# 日志设施

日志设施类似于用于记录信息的缓存。`/etc/syslog.conf` 配置文件中的行决定了日志消息存储的位置。如果我们的设施存储在文件中；`/var/log/syslog.log`

日志设施的值可以是作者之一：auth, cron, daemon, mail, news, network, user。UUCPD（local0, local1, local2, local3, local4, local5, local6, local7）。下一行定义了日志设施以及出现在相关事件日志中的程序。

* "logging.c" LOG_PID, LOCAL_0:

# 教程过程

# 如果你不是开发服务器进程，可以使用与日志相关的系统调用

你可以看到 `simple` 命令的进程 ID 为 1561。最后一个命令显示没有 ID 为 1561 的进程，这意味着 `simple` 是一个孤儿进程。

- 日志级别
- 日志级别或优先级指定日志的严重程度。
- 各种日志级别包括 info、warning、error、alert 和 emergency。你可以看到，在日志中，优先级和消息内容都很。
- syslog 守护进程的配置文件（`syslog.conf`）包含了所有记录的信息。
- 活动

最后，是时候聊聊 `setsid()` 系统调用了。`setsid()` 调用创建一个会话。调用进程成为新会话的组，也是新的控制进程组的组。

# 终止服务器进程

用于发送的 C 代码是 `killProcess`（位于 FileSys 中，以及本教程的其他脚本）。调用进程有一个信号处理器；此功能确保它在收到 `USR1` 时停止——借助信号处理器；此外，它每当收到 `SIGHUP` 信号时增加计数器。

脚本将 PID 写入 `/tmp` 目录以便查找——它也被记录在进程的锁文件中。通过锁文件的帮助，我们可以确保随时只有一个服务器实例在运行。

此处实现了为了写入日志文件的 C 代码：

```
#define LOGFILE "/tmp/1.pid"
#define SIGHUP (SIGUSR1)
int fd = open(LOGFILE, O_RDWR|O_CREAT, 0644);
char buffer[32];
if (fd < 0) {
    exit(1);
}
truncate(fd, 0);
sprintf("%d", getpid());
write(fd, buffer, strlen(buffer));
close(fd);
```

你可以看到一个第一个函数生效的示例。

# 日志文件

这部分将教你如何将信息从服务器发送到 syslog 服务。

# 更高级的示例

这次，开发的进程将做一些更有用的事情，并拥有一套完整的功能。程序将使用硬编码在脚本中的端口号 12345 本地 UDP 连接。通常，大多数服务器进程包括

