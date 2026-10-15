
`/usr/bin/ftpcount`用于统计连接到 FTP 服务器的用户数量以及允许的最大用户数。`ftpwho`命令的输出末尾也可以找到相同的信息。此命令仅接受一个参数`-V`，用于显示与之前的`ftpwho`示例相同的输出。

```
# ftpcount
Service class all        .  4 users (no maximum)
```

#### 使用 `/usr/sbin/ftpshut` 安排 FTP 服务器停机

与任何公共服务器管理一样，让 FTP 服务器用户了解即将发生的停机、服务器何时更新以及其他相关站点信息始终是良好的做法。`ftpshut`命令允许管理员让 FTP 服务器自动完成大部分工作。

`ftpshut`命令使管理员能够根据传递给它的参数在特定时间关闭 FTP 服务器。命令的格式如下，并在`ftpshut`手册页中有说明：

```
ftpshut [ -V ] [ -l min ] [ -d min ] time [ warning-message ... ]
```

`-V`参数显示命令的版本信息。`time`参数是`ftpshut`命令将停止 FTP 服务器的时间。此参数可以采用从当前时间起的分钟数`+ number`，或 24 小时制下的特定小时和分钟，语法为`HH:MM`。

`-l`参数使 FTP 服务器管理员能够指定在关闭前多少分钟服务器将禁止新的连接。默认值为 10 分钟。如果给定的关闭时间少于 10 分钟，则新连接将立即被禁止。

`-d`参数与`-l`参数类似，但控制 FTP 服务器何时终止当前连接。默认情况下，这发生在服务器关闭前五分钟。如果关闭时间少于五分钟，服务器将立即终止当前连接。

执行此命令时，FTP 服务器会在`ftpaccess`文件中`shutdown`部分指定的位置创建一个包含关闭信息的文件。此文件的默认配置为`/etc/shutmsg`。如果使用警告消息执行`ftpshut`命令，则消息会在用户登录到服务器时显示。

```
Name (pheniox:tdc): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
```

```
230-system going down at Mon Sep  3 06:23:00 2001
230-0 users of unlimited on pheniox.
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
```

下面是一个`ftpshut`命令示例：

```
ftpshut -l 5 -d 5 +10 'system going down at %s %N users of %M on %R'
```

此命令指示 FTP 服务器在 5 分钟后断开新连接，在 5 分钟后断开所有当前连接，在 10 分钟后关闭服务器，并在用户登录时显示警告消息。消息可以是文本和表 18.4 中定义的魔术 cookie 的混合物。需要注意的是，消息的最大长度只能为 75 个字符。此外，无需知道魔术 cookie 将占用多少字符，因为系统知道此信息并在 75 个字符处截断消息。

#### 表 18.4 `ftpshut`命令的魔术 Cookie

| Cookie | Description |
|---|---|
| `%s` | Time the system will be shut down |
| `%r` | Time new connections will be denied |
| `%d` | Time current connections will be dropped |
| `%C` | Current working directory |
| `%E` | Server administrator's email address as specified in the `ftpaccess` file |
| `%F` | Available free space in the current working directories partition, in kilobytes |
| `%L` | Local host time |
| `%M` | Maximum number of allowed connections in this user class |
| `%N` | Current number of connections for this user class |
| `%R` | Remote hostname |
| `%T` | Local time, in the form of Fri Aug 31 21:04:00 2001 |
| `%U` | Username given at login |

当向系统发出`ftpshut`时，它会创建一个存储必要信息的文件。`ftprestart`命令会删除所有服务器的此文件，从而取消即将进行的关闭或删除关闭文件并重新启动 FTP 服务器。`ftprestart`只有一个可选参数`-v`，用于显示版本信息。

#### 使用 `/var/log/xferlog` 查看服务器事务日志

`xferlog`文件记录了 FTP 服务器发生过的事务。根据`/etc/ftpaccess`文件中的设置，此文件的内容可以包含发送或接收的文件、由谁发送、带日期戳。表 18.5 列出了此文件的字段。相同的信息也可以在`wu-ftpd`中包含的相应 man 手册页中找到。

#### 表 18.5 `/var/log/xferlog`字段

| Field | Description |
|---|---|
| `current-time` | 当前本地时间，格式为`DDD MMM dd hh:mm:ss YYYY`，其中`DDD`为星期几，`MMM`为月份，`dd`为月份中的日期，`hh`为小时，`mm`为分钟，`ss`为秒，`YYYY`为年份。 |
| `transfer-time` | 传输总时间（秒）。 |
| `remote-host` | 远程主机名。 |
| `file-size` | 传输文件大小（字节）。 |
| `filename` | 文件名。 |
| `transfer-type` | 表示传输类型的单个字符。类型为`a`表示 ASCII 传输，`b`表示二进制传输 |
| `special-action-flag` | 表示服务器采取的任何特殊操作的一个或多个字符标志。值有`C`表示压缩文件，`U`表示未压缩文件，`T`表示 TAR 文件，`-`表示未采取特殊操作 |
| `direction` | 表示文件是从服务器发送还是由服务器接收。 |
| `access-mode` | 用户登录服务器的方式。值有`a`表示匿名访客用户，`g`表示访客用户，对应`/etc/ftpaccess`文件中的`guestgroup`命令，`r`表示本地机器上的真实用户 |
| `username` | 如果以真实用户身份登录，则为用户名。如果访问模式为访客，则给出密码。 |
| `service-name` | 使用的服务名称，通常为 FTP。 |
| `authentication-method` | 使用的身份验证类型。值有`0`表示无，`1`表示 RFC931 身份验证（格式正确的电子邮件地址） |
| `authenticated-user-id` | 这是根据用于访问服务器的身份验证方法返回给服务器的用户 ID。当无法找到经过身份验证的用户 ID 时使用`*`。 |
| `completion-status` | 表示传输状态的单字符字段。值有`c`表示传输完成，`i`表示传输不完整 |

此文件的示例见清单 18.5。

#### 清单 18.5 包含入站和出站日志的示例 `/var/log/xferlog` 文件

```
Mon Sep  3 07:13:05 2001 1 localhost.localdomain 100
/var/ftp/pub/README b  o a testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/configuration a
_ o a testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/temp.txt a o a
testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/tftp-server-
0.17-14.i386.rpm a  o a testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/wu-ftpd-2.6.1-
22.1.386.rpm a  o a testing@test.com ftp 0 * c
```

#### 相关 Ubuntu 和 Linux 命令
