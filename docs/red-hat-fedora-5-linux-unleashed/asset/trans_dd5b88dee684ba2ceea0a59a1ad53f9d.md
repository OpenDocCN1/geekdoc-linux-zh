
该行将匿名类在周一至周五限制为 10 个并发连接，在周六从午夜到晚上 11:00 也如此限制。例如，如果在周六晚上 11:00 超过了并发连接数限制，用户将会看到文件 `/home/ftp/.message_limit_anon_class` 的内容。

关于限制用户连接的更精细控制的语法，可以在 `ftpaccess` 手册页中找到。

## 限制无效密码输入次数

该行允许控制用户在 FTP 服务器终止会话之前可以输入无效密码的次数：

```
loginfails <number>
```

`loginfails` 的默认值设为 5。此命令可以防止没有有效密码的用户反复尝试直到猜对为止。

### 配置用户信息

为公共 FTP 服务器管理员而言，向用户提供有关服务器及其使用的信息是一种良好的实践。充足的用户信息有助于防止用户问题并消除技术支持电话。您还可以利用此信息告知用户管理您的 FTP 服务器使用的限制条件。用户信息为您提供了记录 FTP 服务器应如何使用的极好方式。

您可以使用以下各节中详细介绍的命令，在用户登录服务器以及执行特定操作时向用户显示消息。以下命令允许在用户登录服务器和执行操作时向用户显示消息。

## 显示预登录横幅

此命令是对一个文件的引用，该文件在用户从 FTP 服务器收到登录提示之前显示：

```
banner <path>
```

该文件通常包含识别服务器的信息。路径是相对于系统根目录（/）的绝对路径名，而不是匿名 FTP 用户的主目录基准。条目可能看起来像这样：

```
banner /etc/rh8ftp.banner
```

此示例使用 `/etc` 目录下名为 `rh8ftp.banner` 的文件。文件可以包含一行或多行文本，例如

```
Welcome to Widget, Inc.'s Red Hat Linux FTP server.
This server is only for use of authorized users.
Third-party developers should use a mirror site.
```

当 FTP 用户尝试登录时，横幅将像这样显示：

```
S ftp shuttle2
Connected to shuttle2.home.org.
220-Widget, Inc.'s Red Hat Linux FTP server.
220-This server is only for use of authorized users.
220-Third-party developers should use a mirror site.
220-
220
220 shuttle2 FTP server (Version wu-2.6.2-8) ready.
504 AUTH GSSAPI not supported.
504 AUTH KERBEROS_V4 not supported.
KERBEROS_V4 rejected as an authentication type
Name (shuttle2:phudson):
```

**注意**

请注意，横幅不会替换默认情况下显示主机名和服务器信息（例如 `220 shuttle2 FTP server (Version wu-2.6.2-8) ready.`）的问候文本。

要隐藏版本信息，请在 `ftpaccess` 中使用带有关键字（如 `terse`）的 `greeting` 命令，如下所示：

```
greeting terse
```

FTP 用户随后将在登录文本中看到类似以下的简短消息：

```
220 FTP server ready.
```

此外，并非所有 FTP 客户端都能处理来自 FTP 服务器的多行响应。`banner <path>` 命令是横幅行将文件内容传递给客户端的方式。如果客户端无法中断多行响应，那么该 FTP 服务器对他们来说将毫无用处。您还应该编辑默认横幅以移除身份和版本信息。

## 显示文件

该行指定在登录期间以及用户发出 `cd` 命令时要显示给用户的文本文件：

```
message <path> {<when> {<class> ...}}
```

可选的 `when` 子句可以是 `LOGIN` 或 `CWD=(dir)`，其中 `dir` 是当前目录的名称。可选的 `class` 参数允许消息仅显示给特定类别的用户。

使用消息是提供有关站点上资源位置以及依赖于系统的信息（如替代站点、有关可用数据的一般策略、服务器可用时间等）的好方法。

您可以使用*魔术饼干（magic cookies）*为您的显示消息增添活力。*魔术饼干*是符号常量，会被系统信息替换。表 24.1 列出了 message 命令的有效魔术饼干及其表示。

### 表 24.1 魔术饼干及其描述

| 饼干 | 描述 |
| :--- | :--- |
| $T | 本地时间（格式 Thu Nov 15 17:12:42 1990） |
| $F | CWD 分区中的可用空间（千字节）[并非所有系统都支持] |
| $C | 当前工作目录 |
| $E | `ftpaccess` 中定义的维护者电子邮件地址 |
| $P | 远程主机名 |
| $N | 本地主机名 |
| $u | 通过 RFC931 认证确定的用户名 |
| $J | 登录时给出的用户名 |
| $M | 此类别允许的最大用户数 |
| $Q | 此类别当前的用户数 |
| $B | 分配的磁盘块绝对限制 |
| $b | 首选的磁盘块限制 |
| $0 | 当前块计数 |
| $I | 分配的内核最大数量 (+1) |
| $i | 首选的内核限制 |
| $n | 当前分配的内核数量 |
| $t | 过度使用磁盘的时间限制 |
| $N | 过度使用文件的时间限制 |
| $R | 上传的字节数 |
| $L | 下载的字节数 |
| $xR | 上传/下载比例 (1:n) |
| %xR | 信用字节 |
| $X | 时间限制（分钟） |
| $xE | 自登录以来经过的时间（分钟） |
| %XL | 剩余时间 |
| $xu | 上传限制 |
| $xO | 下载限制 |

为了理解此命令的工作原理，想象一下您希望向所有登录到 FTP 服务器的人显示欢迎消息。条目

```
message /home/ftp/welcome.msg login
message /welcome.msg login
```

向所有登录到服务器的真实用户显示 `welcome.msg` 文件的内容。第二个条目向匿名用户显示相同的消息。

`welcome.msg` 文件并非通过安装 RPM 包创建，但您可以使用文本编辑器创建它。键入以下内容：

```
Welcome to the anonymous ftp service on %L!

There are %N out of %M users logged in.

Current system time is %T

Please send email to %E if there are
any problems with this service.

Your current working directory is %C
```

将此文件保存为 `/var/ftp/welcome.msg`。通过连接到 FTP 服务器来验证其是否有效：

```
220 FTP server ready.
504 AUTH GSSAPI not supported.
504 AUTH KERBEROS_V4 not supported.
KERBEROS_V4 rejected as an authentication type
Name (shuttle:phudson): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
230- Welcome to the anonymous ftp service on shuttle.home.org!
230-
230- There are 1 out of unlimited users logged in.
230-
230- Current system time is Mon Nov 3 10:57:06 2003
230-
230- Please send email to root@localhost if there are
230-any problems with this service.
230-Your current working directory is /
```

## 显示管理员电子邮件地址

该行设置 FTP 管理员的电子邮件地址：

```
email <name>
```

每当指定 `$E` 魔术饼干时，都会打印此字符串。此魔术饼干用于 `message` 行或 `shutdown` 文件中。您应该在登录横幅消息中向用户显示此字符串，以便他们在遇到 FTP 服务器问题时知道如何联系您（管理员）。

不要在显示横幅中使用您的实际电子邮件地址；您需要能够根据需要访问用户电子邮件。相反，请使用别名地址将消息路由到适当的 IT 部门或其他地址。

## 通知用户最后修改日期

`readme` 行告知服务器是否应在特定文件最后修改时向用户显示通知。命令如下：

```
readme <path> {<when {<class>}}}
```

`path` 参数是用户的有效路径。可选的 `when` 参数与 `message` 行中看到的完全相同。`class` 可以是 `class` 文件中定义的一个或多个类别。对于真实用户，路径是绝对的。对于匿名用户，路径是相对于匿名主目录的，默认情况下是 `/var/ftp`。

## 配置系统日志

系统管理的一部分工作涉及审查日志文件，以了解服务器正在做什么、谁访问了它、传输了哪些文件以及其他重要信息。您可以在 `/etc/ftpaccess` 中使用多个命令来控制 FTP 服务器的日志记录操作。

### 重定向日志记录

该行允许管理员重定向 FTP 服务器日志信息的记录位置：

```
log <syslog> {<xferlog>}
```

默认情况下，命令信息存储在 `/var/log/messages` 中，尽管某些 RPM 包中包含的手册页指出该信息写入 `/var/log/xferlog`。请检查您的服务器设置，以获取有关文件传输日志位置的信息。

### 记录所有用户发出的命令

该行启用记录用户发出的所有命令的功能：

```
log commands [<typelist>]
```

`typelist` 是 `anonymous`、`guest` 和 `real` 的逗号分隔列表。如果未提供 `typelist`，则记录所有用户的命令。某些 wu-ftpd RPM 将所有文件传输的日志记录设置到 `/var/log/xferlog`（见下一节）。但是，您可以在 `ftpaccess` 中添加带有 `commands` 关键字的 `log` 命令来捕获用户操作。然后日志记录被启用，用户操作被捕获在 `/var/log/messages` 中。这是一个示例日志文件：

