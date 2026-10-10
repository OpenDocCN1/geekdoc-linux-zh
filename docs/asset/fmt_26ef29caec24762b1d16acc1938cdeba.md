
fthosts 文件的作用是允许或拒绝特定用户或地址连接 FTP 服务器。该文件的格式为 `allow` 或 `deny` 单词，可选接用户名，后接 IP 或 DNS 地址。

```
allow username address
deny username address
```

# 使用命令进行服务器管理

列表 20.3 显示了该文件的示例配置。

## 列表 20.3 用于允许或拒绝用户的 fthosts 配置文件

`**` 是一个通配符，可匹配该地址的任何组合。例如，`allow tdc *.exodous.net` 允许用户 `tdc` 从任何包含域名 `exodous.net` 的地址登录到 FTP 服务器。同样，如果匿名用户来自 201 公共网网类 IP 地址，则不允许其访问 FTP。

对系统 FTP 服务器配置文件的更改只有在重启 `xinetd` 后才会生效，因为配置文件是在启动时解析的。要以 root 身份重启 `xinetd`，请执行命令 `/etc/rc.d/init/xinetd restart`。这会调用在系统启动和关机时任何级别都会使用的同一个 shell 脚本，以停止或启动 `xinetd` 守护进程。`xinetd` 报告其状态如下：

```
# /etc/rc.d/init/xinetd restart
Stopping xinetd [ OK ]
Starting xinetd [ OK ]
```

当 FTP 服务器重启时，它将对所有入站请求开放。

## 使用命令进行服务器管理

`wu-ftpwho` 提供了几个辅助服务器管理的命令。这些命令包括：

- `ftpwho`—显示当前 FTP 服务器用户的相关信息
- `ftpcount`—按类别显示当前服务器用户信息
- `ftpshut`—提供自动服务器关机和用户通知
- `ftpstart`—提供自动服务器重启和移除关机消息

这些命令中的每一个都必须以超级用户权限执行，因为它们引用了 `ftpaccess` 配置文件来获取 FTP 服务器的信息。

### 显示有关已连接用户的信息

`ftpwho` 命令提供了当前连接到 FTP 服务器的用户信息。该命令如下：

```
/usr/bin/ftpwho
```

表格 20.3 显示了 `ftpwho` 显示的输出格式。

| way | 描述 |
| --- | --- |
| Process ID | FTP 服务器进程的进程 ID (PID)。 |
| TTY | 进程的终端 ID。这始终是一个问号 (?)，因为 FTP 守护进程不是交互式登录。 |
| Status | FTP 进程的状态。值有：S: 睡眠（Sleeping），R: 僵尸（Zombie，表示崩溃），R: 运行（Running），N: 正常进程（Normal process）。 |
| Time | 进程使用的处理器时间，以分钟和秒计算。 |
| Details | 告知连接的来源、已连接的用户以及正在执行的命令。 |

列表 20.4 显示了该命令的典型输出。它列出了处理请求的 FTP 守护进程的进程 ID、特定用户所属的类别、总连接时间、连接的用户名以及会话状态。

除了关于每个连接用户提供的信息外，`ftpwho` 还显示了连接用户的总数，并与 `ftppass` 文件中设置的最大值进行比较。这些信息可以用于监控你的 FTP 服务器的使用情况。

你可以向 `ftpwho` 传递一个参数。（你可以通过使用 `ftpwho --help` 命令找到该参数。）你可以传递给 `ftpwho` 的唯一参数是 `-v`。此参数打印出 `wu-ftp` 的版本和许可信息，如下：

```
# ftpwho
Service class all:
10447 ?      SN      0:00 ftppd: anonymous/winky@disney.com: IDLE
1 users (no maximum)
```

使用 `-V` 选项显示版本信息的 `ftpwho` 输出如列表 20.4 所示。

### 列表 20.4 ftpwho -V 命令输出

版权所有 © 1999, 2000, 2001 WU-FTPD 开发小组。

保留所有权利。

部分版权 © 1980, 1985, 1988, 1989, 1990, 1991, 1993, 1994

加州大学摄事会。

部分版权 © 1993, 1994 圣路易斯华盛顿大学。

部分版权 © 1996, 1998 Berkeley Software Design, Inc.

部分版权 © 1989 马萨诸塞塞理工学院。

部分版权 © 1998 Sendmail, Inc.

部分版权 © 1983, 1995, 1996, 1997 Eric P. Allman。

部分版权 © 1997 由 Stan Barber。

部分版权 © 1997 由 Kent Landfield。

部分版权 © 1991, 1992, 1993, 1994, 1995, 1996, 1997

Free Software Foundation, Inc.

本软件及其源代码的使用和分发受 WU-FTPD 软件许可协议（"LICENSE"）条款和条件的约束。

如果你没有收到许可协议副本，可以在网上通过 `http://www.wu-ftpd.org/license.html` 获取。

版本 `wu-2.6.2-8`

### 统计连接数

`/usr/bin/ftpcount` 统计连接到 FTP 服务器的用户数以及允许的最大用户数。这些信息可以在 `ftpwho` 命令的输出末尾找到。该命令仅接受参数 `-V`，显示与上一个 `ftpwho` 示例相同的输出。

```
# ftpcount
Service class all             4 users
```

### 使用 /usr/sbin/ftshutdown 设置服务器停机时间

对于任何服务器管理，使用 `ftshutdown` 让用户知道即将发生的停机、服务器停机时间以及其他相关信息。

# 第 20 章 使用 FTP 进行远程文件服务

`ftshutdown` 命令允许管理员在特定时间关闭 FTP 服务器，根据参数，命令格式如下：

```
ftshutdown [ -V ] [ -l ] [ -d ] time [ warning-message ]
```

`-V` 显示版本信息。`-l` 允许管理员向用户发送警告消息。`-d` 参数指定在关机前多少分钟。

当执行 `ftshutdown` 时，系统会创建一个存储必要信息的文件。`ftstart` 命令移除此文件，以取消关机或重启 FTP 服务器。`ftstart` 只有一个可选参数 `-V`。

## 表格 20.4 魔法 Cookie

| Cookie | 描述 |
| --- | --- |
| `%s` | 系统将关机的时间 |
| `%r` | 新连接将被拒绝 |
| `%d` | 当前连接将被断开 |
| `%C` | 当前工作目录 |
| `%E` | `ftpaccess` 中指定的服务器管理员邮箱地址 |
| `%F` | 当前分区的可用空间，以 KB 为单位 |
| `%L` | 本地时间 |
| `%M` | 此类别的允许连接数 |
| `%N` | 此类别的当前连接数 |
| `%R` | 远程主机 |
| `%T` | 本地时间，格式为 Fri Aug 31 21:04:00 2001 |
| `%U` | 登录用户名 |

## 使用 /var/log/xferlog 查看服务器事务日志

`xferlog` 文件记录了 FTP 服务器发生的事务。根据 `/etc/ftpaccess` 文件的设置，该文件的内容包含发送或接收的文件、用户以及时间戳。表格 20.5 列出了该文件的字段。相同的信息也可以 wu-RPM 包中相应的帮助文档找到。

### 表格 20.5 /var/log/xferlog 字段

| 字段 | 描述 |
| --- | --- |
| current-time | 格式为 DDD MMM dd hh:mm:ss YYYY 当前时间，其中 DDD 是星期，MMM 是月份，dd 是日期，hh 是小时，mm 是分钟，ss 是秒，YYYY 是年份。 |
| transfer-time | 传输的总时间（秒）。 |
| remote-host | 远程主机。 |
| file-size | 传输的文件大小（字节）。 |
| filename | 文件名。 |
| transfer-type | 表示传输类型的单个字符。类型为 a（ASCII 传输）或 b（二进制传输）。 |
| special-action-flag | 一个或多个字符标志，指示服务器执行的任何特殊操作。其值为 C 表示压缩文件，U 表示未压缩文件，T 表示 TAR 包文件 - 表示未执行任何特殊操作。 |
| direction | 表示文件是从服务器发送的，还是由服务器接收的。 |

### 表格 20.5 续

| 字段 | 描述 |
| --- | --- |
| 字段 | 描述 |
