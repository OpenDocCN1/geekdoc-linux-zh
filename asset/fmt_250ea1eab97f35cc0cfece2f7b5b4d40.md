
此条目限制所有组 ID 为 500–550 的用户被视为 `guest` 组，而不是单独的用户。为了使 `guestgroup` 正常工作，你必须像匿名用户一样，为用户的家庭目录设置正确的权限。

## 基于单个 ID 限制权限

`guestuser` 行的工作原理与你刚刚阅读的 `guestgroup` 命令完全相同，只是它指定的是用户 ID (`UID`) 而不是组 ID。命令如下：

```
guestuser <username> [<username>]
```

此命令将 `guest` 用户限制在其具有权限的文件的访问范围内。通常，用户比组拥有更多的权限，因此这种类型的分配可能比 `guestgroup` 行限制更少。

## 限制类中的用户数量

`limit` 命令在给定时间段内限制类中的用户数量。命令如下，包含指定类、用户数、时间段和包含适当消息的文本文件名的字段：

```
limit <class> <n> <time> <message_file>
```

如果在给定时间段内超过列出的类中指定数量的用户，用户将看到 `message_file` 参数中给出的文件的内容。

`times` 参数比较简洁。其格式为 `days, hours` 形式的逗号分隔字符串。有效的 `days` 字符串为 `Su`, `Mo`, `Tu`, `We`, `Th`, `Fr`, `Sa` 和 `Any`。`hours` 字符串以 24 小时格式格式化。示例如下：

```
limit anonymous 10 MoToW@ThFr,Sa0000-2300 /home/ftp/.message_limit_anon_class
```

此行将 `anonymous` 类限制为周一至周五 10 个并发连接，以及周六从午夜到晚上 11:00 的 10 个并发连接。例如，如果周六晚上 11:00 超过了并发连接数，用户将看到文件 `/home/ftp/message_limit_anon_class` 的内容。

关于限制用户连接的更精细控制的语法可以在 `ftpaccess` 手册页中找到。

## 限制无效密码输入次数

此行允许控制用户在 FTP 服务器终止会话之前可以输入多少次无效密码：

```
loginfails <number>
```

`loginfails` 的默认值设为 5。此命令防止没有有效密码的用户不断尝试直到成功。

## 配置用户信息

为公共 FTP 服务器管理员提供良好的服务器及其使用信息是一种良好的实践。足够的用户信息可以帮助防止用户问题并消除技术支持呼叫。你还可以使用此信息通知用户关于使用你的 FTP 服务器的限制。用户信息是你记录如何使用 FTP 服务器的一种绝佳方式。

你可以使用以下章节中详述的命令，在用户登录服务器时以及在执行特定操作时向用户显示消息。以下命令允许在用户登录服务器时以及执行操作时向用户显示消息。

### 显示延长横幅

此命令引用一个在用户从 FTP 服务器接收登录提示之前显示的文件：

```
banner <path>
```

此文件通常包含用于标识服务器的信息。`path` 是相对于系统根 (`/`) 的绝对路径名，而不是匿名用户家庭目录的基底。条目可能如下所示：

```
banner /etc/rh8ftp.banner
```

此示例使用 `/etc` 目录下的名为 `rh8ftp.banner` 的文件。文件可以包含一行或多行文本，例如：

> 欢迎使用 Widget, Inc. 的 Red Hat Linux FTP 服务器。
> 此服务器仅供授权用户使用。
> 第三方开发人员应使用镜像站点。

### 横幅

当 FTP 用户尝试登录时，横幅会像这样显示：

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
Name (shuttle2:phdson):
```

**注意**

请注意，横幅并不会替换默认显示的包含主机名和服务器信息的问候文本，例如：

```
220 shuttle2 FTP server (Version wu-2.6.2-8) ready.
```

若要隐藏版本信息，请在 `ftpaccess` 中使用带有关键字（例如 `terse`）的 `greeting` 命令，如下所示：

```
greeting terse
```

此时，FTP 用户在登录文本中会看到类似以下的简短信息：

```
220 FTP server ready.
```

此外，并非所有 FTP 客户端都能处理来自 FTP 服务器的多行响应。`banner <path>` 命令用于将文件内容传递给客户端作为横幅行。如果客户端无法中断多行响应，则 FTP 服务器对它们来说毫无用处。您还应该编辑默认横幅以移除身份和版本信息。

## 显示文件

此语句指定一个在用户登录以及用户执行 `cd` 命令时显示给用户的文本文件：

```
message <path> {<when> {<class> ...}}
```

可选的 `when` 子句可以是 `LOGIN` 或 `CWD(=dir)`，其中 `dir` 是当前目录的名称。可选的 `class` 参数允许仅向特定一类或几类用户显示消息。

使用消息是提供站点内资源位置信息以及系统依赖信息（如替代站点、关于可用数据的一般策略、服务器可用时间等）的好方法。

您可以使用魔法饼干（magic cookies）让显示的消息栩栩如生。*魔法饼干* 是系统信息替换的符号常量。表 20.1 列出了消息命令有效的魔法饼干及其表示形式。

### 表 20.1 魔法饼干及其描述

| **饼干** | **描述** |
| --- | --- |
| `%T` | 本地时间 (形式为 Thu Nov 15 17:12:42 1990) |
| `%F` | CWD 分区的可用空间 (KiB) [并非所有系统都支持] |
| `%C` | 当前工作目录 |
| `%E` | 在 ftaccess 中定义的管理员电子邮件地址 |
| `%R` | 远程主机名 |
| `%L` | 本地主机名 |
| `%u` | 通过 RFC931 认证确定的用户名 |
| `%U` | 登录时提供的用户名 |
| `%M` | 此类别允许的最大用户数 |
| `%N` | 此类别当前的用户数 |
| `%B` | 分配的磁盘块的绝对限制 |
| `%b` | 首选的磁盘块限制 |
| `%Q` | 当前的块计数 |
| `%I` | 分配的最大 inode 数 (+1) |
| `%i` | 首选的 inode 限制 |
| `%q` | 当前分配的 inode 数 |
| `%H` | 过度使用磁盘的时间限制 |
| `%h` | 过度使用文件的时间限制 |

#### *比率*

| **比率** | **描述** |
| --- | --- |
| `%xu` | 上传的字节数 |
| `%xd` | 下载的字节数 |
| `%xR` | 上传/下载比率 (1:n) |
| `%xC` | 信用字节数 |
| `%xT` | 时间限制 (分钟) |
| `%xE` | 自登录以来的经过时间 (分钟) |
| `%xL` | 剩余时间 |
| `%xU` | 上传限制 |
| `%xD` | 下载限制 |

要理解此命令如何工作，请想象您想向所有登录到 FTP 服务器的人显示欢迎消息。一条条目为：

```
message /home/ftp/welcome.msg login
message /welcome.msg login
```

会将 `welcome.msg` 文件的内容显示给所有登录到服务器的已认证用户。第二个条目向匿名用户显示相同的消息。

`welcome.msg` 文件并非随 RPM 安装而创建，但您可以使用文本编辑器创建它。输入以下内容：

```
Welcome to the anonymous ftp service on %!  

There are %N out of %M users logged in.  

Current system time is %T  

Please send email to %E if there are  
any problems with this service.  

Your current working directory is %C
```

将此文件保存为 `/var/ftp/welcome.msg`。通过连接到 FTP 服务器来验证其是否正常工作：
