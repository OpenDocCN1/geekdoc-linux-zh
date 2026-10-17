
编写复杂的转换条目是一项交给 Linux/UNIX 专家的任务，但带有 `wu-ftpd` 的 `ftpconversions` 文件为普通管理员提供了足够的的示例。构建你自己的简单转换条目并不困难，让我们来检查并解码一个示例：

```
:Z: /bin/compress -d -c %s:T_REG;T_ASCII:0_UNCOMPRESS:UNCOMPRESS
```

在此示例中，第一个前缀（字段 1）为空，因为它尚未被实现，因此该规则不适用于前缀。该规则的第二个字段包含 `.z` 后缀；因此它处理的是使用 `compress` 工具压缩的文件。该规则没有处理添加前缀或后缀，字段 3 和 4 为空。字段 5 是外部命令字段，它告诉服务器运行 `compress` 工具来解压具有 `.z` 扩展的文件，正如 `-d` 参数所指定的。`-c` 选项告诉 `compress` 将 `compress` 工具的输出写入到标准输出（在此情况下是服务器）。`%s` 是应用该规则的文件名。字段 6 指定该文件是 ASCII 格式的普通文件。字段 7 是选项字段，它告诉服务器。最后，最后一个字段是注释，让管理员快速解码该转换规则正在做什么，即解压缩文件。

![](img/757e95bd85c59465935194247625328c_611_0.png)

`wu-ftpd` 的默认 `ftpconversions` 文件中可以指定多个转换规则。额外的示例（例如针对 Sun 的 Solaris 操作系统）可能在额外的 `wu-ftpd` 文档中找到。

# 在 fthosts 文件中使用命令允许或拒绝 FTP 服务器连接

`fthosts` 文件的允许或拒绝特定用户或地址连接到 FTP 服务器。该文件的格式为 `allow` 或 `deny` 后面跟用户名，然后是 IP 地址或 DNS 地址。

```
allow username
deny username
```

列表 23.3 显示了该文件的示例配置。

```
LISTING 23.3 用于允许或拒绝用户的 fthosts 文件
# 示例主机访问文件
#
# '#' 之后的内容被视为注释，
# 空行会被忽略
allow tdc 128.0.0.1
```

## 列表 23.3 继续

```
allow tdc 192.168.101.*
allow tdc insanepenguin.net
allow tdc *.exodous.net
deny anonymous 201.*
deny anonymous *.pilot.net
```

`*` 是通配符，可以匹配该地址的任何部分。例如，`allow tdc *.exodous.net` 不允许用户 `tdc` 从任何包含 `exodous.net` 域名的地址登录 FTP 服务器。同样，如果匿名用户来自 201 公共 C 类 IP 地址，将不允许其访问 FTP。

对 FTP 服务器配置文件的更改只有在重启 `inet` 后才会生效，因为配置文件仅在启动时解析。要以 root 身份重启 `inet`，请执行命令 `/etc/init.d/inetutils-inetd restart`。这将调用在系统启动和任何运行级别关闭时调用的相同脚本来启动 `inet` 守护进程。`inetd` 报告其状态如下：

```
# /etc/init.d/inetutils-inetd restart
Stopping internet superserver inetd:
[ ]
OK
Starting internet superserver inetd:
[ ]
OK
```

一旦重启，FTP 服务器将对所有传入的请求开放。

# 服务器管理

`wu-ftp` 提供了几个命令来辅助服务器管理。这些命令是：

- `ftpwho`--显示当前 FTP 服务器用户的信息
- `ftpcount`--按类别显示当前服务器用户的信息
- `ftprestart`--提供自动服务器重启和移除关机消息

这些每个命令都必须以超级用户权限执行，因为它们引用了 `ftppass` 配置文件来获取 FTP 服务器的信息。

## 显示已连接用户的信息

`_ftpwho` 命令提供当前连接到 FTP 服务器的用户信息。以下是命令行：

`/usr/bin/ftpwho`

表 23.3 显示了 `ftpwho` 显示的输出格式。

| 名称 | 描述 |
| --- | --- |
| Process ID | FTP 服务器进程的进程 ID。 |
| TTY | 进程的终端 ID。这将始终是一个 `?`，因为 FTP 守护进程不是交互式登录。 |
| Status | FTP 进程的状态。值为 S: 睡眠，Z: 僵尸（表示崩溃），R: 运行，N: 正常进程 |
| Time Details | 经过的处理器时间，以分钟和秒为单位。告知进程连接到哪个主机、连接的用户以及当前正在执行的命令。 |

列表 23.4 显示了该命令的典型输出。它列出了处理请求的 ftp 守护进程的进程 ID、该用户所属的类别、连接总时间、用户以什么用户名连接以及其会话状态。

除了提供的每个用户的信息外，`ftpwho` 还会显示在 `ftppass` 文件中看到的任何最大值之内的连接用户总数。此信息可用于监控你的 FTP 使用情况。

## 列表 23.4 ftpwho -V 输出

```
# ftpwho
Service class all 4 users (no maximum)
```

## 统计连接数

`/usr/bin/ftpcount` 统计连接到 FTP 服务器的用户数和允许的最大用户数。相同的信息可以在 `ftpwho` 命令的输出末尾找到。该命令接受一个参数 `-V`，其输出如上一个示例所示。

```
# ftpcount
Service class all 4 users (no maximum)
```

# 使用 /usr/sbin/ftpshut 调度 FTP 服务器停机

与任何公共服务器管理一样，让 FTP 用户了解即将发生的停机、服务器何时更新以及其他相关信息总是良好的做法。`ftpshut` 命令允许管理员让 FTP 服务器自动完成这些工作。

`ftpshut` 命令允许管理员根据传递的某些参数在特定时间关闭 FTP 服务器。该命令格式如下并在 `ftpshut` 手册页中有记录：

```
ftpshut [ -V ] [ -l min ] [ -d min ] [ warning-message ]
```

- `v` 参数显示命令的版本。时间参数是 `ftpshut` 命令停止 FTP 服务器的时间。该参数可以是 `+` 数字（表示从当前时间起的分钟数），或者是 24 小时制下的特定小时分钟，语法为 `HH:MM`。
- `-l` 参数允许 FTP 服务器管理员指定在关机前多少分钟禁用新连接。此参数的默认值为 10。

分钟。如果给定的服务器关闭时间少于10 分钟，则新连接将立即被禁用。

- `d` 参数与 `-l` 参数相似，但它控制 FTP 服务器何时终止当前连接。默认情况下，这将在服务器关闭前五分钟发生。如果关闭时间少于五分钟，服务器将立即终止连接。

当你执行此命令时，FTP 服务器会创建一个文件，将关机信息捕获在 `ftppass` 文件中 `shutdown` 节（shutdown section）下的指定位置。该文件的默认配置为 `/etc/shutmsg`。如果你在带有警告消息的情况下执行 `ftpshut` 命令，这些消息将在用户登录服务器时显示。

Name (phenix:tdc): anonymous

331 Guest login ok, send your complete e-mail address as password.

Password:

```
230-system going down at Mon Sep 3 06:23:00 2001
230-0 users of unlimited on phenix.
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
```

以下是 `ftpshut` 命令示例：

`ftpshut -l 5 -d +10 "system going down at %s %N users of %M on %R"`

此命令告诉 FTP 服务器在 5 分钟后断开新连接，5 分钟后丢弃所有当前连接，10 分钟后关闭服务器，并在用户登录时向其显示警告消息。消息可以是文本和魔术 Cookie（magic cookies）的混合，定义见表 23.4。需要注意的是，消息的长度只能为 75 个字符。此外，知道魔术 Cookie 将占用多少字符并不重要，因为系统知道这些信息，并将消息截断为 75 个字符。

### 表 23.4 ftpshut 命令的魔术 Cookie

| Cookie | 描述 |
| --- | --- |
| `%s` | 系统关闭的时间 |
| `%r` | 拒绝新连接的时间 |
| `%d` | 终止当前连接的时间 |
| `%C` | 当前工作目录 |
