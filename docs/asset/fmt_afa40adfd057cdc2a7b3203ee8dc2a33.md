
如果超过了用户数量，用户将看到 `message_file`。`times` 参数是逗号分隔的天数列表。有效的日期有 `Su`, `Mo`, `We`, `Th`, `Fr`, `Sa`。时间采用 24 小时格式。示例为：

```
limit anonymous 10 0000–2300 /home/ftp/.message_anon
```

该行限制周一至周五 10 个并发连接，以及周六从午夜到晚上 11 点。用户将看到文件。

## 限制密码输入次数

此行允许控制用户在终止会话前输入无效密码的次数：

```
loginfails <number>
```

`loginfails` 的默认值为 5。此命令防止没有密码的用户反复尝试。

## 用户信息

为用户提供有关服务器及其使用的信息是任何公共 FTP 服务器管理员的良好做法。充分的用户可以可以防止问题并减少支持电话。您还可以利用这些信息告知用户有关您的 FTP 服务器的限制。用户信息为您提供记录如何使用您的 FTP 服务器的极佳方法。

可以使用后续章节中详细的命令在登录服务器或用户操作时向其显示消息。

### 显示登录前横幅

此命令指向一个在 FTP 服务器提供登录提示之前显示的文件：

```
banner <path>
```

此文件包含识别服务器的通用信息。路径是相对于系统根 (`/`) 的绝对路径，而不是匿名 FTP 家目录。条目可能如下：

```
banner /etc/ftp.banner
```

此示例使用了 `/etc` 目录下的 `ftp.banner` 文件。该文件可以包含多行文本，例如：

```
Welcome to Widget, Inc.'s Red Hat Linux server.
This server is only for use of authorized users.
Third-party developers should use a mirror site.
```

当 FTP 用户尝试登录时，横幅显示如所示：

```
$ ftp shuffle2.home.org
220-Welcome to Widget, Inc.'s Red Hat Linux server.
220-This server is only for use of authorized users.
220-Third-party developers should use a mirror site.
220.
220.
220 shuffle2 FTP server (Version wu-2.6.2-8) ready.
504 AUTH GSSAPI not supported.
504 AUTH KERBEROS_V4 not supported.
KERBEROS_V4 rejected as an authentication type
```

### 在 ftppass 文件中使用命令配置 wu-ftpd 453

Name (shuttle2:phudson):

#### 注意

请注意，横幅（banner）不会替换默认显示主机名和服务器信息的欢迎文本，例如：

```
220 shuttle2 FTP server (Version wu-2.6.2-8) ready.
```

要隐藏版本信息，可以在 ftppass 中在 `greeting` 命令中使用关键字（例如 `terse`），如下所示：

```
greeting terse
```

FTP 用户随后将在登录文本中看到如下简短消息：

```
220 FTP server ready.
```

此外，并不是所有的客户端都能处理来自 FTP 服务器的多行响应。`banner <path>` 命令是横幅将文件内容传递给客户端的方式。如果客户端无法中断多行响应，则 FTP 服务器对它们来说将毫无用。您还应该编辑默认横幅以移除身份和版本信息。

## 显示文件

此行指定一个在用户登录期间以及使用 `cd` 命令时显示的文本文件：

```
message <path> {when} can<{class> ...}}
```

该选项可以是 `LOGIN` 或 `CWD=(dir)`，其中 `dir` 是当前目录的名称。可选的 `class` 参数允许仅向给定的用户类显示消息。

使用 `messages` 是获取站点位置信息以及依赖于系统的信息的好方法，例如备用站点、关于可用数据的通用策略、服务器可用时间等。

您可以使用魔法标识符（magic cookies）让显示的消息更加丰富。魔法 Cookie 是一种会被系统信息替换的符号常量。表 18.1 列出了 `message` 命令有效的 Cookie 及其表示形式。

### 表 18.1 魔法 Cookie 及其描述描述

| Cookie | 描述 |
| --- | --- |
| `%T` | 本地时间（如 Thu Nov 15 17:12:42 1990） |
| `%F` | CWD 分区的剩余空间（KB）[并非所有系统都支持] |
| `%C` | 当前工作目录 |
| `%E` | 在 ftppass 中定义的维护者邮箱地址 |
| `%R` | 远程主机名 |
| `%L` | 本地主机名 |
| `%u` | 通过 RFC931 认证确定的用户名 |
| `%U` | 登录时提供的用户名 |
| `%M` | 该类允许的最大用户数 |
| `%N` | 该类中的当前用户数 |
| `%B` | 分配磁盘块的绝对限制 |
| `%b` | 磁盘块的首选限制 |
| `%Q` | 当前块计数 |
| `%I` | 最大分配 inode 数量 (+1) |
| `%i` | 选的 inode 限制 |
| `%q` | 当前分配的 inode 数量 |
| `%H` | 过度使用的时间限制 |
| `%h` | 文件数过多的时间限制 |
| Ratios |  |
| `%xu` | 上传字节数 |
| `%xd` | 下载字节数 |
| `%xR` | 上传/下载比例 (1:n) |
| `%xc` | 额度字节 |
| `%xT` | 时间限制（分钟） |
| `%xE` | 登录以来已经过的时间（分钟） |
| `%xL` | 剩余时间 |
| `%xU` | 上传限制 |
| `%xD` | 下载限制 |

要理解此命令如何工作，想象您想向每个登录 FTP 服务器的用户显示一条欢迎消息。输入条目：

```
message /home/ftp/welcome.msg login
message /welcome.msg login
```

这将向所有登录服务器的真实用户显示 `welcome.msg` 文件的内容。第二个条目向匿名用户显示相同的消息。

`welcome.msg` 文件并不是在安装包时创建的，但您可以使用文本编辑器创建它。输入以下内容：

欢迎使用 `%L` 匿名 FTP 服务！

当前有 `%N` 个用户（共 `%M` 个）已登录。

当前系统时间为 `%T`。

如果此项服务有任何问题，请发送邮件至 `%E`。

您当前的工作目录是 `%C`。

将此文件保存为 `/var/ftp/welcome.msg`。通过连接 FTP 服务器来验证其运行情况：

```
220 FTP server ready.
504 AUTH GSSAPI not supported.
504 AUTH KERBEROS_V4 not supported.
KERBEROS_V4 rejected as an authentication type
Name (shuttle:phudson): anonymous
331 Guest login OK, complete your e-mail address as password.
Password:
230-Welcome to the anonymous ftp service on shuttle.home!
230-
230-There are 1 out of unlimited users logged in.
230-
230-Current system time is Nov Mon 3 10:57:06 2003
230-
230-Please send email to root@localhost if there are
230-any problems with this service.
230-Your current working directory is /
```

## 显示管理员邮箱

此行设置 FTP 管理员的邮箱地址：

```
email <name>
```

每当指定 `%E` 魔法 Cookie 时，此字符串就会在 `messages` 行或关闭文件中被打印。您应该在登录横幅中向用户显示此字符串。

## 通知用户最后日期

`readme` 行告诉服务器某个文件已修改。

## 消息

控制用户活动是确保系统服务器安全的重要部分。`ftpaccess` 文件包含许多命令，允许您确定用户在 FTP 会话期间可以执行和不能执行的操作。您可以使用这些权限控制允许用户更改文件权限、删除或覆盖文件，并使用默认权限创建新文件。您将在接后的章节中学习如何使用这些 `ftpaccess` 命令行。
