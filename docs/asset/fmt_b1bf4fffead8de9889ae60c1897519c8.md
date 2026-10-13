
```
deny evilhacker.domain.com /home/ftp/.message.no.evil.hackers
```

该行向任何尝试从 `evilhacker.domain.com` 连接到 FTP 的人显示 `/home/ftp/.message.no.evil.hackers` 文件的内容。要根据其 IP 是否通过 DNS 进行反向解析来拒绝访问，请使用以下命令。

### guestgroup

`guestgroup` 命令在你拥有访客用户但想要限制访问时非常有用。该命令的格式为：

```
guestgroup <classname> <class> ...
```

其中 `<classname>` 是组名称，`<class>` 是使用 `class` 命令定义的类名称。

## 配置其他服务器

`loginfails` 命令允许你设置客户端在断开连接之前可以进行的失败尝试次数。默认情况下，这个数字是五；但你可以使用命令设置它：

```
loginfails <n>
```

其中 `<n>` 是尝试次数。例如，以下行会在用户失败三次后断开其连接：

```
loginfails 3
```

### private

你可能会发现，通过 FTP 与其他用户共享文件，而无需将其放在公共区域或为这些用户提供真实账户是非常方便的。客户端使用 `SITE GROUP` 和 `SITE GPASS` 命令，以便切换到需要密码的特权组。

`/etc/ftpgroups` 中账户组的格式为：

```
access_group_name:encrypted_password:real_group
```

其中 `access_group_name` 是客户端引用该特殊组时使用的名称，`encrypted_password` 是用户访问时需要（通过 `SITE GPASS`）提供的密码，`real_group` 是 `/etc/group` 文件中引用的实际组。

为了让你的 FTP 服务器支持此功能，你需要使用命令设置 `private` 标志：

```
private <switch>
```

其中 `<switch>` 是字符串 `YES`（开启）或 `NO`（关闭）。

## 控制横幅消息

在 FTP 用户连接到你的站点或指定特殊操作时向他们提供消息通常非常有用。这些命令允许你指定这些实例以及相应的关系。使用它们是使你的站点自文档化的极佳方法。

## banner

`banner` 命令允许你在客户端提供登录和密码组合之前在屏幕上显示签名。该命令的格式为：

```
banner <path>
```

其中 `<path>` 是你想要显示的文件的完整路径。请参考此示例：

```
banner /home/ftp/.banner
```

## 配置其他服务器

## email（电子邮件）

该命令允许你指定站点管理员的电子邮件地址。某些错误信息或信息请求会需要提供此行给出的信息。`/etc/passwd` 文件中的默认值为 `root@localhost`。

`email` 命令的格式：

```
email <address>
```

其中 `<address>` 是站点管理员的完整电子邮件地址。

创建一个转发到系统管理员的 "FTP" 电子邮件别名（e-alias）通常是良好的做法。在登录横幅（sign-on banner）中提供此类信息也是一个好主意，这样用户在无法登录系统时就该联系谁。

## message（消息）

该命令允许你设置在客户端登录或进入特定目录时发送的特殊消息。你可以指定多条消息。该命令的格式如下：

```
message <path> <when> {class} ...
```

其中 `<path>` 是要显示的文件的完整路径，`<when>` 是显示消息的条件，`<class>` 是应用此消息命令的类列表。

`<when>` 参数应采取两种形式之一：`LOGIN` 或 `CWD=<dir>`。如果是 `LOGIN`，消息将在成功登录时显示。如果参数设置为 `CWD=<dir>`，则当客户端进入 `<dir>` 目录时显示消息。

`<class>` 参数是可选的。你可以为特定消息列出多个类。如果你只想让消息发送给匿名用户等，这就会非常有用。

文件本身（由 `<path>` 指定）可以包含特殊标记，FTP 服务器会在运行时将它们替换为适当的信息。这些选项如下：

| 选项 | 描述 |
| --- | --- |
| `%T` | 本地时间 |
| `%F` | `<dir>` 所在分区的剩余空间 |
| `%C` | 当前工作目录 |
| `%E` | 站点管理员的电子邮件地址（由 `email` 命令指定） |

## FTP

| 选项 | 描述 |
|---|---|
| `%R` | 客户端主机名 |
| `%L` | 服务器主机名 |
| `%U` | 登录时提供的用户名 |
| `%M` | 指定类允许的最大用户数 |
| `%N` | 指定类中的当前用户数 |

记住，当消息由匿名用户触发时，消息路径需要相对于匿名 FTP 目录。

消息命令示例为：

抱歉，但在您的类中已有 `%R` 位用户，最大允许为 `%M` 位。请在几分钟后重试。

FTP 管理员 (`%E`)

如果该站点达到了 25 个用户的限制，例如，客户端看到类似下面的消息：

抱歉，`technics.domain.com`，但在您的类中已有 25 位用户（最大 25 位）。请在几分钟后重试。

FTP 管理员 (`ftp@domain.com`)

```
message ./toomany_anon LOGIN anonymfacts
```

其中文件 `./toomany_anon` 包含

```

## readme（说明文件）

`readme` 命令允许你指定通知客户端其当前目录下的文件最后修改时间的条件。该命令可以采取以下格式：

```
readme <path> <when> <class>
```

其中 `<path>` 是要提醒客户端关注的文件名（例如，`README`），`<when>` 与 `message` 命令中的 `<when>` 类似，`<class>` 是适用于此命令的类。`<when>` 和 `<class>` 参数是可选的。

记住，当你为匿名用户指定路径时，该文件必须相对于匿名 FTP 目录。

## 控制日志（Controlling Logging）

与任何复杂的网络服务一样，安全性很快就会成为问题。为了应对可能的威胁，跟踪连接以及相应的命令是必要的。以下命令允许你确定服务器软件应该记录多少内容的日志。

![](img/421e47878893966b6e8fcf1c1c761441_167_0.png)

## log commands（日志命令）

通常出于安全考虑，你可能想要记录 FTP 用户的操作。你可以通过使用 `log commands` 选项来实现。客户端调用的每个命令都会设置到你的日志文件中。命令的格式为：

```
log commands <typelist>
```

其中 `<typlist>` 是用逗号分隔的列表，指定应该记录哪些类型的用户。识别出的三类用户是匿名（`anonymous`）、客人（`guest`）和真实（`real`）（参见本章前面类命令的描述获取每个用户类型的描述。）例如，要记录匿名和客人用户的所有操作，你指定指定：

```
log commands anonymous,guest
```

## log transfers（日志传输）

如果你想记录客户端执行的文件传输，而不是通过 `log commands` 语句记录整个会话，你应该使用 `log transfers`。命令的格式为：

```
log transfers <typelist> <directions>
```

其中 `<typelist>` 是用逗号分隔的列表，指定应该记录哪些类型的用户（匿名、客人或真实），`<directions>` 是用逗号分隔的列表，指定传输必须在哪个方向被记录。你可以选择记录的两个方向是入站（`inbound`）和出（`outbound`）。

例如，要记录所有入站和出口匿名传输，你会使用：

```
log transfers anonymous inbound,outbound
```
结果存储在 `/var/xferlog` 中。有关该文件的详细信息。

## 杂杂命令（Miscellaneous Server Commands）

以下命令提供了一些杂项功能。每个命令都为服务器增加了灵活性。

### alias（别名）

`alias` 允许为客户端定义目录快捷方式。它们在客户端使用 `cd` 命令时激活。命令的格式为：

```
alias <string> <dir>
```

其中 `<string>` 是别名，`<dir>` 是应该传输到的实际目录。以下是此命令的示例：

```
alias orb_discography /pub/music/discography
```
因此，如果客户端连接并使用 `cd_discography` 命令，无论它们位于何处都会移动到 `/pub/music/discography`。

### cdpath

类似于 UNIX 环境变量，`cdpath` 命令允许你在调用 `cd` 命令时建立路径列表。`cdpath` 命令的格式为：

```
cdpath <dir>
```
