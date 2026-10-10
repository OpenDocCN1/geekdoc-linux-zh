
# 选项表

| 选项 | 描述 |
| :--- | :--- |
| %R | 客户端主机名 |
| %L | 服务器主机名 |
| %U | 登录时提供的用户名 |
| %M | 登录类中允许的最大用户数 |
| %N | 该类中的用户数量 |

> **注意：** 由匿名登录触发的消息必须相对于匿名 FTP 目录。

消息命令运行示例如下：

```
message ./too.many.users LOGIN anounusers
```

其中 `too.many.users` 文件的内容如下：

```
抱歉 %R，但 %L 的 %M 个用户限额中已使用 %N 个。我们正在努力获取更大的服务器，在此期间感谢耐心等待。请稍后再试。
您的 FTP 管理员，%E
```

**README**

`readme` 命令允许服务器在特定文件最后更新时间时自动通知用户。该命令的格式为：

```
readme path when class
```

其中 `path` 是您希望 FTP 服务器监控的文件的完整路径名，`when` 是您希望告知用户的时间（`when` 的格式与 `message` 命令相同），而 `class` 是该命令适用的类。`when` 和 `class` 参数是可选的。例如：

```
readme ./README CWD=/pub/patches
```

> **注意：** 由匿名登录触发的消息必须相对于匿名 FTP 目录。

# 日志记录

您可以使用 `wu-ftpd` 来配置关于其使用情况应记录哪些信息。这些信息是掌握使用率信息的好方法，有助于您更好地规划和服务组织。

本节讨论用于自定义日志条目的命令。

**LOG 命令**

如果您希望记录连接到您的 FTP 服务的用户输入的每个命令，请使用 `log commands`。其用法如下：

```
log commands typelist
```

其中 `typelist` 是您希望记录其命令的用户类型的逗号分隔列表，如 `class` 命令所描述。有效的用户类型为 anonymous（匿名）、guest（访客）和 real（真实用户）。例如，如果您希望记录所有匿名用户键入的命令，您将键入：

```
log commands anonymous
```

**LOG TRANSFERS**

如果您希望仅记录用户在您服务器之间传输的文件，而不是记录所有键入的命令，您将使用此命令：

```
log transfers typelist directions
```

其中 `typelist` 是您希望记录其命令的用户类型（如 `class` 命令所描述，即 anonymous、guest 和 real），而 `directions` 是传输必须采取的方向的逗号分隔列表，以便其被记录（即 inbound 入站和 outbound 出站）。例如，要记录所有访客用户的入站和出站连接，请键入：

```
log transfers guest inbound,outbound
```

# 其他服务器命令

当然，总有一些命令不适合归入任何特定类别。请考虑以下情况。

**ALIAS**

创建常用目录的快捷方式通常很方便。通过使用 `alias` 命令，您可以做到这一点。该命令的格式为：

```
alias alias-name actual-directory
```

其中 `alias-name` 是别名本身，而 `actual-directory` 是希望设置快捷方式的完整目录。例如：

```
alias redhat /pub/linux/distributions/redhat
```

这将允许用户键入命令：

```
cd redhat
```

系统会自动将其带到 `/pub/linux/distributions/redhat` 目录。

**CDPATH**

作为 shell 中 PATH 环境变量的等价物，`cdpath` 允许您为连接到您的 FTP 服务的用户建立目录路径。该命令的格式为：

```
cdpath directory
```

其中 `directory` 是您希望添加到路径中的目录名称。例如，如果您使用了：

```
cdpath /pub/linux
cdpath /pub/recipies
```

并且用户键入命令 `cd microwave`，`wu-ftpd` 将搜索以下目录：

- `./microwave`
- 名为 `microwave` 的别名
- `/pub/linux/microwave`
- `/pub/recipies/microwave`

![](img/95b125a8bf06051f34d8aba73558b7eb_314_0.png)

> **注意：** 别名和 cdp ath 之间的主要区别在于，别名指定了一个从一个目录名到另一个目录名的单一映射。另一方面，cdp ath 指定了一个目录列表，当用户键入 `cd` 命令时应检查这些目录。

**COMPRESS**

`wu-ftpd` 服务器提供在执行过程中进行文件转换的功能。它能执行的一种特定转换是在文件发送给用户之前对其进行压缩或解压缩。这对于可能没有使用与您相同的压缩工具的客户端，或者希望通过在发送前压缩文件以节省带宽的慢速链路客户端特别有用。

该命令的格式为：

```
compress switch class
```

其中 `switch` 为 ON 或 OFF，而 `class` 为 real、anonymous 或 guest。使用此功能的陷阱在于，您还必须配置您的 `tftp/conversions` 文件。我们将在本章稍后讨论这一点。

**TAR**

与 `compress` 命令类似，`tar` 命令允许客户端在下载文件前对文件进行 tar 或解 tar 操作。（有关使用 `tar` 的更多信息，请参见第 6 章。）此命令的格式为：

```
tar switch class
```

其中 `switch` 为 ON 或 OFF，而 `class` 为 anonymous、real 或 guest。

> **注意：** 这是用户递归下载子目录的一种很好的机制。

# 权限

在 FTP 服务器上设置文件权限非常重要。您需要确保设置了正确的权限，这样您不想共享的文件就不会被共享，而不应被修改的文件也不会被修改。本节讨论的命令有助于您维护这种完整性。

**CHMOD**

此命令允许您决定是否要授予用户更改您站点上文件权限的权利。（他们必须拥有该文件才能更改其权限。）该命令的格式为：

```
chmod switch class
```

其中 `switch` 为 ON 或 OFF，而 `class` 为 anonymous、guest 或 real。通常，您只想将此类型的权限授予真实用户。例如：

```
chmod ON real
```

**DELETE**

`delete` 命令告知服务器用户是否有权删除他们在 FTP 服务器上拥有的文件。该命令的格式为：

```
delete switch class
```

其中 `switch` 为 ON 或 OFF，而 `class` 为 anonymous、guest 或 real。例如：

```
delete ON real
```

**OVERWRITE**

此命令允许您决定是否允许用户通过上传来覆盖现有文件。该命令的格式为：

```
overwrite switch class
```

其中 `switch` 为 ON 或 OFF，而 `class` 为 anonymous、guest 或 real。例如：

```
overwrite ON real
```

**RENAME**

`rename` 命令允许您决定用户是否可以在 FTP 服务器上重命名他们拥有的文件。该命令的格式为：

```
rename switch class
```

**UMASK**

`umask` 命令允许您决定您的 FTP 服务器用户是否可以更改其默认 umask。用户的 umask 决定了其创建的任何文件的默认权限。umask 是八进制数，表示其权限的反义。例如，umask 为 077 意味着创建的任何文件都可以被所有者读取、写入或执行，但不能被其他人访问。

该命令的格式为：

```
umask switch class
```

其中 `switch` 为 ON 或 OFF，而 `class` 为 anonymous、real 或 guest。例如：

```
umask ON real
```

**PASSWD-CHECK**

提供匿名访问的网站通常要求该网站的用户将电子邮件地址作为密码输入；`wu-ftpnd` 允许您决定在运行匿名网站时，对执行密码检查的严格程度。该命令的格式为：

```
passwd-check strictness enforcement
```

其中 `strictness` 为 none、trivial 或 rf622，而 `enforcement` 为 warn 或 enforce。如果 `strictness` 为 none，用户可以在密码字段中输入任何内容，`wu-ftpnd` 都会接受。trivial 仅要求电子邮件地址中必须包含 @ 符号。指定 rf622 要求电子邮件地址完全符合消息头标准。（例如，shah@domain.com 不是符合 rf622 的电子邮件地址。）

此命令的执行方式有两种：warn，意味着如果用户的密码不符合要求，`wu-ftpnd` 将警告用户然后继续；以及 enforce，意味着 `wu-ftpnd` 不允许用户访问，直到他们提供了有效地址为止。

请注意，这仅影响匿名访问。

**PATH-FILTER**

`path-filter` 命令允许您对上传到服务器的文件的文件名应用过滤器。该命令的格式为：

```
path-filter typelist message allowed-regex denied-regex
```

其中 `typelist` 是此命令影响的用户的逗号分隔列表；可用的用户类型为 anonymous、guest 和 real。`Message` 是如果用户的文件名未能通过此过滤器时向用户显示的文件。`Allowed-regex` 是用户想要上传文件时文件名必须匹配的正则表达式。`Denied-regex` 是用户想要上传文件时文件不能匹配的正则表达式。例如，以下行：

```
path-filter anonymous /home/ftp/badfilename UL.* gifs
```

告诉我们，匿名用户必须看到他们上传的文件名以字母“UL”开头，但不能以“.gif”结尾。如果文件名不符合此标准，`/home/ftp/badfilename` 的内容将被发送给用户。

