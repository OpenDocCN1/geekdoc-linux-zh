

该命令将用户限制在特定的目录结构中，这与匿名用户被限制在 /var/ftp 的方式相同。该命令还限制这些用户只能访问其所属组拥有权限的文件。

groupname 参数可以是组名称或该组对应的 GID（组 ID）。如果你使用 GID 作为 groupname 参数，请在其前面加上百分号（%）。你可以使用此命令为一组 ID 范围分配权限，例如：

```
guestgroup %500-550
```

此条目会将所有组 ID 为 500–550 的用户限制为作为 guest group（来宾组）处理，而不是作为单独的用户。为了让 guestgroup 正常工作，你必须像设置匿名 FTP 用户一样，以正确的权限设置用户的家目录。

## 基于个人 ID 限制权限

guestuser 行与你刚才阅读过的 guestgroup 命令的工作方式完全相同，区别在于它指定的是用户 ID (UID) 而不是组 ID。命令如下：

```
guestuser <username> [<username>]
```

该命令限制来宾用户只能访问其具有权限的文件。通常，用户比组拥有更多的权限，因此这种分配方式可能比 guestgroup 行限制得少。

## 限制班级中的用户数量

limit 在指定时间内限制某个班级（class）中的用户数量。这是该命令，它包含用于指定班级、用户数量、时间段以及包含适当消息的文本文件名称的字段：

```
limit <class> <n> <times> <message_file>
```

如果在给定时间段内，指定班级中的用户数量超过限制值，用户将看到 message_file 参数中指定的文件内容。

times 参数格式较为简洁。其格式为逗号分隔的字符串，形式为“天, 小时”。有效的天数字符串包括 Su, Mo, Tu, We, Th, Fr, Sa 和 Any。小时采用 24 小时制格式。示例如下：

```
limit anonymous 10 MoTuWeThFr,Sa0000-2300 /home/ftp/.message_limit_anon_class
```

此行将将 anonymous 班级的并发连接数限制为 10，有效时间为周一至周五全时段，以及周六从午夜到晚上 11:00。如果并发连接数超过限制，或在周六晚上 11:00 时，用户将看到文件 /home/ftp/.message_limit_anon_class 的内容。

关于更精细地限制用户连接的语法，可以在 ftpaccess 的手册页中找到。

## 限制无效密码输入次数

此配置行允许控制用户在 FTP 服务器终止会话之前可以输入无效密码的次数：

```
loginfails <number>
```

loginfails 的默认值设置为 5。此命令可以防止没有有效密码的用户通过反复尝试直到“猜对”为止。

## 配置用户信息

对于任何公共 FTP 服务器的管理员来说，向用户提供有关服务器及其使用方式的信息是一个良好的实践。足够的用户信息可以帮助防止用户问题并减少技术支持电话。你也可以使用这些信息来告知用户管理你 FTP 服务器使用的限制。用户信息是你记录 FTP 服务器应如何使用的极好方式。

你可以使用以下各节中详述的命令，在用户登录服务器或执行特定操作时向他们显示消息。以下命令允许在用户登录服务器或执行操作时向用户显示消息。

### 显示登录前横幅

该命令引用一个文件，该文件在用户从 FTP 服务器收到登录提示之前显示：

```
banner <path>
```

通常，该文件包含用于识别服务器的信息。path 是相对于系统根目录 (/) 的绝对路径名，而不是匿名 FTP 用户家目录的基础路径。条目可能如下所示：

```
banner /etc/rh8ftp.banner
```

此示例使用 /etc 目录下名为 rh8ftp.banner 的文件。该文件可以包含一行或多行文本，例如：

> 欢迎访问 Widget 公司的 Red Hat Linux FTP 服务器。
> 此服务器仅供授权用户使用。
> 第三方开发人员应使用镜像站点。

当 FTP 用户尝试登录时，横幅将显示如下：

```
$ ftp shuttle2
Connected to shuttle2.home.org.
220-Welcome to Widget, Inc.'s Red Hat Linux FTP server.
220-This server is only for use of authorized users.
220-Third-party developers should use a mirror site.
220-
220 shuttle2 FTP server (Version wu-2.6.2-8) ready.
504 AUTH GSSAPI not supported.
504 AUTH KERBEROS_V4 not supported.
KERBEROS_V4 rejected as an authentication type
Name (shuttle2:phudson):
```

![](img/774d40fd20903495c5cd00e2efad3f33_675_0.png)

请注意，横幅不会替换问候语文本，后者默认显示主机名和服务器信息，例如：

```
220 shuttle2 FTP server (Version wu-2.6.2-8) ready.
```

要隐藏版本信息，请在 ftpaccess 中使用 greeting 命令配合关键字（如 terse），如下所示：

```
greeting terse
```

然后，FTP 用户将在登录文本中看到一条简短的消息，例如：

```
220 FTP server ready.
```

此外，并非所有 FTP 客户端都能处理来自 FTP 服务器的多行响应。`banner` `path` 命令是横幅行将文件内容传递给客户端的方式。如果客户端无法中断多行响应，那么该 FTP 服务器对他们来说将毫无用处。你还应该编辑默认横幅，以移除身份和版本信息。

### 显示文件

此行指定一个在用户登录时以及用户发出 `cd` 命令时显示给用户的文本文件：

```
message <path> {<when> {<class> ...}}
```

可选的 `when` 子句可以是 `LOGIN` 或 `CWD=(dir)`，其中 `dir` 是当前目录的名称。可选的 `class` 参数允许仅向指定的一或多个用户类别显示消息。

使用消息是提供有关站点资源位置信息以及系统相关信息的不错方式，例如备用站点、关于可用数据的一般策略、服务器可用时间等。

你可以使用*魔术饼干（magic cookies）*让你的显示消息更生动。魔术饼干是符号常量，它们会被系统信息替换。表 22.1 列出了 message 命令中有效的魔术饼干及其表示形式。

**表 22.1 魔术饼干及其说明**

| 饼干 | 说明 |
| :--- | :--- |
| %T | 本地时间（格式如 Thu Nov 15 17:12:42 1990） |
| %F | CWD 所在分区的空闲空间（KB） |
| | [并非所有系统都支持] |
| %C | 当前工作目录 |
| %E | 在 ftpaccess 中定义的管理员电子邮件地址 |
| %R | 远程主机名 |
| %L | 本地主机名 |
| %u | 通过 RFC931 认证确定的用户名 |
| %U | 登录时提供的用户名 |
| %M | 此班级中允许的最大用户数 |
| %N | 此班级中当前的用户数 |
| %B | 分配磁盘块数的绝对上限 |
| %b | 首选的磁盘块数限制 |
| %q | 当前块计数 |
| %I | 分配的 inode 最大数量（+1） |
| %i | 首选的 inode 限制 |
| %Q | 当前分配的 inode 数量 |
| %H | 过度使用磁盘的时间限制 |
| %h | 过度使用文件的时间限制 |

**比率**

| 饼干 | 说明 |
| :--- | :--- |
| %xu | 上传的字节数 |
| %xd | 下载的字节数 |
| | |
| %xR | 上传/下载比率（1:n） |
| %xC | 信用字节 |
| %xT | 时间限制（分钟） |
| %xE | 自登录以来的流逝时间（分钟） |
| %xL | 剩余时间 |
| %xU | 上传限制 |
| %xD | 下载限制 |

为了理解此命令的工作方式，假设你想向所有登录到 FTP 服务器的用户显示欢迎消息。一个条目为：

```
message /home/ftp/welcome.msg login
message /welcome.msg login
```

向所有登录服务器的真实用户显示 welcome.msg 文件的内容。第二个条目向匿名用户显示相同的消息。

welcome.msg 文件并非在安装 RPM 时创建，但你可以使用文本编辑器创建它。输入以下内容：

