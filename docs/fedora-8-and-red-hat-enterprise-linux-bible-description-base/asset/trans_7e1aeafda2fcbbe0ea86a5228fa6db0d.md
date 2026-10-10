
如果打算允许任何用户具备向 FTP 服务器写入的能力，**write_enable** 值必须设为 **YES**。umask=022 值设置了当本地用户在服务器上创建文件时使用的默认文件权限。（022 值会导致创建的文件具有 644 权限，允许该用户拥有读取和写入权限，而其他所有人仅拥有读取权限。）

与下载类似，默认情况下禁止以 **ascii** 模式进行上传。虽然 **ascii** 下载会为服务器资源耗尽带来潜在的安全漏洞，但 **ascii** 上传显然危险性较低，且可用于上传文本文件。若要允许 **ascii** 上传，请添加以下行：

```
ascii_upload_enable=YES
```

### 匿名用户上传（写入）文件

对于匿名 FTP 用户，上传文件的功能是关闭的。如果希望将其开启，请将以下行添加到 `vsftpd.conf` 文件中：

```
anon_upload_enable=YES
```

要使用匿名上传，必须激活全局写入权限。您还必须确保 `/var/ftp` 目录中包含一个或多个对匿名用户开放写入权限的目录。例如，您可能想要创建一个 incoming 目录并打开其权限（`chmod 777 /var/ftp/incoming`）。

匿名用户上传的文件默认将以 600 权限创建（ftp 用户拥有读写权限，其他任何用户均无法访问，因此即使是上传文件的用户也无法删除甚至查看它们）。例如，若要允许 644 权限，可以添加以下行：

```
anon_umask=022
```

当允许匿名用户上传文件时，您可以授予其有限的修改所上传文件的能力。通过添加以下行，您可以允许匿名用户重命名或删除任何由匿名用户拥有的文件（前提是这些文件位于用户拥有写入权限的目录中）：

```
anon_other_write_enable=YES
```

如果您还希望允许匿名用户创建自己的目录，请添加以下内容：

```
anon_mkdir_write_enable=YES
```

默认情况下，ftp 用户拥有匿名用户上传的文件的所有权。如果您希望指定匿名上传文件由其他用户（您选择的用户）拥有，可以使用 `chown_uploads` 和 `chown_username` 选项。例如，如果您有一个名为 mynewuser 的用户账户，可以按如下方式设置这些选项：

```
chown_uploads=YES
chown_username=mynewuser
```

当然，您可以创建并使用任何您想要的用户名。但是，出于安全原因，您不应该使用 root 登录或任何其他管理登录来进行此操作。

### 添加消息文件

虽然 vsFTPd 不支持诸如 Wu-FTP 等 FTP 服务器所支持的 README 和欢迎文件设置，但您可以在 vsFTPd 服务器的任何可访问目录中添加 `.message` 文件。然后，如果使用默认的 `dirmessage_enable` 选项如下所示，当用户进入该目录时，`.message` 文件中的文本将被显示：

```
dirmessage_enable=YES
```

您至少可能希望在 FTP 服务器匿名用户根目录中至少添加一个 `.message` 文件。默认情况下，该位置是 `/var/ftp/.message`。如果您希望使用除 `.message` 文件以外的文件，可以设置 `message_file` 选项。例如，要在进入目录时显示 `.mymessage` 文件中的文本，可以添加以下行：

```
message_file=.mymessage
```

`.message` 文件为您提供了一个添加服务器内容、版权信息或使用软件说明信息的机会。通过允许不同的消息文件，您可以根据访问者在文件服务器上的位置，定制想要传达的内容。

您还可以设置一行在登录提示之前显示的消息。您可以通过输入以下行来实现，将文本替换为您想要说的任何内容：

```
ftpd_banner=Welcome to My FTP service.
```

作为一种安全措施，您可以考虑添加一个表明运行不同操作系统的横幅。任何能减慢潜在入侵者发现您正在运行的软件的信息，都有助于您更容易地阻止该入侵者进入。

### 记录 vsFTPd 活动

vsFTPd 默认启用了日志记录，您的 vsFTPd 站点的活动会被写入 `/var/log/xferlog` 文件。以下选项启用日志记录并将日志文件更改为 `/var/log/vsftpd.log`：

```
xferlog_enable=YES
xferlog_file=/var/log/vsftpd.log
```

如果您愿意，可以通过将 YES 更改为 NO 来关闭日志记录。（请注意，日志记录使您能够监控潜在的入侵，因此不建议关闭它。）或者，您可以通过更改 `xferlog_file` 选项的值来更改日志文件的位置。请记住，随着大量使用，您的 FTP 服务器可能会产生大量的日志消息。因此，为了使其有用，您需要相当频繁地监控日志。

如果您希望使用生成传输统计信息的工具，可以让 vsFTPd 以 WU-FTPD 和其他 FTP 服务器使用的标准 xferlog 格式记录数据。要将传输数据存储在 xferlog 格式中，请设置以下选项：

```
xferlog_std_format=YES
```

### 设置超时

以下超时值在 vsFTPd 中默认设置（这些值是内置的，因此您无需对 `/etc/vsftpd/vsftpd.conf` 文件进行任何更改即可使它们生效）：

```
accept_timeout=60
connect_timeout=60
idle_session_timeout=600
data_connection_timeout=120
```

`accept_timeout=60` 和 `connect_timeout=60` 值分别决定了客户端在连接超时前建立 PASV 或 PORT 样式连接的时间。两者均设置为 60 秒。（请注意，这两行不会自动包含在配置文件中；如果您想更改它们的值，可以手动添加它们。）`idle_session_timeout=600` 选项会导致如果用户不活动超过 10 分钟（600 秒），FTP 会话将被断开。`data_connection_timeout` 值设置了服务器在断开连接之前等待的时间量，在此期间没有进展发生（默认值为 120 秒）。

### 导航 vsFTPd 站点

用户可能期望使用的大多数 shell 通配符，如问号和方括号，都受 vsFTPd 支持。有一个特别有用的通配符可用于 `ls` 命令，还有一个选项可以开启。星号（`*`）通配符可用于 `ls` 命令。支持在同一行中使用多个星号。您可以添加对 `ls` 的 `-R` 选项的支持，以便用户递归列出当前目录和所有子目录的内容。要开启此功能（默认是关闭的），您可以将以下行添加到 `vsftpd.conf` 文件中：

```
ls_recurse_enable=YES
```

### 在防火墙后设置 vsFTPd

如果您正在配置防火墙后面的 FTP 服务器，您需要做一些特殊的配置，以允许通信通过该防火墙到达您希望允许访问您服务器的那些实体。为了解决这个问题，您可以使用临时端口号（根据需要在一定范围内的随机临时端口号）。有关该问题的描述，请参阅 www.nctftp.com/ncftpd/doc/misc/ftp_and_firewalls.html 上的 “FTP 和您的防火墙” 页面。

## 获取更多关于 FTP 服务器的信息

有很多资源可以帮助您获取更多关于 FTP 服务器的信息。以下是其中一些选择：

- **FAQ** — 要查看 vsFTPd 常见问题解答，请前往 `/usr/share/doc/vsftpd*/FAQ`。
- **RFCs** — Requests For Comments（标准请求）是定义 Internet 上使用标准协议的文件。FTP 的主要 RFC 是 RFC959。您可以从 Internet 上的多种位置获取 RFC，包括 Internet RFC/FYI/STD/BCP 归档库（www.faqs.org/rfcs）。
- **CERT** — 该组织提供了用于设置 FTP 服务器的有用文档。*Anonymous FTP Abuses*（匿名 FTP 滥用）描述了如何应对和恢复 FTP 服务器滥用。它还说明了如何处理软件盗版问题。*Anonymous FTP Configuration Guidelines*（匿名 FTP 配置指南）提供了设置 FTP 区域的一般指导，以及设置可写入 FTP 区域的具体挑战。这两个文档均可从 CERT Tech Tips 页面（www.cert.org/tech_tips）获取。

> **提示：** 我强烈建议阅读来自 CERT 的 FTP 文档。这些文档中的技巧将有助于保护您的 FTP 服务器安全，同时允许您提供希望共享的服务。

## 总结

FTP 服务是通过 Internet 向用户提供文档和软件文件归档的主要方法。随 Fedora 和 RHEL 交付的唯一 FTP 服务器软件包是 Very Secure FTP（vsFTPd）服务器。vsFTPd 服务器依靠标准的 Linux 文件和用户权限，在 Fedora 中运行一个简单但安全的 FTP 环境。
