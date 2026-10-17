
# finger mallory

... Never logged in.

如果你正在追踪入侵者，可以自己从 `last-log` 和 `wtmp` 中隐藏自己的身份，这样入侵者就不知道自己正被监控。运行 `Zap` 需要 `root` 权限——无权限用户不应有访问权限。编译时，使用 `cc -o Zap.c -o zap`。请注意，在 Red Hat Linux 中，你可能需要编辑 `wtmp`、`utmp` 和 `last-log` 文件的路径（`/var/log/wtmp`、`/var/run/utmp` 和 `/var/log/lastlog`）。该工具可在随附的 CD-ROM 上找到。

下载地址：

`ftp://coast.cs.purdue.edu/pub/tools/unix/zap.tar.gz`

# Swatch

UNIX 日志文件提供了海量信息。`Swatch` 工具可将大量的日志记录简化为可操作的项目。它监控写入日志文件的 syslog 消息，并根据模式（例如，有人反复尝试以 `root` 登录的证据）采取预配置的动作（例如，呼叫我的机号号码）。本章将介绍如何安装、配置和运行 `Swatch`，用于实时日志监控和日志文件审计。

## 引言

对于 UNIX 系统管理员来说，监控是一项艰巨的任务，特别是对于那些负责大量主机安全状态的人来说。即使是稍显繁忙的服务器，每天也会产生数千行日志信息，这测试了任何个人筛选所有信息的能力。日志在入侵或安全漏洞发生后往往被忽略，或仅用于审计目的，这并不意外。

`Swatch`（即 Simple WATCH）的设计是为了减轻监控和审计日志文件的负担。该程序的作者描述了他们管理一个拥有 12 台服务器和 50 台机器的设施，所有机器都向一个单一日志主主机报告——重要的日志信息淹没在杂质中。他们开发了 `Swatch` 用来筛选日志，并对报告的事件（即检测到的模式）采取简单的动作。他们在程序中有四个目标：

- 它应该是易于使用的
- 它应该支持一组针对特定消息采取的简单动作
- 它应该支持用户自定义，以便他们定义自己的动作
- 它应该能够根据需要重新配置，而无需人工干预¹

`Swatch` 是他们创建的基于 Perl 的程序，多年来广泛部署，并由作者 Todd Atkins 进一步开发。它已成为许多 UNIX 站的标准配置，包括一些大型安装环境。正如 Lockheed Martin Aeronautics 的一名管理员指出的：“`Swatch` 是我们在真实环境中真的在使用的东西……”² 它已经变得非常主流。

1. Stephen E. Hansen 和 E. Todd Atkins, Stanford University. “Automated System Monitoring and Notification with Swatch,”1993 LISA Conference. 该论文的 Postscript 版本包含在 `Swatch` 分发包中。或访问 `http://www.stanford.edu/~atkins/swatch/lisa93.html`
2. Alek Komarnitsky, Swatch: Automated UNIX System Monitoring & Notification. 访问 `http://www.komar.org/komar/alek/pres/swatch/cover.html`

它包含在某些系统中——例如，Red Hat Linux 包含一个易于安装的 `Swatch` RPM 包。

> 像 `Swatch` 这样的工具的日志文件监控和审计功能应该包含在每个 UNIX 和 Linux 发版中——如果没有，请询问供应商为什么。

## Swatch 概述

`Swatch` 有三种使用方式。它最初的设计是积极监控通过 UNIX syslog 实用写入日志文件的消息。它也可以用于审计——即在单次通过中检查和检查日志文件。最后，它还可以接受来自程序的输入——这对于检查不是以纯文本存储的进程日志非常方便。运行 `Swatch` 的这三种方法（以及相关选项）在第209页的“运行 Swatch”中有更详细的描述。

> `Swatch` 为 syslog 设计，可以监控任何日志文件，包括连接时间记录、slog、Web访问日志等。

无论如何运行 `Swatch`，该工具都依赖于两个关键项：事件模式和相应的动作，这两者都在 `swatch` 配置文件中指定。

## 模式

`Swatch` 可以对各种记录的日志事件采取行动，因为它会匹配日志记录中出现的正则表达式或关键词；“reboot”、“Filesystem Full”、“BAD SU” 和“yourcompetitor.com”都是可能需要采取的模式。`Swatch` 会接受任何与 Perl 兼容的正则表达式， Perl 的行为类似于 `egrep` 程序，而 `egrep` 又是基于 `grep` 程序构建的。

> 有关 `Swatch` 中使用的正则表达式的更多信息，请参阅 `egrep`（或 `grep`）和 `perl` 的手册（man pages）。

# 动作

根据 `.swatchrc` 配置文件中的规范，`Swatch` 监控特定模式并采取以下动作之一：

- `echo`—以反色模式显示消息
- `bell`—显示消息并响起系统铃
- `mail`—将消息邮件给用户
- `exec`—执行命令
- `pipe`—将消息通过到程序
- `write`—使用 `write` 命令通知
- `ignore`—什么都不做

## Swatch 配置文件

`Swatch` 的操作由一个简单的配置文件设置，其中包含制表符分隔的字段：

```
/pattern/ action
```

前两个字段——模式和动作是最关键的。模式是需要匹配的正则表达式，用斜杠包围。如果你想跟踪 Mallory 的活动，模式 `/mallory/` 会捕获它。如果你想看到所有的 `inetd` 消息，`/inetd/` 会提取它们。两个正则表达式可以用管道符 `|` 连接。动作由上述列表的项目之一组成：`echo`, `bell`, `mail`, `exec`, `pipe`, `write` 或 `ignore`。回显文本的外观可以通过关键词进一步指定：`normal`, `bold`, `underscore`, `blink` 或 `inverse`——尽管某些终端不支持 `bold`、`underscore` 或 `blink`。

# 概述（续）

> 如果你运行 Red Hat Linux 和 `bash`，字体、下划线和闪烁模式将不起。你只能使用 `normal`（默认）或 `inverse`，后者可以突出消息。

# 注意

`bell` 动作（`bell=n`）会响起 `n` 次系统铃。紧急消息可以设置铃声响几次。当你在办公室但不在运行 `Swatch` 的终端时，铃声非常有用——例如，每当有失败的登录时，设置它响三次。

`echo` 和 `bell` 动作在 `Swatch` 2.2 分发包包含的“Personal Swatch configuration”中有很好的体现。它被设置为以反色模式显示错误的登录和日志，并在重要事件发生时响三次。其他项目（如 `sendmail`、`新闻`、`网络时间`）被忽略。大多数情况下，内核问题（“文件系统满”）也会响铃。

# 列表 9.1 个人 Swatch 配置文件

```
#
# Personal Swatch configuration file
#
```

```
# 提醒我无效的登录尝试并找出
# 是哪个系统
/INVALID|REPEATED|INCOMPLETE/      echo=inverse,bell-3
```

```
## 重要程序错误
/LOGIN/                          echo=inverse,bell-3
/passwd/                         echo=bold,bell-3
/ruserok/                         echo=bold,bell-3
```

```
## 忽略这些内容
/sendmail/.nntp/.xntp|ntpd/,faxspool/      ignore
```

```
# 报告异常 tftp tp 信息
/tftpd.*(ncd|kfps|normal exit)/      ignore
/tftpd/                           echo,bell-3
```

```
## 内核问题
/(panic|halt|SunOS Release)/ echo-bold,bell
/file system full/ echo-bold,bell-3
/vmunix*(at|on)/ ignore
/vmunix/ echo,bell
```

```
/finger.*(root|[Tt]ip guest)/ echo-bold
/atkins/ echo-inverse,bell-3
```

```
/su:/ echo-bold
/.* echo
```
