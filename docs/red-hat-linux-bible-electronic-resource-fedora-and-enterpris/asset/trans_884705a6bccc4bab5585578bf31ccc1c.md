
默认情况下，`ftp` 用户拥有来自匿名用户的上传文件的所有权。如果想指定匿名上传文件由其他用户（由你选择）拥有，可以使用 `chown_uploads` 和 `chown_username` 选项。例如，如果你有一个名为 `mynewuser` 的用户账户，可以按如下方式设置这些选项：

```
chown_uploads=YES  
chown_username=mynewuser
```

当然，你可以创建并使用任何你想要的用户名。然而，出于安全原因，你不应为此目的使用 `root` 登录或其他任何管理员登录。

## 添加消息文件

虽然 vsFTPD 不支持 WU-FTP 支持的 `README` 和 `welcome` 文件的安排，但你可以向 vsFTPd 服务器上的任何可访问目录添加 `.message` 文件。然后，如果你按如下方式使用默认的 `dirmessage_enable` 选项，当用户进入目录时，`.message` 文件中的文本将被显示：

```
dirmessage_enable=YES
```

你至少可能想要为匿名用户的 FTP 服务器根目录添加一个 `.message` 文件。默认情况下，该位置是 `/var/ftp/.message`。如果你想使用 `.message` 文件之外的文件，可以设置 `message_file` 选项。例如，要在进入目录时显示 `.mymessage` 文件中的文本，可以添加以下行：

```
message_file=.mymessage
```

你还可以设置一条单行消息在登录提示之前显示。你可以通过输入以下行来实现，将文本替换为你想要说的任何内容：

```
ftpd_banner=Welcome to My FTP service.
```

## 记录 vsFTPd 活动

vsFTPd 默认启用日志记录，你的 vsFTPd 站点的活动会被写入 `/var/log/vsftpd.log` 文件。以下选项以这种方式启用日志记录：

```
xferlog_enable=YES  
xferlog_file=/var/log/vsftpd.log
```

如果你愿意，可以通过将 `YES` 改为 `NO` 来关闭日志记录（不推荐，因为日志记录允许你监视潜在的入侵）。或者你可以通过更改 `xferlog_file` 选项的值来更改日志文件的位置。日志文件以标准格式输出（即与 WU-FTPD 相同的方式），基于以下选项：

```
xferlog_std_format=YES
```

## 设置超时

以下超时在 vsFTPd 中默认设置（这些值是内置的，因此你无需对 `/etc/vsftpd/vsftpd.conf` 文件做任何更改即可使其生效）：

```
accept_timeout=60
connect_timeout=60
idle_session_timeout=600
data_connection_timeout=120
```

`accept_timeout=60` 和 `connect_timeout=60` 值分别决定客户端在连接超时之前建立 PASV 或 PORT 风格连接的时间。两者均设置为 60 秒。`idle_session_timeout=600` 选项会导致如果用户非活动时间超过 10 分钟（600 秒），FTP 会话将被丢弃。`data_connection_timeout` 值设置在没有进展的情况下，服务器在丢弃连接之前等待的时间（此处默认值为 120 秒，即两分钟）。

### 浏览 vsFTPd 站点

总体而言，vsFTPd 为尝试浏览 FTP 站点的客户端提供的快捷方式不如 WU-FTPD 多。例如，用户可能期望使用的大多数 shell 通配符，如问号和方括号，均不受支持。

然而，有一个非常有用的通配符可以与 `ls` 命令一起使用，还有一个可以开启的选项。星号 (*) 通配符可与 `ls` 命令一起使用。同一行中支持多个星号。你可以为 `ls` 的 `-R` 选项添加支持，以便用户可以递归列出当前目录和所有子目录的内容。要开启此功能（默认关闭），你可以将以下行添加到 `vsftpd.conf` 文件中：

```
ls_recurse_enable=YES
```

## 使用华盛顿大学 FTP 服务器（WU-FTPD）

虽然 WU-FTPD 已从发行版中移除，但你仍可通过从 `rpmfind.net` 下载并安装以下软件包来使用 WU-FTPD：

- anongftp-4.0-12.i386.rpm
- wu-ftpd-2.6.2-8.i386.rpm

安装 WU-FTPD 时，它处于禁用状态。然而，大部分 FTP 配置已经就绪。

> **NOTE**：请参阅“启动和关闭 WU-FTPD 服务”以了解如何启动 FTP 服务器。

以下各节描述了首次安装 `wu-ftpd` 软件包时的设置：

- FTP Daemon — FTP 守护进程在 /etc/xinetd.d/wu-ftpd 文件中设置为 /usr/sbin/in.ftpd。当有人从你的计算机请求 FTP 服务（可能在 21 端口），xinetd 守护进程（监听大量端口）会启动 FTP 守护进程来处理该 FTP 登录请求。守护进程使用 -l 选项运行（以便 syslog 将 FTP 请求记录到 /var/log/messages）以及 -a 选项（以便使用 /etc/ftpassaccess 文件定义访问权限）。

- Access Permissions (/etc/ftpassaccess) wu-ftpd 软件包提供的 ftpaccess 文件相当严格，尽管你可以将其更改为你喜欢的任意开放或严格程度。以下是该文件最初的设置方式：

- deny and allow — 以下行用于设置哪些用户账户允许访问 FTP 服务，哪些被拒绝。deny-uid 和 deny-gid 条目阻止 ID 为 99 或更小或 65534 或更大的任何用户或组账户访问 FTP 服务。allow-uid 和 allow-gid 行通过允许 ftp 用户和组使用 FTP 服务来对拒绝规则作出例外。

```
deny-uid %-99 %65534-
deny-gid %-99 %65534-
allow-uid ftp
allow-gid ftp
```

- guestuser * — 此行默认使所有用户将其主目录作为其根目录。因此，如果你的主目录为 /home/jake 且你打开了到该计算机的 FTP 连接，你只能看到 /home/jake 或其子目录中的文件。（要更改此行为，要么在该行前添加注释字符 #，要么添加 realuser user 行，将 user 替换为你希望允许其在主目录外更改目录的用户名。）

- email root@localhost — 与 FTP 服务器管理相关的电子邮件默认发送到本地计算机上的 root 用户。

- loginfails 5 — FTP 连接在连续五次登录失败后终止。（这会减慢试图猜测你服务器密码的人的速度。）

- readme README* — 当用户登录（login）或更改到任何其他可访问目录（cwd=*）时，如果存在 README 文件，用户会被通知其存在。默认情况下，不存在 README 文件。对于任何以单词 README 开头的文件，服务器会显示一条消息，内容为“Please read the file README.whatever。”

- message — 这表示 /welcome.msg 文件中的消息应在用户登录 FTP 时显示。类似的行表示当用户进入包含此类文件的目录时，.message 文件将被显示。默认情况下，这些文件均不存在。如果你希望在 FTP 服务器上使用它们，必须自行创建它们。

> NOTE: `/welcome.msg` 文件相对于 FTP 用户登录的根目录。访客用户（如 anonymous）默认情况下的根目录为 `/var/ftp`。因此，`welcome.msg` 文件必须位于 `/var/ftp` 中。

- compress yes all — 这为所有用户启用 FTP 站点的文件压缩。compress 命令是 UNIX 系统中使用的标准压缩命令（尽管在 Linux 等自由操作系统中更常使用 gzip）。执行压缩的 compress 命令行在 /etc/ftpconversions 中定义。（由 compress 存储的文件具有 .Z 后缀。）

- tar yes all — 这为 FTP 站点的所有用户启用 tar 压缩。tar 命令是 UNIX 中用于创建多个文件归档的标准命令。执行压缩的 tar 命令在 /etc/ftpconversions 中定义。（由 tar 存储的文件具有 .tar、.tar.gz 或 .tar.Z 后缀。）

- chmod no guest, anonymous — 这阻止 guest 和 anonymous 用户名更改任何文件或目录的权限。

- delete no anonymous — 这阻止 anonymous 用户名删除文件或目录。

- overwrite no anonymous — 这阻止 anonymous 用户名覆盖现有文件或目录。

- rename no anonymous — 这阻止 anonymous 用户名重命名任何文件或目录。

- log transfers anonymous, guest, real inbound, outbound — 这记录匿名用户、访客用户以及任何真实用户（即在 Linux 系统上拥有自己的用户账户的用户）的文件传输。上传（inbound）和下载（outbound）传输均被记录。

- shutdown /etc/shutmsg — 这检查 `/etc/shutmsg` 文件以查看服务器是否即将关闭。如果是，你的 FTP 服务器会向当前 FTP 用户发送消息，警告他们服务器即将关闭。它还拒绝新的 FTP 连接，并在关闭前指定的时间断开当前用户连接。（默认情况下，`/etc/shutmsg` 文件不存在。）请参阅本章后面关于设置 FTP 关闭的部分，了解如何为计划的 FTP 关闭设置关闭文件。

- passwd-check rfc822 warn — 这检查匿名登录的密码是否为符合 rfc822 的地址。换句话说，FTP 服务器要求提供任何有效的电子邮件地址作为匿名登录的密码。如果地址不符合（即不是 user@host.domain 形式），服务器会“警告”用户但仍允许用户登录。
