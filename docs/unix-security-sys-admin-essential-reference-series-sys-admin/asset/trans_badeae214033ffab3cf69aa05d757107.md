

图 8.1 显示了 /etc/passwd 和 /etc/security/passwd 文件中的示例条目。第一行是 /etc/passwd 中用户的条目；接下来的四行是 /etc/security/passwd 中用户的条目。password 是编码后的密码，lastupdate 是最后一次密码更改的时间和日期，以自 1970 年 1 月 1 日（epoch）以来的秒数计。flags 可以是以下值之一。

NOCHECK /etc/security/login.cfg 中定义的密码限制不被强制执行。这些限制定义了密码老化、字符集以及密码中字符的最大重复次数。

ADMCHG 密码最后是由安全组成员更改的。用户登录时必须更改密码。

ADMIN 只有 root 可以更改此密码。

## 日志文件

AIX 在其中存储登录相关数据的日志文件维护了多个文件。除 /etc/security/lastlog 外，所有这些文件都会一直增长，直到手动减小为止。

/etc/security/failedlogin 包含因任何原因失败的所有登录，无论是无效密码还是用户 ID。此文件包含二进制数据，并且不记录失败的 su 命令。文件的内容可以用 who /etc/security/failedlogin 显示，如以下示例所示。

```
richter pts/4 Sep 09 10:50 (tiger)
root pts/4 Sep 09 10:50 (tiger)
UNKNOWN pts/4 Sep 09 10:50 (tiger)
```

输出列出用户 ID、终端、时间和日期，以及如果登录来自另一台机器则列出远程主机。未知用户 ID 被记为 UNKNOWN。

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_87_0.png)

/var/adm/wtmp 记录所有登录和注销事件。此文件还包括通过 cron 或 at 启动的批处理程序引起的条目，以及由 init 引起的运行级别更改。此文件具有与 /etc/security/failedlogin 相同的格式。如果要记录条目，则必须存在此文件。

/var/adm/sulog 包含 su 命令的所有调用。它是一个 ASCII 文件，其条目如下例所示。

```
SU 09/06 14:09 + pts/1 richter-root
SU 09/06 14:20 - pts/4 richter-root
```

每一行代表一次 su 调用，包含日期、时间、终端、命令的成功 (+) 或失败 (-) 、调用者的用户 ID（本例中为 richter），以及获得的权限（root）。如果要记录条目，则必须存在此文件。

/etc/security/lastlog 包含每个用户最近一次成功或失败登录的详细信息，例如终端、时间和日期，如以下示例所示。

```
richter:
  time_last_login = 779093602
  tty_last_login = hft/0
  host_last_login = tiger
  unsuccessful_login_count = 0
  time_last_unsuccessful_login = 779039875
  tty_last_unsuccessful_login = hft/0
  host_last_unsuccessful_login = tiger
```

这是一个由 root 拥有的 ASCII 文件。time 以自 epoch 以来的秒数记录。成功登录会将字段 unsuccessful_login_count 重置为 0。

## 报告工具

我在此介绍的工具每天检查 /etc/security/failedlogin 并将结果通过邮件发送给系统管理员。lastlogin shell 脚本（清单 8.1）提供 /etc/security/lastlog 的可打印输出。logins 脚本（清单 8.3）按月压缩并保留 /var/adm/sulog 和 /var/adm/wtmp。安全漏洞的影响有时需要一段时间才会显现。通过保留 sulog 和 wtmp 文件以供参考，系统管理员可能能够找到最近更改的系统二进制文件，并使用 inode 和文件更改时间来追踪当时谁已登录以及使用了哪个终端或远程主机。

## 重新打印登录数据

lastlogin shell 脚本读取 /etc/security/lastlog 并根据各种选择标准报告用户。命令语法如下。

```
lastlogin [-c number] [-l days|-r days|-u days] [-h hosts] [-t ttys] [-f file] [user...]
```

### 清单 8.1 lastlogin shell 脚本提供 /etc/security/lastlog 的可打印输出。

```
# Thomas Richter
# Print the last logins in human readable form
# lastlogin [-c number] [-l units|-r units|-u units] [-h hosts] \
# [ -t ttys] [-f file] [user...]
# Following flags are supported:
# -c number: List all users which have an invalid login count
# greater or equal than number.
# -f file: Read input from file, default is /etc/security/lastlog.
# -h hostlist: List all users who logged on from a host in hostlist.
# Hostlist is a comma separated list of host names.
# Default is any host.
# -l units: List all users who have logged on during the last n units.
# If units is zero, list the last logged on details of every entry.
# Displayed fields are time_last_login, tty_last_login,
# host_last_login and unsuccessful_login_count.
# -r units: List all users whose log on failed on during the last n units.
# If units is zero, list refused logged data of every entry.
# Displayed fields are time_last_unsuccessful_login, tty_last_unsuccessful_login,
# host_last_unsuccessful_login and unsuccessful_login_count.
# -t terminallist: List all users who logged on from a terminal in terminallist.
# Terminallist is a comma separated list of terminal names. Default is any terminal.
# -u units: List all users who have not logged on for than n units.
# Displayed fields are time_last_login, tty_last_login,
# host_last_login and unsuccessful_login_count.
# Parameter can be user names.
# All options are and conditions.
# Terminallist and hostlist are mapped against unsuccessful terminal or
# host names if flag -r is specified.
PATH=/usr/bin
typeset -i counter=1 refused=1 last=1 current unused=1
infile=/etc/security/lastlog
# Sort for last/unsused login time
sortfield="*"
current="/var/adm/local/cvttime"
ttyList="*"
hostList="*"
```
