

`-l` 和 `-a` 选项是默认指定的。`-l` 选项指定通过 syslog 设施记录每个 FTP 会话，而 `-a` 选项指定启用在 `/etc/ftpaccess` 中指定的访问控制配置。这两个参数非常有用，不应移除。有关其他选项，请参阅 ftpd 的手册页（man page）。

如果你对 `/etc/xinetd.d/vu-ftpd` 或 `/etc/services` 进行了任何更改，请通过发送 SIGUSR1 信号来告知 xinetd 重新加载配置，如下所示：

```
kill -USR1 PID of xinetd

or

killall -USR1 xinetd
```

## /etc/ftpaccess

这是 FTP 服务器的主要配置文件。此文件包含以下格式的配置信息：

```
keyword one or more options
```

默认的 `/etc/ftpaccess` 文件如清单 10-1 所示。

### 清单 10-1 默认的 `/etc/ftpaccess` 文件

```
class    all     real,guest,anonymous    *
email    root@localhost
loginfails    5
readme    README*    login
readme    README*    cwd=*
message    /welcome.msg    login
message    .message    cwd=*
compress    yes    all
```

```
tar           yes    all
chmod         no     guest,anonymous
delete        no     guest,anonymous
overwrite     no     guest,anonymous
rename        no     guest,anonymous

log transfer  anonymous,real inbound,outbound

shutdown /etc/shutmsg

passwd-check  rfc822 warn
```

这是服务器最重要的配置文件，因此本章将对此进行详细讨论。你可以在该文件中指定五种类型的配置信息。

### 访问配置

可以使用 class、deny、limit、noretrieve、loginfails、private、autogroup 和 guestgroup 关键字指定访问配置。

#### class

**语法：** `class classname typelist addrglob`
**默认：** `class all real,guest,anonymous *`

class 关键字用于定义类名并指定属于该类的用户类型。它还指定了类成员可以访问 FTP 服务器的 IP 地址或域名。参数如下：

- **classname.** 类的任意名称。
- **typelist.** 用户类型的逗号分隔列表。有三种可用的用户类型：real（真实用户）、anonymous（匿名）和 guest（访客）。真实用户是指在 `/etc/passwd` 或 `/etc/shadow` 文件中拥有有效用户名和密码的用户。
- **addrglob.** 可以是主机的 IP 地址、带通配符的部分 IP 地址（例如 206.171.50.*）、主机名（例如 blackhole.nitec.com）或带通配符的部分域名（例如 *.nitec.com）。

默认的 `/etc/ftpaccess` 文件包含一个名为 `all` 的类定义，它指定类型为 `real`、`guest` 和 `anonymous` 的用户可以从任何地方访问 FTP 服务器。通配符 `*` 用于表示“任何地方”。

在以下示例中，仅授予从 `206.171.50.0` 网络访问服务器的真实用户的 FTP 访问权限：

```
class    all    real 206.171.50.*
```

你还可以使用域名代替 IP 地址，如下例所示：

```
class    all    real *.nitec.com *.ad-engine.com
```

上述类定义允许真实用户从 `nitec.com` 和 `ad-engine.com` 域中的任何机器登录。

如果你不打算在 FTP 服务器上允许匿名或访客账户，可以从 `all` 类的默认 `typelist` 中移除 `guest` 和 `anonymous` 关键字。

#### deny

**语法：** `deny addr_glob message_file`
**默认：** 无

此关键字用于拒绝与指定 IP 地址或域名匹配的主机的 FTP 服务。例如，

```
deny  *.edu
```

指示 FTP 服务器拒绝任何尝试从美国大学访问服务器的人。以下是另一个示例：

```
deny  *.com   /etc/goaway.msg
```

此配置拒绝任何 `*.com` 域中的人员的 FTP 访问，并显示 `/etc/goaway.msg` 文件。

#### limit

**语法：** `limit class n times message_file`
**默认：** 无

此关键字限制指定类的同时用户登录数。参数如下：

- **n.** 允许访问的用户数量。
- **times.** 指定限制何时生效。时间可以以 24 小时制格式指定。例如，0700–1700 是涵盖上午 7 点至下午 5 点的范围。时间格式也可以包括天数，如表 10-1 所示。

**表 10-1 limit 的时间格式**

| 关键字 | 含义 |
| :--- | :--- |
| Any | 任何时间 |
| Wk | 任何工作日 |
| Sa | 星期六 |
| Su | 星期日 |
| Mo | 星期一 |
| Tu | 星期二 |
| We | 星期三 |
| Th | 星期四 |
| Fr | 星期五 |

你还可以组合天数。例如：SaSu07–17 涵盖从上午 7 点到下午 5 点的周末。以下是一个设置访问限制的配置示例：

```
class  local   real     *.nitec.com
class  remote  anonymous  *

limit local  200  Any /etc/msgs/msg.toomany
limit remote 100  Any /etc/msgs/msg.toomany
```

上述配置允许来自 nitec.com 域的多达 200 名用户在任何时间登录，并且仅允许 100 名匿名用户在任何时间访问系统。

#### noretrieve

**语法：** `noretrieve filename filename . . .`
**默认：** 无

此关键字禁止 FTP 用户检索指定名称的文件。例如，

```
noretrieve /etc/passwd
```

禁止任何人检索 /etc/passwd 文件。会显示诸如“/etc/passwd 被标记为不可检索”之类的消息。请注意，如果文件名不包含完全限定路径名，则所有具有此类名称的文件都被标记为不可检索。例如，

```
noretrieve passwd core
```

防止任何人从任何目录检索任何名为 passwd 或 core 的文件。文件名中不能使用通配符。

#### loginfails

**语法：** `loginfails number`
**默认：** `loginfails 5`

此关键字定义用户在断开连接前可以尝试登录的次数。当用户在指定次数内未能输入有效的用户名/密码对进行登录时，会记录错误消息并断开该用户的连接。

#### private

**语法：** `private yes or no`
**默认：** 无

wu-ftpd 服务器提供了一组非标准的扩展 FTP 命令。其中一个命令称为 SITE，被视为安全风险。因此，不建议使用 private 关键字。事实上，随 Red Hat 发行的 wu-ftpd 默认版本中已禁用了 SITE 命令。你需要自行编译 wu-ftpd 才能启用 SITE 命令，但不推荐这样做。

#### autogroup

**语法：** `autogroup groupname class [class . . . ]`
**默认：** 无

此关键字允许你更改匿名用户的有效组 ID，前提是该用户属于一个或多个指定的类。

### 信息配置

可以使用 banner、email、message 和 readme 关键字指定信息配置。

#### banner

**语法：** `banner filename`
**默认：** 无

此关键字可用于显示指定文件的内容。通常，许多系统使用横幅（banner）来标识系统并提供用户策略和联系信息。

如果你使用 banner 关键字在登录前显示文件，某些非标准 FTP 客户端可能无法登录，因为它们无法处理来自服务器的多行响应。

#### email

**语法：** `email user@host`
**默认：** `email root@localhost`

此关键字设置 FTP 站点管理员的电子邮件地址。

#### message

**语法：** `message path {when [class . . . ]}`
**默认：** `/welcome.msg login`, `.message cwd=*`

此关键字用于设置在用户登录系统或使用更改目录命令切换目录时显示的文件名称。例如，上面显示的第一个默认设置会在用户成功登录时显示 /welcome.msg 文件的内容。第二个默认设置会在用户更改目录时显示 .message 文件的内容。如果要显示的文件缺失，则不会显示任何内容。

