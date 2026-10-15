
| Status | FTP 进程的状态。取值有 S: 睡眠 Z: 僵尸，表示崩溃 R: 运行中 N: 正常进程 |

| Time | 进程已使用的经过处理器时间，以分钟和秒为单位。 |

| Details | 说明进程连接自哪个主机、连接的用户以及当前正在执行的命令。 |

列表 23.4 显示了此命令的典型输出。它列出了处理请求的 ftp 守护进程的进程 ID，用户所属的类别，总连接时间，用户以哪个用户名连接，以及会话的状态。

除了提供每个已连接用户的信息外，`ftpwho` 还会显示已连接用户总数以及 `ftpassess` 文件中可能设置的任何最大数。此信息可用于监控 FTP 服务器的使用情况。

您可以向 `ftpwho` 传递一个参数。 （您可以通过使用 `ftpwho -help` 命令找到该参数。）您可以传递给 `ftpwho` 的唯一参数是 `-v`。该参数打印 `wu-ftpd` 的版本和许可信息，如下所示：

```
# ftpwho
Service class all:
10447 ?      SN      0:00 ftpd: localhost: anonymous/winky@disney.com: IDLE
1 users (no maximum)
```

使用 `-V` 选项的 `ftpwho` 输出，该选项显示版本信息，如列表 23.4 所示。

# LISTING 23.4 `ftpwho -V` Command Output

Copyright © 1999,2000,2001 WU-FTPD Development Group.

All rights reserved.

Portions Copyright © 1980, 1985, 1988, 1989, 1990, 1991, 1993, 1994

  The Regents of the University of California

Portions Copyright © 1993, 1994 Washington University in Saint Louis.

Portions Copyright © 1996, 1998 Berkeley Software Design, Inc.

Portions Copyright © 1989 Massachusetts Institute of Technology.

Portions Copyright © 1998 Sendmail, Inc.

Portions Copyright © 1983, 1995, 1996, 1997 Eric P. Allman.

Portions Copyright © 1997 by Stan Barber.

Portions Copyright © 1997 by Kent Landfield.

Portions Copyright © 1991, 1992, 1993, 1994, 1995, 1996, 1997

Free Software Foundation, Inc.

Use and distribution of this software and its source code are governed

by the terms and conditions of the WU-FTPD Software License ("LICENSE").

If you did not receive a copy of the license, it may be obtained online

at http://www.wu-ftpd.org/license.html.

Version-v2.6.2-8

# 统计连接数

`/usr/bin/ftpcount` 统计连接到 FTP 服务器的用户数以及允许的最大用户数。 此信息也可在 `ftpwho` 命令输出的末尾找到。此命令仅接受一个参数 `-v`，它显示与之前的 `ftpwho` 示例相同的输出。

```
# ftpcount
Service class all                 -    4 users (no maximum)
```

# 使用 `/usr/sbin/ftpshut` 安排 FTP 服务器停机

与任何公共服务器管理一样，让 FTP 服务器用户了解即将发生的停机、服务器何时更新以及其他相关站点信息始终是良好的做法。 `ftpshut` 命令允许管理员让 FTP 服务器自动完成大部分工作。

`ftpshut` 命令允许管理员根据传递给它的一些参数在特定时间关闭 FTP 服务器。命令的格式如下，并在 `ftpshut` 手册页中有说明：

```
ftpshut [ -V ] [ -l min] [ -d min] time [ warning-message ... ]
```

`-V` 参数显示命令的版本信息。 `time` 参数是 `ftpshut` 命令将停止 FTP 服务器的时间。此参数可以采用 `+ number` 表示从当前时间开始的分钟数，或采用 24 小时制格式的特定小时和分钟，语法为 `HH:MM`。

`-l` 参数允许 FTP 服务器管理员指定在关闭前多少分钟服务器将禁用新连接。默认值为 10 分钟。如果给定的关闭时间少于 10 分钟，新连接将立即被禁用。

`-d` 参数与 `-l` 参数类似，但控制 FTP 服务器何时终止当前连接。默认情况下，这将在服务器关闭前五分钟发生。如果关闭时间少于五分钟，服务器将立即终止连接。

执行此命令时，FTP 服务器会在 `ftpaccess` 文件中 `shutdown` 部分指定的位置创建一个包含关闭信息的 文件。默认配置为此文件为 `/etc/shutmsg`。如果您使用警告消息执行 `ftpshut` 命令，则消息会在用户登录到服务器时显示。

```
Name (pheniox:tdc): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
230-system doing down at Mon Sep 3 06:23:00 2001
230-0 users of unlimited on pheniox.
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
```

下面是一个 `ftpshut` 命令示例：

```
ftpshut -l 5 -d 5 +10 "system going down at %s %N users of %M on %R"
```

此命令告诉 FTP 服务器在 5 分钟后断开新连接，在 5 分钟后断开所有当前连接，在 10 分钟后关闭服务器，并在用户登录时显示警告消息。消息可以是文本和表 23.4 中定义的魔术 cookie 的混合物。需要注意的是，消息长度只能为 75 个字符。此外，不必知道魔术 cookie 将占用多少个字符，因为系统知道此信息并且会在 75 个字符处截断消息。

## 表 23.4 ftpshut 命令的魔术 Cookie

| Cookie | 描述 |

|---|---|

| `%s` | 系统将关闭的时间 |

| `%r` | 新连接将被拒绝的时间 |

| `%d` | 当前连接将被断开的时间 |

| `%C` | 当前工作目录 |

| `%E` | 服务器管理员的电子邮件地址，如 `ftpassess` 文件中指定的 |

| `%F` | 当前工作目录所在分区中的可用空闲空间，以千字节为单位 |

| `%L` | 本地主机时间 |

| `%M` | 此用户类别允许的最大连接数 |

| `%N` | 此用户类别的当前连接数 |

| `%R` | 远程主机名 |

| `%T` | 本地时间，格式为 Fri Aug 31 21:04:00 2001 |

| `%U` | 登录时提供的用户名 |

当向系统发出 `ftpshut` 时，它会创建一个存储必要信息的文件。`ftprestart` 命令会为所有服务器删除此文件，从而取消即将进行的关闭或删除关闭文件并重新启动 FTP 服务器。`ftprestart` 只有一个可选参数，`-v`，用于显示版本信息。

## 使用 `/var/log/xferlog` 查看服务器事务日志

`xferlog` 文件记录了 FTP 服务器发生过的事务日志。根据 `/etc/ftpaccess` 文件中的设置，此文件的内容可以包含谁在何时发送或接收了哪些文件，并附带日期戳。表 23.5 列出了此文件中的字段。相同的信息也可以在 `wu-ftpd` 包中包含的相应 man 手册页中找到。

## 表 23.5 `/var/log/xferlog` 字段

| 字段 | 描述 |

|---|---|

| current-time | 当前本地时间，格式为 DDD MMM dd hh:mm:ss YYYY，其中 DDD 为星期几，MMM 为月份，dd 为月份中的日期，hh 为小时，mm 为分钟，ss 为秒，YYYY 为年份。 |

| transfer-time | 传输总时间，以秒为单位。 |

| remote-host | 远程主机名。 |
