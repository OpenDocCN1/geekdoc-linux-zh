
如果您想让服务器持续运行（例如 Web 服务器），则必须为其配置一个在系统启动时初始化的脚本。在 Red Hat 上，这意味着要在 `/etc/rc/init.d` 目录下为其创建一个 init 脚本，以便在系统启动时运行。您也可以通过在命令行输入带有任何选项或参数的 `wu-ftpd` 命令来直接启动 FTP 服务器。`wu-ftpd` 服务器可以使用多个选项调用。通常，使用 `-l` 选项调用，该选项允许用户设置行超时，断开一段时间内没有活动的用户。`-d` 选项显示调试信息，而 `-u` 则设置上传文件的掩码。

### 表 23-1：wu-ftpd 选项

| 选项 | 效果 |
| :--- | --- |
| -d | 将调试信息写入 syslog |
| -l | 在 syslog 中记录每个 FTP 会话 |
| -tseconds | 将活动超时时间设置为指定的秒数（默认为 15 分钟） |
| -Tseconds | 用户设置超时时允许的最大超时时间（默认为两小时） |
| -a | 启用使用 ftppass 配置文件 |
| -A | 禁用使用 ftppass 配置文件 |
| -L | 将发送到 ftpd 服务器的命令记录到 syslog |
| -I | 将 ftpd 接收的文件记录到 xferlog |
| -o | 将 ftpd 传输的文件记录到 syslog |

### wuftpd 配置 wu-ftpd 服务器

Red Hat 为 KDE 桌面提供了一个名为 `wuftpd` 的 GUI 版 `wu-ftpd` 配置工具。尽管仍在开发中，但当前版本已可以轻松地配置您的 `ftppass` 文件。在 Red Hat 上，您可以从 KDE 桌面访问 `wuftpd`。`Wuftpd` 提供了一系列选项卡面板，用于控制用户和上传、指定服务器目录以及设置虚拟主机等任务。图 23-1 显示了安全面板，您可以在其中指定无法访问的文件，控制真实用户、访客和匿名用户对基本命令的访问，并指定允许的登录失败次数。

![](img/6cd7e3ee37600d2fcd508ba45f870a38_380_0.png)

图 23-1：kwufpd

通过 `kwufpd`，您可以设置虚拟主机。在图 23-2 所示的虚拟主机面板上，您可以指定虚拟主机信息，如主机名、根目录和日志文件。点击 `Add` 按钮创建虚拟主机条目，然后输入信息。您也可以通过 `reftools` 访问它。

![](img/6cd7e3ee37600d2fcd508ba45f870a38_380_1.png)

图 23-2：使用 kwufpd 的虚拟主机

注意：您还可以使用 `Linuxconf` 和 `Webmin` 来管理 `wu-ftpd` 服务器。Linux 要求加载其 `wu-ftpd` 模块。

### wu-ftpd 服务器配置文件

您可以使用许多配置选项来使 FTP 服务器适应您站点的特定需求。`wu-ftpd` 使用位于 `/etc` 目录下的多个配置文件。所有文件都以 `ftpasswd` 模式开头。主配置文件名为 `ftpaccess`。在此处，您可以为指定的目录提供基本信息和访问权限。`fthosts`、`ftusers` 和 `ftgroups ftconversions` 指定了在文件传输前后如何对文件的归档和压缩操作。`xferlog` 是存储服务器执行的所有操作运行日志的文件。

### ftpaccess

`ftpaccess` 文件决定了用户在访问您的 FTP 站点后的功能。可以指定访问、信息、权限、日志和若干杂功能。您可以创建为某些目录创建别名的条目，在 FTP 用户登录时显示消息，或防止匿名用户删除文件。`loginentry` 决定了用户在被断开之前可以尝试的登录次数，email 条目指定了 FTP 管理员的邮箱地址。`ftppasswd` 的 Man 手列出了可能的条目。Red Hat 系统上使用的配置 `ftppasswd` 文件位于本节。更多常用的 `ftppasswd` 条目请参见表 23-2。有关更多详细信息，请检查 `ftppasswd` 手页和 `wu-ftpd` 文档。

在 `ftppasswd` 文件中，您为不同类型的用户（称为类）设置功能。存在不同类型的用户：匿名、访客和真实用户。匿名用户是任何使用匿名登录名的用户。访客用户通过 `guestgroup` 或 `gusterer` 选项获得特殊的访客访问权限。真实用户是指在系统中拥有账户并使用 FTP 连接访问系统的用户。您可以使用 `class` 选项定义您的用户。在所示的 `ftppasswd` 文件中，创建一个名为 `all` 的类，包含所有匿名、访客和真实类型的用户。

`message` 条目指定了显示消息的文件以及显示消息的时间。您可以设置在用户登录时显示消息，并在用户进入特定目录时显示其他消息。例如，以下条目将在用户登录时显示 `/welcome.msg` 文件中的消息：

```bash
message /welcome.msg login
```

### 表 23-2：/etc/ftppasswd wu-ftpd 配置文件

| 访问功能 |  |
| :--- | --- |
| autogroup group classglob | 允许分组 classglob |
| email address | 指定 FTP 管理员的邮箱地址。 |
| message file { when ... } | 指定显示消息的文件以及显示消息的时间。 |
| loginentry | 决定用户在被断开之前可以尝试的登录次数。 |
| password file | Red Hat 系统上使用的 ftppasswd 文件。 |
| virtual host list | 指定虚拟主机信息，如主机名、根目录和日志文件。 |

### 表 23-2: /etc/ftpaccess wu-ftpd 配置文件

| 访问权限 | 说明 |
| :--- | :--- |
| delete yes | no typelist | 允许或禁止删除文件 (rm)。 |
| 权限能力 | 说明 |
| overwrite yes | no typelist | 允许或禁止修改文件。 |
| rename yes | no typelist | 允许或禁止重命名文件 (mv)。 |
| umask yes | no typelist | 允许或禁止创建文件。 |
| passwd-check none | trivial | rfc822 (enforce) | warn | 定义服务器对匿名 FTP 的密码检查模式级别和强制执行；rfc822 要求具有有效电子邮件格式的电子邮件地址。 |
| path-filter mesg allowed_charset { disallowed regexpx,...} | 对于 typelist 中的用户，path-filter 定义了控制文件名可以或不可变为什么的的正则表达式：可能会出现多个被禁止的正则表达式。 |
| upload root-dir dirglob yesno owner group ["dirs"]nodirs | 定义一个带有 dirglob 属性的目录，允许或拒绝上传。 | 要设置权限，请使用 yes 或 no 命令，后跟用户类型或类的列表。此处了 Red Hat 系统上的 ftpaccess 示例。在此示例中，所有用户都可以执行 tar 和 compress 操作，但禁止匿名和访客用户使用 chmod、delete、overwrite 和 rename 操作。他们还不能删除文件、修改文件或更改其名称或权限。

/etc/ftpaccess

```text
### 定义用户类
class all real,guest,anonymous *

### FTP 管理员的电子邮件地址
mail root@localhost

### 每个连接允许 5 次登录失败
logfails 5

### 登录和切换目录时的 README 文件
readme README* login
read README* cwd*

### 登录和切换目录时的消息文件
message /welcome.msg login
message .message cwd*

### 设置权限
# 允许访问压缩和 tar 操作。
compress yes all
tar all

### 禁止访客和匿名用户访问某些命令
chmod no guest,anonymous
delete no guest,anonymous
overwrite no guest,anonymous
rename no guest,anonymous

### 记录文件传输、关机通知、密码邮箱地址
log transfers anonymous,real inbound,outbound
shutdown /etc/shutdownmsg
passwd-check rfc822 warn
```

你可以通过进一步修改 `ftppass` 文件来控制对特定用户或用户组的访问，只需为他们定义一个类并对该类设置限制。例如，你可以所示为来自特定主机的连接定义一个类：
```text
