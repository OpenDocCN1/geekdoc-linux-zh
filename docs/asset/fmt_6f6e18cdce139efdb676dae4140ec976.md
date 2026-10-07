
## 表 11.3 syslog 严重性级别（严重性递减）

| 级别 (Level) | 大致含义 |
| :--- | :--- |
| emerg | 恐慌 (Panic) |
| alert | 紧急情况 |
| crit | 关键状态 |
| err | 其他错误情况 |
| warning | 警告消息 |
| notice | 可能值得调查的事 |
| info | 信息性消息 |
| debug | 仅用于调试 |

消息的严重性级别指定了其重要性。级别之间的区别有时是模糊的。`notice` 和 `warning` 之间有明显区别，`warning` 和 `err` 之间也有区别，但 `alert` 与 `crit` 所表达的确切含义仅存推测。

在 `syslog.conf` 文件中，级别表示消息要被记录必须具备的最低重要性。来自邮件系统且级别为 `warning` 的消息将匹配选择器 `mail.warning` 以及选择器 `mail.info`、`mail.notice`、`mail.debug`、`*`、`info` 和 `*.debug`。`syslog.conf` 指定 `mail.info` 消息记录到一个文件中，`mail.warning` 消息也会去那里。

> 作为基础语法的改进，Linux 版本的 syslog 允许在优先级前加上 `=` 和 `!` 字符，分别表示“仅限优先级”和“除此优先级及以上以外”。表 11.4 显示了示例。

## 表 11.4 syslog.conf 中 Linux 优先级限定符示例

| 选择器 (Selector) | 含义 |
| :--- | :--- |
| mail.info | info 优先级及以上的邮件相关消息 |
| mail.=info | 仅限 info 优先级的消息 |
| mail.info;mail.err | 仅限 info、notice 和 warning 优先级 |
| mail.debug;mail!=warning | 除 warning 以外的所有优先级 |

`action` 字段告诉 syslog 如何处理每条消息。选项列于表 11.5。

## 表 11.5 Syslog 操作

| 操作 (Action) | 含义 |
| :--- | :--- |
| filename | 将消息追加到本地机器的文件 |
| @hostname | 将消息转发到 *hostname* 上的 **syslog** |
| @ipaddress | 将消息转发到主机 *ipaddress* 上的 **syslog** |
| /filename | 将消息写入命名管道 *fifoname* |
| user1,user,... | 如果 *users* 已登录，则将消息写入其屏幕 |
|  | 将消息写入所有当前登录的用户 |

- * 更多信息请参阅 `filename`（或 `fifoname`）（Linux 版本的 syslog）。

如果使用了 *filename*（或 *fifoname*），该名称应为绝对路径。如果你在 Linux 系统上指定了一个不存在的文件，当 `syslog` 首次将消息指向它时，将创建该文件。在其他系统上，文件必须已经存在；`syslog` 不会创建。

在 Linux 发行版上，你可以在 *filename* 前加连字符，表示该日志不应轮转（rotate）。如果你指定了一个不存在的文件，`syslog` 在消息首次指向它时将创建该文件。在其他系统上，文件必须已经存在。

## 第 11 章 Syslog 与日志文件

### 非主主机的 syslog.conf 文件

# 紧急情况：通知所有已登录的用户
*emerg:user.none

# 将重要消息转发到中央日志记录器
*warning.lpr.local1.none @netloghost
daemon.auth.info @netloghost

# 也将一些本地日志发送到中央日志记录器
local2.info:7.debug @netloghost

# 将打印错误保留在本地
lpr.debug /var/log/lpd-errs

# 将 sudo 日志记录到 local2 -在此处保留副本
local2.info /var/log/sudo.log

# 将内核消息保留在本地
kern.info /var/log/kern.log

此配置没有在本地保留大量的日志信息。值得注意的是，如果 netlog 宕机或无法访问，日志消息将会丢失。你可能可能保留一份重要消息的本地副本，以防止这种可能性。

在安装了本地软件的站点，大量消息可能会被不恰地记录到设施（facility）服务器的紧急（emerg）级别。在这个示例中，user/emerg 在第一行非注释行通过 user.name 子句被指定。

第二行和第三行将所有重要消息转发到中央日志主机；显式排除了来自打印系统和校园范围内的访问系统（local1）的消息。第四行也将部分本地信息转发到 netlog。最后三项保留了打印错误、`sudo` 消息和内核消息的本地副本。

### 中央日志主机

此示例适用于 netlog，它是一个为拥有约 7,000 台主机的中型网络提供的中央、安全的日志主机。

```
# 主日志主机（master logging host）的 syslog.conf 文件
# 将紧急消息发送到控制台和日志文件，带有时间延迟
*emerg /dev/console
*err,kern.mark,debug,auth,user.none /dev/console /var/log/console.log
auth.notice /var/log/console.log

# 将非紧急消息发送到常规日志文件
*err,user.none;kern.debug /var/log/messages
daemon.auth.notice;mail.crit /var/log/messages
lpr.debug /var/log/lpd-errs
mail.debug /var/log/mail.log
```

### syslog 的替代方案

### 本地授权消息，例如 sudo 和 npasswd
local2.debug /var/log/sudo.log
local2.alert /var/log/sudo-errs.log
auth.info /var/log/auth.log

# 其他本地内容
local0.info /var/adm/nbl.log
local4.notice /var/adm/da.log
local6.debug /var/adm/annex-isn.log
local7.debug /var/admlog/tcp.log

# 本地消息（在未指定设施时的默认值）
user.info /var/admlog/user.log

来自本地程序和网络上 syslog 的消息会被写入日志文件。在某些情况下，每个设施的输出被放在它自己的文件中。

中央日志主机在写入消息时为每条消息生成时间戳。时间戳并不反映源主机的时间。如果你有位于多个时区的机器，或者你的系统时钟没有同步，那么时间戳将具有误导性。

### Syslog 调试

`logger` 命令用于从 shell 脚本提交日志条目。你也可以用它来测试 syslogd 配置文件的更改。例如，如果你添加了以下行：

```
local5.warning /tmp/evi.log
```

并要验证其运行正常，请运行

```
hup$ logger -p local5.warning "test message"
```

包含 "test message" 的行应该被写入 `/tmp/evi.log`。如果这种情况没有发生，可能是你忘记创建 evi.log，没有给文件赋予适当的权限，或者没有向 syslog 发送挂断信号（hangup signal）。也许你使用了空格而不是制表符？

### syslog 的替代方案

尽管 syslog 长期以来一直是 UNIX 和 Linux 的主日志日志系统，但人们已经开发出了几种替代方案，试图解决 syslog 的某些缺点。其中之一是 `syslog-ng`（syslog 的下一代版本），它现在被默认用在 SUSE 系统上。从配置的角度来看，它与标准 syslog 非常不同，我们没有在书中详细描述它。如果你想在非 SUSE 系统上尝试它，可以从 balabit 获取。

`Syslog-ng` 增加了额外的配置设施、基于消息内容的过滤、消息完整性，以及在消息转发时对防火墙限制的更好支持。

## 第 11 章 Syslog 与日志文件

`Syslog-ng` 增加了额外的配置设施、基于消息内容的过滤、消息完整性，以及在消息转发时对防火墙限制的更好支持。

### 11.3 AIX 日志记录与处理

`dmesg` 和 `klog` 都通过命令行标志设置控制台。例如：

```
ubuntu$ dmesg -n 2
```

级别 7 最详细并包含调试信息。级别 1 包含 panic 消息（数字越小越严重）。所有内核消息继续进入缓冲区（进入 syslog），无论它们是否被转发到控制台。内核在 `/proc/sys` 目录下提供了一些控制，允许从源头阻塞重复的消息。有关设置内核参数的通用机制的更多信息，请参阅第 421 页。特定的控制文件是 `/proc/sys/kernel/ratimit`，它指定了一旦激活阻塞，内核消息之间的最小秒数（默认为 5），以及 `/proc/sys/kernel/ratimit_burst`，它指定了在激活阻塞前允许多少组消息（默认为 10）。这些参数是建议性的，因此不能保证大量的消息流会被拦截。它们仅适用于在内核中使用 `ratelimit()` 函数创建的消息。

遗憾的是，系统启动日志不如内核日志管理良好。

红帽企业 Linux 使用 `initlog` 命令捕捉启动命令的输出并提交给 syslog。遗憾的是，每次运行命令时必须显式提到 initlog，因此获取这些信息是以复杂性为代价的。消息通常很容易进入 `/var/log/boot.log`。

我们的其他示例系统没有记录启动脚本输出的统一努力。某些信息由单独命令和守护进程记录，但很多未被记录。

### 11.3 AIX 日志记录与处理

AIX 管理日志的方式与其他 UNIX 系统不同。虽然默认安装中包含 syslog，但并未对其进行配置。相反，AIX 依赖一个名为 `errdemon` 的专用守护进程进行错误报告。`errdemon` 用于处理系统诊断消息（例如硬件故障或文件系统满通知），而不是处理单个守护进程的日志。因此，明智系统管理员将依靠 errdemon 的智慧

针对 AIX 的特定诊断程序和用于集中化应用程序日志的自定义配置 syslog。

`errdemon` 在系统启动时于 `/etc/rc.bootc` 中启动，并从特殊文件 `/dev/error` 中读取错误事件。内核和某些 AIX 用户应用程序都会根据 `/dev/adm/ras/errtmpl` 中预定义的模板向此文件写入错误。`errdemon` 将新条目与模板进行比较，并将输出以二进制格式写入到文件 `/var/adm/ras/errlog` 中。AIX 非常偏爱二进制格式！

`errlog` 是一个循环文件，因此当文件达到最大 own（默认为 1MB）时，它会用最新的事件覆盖第一个事件。`errdemon` 会添加尚未写入日志的缓冲区。可以通过直接运行 `/usr/lib/errlog` 来查看或调整这些设置。调用细节请参阅主页。

由于 errlog 不是文本文件，你需要使用另一个名为 `errpt` 的专有工具来读取其内容。在不带任何参数的情况下，errpt 会以短格式打印日志中所有事件列表。添加 `-a` 参数可获得详细输出。我们 AIX 系统中的一个示例条目如下：

```
aix errpt -a
```

```
LABEL: DMPCHK_NOSPACE
IDENTIFIER: F89FB899
Date/Time: Sat Mar 21 15:00:01 MST 2009
Sequence Number: 224
Machine Id: 0001A4C4D700
Node Id: ibm
Class: O
Type: PEND
WPAR: Global
Resource Name: dumpcheck
```

描述

拷贝目录太小。

可能的原因

包含拷贝目录的文件系统中没有足够的空闲空间来容纳转储文件（dump）。

建议的操作

增加该文件系统的大小。

详细数据

文件系统名称：`/var/adm/ras`

当前可用空间 (kb)：108476

当前估计转储大小 (kb)：197836

此特定事件表明系统转储文件将无法放入指定的存储文件系统中。大多数部分标签都是自言易懂的，但更多细节请参见 `errpt`。

尽管 `errpt` 是独立 AIX 系统上有用的日志数据源，但它的使用可能会干扰广泛定义的企业日志策略。你可能需要编写一些脚本来以 syslog 格式捕获 `errpt`，或将其转发以进行集中归档。IBM 广泛的在线文档还显示了如何通过对象管理器（Object Manager）将错误报告发送 syslog。

你可能需要删除错误日志中的条目，IBM 提供了 `errclear` 命令来实现此功能。`errclear` 会删除所有于指定天数之前的消息。例如，`errclear 7` 会删除超过一周的错误消息。

运行 `errclear 0` 可以清除所有错误消息，或运行 `errclear -j identifier 0` 清除特定消息。

## AIX 下的 syslog 配置

默认情况下，AIX 的 `syslog.conf` 文件由长长的注释列表和无需解析的数据组成。系统管理员负责以与其它系统设置一致的方式配置 syslog。
