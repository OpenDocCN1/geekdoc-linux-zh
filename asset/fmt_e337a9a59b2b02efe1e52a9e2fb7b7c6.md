
在此示例中，任何尝试从名为 `maple`、`snowbird` 或 `oak` 的计算机登录你 FTP 服务的用户将被拒绝访问你的系统。用户尝试登录后，将向用户显示来自指定文件（在本例中为 `/etc/ftpdeny.msg`）的消息，且不会建立连接。要使用此功能，你需要自己创建该文本文件。

## 启动和关闭 FTP 服务

一旦你配置了服务器，就准备好启动它。WU-FTPD 的启用或禁用取决于 `/etc/xinetd.d/wu-ftp` 文件。要临时关闭 FTP 服务，你可以使用 `ftpasswd` 命令。

## 启动 WU-FTPD

要启用禁用的 WU-FTPD，你必须修改 `/etc/xinetd.d/wu-ftp` 文件中的 `disable = yes` 选项。以 root 用户身份打开该文件，使用任何文本编辑器，将其更改为：

```
disable = no
```

接下来，你需要重启 xinetd 守护进程使更改生效。你可以通过 root 用户执行以下命令：

```
# /etc/init.d/xinetd restart
Stopping xinetd:  [ OK ]
Starting xinetd:  [ OK ]
```

现在尝试 `ftp` 命令或其他 FTP 客户端连接你的 WU-FTPD 服务器。

## 关闭 WU-FTPD

通过 `ftpasswd` 命令，你可以立即关闭服务器，也可以设置它在未来的某个时间关闭。当你运行 `ftpasswd` 时，它会创建一个关闭文件。当 FTP 服务被关闭后，你需要删除该文件。

`ftpasswd` 命令会关闭 FTP 服务。任何当前连接到 FTP 服务的用户都将被断开连接。当他们输入 `ftpasswd` 命令时，将看到“FTP server down -- please try again later”或简单的“Not connected”。要立即关闭服务，请输入：

```
# ftpasswd
```

### 第四部分：红帽 Linux 网络与服务器设置

### `ftpush -l 20 -d 3`

在第一个示例中，服务器设置为在 20:18 关闭（或 12 小时制下的下午 8:18）。

在第二个示例中，`-l` 选项指定了服务器关闭前的剩余分钟数（在此示例中为 20 分钟）。`-d` 选项指定了 FTP 服务关闭前断开已连接用户的的分钟数。（如果不使用 `-d` 选项，用户将在关闭前五 分钟被断开连接。）

为了在关闭 FTP 服务时显得不那么“不合群”，发送一条警告消息让用户知道 FTP 将关闭是一个很好的主意。以下是在关闭 FTP 时如何发送关闭警告消息的示例：

```
ftps 20:15 "FTP will go down. Finish and disconnect."
```

### 重启 FTP

在运行 `ftpshut` 之后，它会在 `/etc` 和 `/var/ftp/ftpc` 两个目录中各创建一个名为 `shutmsg` 的文件。当你的 FTP 服务器关闭时，它将一直保持关闭状态，直到这些文件被删除。因此，要重启 FTP 服务器，你只需要执行以下操作（作为 root 用户）：

```
# rm /etc/shutmsg /var/ftp/etc/shutmsg
```

上述命令会删除这些文件。此时，用户将能够立即重新连接到你的 FTP 服务器。你可以使用的另一个重启 FTP 服务器的命令是 `ftpstart` 命令。

### 监控 WU-FTP 服务器

当你从电脑上设置一个供通用使用的的服务时，监控它是一个好主意。你可以使用许多用于监控计算机文件系统的技术来监控你的 FTP 服务器（例如用于监控磁盘空间消耗各种工具）。但是，为了跟踪 FTP 系统的活动，FTP 提供了日志功能。

### 连接日志

当启用 `ftpd` 进程（通过 `/etc/xinetd.d/wu-ftpd` 文件中的条目）时，命令行中会添加 `-l` 选项。该选项会将每个 FTP 会话记录到 syslog 设施。因此，提供有关 FTP 活动某些信息的消息将发送到你的 `/var/log/messages` 文件中：

- 尝试连接 FTP 服务的用户名、主机名和 IP 地址。
- 他们登录时的用户名（匿名用户等）。
- FTP 服务何时以及如何为用户断开连接。

## 第 20 章：设置 FTP 服务器 791

你可以使用这些信息来监控你的服务器。例如，如果有人试图入侵你的系统，你可以看到多次失败的登录尝试。你还可以看到收到的匿名 FTP 请求是否超过了你的处理能力（这可能会促使你获取一台更强大的服务器，或者研究你是否正受到拒绝服务攻击）。

### 文件传输日志

如果会话期间存在文件传输，它们会被记录在 `/var/log/xferlog`。在那个文件中，你可以看到导入和导出的文件传输。以下是 `/var/log/xferlog` 中两个日志条目的示例：

```
Sat Aug 17 21:26:20 2002 oak 1625 /in/log b r mke ftp 1 root c
Sat Aug 17 21:27:23 2002 pine 124 /pub/a.txt a r mke ftp 1 root c
```

在第一个示例中，传输发生在 2002 年 8 月 17 日（星期六） 21:26:20。远程主机名是 `oak`，文件大小为 1625 字节。传输的文件名为 `log`，并被放在 FTP 服务器的 `/` 目录下。传输类型为二进制 (`b`)。下划线 (`_`) 表示没有采取特殊操作（如文件压缩或解压）。`i` 表示这是一个导入传输。用户是一个名为 `mike` 的真实用户 (`r`)。服务调用了 `ftp`。使用 RFC9331 认证完成验证 (`1`)。通过认证方法返回的用户是 `root`。`c` 表示传输已完成。

在第二个示例中，有几项值得关注。远程计算机名称是 `pine`。文件使用 ASCII 传输方法 (`a`) 进行传输。文件 `/pub/a.txt` 从服务器传输出 (`o`)。

### 使用非常安全的 FTP 服务器 (vsFTPD)

你可以使用 Very Secure FTP Server Wu-FTPD 作为你的 FTP 服务器。虽然它的历史时间没有 WU-FTPD 长，但 vsFTPD 正在成为需要支持数百或数千并发下载的 FTP 站点的首选 FTP 服务器。它也被设计用于保护你的系统免受大多数常见攻击。

红帽公司在其在其 FTP 服务器 (`ftp.redhat.com`) 上使用 vsFTPD。Linux/GNU 世界的其他组织也切换到了 vsFTPD，包括 Debian Linux (`ftp.debian.org`)、GNU 项目 (`ftp.gnu.org`) 和 RPM Find (`ftp://rpmfind.net`)。

除了安全性和扩展性外，vsFTPD 的设计还为了简单性。因此，配置 vsFTPD 的选项比你在 WU-FTPD 中找到的少，你被预期依赖标准的 Linux 文件和目录权限为你的服务器提供精细的访问。开始使用 vsFTPD 或使用它替换 WU-FTPD 相当简单。

### 快速启动 vsFTPD

通过启用 vsFTPD，你几乎可以立即运行它。注意：如果你的 FTP 服务器无法访问，你可能需要确保已正确配置它。要这样做，请修改 `/etc/vsftd.conf`：

1. 使用 vsFTPD 前，请确保已安装软件包。
2. 通过更改 `vsftd.conf` 中的以下行来启用 vsFTPd：
```
disable = no
```
3. 使用以下命令重启 vsFTPd：
```
# /init.d/ftpd restart
```
4. 尝试匿名登录服务器：
```
$ ftp localhost
220 ready
331 请指定密码。
Password: ******
230 登录成功
Remote system is binary
```
如果你看到了上述消息，你的 FTP 服务器现在正在运行。下一节将解释 `/etc/vsftd.conf`。

## 配置 vsFTPD

你想对 vsFTPD 进行的大部分配置都可以在 `/etc/vsftd.conf` 中完成。尽管许多值没有显式列在该文件中，但你可以通过设置 `option=value` 语句来覆盖默认值。你可以设置用户如何访问 vsFTPD、如何记录日志以及如何设置超时。

通过以下章节了解更多关于 vsFTPD 默认配置以及你如何配置服务器的信息。

### 用户账户

访问 vsFTPD 的用户默认是匿名用户和任何真实用户。这些功能由以下行设置：

```
anonymous_enable=YES
local_enable=YES
```

`anonymous_enable` 允许用户使用匿名或 ftp 用户登录。任何具有本地账户（在 `/etc/passwd` 中）的用户都可以在 `local_enable` 设置为 YES 的情况下登录 FTP 服务器。此规则的例外是，默认情况下，所有位于 `/etc/vsftpd.userlist` 中的用户都被拒绝。

检查 `vsftpd.userlist` 文件查看哪些用户被拒绝访问 vsFTPD。你可以通过设置 `userlist_file` 参数向此列表添加其他用户，或更改列表的位置。

如果你喜欢，可以更改 `/etc/vsftpd.userlist` 的含义，使得列表中的用户允许使用 FTP 服务。设置 `userlist_deny=NO` 并更改列表以仅包含你希望授予服务器访问权限的用户。（所有其他用户，包括匿名和 ftp，都将被拒绝）。

### 设置 FTP 访问

vsFTPD 服务器提供了一种不灵活但更简单安全的访问权限方法。与其使用 FTP 服务中的设置来选择性地阻止特定目录的下载和上传（如 WU-FTP 所示），可以使用标准的 Linux 文件和目录权限来限制访问。然而 `/etc/vsftd.conf` 文件中的以下设置允许用户从你的 vsFTPD 服务器获取文件并将其存入服务器。

### 下载文件

任何具有有效登录的用户（匿名或真实用户，排除某些管理登录）都可以从 vsFTPD 服务器下载文件，默认情况下如此。当然，下载能力

特定文件或特定目录下的文件受以下 Linux 基本特性的管理：

你可以使用 `local_user` 选项更改普通用户的根目录，使其被限制在自己的主目录内。通常情况下你可能并不希望这样做，因为在普通登录时使用相同的用户名和密码不会对你的用户设置任何限制。为了在使用 vsFTPpd 时将所有普通用户限制在它们自己的主目录内，请向 `/etc/vsftpd.conf` 文件中添加此行内容：

```
local_user=YES
```

`/etc/vsftpd.conf` 文件中的一个设置可以影响文件的下载方式。默认情况下，设置了以下值以防止文件以 ASCII 模式下载：

```
ascii_download_enable=NO
```

默认情况下，所有下载都以二进制模式进行。尽管 vsFTPd 看起来允许用户切换到 ASCII 模式，但如果禁用了此设置，ASCII 模式将无法工作。

## 从本地用户上传（写入）文件

在 `/etc/vsftpd.conf` 文件中设置了几个值，允许在 vsFTPd 会话期间上传文件。这些默认值允许任何拥有普通本地用户账户的用户上传文件：

```
write_enable=YES
umask=022
```

如果你打算允许任何用户向 FTP 服务器写入的能力，则 `umask` 值必须为 `YES`。`umask=022` 值设置了本地用户在服务器上创建文件时使用的默认文件权限。（022 值导致创建的文件具有 644 权限，允许用户读取，而其他人仅具有读取权限。）

默认情况下，禁止以 ASCII 模式上传。虽然 ASCII 下载会为你的服务器造成资源耗尽的潜在漏洞，但 ASCII 上传显然没有那么危险，并且可以用于上传文本文件。要允许 ASCII 上传，请添加以下行：

```
ascii_upload_enable=YES
```

### 从匿名用户上传（写入）文件

匿名 FTP 用户的上传文件功能已关闭。如果你想开启它，请向 `/etc/vsftpd.conf` 文件中添加以下行：

```
anon_upload_enable=YES
```

你还需要确保 `/var/ftp` 目录包含一个或多个对匿名用户开放权限的目录。例如，你可能想创建一个 `incoming` 目录并开放其权限（`chmod 777 /var/ftp/incoming`）。

匿名用户上传的文件默认将具有 600 权限（ftp 用户具有读/写权限，任何其他用户无法访问）。要允许 644 权限，例如，你可以添加以下行：

```
umask=077
```

一旦你允许匿名用户上传文件，就可以授予他们更改其所上传文件的有限权限。通过添加以下行，你可以允许匿名用户重命名或删除任何由匿名用户拥的文件（前提是文件位于用户具有写入权限的目录中）：

```
anon_other_enable=YES
```

如果你还想允许匿名用户创建自己的目录，请添加以下内容：

```
mkdir_dir_enable=YES
```

默认情况下，ftp 用户拥有匿名用户上传的文件的所有权。如果你想指定匿名上传的文件由另一个用户（由你选择）所有，可以使用 `chown_uploads` 和 `chown_username` 选项。例如，如果你有一个名为 `newuser` 的用户账户，可以这样设置这些选项：

```
chown_uploads=YES
chown_username=newuser
```

当然，你可以创建并使用任何你名称。但是，出于安全考虑，你不应使用 root 登录或任何其他管理员登录为此目的。

## 添加消息文件

虽然 vsFTPd 不支持 WU-FTPd 支持的 README 和欢迎文件安排，但你可以向你的 vsFTPpd 服务器上的任何匿名目录添加 `.message` 文件。然后，如果你按照如下所示使用默认的 `dimessage_enable` 选项，当用户进入该目录时将显示 `.message` 文件中的文本：

```
dimessage_enable=YES
```

你可能最不想为匿名用户 FTP 服务器的根目录添加 `.message` 文件。默认情况下，该位置是 `/var/ftp/.message`。如果你想使用 `.message` 文件以外的文件，可以设置 `message_file` 选项。例如，为了在进入目录时显示 `.mysessage` 文件的文本，你可以添加以下行：

```
message_file=.mysessage
```

你还可以设置一条在登录提示符之前显示的单行消息。你可以通过输入以下行来实现，将文本替换为任何你想说的话：

```
ftpd_banner=Welcome to My FTP service.
```

## 记录 vsSFTPd 活动

vsFTPd 默认开启日志记录，你的 vsFTPd 站点活动将被写入 `/var/log/vsftpd` 日志文件。以下选项启用此类日志：

```
xferlog_enable=YES
xferlog_file=/var/log/vsftpd.log
```

如果你喜欢，可以通过将 `YES` 改为 `NO` 来关闭日志记录（不推荐，因为日志记录允许你监控潜在的入侵）。或者通过更改 `xferlog_file` 选项的值来更改日志文件的位置。日志以标准格式输出（与 WU-FTPd 的格式相同）：

```
xferlog_format=YES
```

## 设置超时

vsFTPd 默认设置了以下超时时间（以便其生效）：

```
accept_timeout=60
connect_timeout=60
idle_session_timeout=600
data_connection_timeout=120
```
