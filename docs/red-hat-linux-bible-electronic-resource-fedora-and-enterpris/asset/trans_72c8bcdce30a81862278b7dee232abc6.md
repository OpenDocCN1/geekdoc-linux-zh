
日志文件被检查、消息如何被过滤，以及日志摘要电子邮件发送的频率。您可能还想更改 syslog 设施监控的功能以及 syslog 监控的级别，如果您对调试特定系统功能感兴趣的话。

> **NOTE:** 近期，Red Hat 已将 logwatch 软件包添加到发行版中。Logwatch 配置为每天运行一次以监控您的日志文件。虽然 logwatch 并不是像 LogSentry 那样全面的工具，但您可以期望每天收到一份 logwatch 电子邮件，其中突出显示其检测到的任何危险系统活动。该电子邮件发送给您计算机的系统管理员。

## 下载和安装 LogSentry

您可以在 `rpmfind.net` 以及互联网上的多个 FTP 站点找到 `logsentry` 软件包。下载 `logsentry` 后，只需从下载它的目录运行以下命令即可安装软件包：

```
# rpm -Uhv logsentry*
```

LogSentry 软件包包含四个配置文件（位于 `/etc/logsentry` 目录中）、运行 `logcheck.sh` 的 `cron` 文件（位于 `/etc/cron.d/logsentry.cron` 中），以及 `logcheck.sh` 和 `logtail` 命令（位于 `/usr/sbin` 中）。`/usr/share/doc/logcheck*` 目录中还有 README 文件。

由于网络上流传着不同版本的 LogSentry，包括名为 logcheck 的旧版本，命令的位置和使用 LogSentry 的说明可能与我在此描述的不同。例如，原版 logcheck 软件包可能在 `/usr/bin` 中包含用于运行 logcheck 的 `logcheck.sh` 脚本。此处使用的 logsentry 软件包是 `logsentry-1.1.1-1.i686.rpm`。

## 设置 LogSentry

您无需执行任何操作即可使 LogSentry 正常工作。安装 LogSentry 后，它每天午夜运行一次。然后结果会通过电子邮件发送给本地主机计算机上的 `root` 用户。然而，您可以做几件事来根据特定需求定制 LogSentry。有关更多信息，请参阅本章后面的“根据您的需求配置 LogSentry”部分。

## 运行 LogSentry

安装 logsentry 软件包时，会在 `/etc/cron.d` 目录中放置一个名为 `logsentry.cron` 的脚本。在这种情况下，`/etc/cron.d/logsentry.cron` 脚本 simply 运行 `/usr/sbin/logcheck.sh` 脚本。

由于 `logsentry.cron` 脚本每小时运行一次，这意味着您（或管理员）每天会收到 24 条电子邮件，每条都包含经过过滤的日志消息。您可以创建自己的 `cron` 脚本来按您喜欢的任何计划启动 `logcheck.sh`。

**NOTE:** `/usr/sbin/logcheck.sh` 脚本使用 `/usr/sbin/logtail` 命令仅收集您尚未看到的日志消息。logtail 命令通过为 Logcheck 监控的每个日志文件创建一个 `.offset` 文件来实现这一点。下次运行 Logcheck 时，只会检查自上次运行以来到达的日志消息。

## 使用 LogSentry

设置并运行 LogSentry 后，要开始使用 LogSentry，您只需阅读 LogSentry 发送给您的电子邮件即可。默认情况下，您的 Red Hat Linux 系统上的 root 用户每小时会收到一条来自 LogSentry 的电子邮件。匹配且未被排除的日志消息在每封电子邮件中按以下三个标题之一进行分类：

- * **Active System Attack Alerts:** 表示可能代表对您系统的攻击的消息。
- * **Security Violations:** 包括可能表示存在问题但不一定是对您系统的攻击的失败和违规行为。
- * **Unusual System Events:** 包括所有既未匹配也未被排除的日志消息。

以下是 LogSentry 电子邮件消息的示例。

```
Return-Path: <root@localhost.localdomain>
Received: (from root@localhost)
Subject: maple 11/06/03:19.01 ACTIVE SYSTEM ATTACK!
Status: R

Active System Attack Alerts
=========================
Nov  6 18:02:28 maple portSentry[1102]: attackalert: Possible stealth
scan from unknown host to TCP port: 111 (accept failed)
Nov  6 18:33:26 maple sendmail[1863]: f37lXJw01863: "wiz" command from
 duck.handsonhistory.com [10.0.0.28] (127.0.0.1)
Nov  6 18:33:29 maple sendmail[1863]: f37lXJw01863: "debug" command from
 duck.handsonhistory.com [10.0.0.28] (127.0.0.1)

Security Violations
===================
Nov  6 18:02:28 maple portSentry[1102]: attackalert: Possible stealth
scan from unknown host to TCP port: 111 (accept failed)
Nov  6 18:39:14 maple -- root[121]: ROOT LOGIN ON tty1

Unusual System Events
=====================
Nov  6 18:01:35 maple last message repeated 291877 times
Nov  6 18:14:10 maple last message repeated 297510 times
Nov  6 18:20:58 maple kernel: SB 4.16 detected OK (220)
Nov  6 18:20:58 maple kernel: SB16: Bad or missing 16 bit DMA channel
Nov  6 18:20:58 maple kernel: sb: 1 Soundblaster PnP card(s) found.
Nov  6 18:38:37 maple syslog: syslogd startup succeeded
Nov  6 18:38:37 maple kernel: klogd 1.4-0, log source = /proc/kmsg
started.
Nov  6 18:38:37 maple kernel: Inspecting /boot/System.map-2.4.2-0.1.49
```

在前面的电子邮件中，在“活动系统攻击警报”标题下，您可以看到 PortSentry 服务检测到了对端口 111（portmapper 服务）的扫描。接下来的两条消息表明，来自主机 duck.handsonhistory.com 的用户试图扫描 sendmail 以查看是否可以访问 debug 和 wiz 服务。在“安全违规”标题下，可能的隐蔽扫描再次出现。还检测到 root 用户的正常登录（尽管在这种情况下它没有构成特别威胁）。

在“异常系统事件”标题下，如前所述，包含所有未被匹配（特意添加到另一类别）或被排除（特意忽略）的消息。许多正常的系统活动消息都会出现在这里。随着时间的推移，您可能希望明确包含或排除您经常看到的消息，或引起您注意的潜在问题。例如，前面的“last message repeated 291877 times”行表示潜在的拒绝服务攻击。您可能希望将关键字“message repeated”添加到您的 logcheck.hacking 列表中。同样，“Soundblaster PnP card(s) found”也可以添加到 logcheck.ignore 文件中，因为该消息反映了正常处理。

通常，您希望通过防止攻击者访问您的系统来对检测到的攻击做出反应。如果攻击者确实进入了系统，您希望将其清除并尽可能清理造成的损害。PortSentry 软件包是检测、记录并拒绝攻击者访问您系统的优秀工具，本章后面会讨论该软件包。

## 根据您的需求配置 LogSentry

安装 LogSentry 后，它无需任何配置即可运行。然而，为了更好地满足您的需求，您可以修改多个配置文件。以下部分描述了这些文件。

### 编辑 logcheck 脚本

`/usr/sbin/logcheck.sh` 脚本扫描您的日志文件并对通过电子邮件发送的日志消息进行分类。您可以通过更改脚本中的变量值来更改 logcheck.sh 脚本的大部分行为。要更改 logcheck.sh 脚本的行为，请按照以下步骤操作：

- 1.  复制 `/usr/sbin/logcheck.sh` 文件。例如：

```
# cp /usr/sbin/logcheck.sh /usr/sbin/logcheck.sh.old
```

- 2. 以 **root** 用户身份登录后，使用任何文本编辑器打开脚本并进行任何更改。以下项目符号列表描述了您可能想要更改的值。

- • **SYSADMIN**：此变量将 root 用户定义为运行 Logcheck 后接收电子邮件的人。您可以将 *root* 更改为您希望接收 LogSentry 消息的任何人。这可以是本地用户，也可以是其他计算机上的用户（即 *user@hostname*）。

```
SYSADMIN=root
```

- • **TMPDIR**：设置 LogSentry 在处理期间写入临时文件的位置。该目录在 LogSentry 启动时创建，并在 Logcheck 完成前删除。您可以通过修改以下条目来更改位置：

```
TMPDIR=/tmp/logcheck$$-$RANDOM
```

- • **GREP**：logcheck.sh 脚本依赖于支持 *-i*、*-v* 和 *-f* 选项的 *grep* 命令来搜索日志文件。默认情况下，使用 *egrep* 命令用于此目的。您可以通过修改以下变量将值更改为 *grep* 或其他命令：

```
GREP=egrep
```

- • **MAIL**：LogSentry 使用 *mail* 命令发送电子邮件。要让 LogSentry 使用除 *mail* 命令之外的命令向管理员发送电子邮件，请更改以下 *mail* 变量：

```
MAIL=mail
```

- • **Filter files**：LogSentry 定义了四个过滤文件。每个文件都包含用于查找消息或排除包含这些关键字的消息的关键字。以下变量设置为指示四个 LogSentry 过滤文件的位置：

```
HACKING_FILE=/etc/logsentry/logcheck.hacking
VIOLATIONS_FILE=/etc/logsentry/logcheck.violations
VIOLATIONS_IGNORE_FILE=/etc/logsentry/logcheck.violations.ignore
IGNORE_FILE=/etc/logsentry/logcheck.ignore
```

有关过滤文件的更多信息，请参阅本章后面的“更改 LogSentry 过滤文件”部分。

- • **Log files**：您可能想要更改的 */usr/sbin/logcheck.sh* 脚本中的最后条目指定了 *logcheck.sh* 脚本监控哪些日志文件。默认情况下，脚本运行 *logtail* 命令检查 *messages*、*secure* 和 *maillog* 文件（位于 */var/log*）。以下行定义了要检查哪些日志文件，并确定 *logtail* 的输出临时写入的位置。

```
$LOGTAIL /var/log/messages > $TMPDIR/check.$$
```
