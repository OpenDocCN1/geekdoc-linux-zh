
在此示例中，前缀字段 (1) 为空，因为它尚未实现，因此此规则不适用于前缀。该规则的第二个字段包含 `-Z` 前缀；因此处理的是使用压缩工具压缩的文件。该规则未涉及添加前缀或后缀，字段 3 和 4 为空。字段 5 是外部命令字段，告诉服务器使用指定的压缩工具解压所有 `.z` 扩展的文件，并指定 `-d` 参数。`-c` 选项告诉压缩程序将压缩输出写入标准输出（在这种情况下是服务器）。`%s` 是应用该规则的文件名。字段 6 指定该文件是 ASCII 格式的普通文件。字段 7 告诉服务器该命令解压缩文件。最后，最后一个字段是注释，让管理员快速解码转换规则的作用——即，解压缩文件。

## 使用 fthosts 文件允许或拒绝 FTP 服务器连接

### 示例

`ftpversions` 文件中可以指定多个转换规则。

### 使用 fthosts 文件允许或拒绝 FTP 服务器连接

`fthosts` 的目的是允许或拒绝特定的用户或地址。该文件的格式为 `allow` 或 `deny`，后面可选跟跟用户名，然后是 IP 地址。

列表 18.3 显示了文件的配置：

```
# 访问控制文件
# # 之后是注释
# 空行会被忽略

allow tdc 128.0.0.1
allow tdc 192.168.101.*
allow tdc *.net
deny anonymous .*
```

`*` 是匹配任何地址的通配符。同样，`anonymous` 用户不允许从域名访问 FTP 服务器。

配置更改只有在重启后才会生效。要以 root 身份重启，执行命令 `/etc/init.d/inetd restart`。这将调用与系统启动时相同的 shell。

```
/etc/init.d/inetd restart
```

一旦启动，FTP 服务器即可访问所有传入请求。

## 用于服务器管理的命令

wu-ftp 提供了一些辅助服务器管理的命令。这些命令有：

- `ftpwho`：显示当前 FTP 用户信息
- `ftpcount`：按类别显示当前用户信息
- `ftpshutdown`：提供自动关闭服务器和用户通知
- `ftrestart`：提供自动重启服务器和关闭消息

这些命令必须以超级用户权限执行，因为它们引用了 `passwd` 配置文件来获取 FTP 服务器的信息。

## 显示连接用户

`ftpwho` 命令提供了关于连接到 FTP 服务器的用户的信息。命令行如下：

`/usr/bin/ftpwho`

表格 18.3 显示了 `ftpwho` 输出的格式。

| 名称 | 描述 |
| --- | --- |
| Process ID | FTP 服务器进程的进程 ID。 |
| TTY | 进程的终端 ID。因为 FTP 守护进程不是交互式登录，此处显示为 ? |
| Status | FTP 进程的状态。值为 S: 睡眠，Z: 僵尸，表示崩溃 |
| Time | 进程使用的经过时间（分钟和秒）。 |
| Details | 告知来自哪个主机连接、连接的用户以及当前执行的命令。 |

列表 18.4 显示了该典型输出。它列出了处理请求的 FTP 守护进程 PID、用户所属的类别、总连接时间、连接用户名以及会话状态。

除了提供关于每个连接用户的信息外，`ftpwho` 还会显示连接用户的总数，该人数相对于 `ftppass` 文件中可能设置的最大值。这些信息可以用于监控你的 FTP 服务器的使用情况。

你可以向 `ftpwho` 传递一个参数（你可以使用 `ftpwho -help` 命令查找该参数）。你可以传递给 `ftpwho` 的唯一参数是 `-v`。该参数打印出 wu-ftpd 的版本和许可信息，如下：

```
10447 ?  0:00 ftppd: localhost: anonymous/winky IDLE

1 users (no maximum)
```

使用 `-V` 选项显示版本信息的 `ftpwho` 输出如列表 18.4 所示。

### 列表 18.4 ftpwho -V 命令输出

> 版权 © 1999,2000,2001 WU-FTPD 开发小组。
> 保留所有权利。
>
> 部分版权 © 1980, 1985, 1988, 1989, 1990, 1991, 1993, 1994
> 加州大学董事会。
> 部分版权 © 1993, 1994 圣路易斯华盛大学。
> 部分版权 © 1996, 1988 Berkeley Software Design, Inc.
> 部分版权 © 1989 马萨诸塞理工学院。
> 部分版权 © 1998 Sendmail, Inc.
> 部分版权 © 1983, 1995, 1997 Eric P. Allman。
> 部分版权 © 1997 Stan Barber。
> 部分版权 © 1991, 1992, 1993, 1994, 1995, 1996, 1997
> 部分版权 © 1997 Kent Landfield.
> 自由软件基金会。
>
> 本软件及其源代码的许可和分发受 WU-FTPD 软件许可协议（"LICENSE"）条款和条件的约束。
>
> 如果你没有收到许可协议副本，可以在网上 http://www.wu-ftpd.org/license.html 获取。
> 版本 wu-2.6.2-8

## 统计连接数

`/usr/bin/ftpcount` 统计连接到 FTP 服务器的用户数以及允许的最大用户数。这些信息可以在 `ftpwho` 命令的输出末尾找到。该命令仅接受一个参数 `-v`，它显示与上一个 `ftpwho` 示例相同的输出。

```
服务类 all - 4 users (no maximum)
```

## 使用 /usr/sbin/ftpshut 调度 FTP 服务器停机

与任何服务管理一样，让 FTP 服务器用户了解即将到来的停机、服务器何时更新以及其他相关的站点信息始终是一个良好的做法。`ftpshut` 命令允许管理员让 FTP 服务器自动完成大部分工作。

`ftpshut` 命令允许管理员根据传递给它的某些参数在特定时间关闭 FTP 服务器。命令的格式如下，并在 `ftpshut` 手页中有所记录：

```
ftpshut [-V] [-l min] [-d min] time [warning-message ... ]
```

`-V` 参数显示命令的版本信息。`time` 参数指定 `ftpshut` 命令停止 FTP 服务器的时间。该参数接受从当前时间起的分钟数 `+ 数字`，或者 24 小时制格式（语法为 HH:MM）的特定小时和分钟。

`-l` 参数允许 FTP 服务器管理员指定在关闭服务器前多少分钟开始禁用新连接。默认值为 10 分钟。如果给出的关机时间小于五分钟，则将立即禁用新连接。

`-d` 参数与 `-l` 参数类似，但它控制 FTP 服务器何时终止当前连接。默认情况下，这发生在服务器关闭五分钟前。如果关机时间小于五分钟，服务器将立即终止当前连接。

当你执行此命令时，FTP 服务器会在 `ftppass` 文件中 `shutdown`（停机）部分指定的位置创建一个包含停机信息的文件。该文件的默认配置为 `/etc/shutmsg`。如果你带有警告消息执行 `ftpshut` 命令，这些消息将在用户登录服务器时显示。

```
名称 (phenix:tdc): anonymous

33! 访客登录成功，请将你的完整电子邮件地址作为密码。

密码：
230-系统正在关机 2001年9月3日 06:23:00

230-phenix 上的无限用户 0。

230 访客登录成功，适用访问限制。
远程系统类型为 UNIX。

正在使用二进制模式传输文件。
```

## 使用命令进行服务器管理

这是一个 `ftpshutdown` 示例：

```
ftpshutdown -l 5 -d 5 +10 "system going down at %s %N users of %M on %R"
```

此命令告诉 FTP 服务器 5 分钟后断开新连接，5 分钟后删除所有当前连接，10 分钟后关闭服务器，并在用户登录时向其显示警告消息。消息可以是文本和表 18.4 中定义的魔法术符（magic cookies）的混合。需要注意的是，消息最多只能有 75 个字符。此外，了解魔法术符占用多少字符并不重要，因为系统知道这些信息并将消息截断为 75 个字符。

### 表 18.4 ftpshutdown 的魔法术符

| 魔法术符 | 描述 |
| :--- | :--- |
| %s | 系统将关机的时间 |
| %f | 新连接将的拒绝的时间 |
| %d | 当前连接将的删除的时间 |
| %C | 工作目录 |
| %E | `ftpaccess` 文件中指定的服务器地址 |
| %F | 当前分区的可用空间（千字节） |
| %L | 本地主机名 |
| %M | 用户允许的最大连接数 |
| %R | 远程主机名 |
| %T | 本地时间，格式为 Fri 31 21:04:00 |
| %U | 登录时提供的用户名 |

当执行 `ftpshutdown` 时，系统会创建一个存储必要信息的文件，用于取消即将到来的停机或重启 FTP 服务器。`ftpstart` 命令仅有一个可选参数 `-V` 用于显示版本信息。

## 使用 /var/log/xferlog 查看事务日志

`xferlog` 提供了与 FTP 服务器发生的事务日志。根据 `/etc/ftpaccess` 中的设置，该文件的内容可以包含发送或接收的文件，并带有时间戳。表 18.5 列出了该文件的字段。相同的信息也可以在相应的 `ftp` 页面中找到。

### 表 18.5 /var/log/xferlog 字段

| 字段 | 描述 |
| :--- | :--- |
| current-time | 本地时间，格式为 DDD hh:mm:ss YYYY，其中 DDD 是星期，MMM 是月份，dd 是日期，hh 是小时，mm 是分钟，ss 是秒，YYYY 是年份。 |
| transfer-time | 传输的总秒数。 |
| remote-host | 远程主机名。 |
| file-size | 传输的文件大小（字节）。 |
| filename | 文件名。 |
| transfer-type | 表示传输类型的字符。a 表示 ASCII 传输，b 表示二进制传输 |
| special-action-flag | 表示服务器执行的任何操作。值为 C 表示压缩文件，U 表示未压缩文件，T 表示已传输的文件，- 表示未操作。 |
| direction | 表示文件是从服务器发送还是接收的。 |
| access-mode | 用户登录服务器的方式。值为 a 表示匿名访客用户，g 表示访客用户，r 表示本地机器上的真实用户。 |
| username | 如果作为真实用户登录，则是用户名。如果访问模式为访客，则提供密码。 |
| service-name | 使用的服务名称，通常是 FTP。 |
| authentication-method | 使用的身份验证类型。值为 O 表示无 |
| authenticated-user-id | RFC931 认证（格式正确的电子邮件地址）。这是根据访问服务器的方法返回给服务器的用户 ID。如果找不到认证的用户 ID，则使用 *。 |
| completion-status | 表示传输状态的字符字段。值为 c 表示传输完成，i 表示传输未完成 |

该文件的示例见列表 18.5。

```
列表 18.5 带有入出站日志的 /var/log/xferlog 示例

Mon Sep 3 07:13:05 2001 1 localhost.localdomain 100 /var/ftp/pub/README b o testing@test.com ftp 0 * c

Mon Sep 3 02:35:05 2001 1 helios 8 /var/ftp/pub/configuration a o testing@test.com ftp 0 * c

Mon Sep 3 02:35:05 2001 1 helios 8 /var/ftp/pub/temp.txt a o testing@test.com ftp 0 * c

Mon Sep 3 02:35:05 2001 1 helios 8 /var/ftp/pub/tftp-server-0.17-14.i386.rpm a o testing@test.com ftp 0 * c

Mon Sep 3 02:35:05 2001 1 helios 8 /var/ftp/pub/wu-ftpd-2.6.1-22.i386.rpm a o testing@test.com ftp 0 * c
```
