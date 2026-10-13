
`-v` 参数显示命令的版本信息。`time` 参数是 `ftshutdown` 命令停止 FTP 服务器的时间。该参数可以接受从当前时间起算的分钟数（`+` 数字），或者是采用 `HH:MM` 格式的 24 小时制的小小时或分钟。

`-l` 参数允许 FTP 服务器管理员指定在关机前多少分钟服务器将禁用新连接。其默认值为 10 分钟。如果给定的关机时间小于 10 分钟，则新连接将立即禁用。

`-d` 参数与 `-l` 参数类似，但它控制 FTP 服务器何时终止当前连接。默认情况下，这将在服务器关闭五分钟前发生。如果关机时间少于五分钟，服务器将立即终止连接。

当你执行此命令时，FTP 服务器会在 `ftpassconf` 文件中 `shutdown` 部分指定的位置创建一个包含关机信息的文件。该文件的默认配置为 `/etc/ftmsg`。如果你在执行 `ftshutdown` 命令时带有警告消息，则这些消息将在用户登录服务器时显示。

Name (phenix:tdc): anonymous

331 Guest login ok, send your complete e-mail address as password.

Password:

230-system going down at Mon Sep 3 06:23:00 2001

230-0 users of unlimited on phenix.

230 Guest login ok, access restrictions apply.

Remote system type is UNIX.

Using binary mode to transfer files.

以下是一个 `ftshutdown` 命令示例：

```
ftshutdown -l 5 -d 5 +10 "system going down at %s %N users of %M on %R"
```

该命令告诉 FTP 服务器在 5 分钟后断开新连接，5 分钟后丢弃所有当前连接，10 分钟后关闭服务器，并在用户登录时显示警告消息。消息可以是文本和表 18.4 中定义的魔术 Cookie（magic cookies）的混合。请记住消息的长度只能为 75 个字符。此外，知道魔术 Cookie 将占用多少字符并不重要，因为系统知道这些信息并将在 75 个字符处截断消息。

### 表 18.4 ftshutdown 的魔术 Cookie

| Cookie | 描述 |
| :--- | :--- |
| `%s` | 系统将 |
| `%c` | 时间 |
| `%d` | 当前 |
| `%E` | 类型（的） |
| `%F` | 空闲空间 |
| `%L` | 本地时间 |
| `%M` | 最大数量 |
| `%N` | 远程主机名 |
| `%R` | 远程 |
| `%T` | 登录为 |

### 表 18.5 /var/xferlog 字段

| 字段 | 描述 |
| :--- | :--- |
| current-time | 本地时间 |
| remote-host | 远程主机名 |
| file-size | 传输的文件的大小 |
| filename | 文件名 |
| transfer-type | 表示传输类型的单个字符 |
| special-action-flag | 表示所执行操作的一个或多个标记 |
| direction | 表示文件是从发送还是接收的 |
| access-mode | 用户登录的方式 |
| username | 登录用户 |
| service-name | 使用的服务名称，通常为 FTP |
| authentication-method | 使用的验证方法 |
| authenticated-user-id | 返回给服务器的用户 ID |
| completion-status | 表示传输状态的单个字符 |

# 第 18 章 安全文件协议 (FTP)

`xferlog` 文件记录了发生的情况。根据 `/etc/ftpaccess` 中的设置，该文件的内容可以包含。表 18.5 列出了这些字段。`ftpstart` 有一个可选参数 `-v` 用于显示版本信息。使用 `/var/xferlog` 查看服务器发送的文件。

此文件的示例见列表 18.6。

### 列表 18.6 带有入站和出站日志的 /var/xferlog 文件

```
Mon Sep 3 07:13:05 2001 1 localhost.localdomain 100
/var/ftp/pub/README b 0 a testing@test.com ftp 0 * c
Mon Sep 3 02:35:35 2001 1 helios 8 /var/ftp/pub/configuration a
_ 0 a testing@test.com ftp 0 * c
Mon Sep 3 02:35:35 2001 1 helios 8 /var/ftp/pub/temp.txt a 0 o a
testing@test.com ftp 0 * c
Mon Sep 3 02:35:35 2001 1 helios 8 /var/ftp/tftp-server-
0.17-14.i386.rpm a 0 o a testing@test.com ftp 0 * c
```
