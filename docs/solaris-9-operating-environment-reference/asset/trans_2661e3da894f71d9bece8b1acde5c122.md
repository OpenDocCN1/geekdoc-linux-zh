

# uptime

# uptime — 显示系统运行时间

# 概要

/usr/bin/uptime

# 描述

uptime 命令打印当前时间、系统运行长度，以及过去 1、5 和 15 分钟内运行队列中的平均作业数。它本质上是某个命令(1) 输出的第一行。

> 注意 — 你可以使用 `who -b` 命令来显示系统最后启动的时间。

# 示例

以下示例显示了 uptime 的输出。

```
castle@ uptime
10:47am up 27 day(s), 50 mins, 1 user, load average: 0.18, 0.26, 0.20
castle@
```

# 属性

有关以下属性的描述，请参阅 attributes(5)：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNWsu |

# 参阅

w(1), who(1), whodo(1M), attributes(5)

# users — 显示登录用户的精简列表

# 概要

/usr/ucb/users [filename]

# 描述

users 命令以精简的行格式列出当前登录系统的用户登录名。指定 filename 可告诉 users 从哪里查找信息；默认情况下，它检查 /var/adm/utmpx。

users 命令等同于输入 `who -q`。

# 1494

# uucp, uulog, uaname

# 示例

以下示例显示四个用户登录了 castle 系统。

```
castle$ users
winsor ray des rob
castle%
```

# 文件

```
/var/adm/utmpx
```

# 属性

有关以下属性的描述，请参阅 attributes(5)：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNWscpu |

# 参阅

who(1), attributes

# uucp, uulog, uaname — UNIX到UNIX 系统复制

# 概要

```
/usr/bin/uucp [-c] [-C] -d [-f] [-grade] [-jmr] [-user] [-sfile] [-xdebug-level]
source-file destination-file
/usr/bin/uulog [-ssys] [-f system] [-x] [-number] system
/usr/bin/uaname [-c -1]
```

# 描述

uucp (UNIX-to-UNIX copy) 命令套是数据通信子系统的一部分，它允许你在系统之间传输 ASCII 和二进制文件、执行命令、为以后的传输排队作业，并在传输失败时自动重试。完整的 uucp 命令套包含了用户命令和功能、安全特性、日志记录和调试工具，以及多种数据传输协议。本节描述了 uucp、uulog 和 uan 命令。

# uucp

uucp 将由 `source-file` 参数指定的文件复制到 `destination-file` 参数指定的位置。

# uulog

uulog 查询 uucp 或 uuxqt 事务的日志文件，该文件路径为 /var/uucp/.Log/uucico/system 或 /var/uucp/.Log/uxxqt/system。

# uaname

uaname 列出 uucp 已知的系统名称。

# uucp, uulog, uuname

出于安全考虑，远程访问文件的范围可能受到严格限制。你可能无法通过路径名访问文件；请请求远程系统的负责人员将文件发送给你。出于同样的原因，你可能无法将文件发送到任意路径名。作为分布式，远程访问的文件是指是以 /var/spool/uupublic（相当于 ~）开头的文件。所有文件都由 uucp 接收。

受保护的文件和位于保护目录下的文件归请求者所有，可以通过 uucp 发送。然而，如果请求者是 root 且目录对其他人不可搜索，或者文件对其他人不可读，则请求失败。
传递到远程系统的字符串可能不会在本地系统调用 uucp 的进程相同的区域（locale）中进行评估。
配置文件必须被视为 C-（或 POSIX-）文本文件。

# 选项

# uucp

- -c
  - 不将本地文件复制到打印机目录以传输到系统（默认）。
  - 强制将本地文件复制到打印机目录以传输。
  - 为文件复制创建所有必要的目录（默认）。
  - 不为文件复制创建中间目录。
-grade
  - 指定单个字母、数字或定义服务等级的字母数字字符串作为等级。使用 uuglist 命令可以确定使用单个字母、数字或字母数字字符串作为服务等级是否合适。uulist 命令的输出是可用服务等级列表，或提示使用单个字母或数字作为服务等级的消息。
-j
  - 在标准输出上打印 uucp 作业识别字符串。可以通过 uustat 查看此作业识别以获取 uucp 作业的状态。
-m
  - 传输时向请求者发送邮件。
-n
  - 通知用户传输完成。
-r
  - 将作业排队等待传输。
-sfile
  - 报告传输状态。
-xdebug-level
  - 调试输出，0 到 9 之间的数字。
-x
  - 调试信息。

# 1494

# uucp, uulog, uaname

-s
  - 报告传输状态。
-r
  - 将作业排队等待传输。
-n
  - 通知用户传输完成。
-m
  - 传输时向请求者发送邮件。

# 1496

# uucp, uulog, uaname

-f
  - 使用日志文件。
-n
  - 使用行数。
-s
  - 使用系统名。
-sys
  - 使用系统文件。
-x
  - 使用 字符。

# 1497

# uucp, uulog, uuname

-c
  - 使用登录名。
-f
  - 使用日志文件。
-m
  - 使用邮件选项。
-n
  - 使用行数。
-r
  - 将作业排队等待传输。
-sys
  - 使用系统文件。
-x
  - 使用 字符。

