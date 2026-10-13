
指定启用 /etc/ftpaccess 中指定的访问控制配置。这两个参数非常有用，不应删除。有关其他选项，请参阅 ftpd 手册页。

运行 FTP 服务器而不使用 TCP 包装器 (/usr/sbin/tcpd) 是可能的，但强烈不建议这样做。但是，如果你有非常充分且合理的理由在不使用 TCP 包装器的情况下运行它，则必须按如下方式更改 FTP 服务的默认 /etc/inetd.conf 行：

```
ftp stream tcp nowait root /usr/sbin/in.ftpd -l -a
```

这假定你的 in.ftpd 可执行文件位于 /usr/sbin 目录中。

如果对 /etc/inetd.conf 或 /etc/services 进行了任何更改，请通过发送 SIGHUP 信号来通知 inetd 重新加载配置，如下所示：

```
kill -HUP PID of inetd
```

or

```
killall -HUP inetd
```

## /etc/ftpaccess

这是 FTP 服务器的主要配置文件。该文件包含以下格式的配置信息：

```
keyword one or more options
```

默认的 /etc/ftpaccess 文件如清单 10-1 所示。

### 清单 10-1 默认的 /etc/ftpaccess 文件

```
class all real,guest,anonymous *

email root@localhost

loginfails 5

readme README* login
readme README* cwd=*
```

### 清单 10-1 继续

```
message /welcome.msg login
message .message cwd=*

compress yes all
tar yes all
chmod no guest,anonymous
delete no guest,anonymous
overwrite no guest,anonymous
rename no guest,anonymous
```

```
log transfers anonymous,real inbound,outbound
```

```
shutdown /etc/shutmsg
```

```
passwd-check rfc822 warn
```

这是服务器最重要的配置文件，因此本章将对其进行详细讨论。你可以在此文件中指定五种类型的配置信息。

## 访问配置

访问配置可以使用 class、deny、limit、noretrieve、loginfails、private、autogroup 和 guestgroup 关键字进行指定。

### class

```
Syntax: class <classname> typelist addrglob
Default: class all real,guest,anonymous *
```

class 关键字用于定义类名并指定属于该类的用户类型。它还指定了类成员可以访问 FTP 服务器的 IP 地址或域名。

参数如下：

- **classname.** 类的任意名称。
- **typelist.** 用户类型的逗号分隔列表。可用的用户类型有三种：real、anonymous 和 guest。real 用户是指在 /etc/passwd 或 /etc/shadow 文件中有有效用户名和密码的人。
- **addrglob.** 可以是主机的 IP 地址、带通配符的部分 IP 地址（如 206.171.50.*）、主机名（如 blackhole.nitec.com）或带通配符的部分域名（如 *.nitec.com）。

默认的 /etc/ftpaccess 文件包含一个名为 all 的类定义，指定类型为 real、guest 和 anonymous 的用户可以从任何地方访问 FTP 服务器。通配符 * 用于表示“任何地方”。

在以下示例中，仅允许从 206.171.50.0 网络访问服务器的 real 用户进行 FTP 访问：

```
class all real 206.171.50.*
```

你也可以使用域名代替 IP 地址，如以下示例所示：

```
class all real *.nitec.com *.ad-engine.com
```

前面的类定义允许 real 用户从 nitec.com 和 ad-engine.com 域中的任何机器登录。

如果不打算在 FTP 服务器上允许匿名或访客账户，可以从 all 类的默认 typelist 中删除 guest 和 anonymous 关键字。

### deny

语法：deny addrglob message_file
默认值：none

该关键字用于拒绝与指定 IP 地址或域名匹配的主机的 FTP 服务。例如，

`deny *.edu`

告诉 FTP 服务器拒绝任何尝试从美国大学访问服务器的人的访问。另一个示例是：

`deny *.com /etc/goaway.msg`

此配置拒绝 .com 域中任何人的 FTP 访问，并显示 /etc/goaway.msg 文件。

### limit

语法：`limit class n times message_file`
默认值：none

该关键字限制指定类的同时用户登录数。参数如下：

- **n.** 允许访问的用户数。
- **times.** 指定限制应适用的时间。时间可以用 24 小时制格式指定。例如，0700–1700 是一个涵盖上午 7 点至下午 5 点的范围。时间格式还可以包括日期，如表 10-1 所示。

### 表 10-1 limit 的时间格式

| 关键字 | 含义 |
|---|---|
| Any | 任何时间 |
| Wk | 任何工作日 |
| Sa | 星期六 |
| Su | 星期日 |
| Mo | 星期一 |
| Tu | 星期二 |
| We | 星期三 |
| Th | 星期四 |
| Fr | 星期五 |

你也可以组合日期。例如：SaSu07-17 涵盖周末上午 7 点至下午 5 点。以下是设置访问限制的示例配置：

```
class local real anonymous *.nitec.com
class remote anonymous *

limit local 200 Any /etc/msgs/msg.toomany
limit remote 100 Any /etc/msgs/msg.toomany
```

前面的配置允许 nitec.com 域的用户在任何时间最多登录 200 人，并且仅允许 100 个匿名用户在任何时间访问系统。

### noretrieve

语法：noretrieve filename filename . . .
默认值：none

该关键字拒绝 FTP 用户检索命名文件的能力。例如，

```
noretrieve /etc/passwd
```

拒绝任何人检索 /etc/passwd 文件的能力。会显示类似“/etc/passwd 已标记为不可检索”的消息。请注意，如果文件名不包含完全限定路径名，则所有具有此类名称的文件都将被标记为不可检索。例如，

```
noretrieve passwd core
```

防止任何人从任何目录检索名为 passwd 或 core 的文件。文件名中不能使用通配符。

### loginfails

语法：loginfails number
默认值：loginfails 5

该关键字定义用户在断开连接之前可以尝试登录的次数。当用户在指定次数内未能输入有效的用户名/密码组合进行登录时，会记录错误消息并断开用户连接。

### private

语法：private yes or no
默认值：none

wu-ftpd 服务器提供了一组扩展的非标准 FTP 命令。其中一个命令称为 SITE，被认为是一个安全风险。因此，不建议使用 private 关键字。事实上，Red Hat 随附的 wu-ftpd 默认版本中已禁用 SITE 命令。你必须自行编译 wu-ftpd 才能启用 SITE 命令，这是不推荐的。

### guestgroup

语法：guestgroup groupname groupname . . .
默认值：none

该关键字指定应被视为访客用户账户的用户组。

### autogroup

语法：autogroup groupname class [class . . .]
默认值：none

该关键字允许你在匿名用户属于一个或多个指定类时更改其有效组 ID。

## 信息配置

信息配置可以使用 banner、email、message 和 readme 关键字进行指定。

### banner

语法：banner filename
默认值：none

该关键字可用于显示指定文件的内容。通常，许多系统使用横幅来标识系统并提供用户策略和联系信息。

如果使用 banner 关键字在登录前显示文件，一些非标准 FTP 客户端可能无法登录，因为它们无法处理服务器的多行响应。

### email

语法：email user@host
默认值：email root@localhost

该关键字设置 FTP 站点管理员的电子邮件地址。

### message

语法：message path {when {class . . .}}
默认值：message /welcome.msg login
message .message cwd=*

该关键字用于设置在用户登录系统或使用更改目录命令更改目录时要显示的文件名。例如，刚才显示的第一个默认设置会在用户成功登录时显示 /welcome.msg 文件的内容。第二个默认设置会在用户更改目录时显示 .message 文件的内容。当要显示的文件丢失时，不会显示任何内容。

要显示的文件可以包含表 10-2 所示的一个或多个魔术 cookie 字符串。

### 表 10-2 消息文件的魔术 Cookie 字符串

| Cookies | 替换文本 |
|---|---|
| %C | 当前工作目录 |
| %E | ftpaccess 中定义的维护人员的电子邮件地址 |
| %F | CWD 分区中的可用空间（K） |
| %L | 本地主机名 |
| %M | 此类允许的最大用户数 |
| %N | 此类中的当前用户数 |
| %R | 远程主机名 |
| %T | 本地时间（格式为“Thu Nov 15 17:12:42 1990”） |
| %U | 通过 RFC 931 身份验证确定的用户名 |
| %U | 登录时提供的用户名 |

### 清单 10-2 /welcome.msg 文件示例

```
Hello %U

Welcome to %L. You are user %N of possible %M users.
You are logging in from %R.

Local time is %T
```
