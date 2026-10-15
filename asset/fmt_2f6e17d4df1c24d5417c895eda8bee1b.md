
## 配置服务

要退出 FTP 客户端软件，只需在 `ftp>` 提示符处输入 `bye`。如果你想测试私有 FTP 服务器，请重新运行 FTP 客户端，但要使用你的登录名而不是匿名登录。这是一个示例：

```
[root@denon ~] ftp denon

Connected to denon.domain.com

220 denon.domain.com FTP server (Version wu-2.4.2-academ[BETA-12](1))

--> Wed Mar 5 12:37:21 EST 1997 ready.

Name (denon:root): ssh

331 Password required for ssh.

Password: march1031  [屏幕上不会显示此内容]

230 User ssh logged in.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp>>
```

## FTP 服务器如何工作

FTP 服务由 `/etc/inetd.conf` 文件控制，并在每当有人连接到 FTP 端口时自动被调用。（端口是网络连接到特定服务的本地关联。例如，端口 `21` 关联到 FTP，端口 `23` 关联到 Telnet 等。）当检测到连接时，FTP 守护进程 (`/usr/sbin/in.ftpd`) 被调用会话开始。在 `/etc/inetd.conf` 文件中，默认的 Red Hat 发行版包含了发生此步骤所需的行。

服务启动后，客户端需要提供用户名和密码。设置了两个特殊的用户名——`anonymous` 和 `ftp`，用于允许访问公共文件。任何其他访问都要求用户在服务器上拥有一个账户。

如果用户使用其账户访问服务器，将会执行额外的检查以确保该用户具有有效的 shell。没有有效 shell 的用户将被拒绝访问系统。如果你想允许用户对服务器进行有限的访问（例如，POI 邮件），但不想让他们通过 Telnet 或 FTP 登录，这就会很有用。要使 shell 变得有效，它必须列在 `/etc/shells` 文件中。如果你决定安装新的 shell，请务必将其添加到你的 `/etc/shells` 列表中，以便使用 shell 的人员可以通过 FTP 连接到系统。

访问 FTP 服务器的用户在首次登录时会被放置在他们的主目录中。此时，他们可以切换到系统中他们有权限的任何目录。另一方面，匿名用户受到多项限制。

匿名用户被放置在 FTP 用户的主目录中。默认情况下，该目录由 `anftp` RPM 包设置为 `/home/ftp`。当用户到达那里后，FTP 服务器会执行 `chroot` 系统调用，从而有效地将程序的根目录更改为 FTP 用户的目录。访问系统中的任何其他目录（包括 `/bin`、`/etc` 和 `/lib` 目录）将被拒绝。根目录的这种更改具有副作用，即服务器无法[]。

## 配置你的服务器

控制谁可以和不可以进入你的站点的能力是精细调整你匿名服务器的关键组件。以下命令定义了用于确定每个用户应该被放在哪个组中的标准。

### 控制访问——`ftpaccess` 文件

`/ftpaccess` 文件是控制谁以及多少用户可以访问服务器的主要手段。文件中的每一行都定义了一个属性或设置了其值。

以下命令控制访问：
- `class`
- `autogroup`
- `deny`
- `guestgroup`
- `limit`
- `loginfo`
- `private`

以下命令控制服务器告诉客户端的信息：
- `banner`
- `email`
- `readme`

这些命令控制日志功能：
- `log`
- `transfer`

以下是杂项命令：
- `alias`
- `cd`
- `compress`
- `shutdown`

权限控制由以下命令设置：
- `chmod`
- `delete`
- `overwrite`
- `rename`
- `umask`
- `passwd-check`
- `path-filter`
- `upload`

### 控制用户访问

#### `class`

`class` 命令定义了访问你服务器的用户类。你可以定义任意数量的类。每个类的格式如下：

```
class <classname> <typelist> <addrglob> [-addrglob> ...]
```

其中 `<classname>` 是你定义的名称，`<typelist>` 是允许进入该类的类型，`<addrglob>` 是允许访问该类的 IP 地址范围。

`<typelist>` 是一个逗号分隔的列表，其中每个项目都有三个值之一：`anonymous`、`guest` 或 `real`。匿名用户是指任何以匿名用户或 `ftp` 连接到服务器并只想访问可用文件的用户。`guest` 用户之所以特殊，是因为他们本身在系统中没有账户，但对组的关键部分具有特殊访问权限（`real` 用户 用户）。

`<addrglob>` 采用正则表达式的形式，其中 `*` 表示所有站点。多个 `<addrglob>` 可以与特定的类关联。

该行

```
class anonclass anonymous *
```

定义了类 `anonclass`，它仅包含匿名用户。他们可以从网络的任何地方发起连接。

另一方面，该行

```
class localclass real 192.168.42..*
```

仅允许来自局域网且拥有 FTP 服务器账户的真实用户通过 FTP 访问其账户。

### `autogroup`

`autogroup` 命令用于通过在匿名用户登录时自动为其分配特定的组权限，从而更严格地控制对匿名用户的访问。`autogroup` 行的格式为：

```
autogroup <groupname> <class> [<class> ...]
```

其中 `<groupname>` 是想要为匿名用户设置的组名，`<class>` 是使用 `class` 命令定义的类名。你可以为一个 `autogroup` 设置多个 `<class>` 条目。只有 `<class>` 中引用的匿名用户会受 `autogroup` 的影响。

请记住，你赋予用户权限的组必须存在 `/etc/group` 文件中。

### `deny`

`deny` 命令允许你根据主机名、IP 地址或其主机名是否可以通过 DNS 反向解析，显式地拒绝某些主机的服务。`deny` 命令的格式为：

```
deny <addrglob> <message_file>
```

其中 `<addrglob>` 是一个包含要拒绝地址的正则表达式，`<message_file>` 是包含消息的文件名，当主机连接时将显示该消息。

以下是一个示例 `deny` 行：

```
deny evilhacker.domain.com /home/ftp/.message.no.evil.hackers
```

此行向任何尝试从 `evilhacker.domain.com` 通过 FTP 连接的人显示 `/home/ftp/.message.no.evil.hackers` 文件的内容。若要根据用户 IP 地址是否能反向解析为其主机名来拒绝访问，请在 `<addrglob>` 中使用字符串 `!!named`。

### `guestgroup`

当你拥有真实用户但希望他们仅拥有限制性的 FTP 权限时，`guestgroup` 命令非常有用。该命令的格式为：

```
guestgroup <groupname> [<groupname> ...]
```

其中 `<groupname>` 是你想要限制的组名（从 `/etc/group` 中获取）。

当用户的组被限制时，该用户被处理的方式非常类似于匿名访问者；因此，匿名访问者所需的相同设置必须在该用户的账户中执行。用户的密码条目在目录字段也略有不同。*

用户主目录字段由 `/` 字符分隔。在分隔符之前，系统需要的是有效根目录，在分隔符之后是用户的相对主目录。例如，考虑以下密码条目：

```
user1:encrypted password:500:128:user 1:/ftp/:user1:/bin/ftponly
```

在这里，`/ftp` 是用户的新相对根目录（`bin`、`etc` 和 `lib` 目录需要在 `/ftp` 下创建，以供第一条命令和其他必要的库使用）。`/ftp/user1` 是用户的主目录。

### `limit`

`limit` 命令允许根据类和一天中的时间控制通过 FTP 登录系统的人数。如果你有一个热门的存档，但系统在工作期间需要对用户可用，那么这种功能就特别有用。`limit` 命令的格式为：

```
limit <class> <n> <times> <message_file>
```

其中 `<class>` 是要限制的类，`<n>` 是该类中允许的最大人数，`<times>` 是限制生效的时间段，`<message_file>` 是达到最大限制时显示给客户端的文件。

`<times>` 参数的格式较为复杂。该参数的形式为逗号分隔的字符串，每个选项代表单独的一天。周日到周六的形式分别为 `Su, Mo, Tu, We, Th, Fr, 和 Sa`，所有工作日都可以引用为 `Wk`。时间应保持军事时间格式，小时和分钟之间不使用冒号分隔。范围由字符字符指定。

例如，要限制 `anonools` 类周一至周四全天，周五从午夜到下午 5 点，你可以使用以下 `limit` 行：

```
limit anonools 10 MoTuWeTh,Fr0000-1700 /home/ftp/.message.too_many
```

在这种情况下，如果触发了限制，文件 `/home/ftp/.message.too_many` 的内容将显示给连接的用户

### `loginfails`

`loginfails` 命令允许设置客户端在断开连接之前可以进行的失败登录尝试次数。默认此值为五；但你可以通过使用命令进行设置：

```
loginfails <n>
```

其中 `<n>` 是尝试次数。例如，以下行在用户尝试三次失败后断开其与 FTP 服务器的连接：

```
loginfails 3
```

### `private`

你可能会发现，通过 FTP 与其他用户共享文件而无需将文件放在完全公开的地方，或无需为这些用户在服务器上提供真实账户是非常方便的。客户端使用 `SITE GROUP` 和 `SITE GPASS` 命令可以切换到需要密码的特权组。

要让你的 FTP 服务器支持此功能，你需要使用命令设置 `private` 标志：

```
private <switch>
```

其中 `<switch>` 是用于开启的 `YES` 或关闭的 `NO`。

由于你需要为这些组设置密码，请使用以下内容 `/etc/group` 的格式为：

```
group_name:encrypted_password:real_group
```

其中 `group_name` 是组名，`encrypted_password` 是加密密码，`real_group` 是组。

## 控制横幅消息

在用户连接时向他们提供消息通常很有用。这些命令允许你指定这些实例。使用它们是使站点具有自文档功能的好方法。

### `banner`

`banner` 命令允许在客户端提供登录和密码之前在屏幕上显示内容。这是一个显示服务器策略、上传位置以及匿名用户如何登录说明的重要机会。`banner` 命令的格式为：

```
banner <path>
```

其中 `<path>` 是你想显示的文件的完整路径。考虑此示例：

```
banner /home/ftp/.banner
```

### `email`

`email` 命令允许你指定站点管理员的电子邮件地址。某些错误消息或信息请求会根据需要提供此行提供的信息。`/ftpaccess` 文件中的默认值是 `root@localhost`。命令的格式为：

```
email <address>
```

其中 `<address>` 是站点管理员的完整电子邮件地址。

创建一个转发到系统管理员的“FTP”别邮箱通常是良好的做法。在登录横幅中提供此类信息也是好主意，这样用户在无法登录时知道该联系谁。

### `message`

`message` 命令允许你设置在客户端登录或切换到特定目录时发送的特殊消息。你可以指定多条消息。此命令的格式为：

```
message <path> <when> {class>
```

其中 `<path>` 是要显示的文件的完整路径，`<when>` 是显示消息的条件，`class>` 是适用于此消息的类列表。`<class>` 参数是可选的。你可以为特定消息列出多个类。这种功能非常有用，例如，如果你只想向匿名用户发送特定的消息。

消息文件本身（由 `<path>` 指定）可以包含特殊标记，FTP 服务器在运行时会将这些标记替换为适当的信息。这些选项如下：

| 选项 | 说明 |
| :--- | :--- |
| `%T` | 本地时间 |
| `%F` | `<dir>` 所在分区的剩余空间 |
| `%C` | 当前工作目录 |
| `%E` | 站点维护者的电子邮件地址（通过 `email` 命令指定） |
| `%R` | 客户端主机名 |
| `%L` | 服务器主机名 |
| `%U` | 登录时提供的用户名 |
| `%M` | 指定类别中允许的最大用户数 |
| `%N` | 指定类别中的当前用户数 |

请记住，当消息由匿名用户触发时，消息路径需要相对于匿名 FTP 目录。

示例消息命令为

```
message ./.toomy_anon LOGIN anonfolks
```

其中文件 `./.toomy_anon` 包含：

抱歉 `%T`，但您的类别中已有 `%N` 位用户，最大人数为 `%M` 位。请在几分钟后重试。
FTP 管理员 (`%E`)

如果此站点达到了 25 个用户的限制，客户端将看到类似下方的消息：

抱歉，`technics.domain.com`，但您的类别中已有 25 位用户，最大人数为 25 位。请在几分钟后重试。
FTP 管理员 (`ftp@domain.com`)

### `readme`

`readme` 命令允许您指定在何种条件下，通知客户端其当前目录下的某个文件最后修改时间。该命令可以采用以下形式

```
readme <path> <when> <class>
```

其中 `<path>` 是您想要向客户端提醒的文件名（例如 `README`），`<when>` 与消息命令中的 `<when>` 类似，`<class>` 是适用于此命令的类别。`<when>` 和 `<class>` 参数是可选的。

请记住，当为匿名用户指定路径时，文件必须相对于匿名 FTP 目录。

## 控制日志

与任何复杂的网络服务一样，安全性很快就会成为一个问题。为了应对可能的威胁，跟踪所建立的连接以及相应的命令是必要的。以下命令允许您确定服务器软件应该记录多少日志（如果有的话）。

### `log` 命令

通常出于安全考虑，您可能希望记录 FTP 用户的操作；您可以通过使用 `log commands` 选项来实现。客户端调用的每个命令都会发送到您的日志文件中。命令的格式为

```
log commands <typelist>
```

其中 `<typelist>` 是一个逗号分隔的列表，指定应该记录何种类型的用户。识别出的三类用户是匿名（`anonymous`）、客人（`guest`）和真实（`real`）。（参见本章前面对 `class` 命令的描述以获取每个用户类型的描述。）例如，要记录匿名和客人用户执行的所有操作，可以通过以下方式指定：

```
log commands anonymous,guest
```

### `log transfers`

如果您只想记录客户端进行的文件传输，而不是使用 `log commands` 语句记录整个会话，则应该使用 `log transfers`。该命令的格式为

```
log transfers <typelist> <direction>
```

其中 `<typelist>` 是一个逗号分隔的列表，指定应该记录何种类型的用户（匿名、客人或真实），`<direction>` 是一个逗号分隔的列表，指定传输必须在哪个方向进行以便被记录。可以选择记录的两个方向是入站（`inbound`）和出站（`outbound`）。

例如，要记录所有入站和出站的匿名传输，您将使用以下命令：

```
log transfers anonymous inbound,outbound
```

生成的日志存储在 `/var/log/xferlog` 中。参见关于该文件的章节获取更多信息。

## 杂项服务器命令

以下命令提供了一些杂项配置项。每个命令都为服务器增加了大量的灵活性，使其对作为管理员的您更加实用。

### `alias`

`alias` 命令允许您为 FTP 客户端定义目录别名。当客户端使用 `cd` 命令并指定别名时，这些别名会被激活。此功能对于为经常请求的文件提供快捷方式非常有用。命令的格式为

```
alias <string> <dir>
```

其中 `<string>` 是别名，`<dir>` 是用户应到的实际目录。以下是该命令的示例：

```
alias orb_discography /pub/music/ambient/orb_discography
```

因此，如果客户端连接并使用 `cd orb_discography`，他们将自动移动到 `/pub/music/ambient/orb_discography` 目录，无论他们当前位于何处。

### `cdpath`

类似于 `PATH` 环境变量，`cdpath` 命令允许您在客户端调用 `cd` 命令时建立一个路径检查列表。`cdpath` 命令的格式为

```
cdpath <dir>
```

其中 `<dir>` 是客户端使用 `cd` 命令时要检查的服务器上的目录。请记住对匿名用户使用相对于 FTP 主目录的相对目录。`cdpath` 命令的示例为

```
cdpath /pub/music

cdpath /pub/coffee
```

如果客户端立即输入 `cd instant`，服务器将按照以下顺序检查目录：

- 1. `/instant`
- 2. 为 `instant` 的别名（更多信息见 `alias` 描述）
- 3. `/pub/music`
- 4. `/pub/coffee`

### `compress`

### `tar`

与 `compress` 命令几乎完全相同，`tar` 指定服务器是否将解压一个文件。该命令的格式为

```
tar <switch> <class>
```
