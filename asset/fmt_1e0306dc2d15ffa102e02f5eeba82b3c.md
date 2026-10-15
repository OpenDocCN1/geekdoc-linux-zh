
如果此服务有任何问题，请发送邮件至 `%E`。

你当前的工作目录是 `%C`

将此文件保存为 `/var/ftp/welcome.msg`。通过连接 FTP 服务器来验证其是否有效：

```
220 FTP server ready.
504 AUTH GSSAPI not supported.
504 AUTH KERBEROS_V4 not supported.
504 KERBEROS_V4 rejected as an authentication type
Name (shuffle:phudson): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
230-Welcome to the anonymous ftp service on shuttle.home!
230-
230-There are 1 out of unlimited users logged in.
230-
230-Current system time is Mon Nov 3 10:57:06 2003
230-
230-Please send email to root@localhost if there are
230-any problems with this service.
230-Your current working directory is /
```

# 显示管理员邮箱地址

此行设置了 FTP 管理员的邮箱地址：

```
email <name>
```

每当指定 `%E` 魔法 Cookie 时，就会打印此字符串。该魔法 Cookie 可用于消息行或关机文件。你应该在登录横幅（banner）中向用户显示此字符串，以便他们在 FTP 服务器出现问题时知道如何联系你（管理员）。

# 在 ftppass 文件中使用命令配置 wu-ftpd

## 注意

不要在登录横幅中使用你的真实邮箱地址；你可能希望在需要时访问邮箱。相反，请使用别名将消息路由到相应的 IT 部门或其他地址。

# 通知用户修改日期

`readme` 文件告诉服务器，当特定文件被修改时是否应向用户显示通知。命令如下：

```
readme <path> {when <class>>
```

`path` 参数是用户的任何有效路径。可选的 `when` 参数与消息行中的完全相同。`class` 可以是类文件中定义的一个或多个类。对于真实用户，路径是绝对的。对于匿名用户，路径相对于匿名主目录，该目录默认为 `/var/ftp`。

# 配置系统日志

系统管理的一部分包括查看日志文件，以了解服务器正在做什么、谁访问了它、传输了哪些文件以及其他重要信息。你可以使用 `/etc/ftppass` 中的多个命令来控制你的 FTP 服务器的日志操作。

# 重定向日志记录

此行允许管理员重定向 FTP 服务器日志信息的记录位置：

```
log syslog<+xferlog>
```

默认情况下，命令信息存储在 `/var/log/messages` 中，但某些软件包中的 man 手页说明这些信息将写入 `/var/log/xferlog`。请检查服务器设置以获取文件传输日志的位置。

# 允许用户压缩文件

此行决定了用户是否能够对文件使用 `compress` 命令：

```
compress <yes|no> [<classglob>
```

`yes|no` 参数用于开启或关闭权限，`classglob` 是一个普通字符串，指定一个或多个定义的用户类。使用此命令产生的转换在 `ftpconversions` 文件中指定，该文件包含了对特定扩展名的文件使用何种压缩或提取命令的指示，例如 `.z` 使用 `compress` 命令，`.gz` 使用 `gunzip` 命令等。请参阅本章节后面的“配置 FTP 服务器文件转换操作”。

# 分配或拒绝使用 tar 的权限

此行决定了用户是否能够对文件使用 `tar`（磁归档）命令：

```
tar <yes|no> [<classglob> ...]
```

`yes|no` 参数用于开启或关闭权限，`classglob` 是一个普通字符串，指定一个或多个定义的用户类。同样，使用此命令产生的转换在 `ftpconversions` 文件中指定。

# 确定适用于用户创建上传文件的权限

此行与权限控制部分的其他命令略有不同。`umask` 命令决定了用户以什么权限创建新文件；其格式如下：

```
umask <yes|no> <typelist>
```

`yes|no` 参数决定了在上传文件时是否允许用户使用默认权限创建文件。与你在本节较早读过的 `overwrite` 命令一样，此行专门针对上传文件，因为客户端机器决定了如何从下载创建新文件。

# 配置指向 cdpath 的命令

此别名允许管理员为目录提供除标准名称之外的另一个名称：

```
alias <string> <dir>
```

`alias` 行仅适用于 `cd` 命令。如果一个常用的目录埋在匿名 FTP 用户目录树的深处，此行特别有用。一个条目如下：

```
alias linux-386 /pub/slackware/11/i386/
```

此行将允许用户输入 `cd linux-386` 并自动跳转到 `/pub/slackware/11/i386` 目录。

# 配置 FTP 服务器文件转换操作

`cdpath <dir>` 行指定了 `cd` 命令查找用户输入的字符串的顺序。搜索路径按照 `ftppass` 文件中 `cdpath` 行的输入顺序进行。

例如，如果 `ftppass` 文件中存在以下 `cdpath` 条目：

```
cdpath /pub/slackware/
cdpath /pub/linux/
```

当用户执行 `cd i386` 时，服务器将在 `/pub/slackware` 目录下的任何定义别名中搜索，然后在 `/pub/linux` 目录搜索。如果定义了大量的别名，建议使用创建目录的符号链接代替别名。这将减少 FTP 服务器的工作量并缩短用户等待。

# shutdown 文件的结构

`shutdown` 命令告诉服务器查找由 `ftpput` 命令或用户生成的关闭消息。`shutdown` 命令配合关闭文件的路径使用，如下：

```
shutdown /etc/uftputshutdown
```

如果该文件存在，服务器将检查该文件以确定服务器何时应该关闭。该文件的语法如下：

```
<year> <month> <day> <hour> <minute> <deny_offset> <disc_offset> <text>
```

`year` 可以是 1970 年（纪元）之后的任何年份，`month` 为 0–11，`hour` 为 0–23，`minute` 为 0–59，`deny_offset` 是服务器关闭前用户禁用新连接的分钟数，`disc_offset` 是已连接用户被断开之前的分钟数，最后是登录时显示给用户的消息。此外，在消息部分中定义的有效魔术 Cookie（magic cookies）以及表 23.2 中列出的也是可用的。

表 23.2 shutdown 文件的魔术 Cookie

| Cookie |  |

| :--- | :--- |

| `%s` | 我们将关闭的时间 |

| `%r` | 拒绝新连接的时间 |

| `%d` | 断开当前连接的时间 |

# 配置 FTP 服务器文件转换操作

FTP 服务器可以在传输过程中转换文件，以自动对文件进行压缩和解压。假设用户正在传输一个文件到他的 Microsoft Windows 机器，该文件在 Linux 机器上经过了 `TAR` 归档和 `gzip`压缩。如果用户没有安装解压这些文件的归档工具，他们将无法访问或使用这些文件。

作为 FTP 服务器管理员，你可以配置 FTP 服务器在下载前自动归档这些文件，从而支持可能没有解压缩能力的站点用户。此外，你可以为用户配置上传区域，并配置 FTP 服务器自动压缩传输到服务器的任何文件。

`ftpconversions` 文件的格式结构为：

```
1:2:3:4:5:6:7:8
```

其中 1 是删除前缀（strip prefix），2 是删除后缀（strip postfix），3 是添加前缀（add-on prefix），4 是添加后缀（add-on postfix），5 是外部命令，6 是类型，7 是选项，8 是描述。

### 删除前缀 (Strip Prefix)

删除前是非文件名开头应被删除的一个或多个字符。

### 删除后缀 (Strip Postfix)

删除后缀是文件名末尾应被删除的一个或多个字符。

### 添加前缀 (Add-On Prefix)

添加前缀是文件名开头应添加的一个或多个字符。

### 添加后缀 (Add-On Postfix)

添加后缀是文件名末尾应添加的一个或多个字符。

# 转换操作示例
