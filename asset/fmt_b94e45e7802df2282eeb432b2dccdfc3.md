
## 12. 滚动到页面底部并点击项目管理界面链接

## 13. 提示时，输入列表管理员密码

现在你可以配置邮件列表的外观、感觉和行为。你可能需要考虑的重要信息包括：

- *隐私选项* —— 你希望列表是公开的还是私有的（即在你的组织内部？）？你允许谁查看你的成员列表？
- *发送过滤器* —— 谁可以向列表发布消息？列表是审核的还是未审核的？列表是否可能是单向的，例如作为联系客户的方式？
- *成员管理* —— 你的成员可以看到其他成员的信息吗？你添加和删除成员的策略是什么？

## 14. 当你完成选项配置，确保提交你的更改

# 第四部分：Fedora 网络和服务器设置

图 19-3：在 `mailman` 中创建多个邮件列表。

此时，你可以允许用户加入列表。鼓励他们探索并设置他们自己的用户偏好。

如果你在配置 `mailman` 时遇到问题，请参考 `/usr/share/doc/mailman-*` 目录下的 `INSTALL`、`REDHAT` 和 `README` 文件。

## 总结

Fedora 包含了全系列用于配置和管理邮件服务器的工具。对于邮件传输代理，Fedora 包含了 `Sendmail` 和 `Postfix` 软件包。两者都被认为是优秀的、专业级的邮件服务器。

为了允许用户从服务器访问其邮箱箱，Fedora 包含了 `dovecot` 和 `cyrus-imap` 软件包。这些软件包实现了 `POP3` 和 `IMAP` 协议，允许在服务器上下载或处理电子邮件。你还可以配置 `SquirrelMail` 以允许用户通过基于 Web 的界面访问其邮箱。

要在 Fedora 中设置邮件列表，你可以使用 `mailman` 软件包。除了包含非常灵活的配置工具外，`mailman` 还提供了简单的基于 Web 的访问邮件列表偏好和存档。

# 第 20 章 设置 FTP 服务器

## 本章内容

- 理解 FTP 服务器
- 使用 vsSFTP 服务器
- 获取更多关于 FTP 服务器的信息

文件传输协议（`FTP`）多年来一直是共享文件的标准方法。即使随着 Web 的普及使得 `Gopher` 和 `WAIS` 等服务过时，`FTP` 服务器仍然是共享文件的最常见方式。

## 理解 FTP 服务器

文件传输协议（`FTP`）多年来一直是共享文件的标准方法。即使随着 Web 的普及使得 `Gopher` 和 `WAIS` 等服务过时，`FTP` 服务器仍然是共享文件的最常见方式。

## FTP 服务器的属性

当 `FTP` 在多用户系统中实现时，只有文件系统的部分部分用于公共访问。从公共账户访问 `FTP` 的那些（默认匿名用户名）会自动被赋予一个 `FTP` 目录 (`/var/ftp`) 作为其根目录。然后，匿名用户可以访问该点下的文件和目录。访问 `FTP` 服务器的依赖于使用 `UNIX` 登录名的登录过程（即在 `/etc/passwd` 中的用户）。虽然字符串可以使用匿名作为用户名登录系统，但在系统中拥有账户的用户可以使用自己的用户名通过 `FTP` 登录，并很可能访问文件系统的大部分（特别是他们私有的文件和目录）。

## FTP 用户类型

几种不同类型的用户可以登录并使用 `FTP` 服务器。真实用户代表在包含你 `FTP` 服务器的 Fedora 系统上拥有登录账户的用户类别（即你认识他们，并且允许他们用于 `FTP` 之外的其他用途）。访客

## 第 20 章：设置 FTP 服务器

`user` 类似于用户账户，不同之处在于客用户对计算机文件系统的访问受到更多限制。`anonymous` 用户名是提供公共访问最常用的名称。

`vsFTPd` 服务器还支持虚拟用户概念。为 `vsFTPd` 创建虚拟用户的推荐方法是配置 `PAM`（可插拔身份验证模块）以指向每个用户的配置文件。关于如何配置 `vsFTPd` 以允许虚拟用户的教程，可以在 `www.linux-corner.net/linux/services/ftp.html` 找到。

> 注意：虽然 `vsFTPd` 是 Fedora 中完整的 `FTP` 服务器软件，但作为 Red Hat Linux 的一部分的 `WU-FTPd` 服务器在 Web 上仍然可用。但是，对于这一点，你必须决定是可以在你的服务器上运行 `vsFTPd`，还是下载并安装 `WU-FTPD`（`wu-ftpd` 软件包）。你选择的任何一个都将涵盖你计算机上 `FTP` 服务的完整功能。来自前一版《Red Hat Linux Bible》中关于设置 `WU-FTPd` 的描述可以从本书的配套网站：`www.wiley.com/combbooks/negus` 找到。

## 使用 Very Secure FTP Server

Very Secure FTP Server (`vsFTPd`) 是 Fedora 发行版中唯一需要支持数千个并发下载的 `FTP` 服务器软件。它还设计用于保护你的系统免大多数常见攻击的影响。

Red Hat 本身在其自己的 `FTP` 服务器 (`ftp.redhat.com`) 上使用 `vsFTPd`。Linux/GNU 世界的其他组织也已切换到 `vsFTPd`，包括 Debian Linux (`ftp.debian`) 和 GNU 项目 (`ftp.gnu.org`)。

除了安全性和扩展性外，`vsFTPd` 的设计还考虑了简单性。因此，配置 `WU-FTPD`（一个仍被广泛使用的旧版 `FTP` 服务器软件包）的选项较少，因此你需要依靠标准的 Linux 文件和目录权限来为你的服务器提供精细的访问。开始使用 `vsFTPd` 或使用它替换 `WU-FTPD` 都非常简单。

## 快速启动 vsFTPd

通过启用 `vsFTPd` 服务，你可以几乎立即运行带有默认值（在 `/etc/vsftpd/vsftpd.conf` 文件中设置）的 `FTP` 服务。以下是设置并运行 `vsFTPd` 的快速步骤。

> 注意：如果你在计算机上一直使用 `WU-FTPd` 服务器并正准备切换到 `vsFTPd`，你需要关闭 `WU-FTPd`。要做到这一点，请将 `/etc/xinetd.d/wu-ftpd` 文件中的 `disable=no` 改为 `disable=yes`。然后，一旦你完成了后续步骤，`vsFTPd` 将接管默认 `FTP`，访问 `/var/ftp` 目录并监听默认 `FTP` 端口。这两个软件包有不同的默认设置，你可能需要进行额外的调优以让 `vsFTPd` 按照你的预期运行。

## 第四部分：Fedora 网络与服务器设置

1. 要使用 vsFTPD 服务器，你必须确保已安装 vsFTPD 软件包。

```bash
# rpm -q vsftpd
```

2. 输入以下行来启用 vsFTPD 服务器（作为 root 用户）：

```bash
# chconfig vsftpd on
```

3. 按如下方式启动 vsFTPD 服务器：

```bash
# service vsftpd start
```

4. 尝试作为匿名登录 FTP 服务器（使用任何电子邮件地址作为密码）（如果你通过网络连接，请改用更安全的 `sftp` 命令）：

```bash
$ ftp localhost
Connected to your
220 (vsFTPD 1.2.1)
530 Please login with USER and PASS
Name (localhost:chris): anonymous
331 Please specify the password.
Pasword: ******
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

如果你看到了与上述类似的消息，说明你的 vsFTPD 服务器现在已运行。接下来，尝试从网络上的另一台计算机访问服务器以确保它是可访问的。

> 注意：如果你的 `FTP` 服务器外部无法访问，你可能需要确保你的网络配置正确，并且防火墙允许访问端口 `21`。请参阅附录 C 获取有关让网络服务工作的信息。

下一节将解释 `/etc/vsftpd/vsftpd.conf` 文件。

## 配置 vsFTPD

`vsFTPD` 的大部分配置都在 `/etc/vsftpd/vsftpd.conf` 中完成。虽然 `vsftpd.conf` 中没有显式设置许多值，但通过在该文件中设置 `option=value` 语句，你可以覆盖某些内容，例如哪些用户可以访问 `vsFTPD` 服务器、如何记录日志以及如何设置超时时间。

### 用户账户

可以访问 `vsFTPd` 服务器的用户默认包括匿名用户和系统上的任何真实用户账户（`guest` 仅仅是一个被限制在自己的主目录下的真实用户账户）。以下行设置了这些用户访问特性：

```
anonymous_enable=YES
local_enable=YES
```

## 第 20 章：设置 FTP 服务器

### 从本地用户上传（写入）文件

`vsftpd.conf` 文件中的两个值允许在 `vsFTPd` 会话期间上传文件。以下默认设置允许任何具有普通本地用户账户的用户上传文件：

```
write_enable=YES
local_umask=022
```

如果你打算允许用户具有向 `FTP` 服务器写入文件的能力，则 `write_enable` 的值必须为 `YES`。`umask=022` 值设置了本地用户在服务器上创建文件时使用的默认文件权限。（022 值使得创建的文件具有 644 权限，允许用户具有读取和写入权限，而其他所有人具有读取权限。）

与下载类似，默认情况下禁止 ascii 格式的上传。虽然 ascii 下载会留下一个可能耗尽你服务器资源的潜在安全漏洞，但 ascii 上传显然没有危险，并且对于上传文本文件非常有用。要允许 ascii 上传，请添加以下行：

```
ascii_upload_enable=YES
```

### 从匿名用户上传（写入）文件

匿名 `FTP` 用户的上传文件功能已关闭。如果你想将其开启，请在 `vsftpd.conf` 文件中添加以下行：

```
anon_upload_enable=YES
```

你还必须确保 `/var/ftp` 目录包含一个或多个对匿名用户开放写入权限的目录。例如，你可能想创建一个 `incoming` 目录并开放其权限（`chmod 777 /var/ftp/incoming`）。

匿名用户上传的文件默认将以 600 权限创建（ftp 用户的读取/写入权限，任何其他用户无法访问，这样上传文件的用户就无法删除它们）。例如，要允许 644 权限，你可以添加以下行：

```
anon_umask=022
```

当你允许匿名用户上传文件时，你可以授予他们更改其上传文件的有限能力。通过添加以下行，你可以允许匿名用户重命名或删除任何由匿名用户拥有的文件（前提是文件位于用户具有写入权限的目录中）：

```
anon_other_write_enable=YES
```

如果你还想允许匿名用户创建自己的目录，请添加以下：

```
anon_mkdir_write_enable=YES
```

默认情况下，ftp 用户获得匿名用户上传文件的所有权。如果你想指定匿名上传由另一个用户（由你选择）所有，可以使用 `chown_uploads` 和 `chown_username` 选项。例如，如果你有一个名为 `myuser` 的用户账户，可以这样设置这些选项：

```
chown_uploads=YES
chown_username=myuser
```

当然，你可以创建并使用任何用户名。但是出于安全考虑，你不应该为此目的使用 root 登录或任何管理员登录。

### 添加消息文件

虽然 `vsFTPD` 不像 `WU-FTP` 那样支持对 `README` 和欢迎文件的 `FTP` 服务器布局，但你可以向 `vsFTPD` 服务器上的任何可访问目录添加 `.message` 文件。如果你如下所示使用 `dirmessage_enable` 选项，当用户进入目录时，将显示 `.message` 文件中的文本：

```
dirmessage_enable=YES
```

你可能最不想为匿名用户的 `FTP` 服务器根目录添加 `.message` 文件。默认位置是 `/var/ftp/.message`。如果你想使用 `.message` 文件以外的文件，可以设置 `.message_file` 选项。例如，要在进入目录时显示来自 `.mymessage` 文件的文本，你可以添加以下行：

```
message_file=.mymessage
```

你还可以设置在登录提示之前显示单行消息。你可以通过输入以下行来实现，将文本替换为任何你想说的内容：

```
ftpd_banner=Welcome to My FTP service.
```

### 记录 vsFTPD 活动

`vsFTPD` 默认启用日志记录，你的 `vsFTPD` 站点的活动将被写入 `/var/log/xferlog`。以下选项启用日志记录并将日志文件更改为 `/var/log/vsftpd.log`：

```
xferlog_enable=YES
xferlog_file=/var/log/vsftpd.log
```

你可以通过将 `YES` 改为 `NO` 来关闭日志记录。（但注意，日志记录允许你监控潜在的入侵，因此不建议关闭。）或者你也可以通过更改 `xferlog_file` 选项的值来更改日志文件的位置。

如果你能够使用生成传输统计数据的工具，可以使 `vsFTPD` 将日志数据写入 `WU-FTP` 和其他 `FTP` 服务器使用的标准 `xferlog` 格式。要以 `xferlog` 格式存储你的传输数据，请设置以下选项：

```
xferlog_std_format=YES
```

### 设置超时

`vsFTPd` 默认设置了以下超时时间（这些值是内置的，因此你不需要对 `/etc/vsftpd/vsftpd.conf` 文件进行任何更改即可生效）：

```
accept_timeout=60
connect_timeout=60
idle_session_timeout=600
data_connection_timeout=120
```

`accept_timeout=60` 和 `connect_timeout=60` 值分别定义了客户端超时之前建立 PASV 或 PORT 风格连接所需的时间。`idle_session_timeout=600` 和 `data_connection_timeout=120` 值定义了连接被断开的时间。

### 导航 vsFTPD

以下超时时间在 `vsFTPd` 中默认设置（这些值是内置的，因此你不需要对 `/etc/vsftpd/vsftpd.conf` 文件进行任何更改即可生效）：

```
accept_timeout=60
connect_timeout=60
idle_session_timeout=600
data_connection_timeout=120
```

`accept_timeout=60` 和 `connect_timeout=60` 值定义了客户端超时之前建立 PASV 或 PORT 风格连接所需的时间。`idle_session_timeout=600` 和 `data_connection_timeout=120` 值定义了连接被断开的时间。

如果你能够使用生成传输统计数据的工具，可以使 `vsFTPD` 将日志数据写入 `WU-FTP` 和其他 `FTP` 服务器使用的标准 `xferlog` 格式。

## 获取更多关于 FTP 信息

有很多资源可以获取更多关于 `FTP` 信息。这里有一些：

- FAQ: 要检查 FAQ，请访问...
- RFCs: 请求意见是定义协议的文档。`FTP` 的 RFC 是 `RFC959`。
- CERT: 该组织提供了关于滥用的有用文档。
- Configuration Guidelines: 为设置 `FTP` 提供通用指南。

## 总结

`FTP` 服务是在互联网上提供存档的主要方法。Fedora 提供的唯一 `FTP` 服务器是非常安全 `FTP` (`vsFTPd`)。`vsFTPd` 服务器依赖标准的 Linux 和用户权限提供一个简单且安全的环境。

# 第 21 章：设置 Web 服务器

- Web 服务器简介
- 快速启动 Apache Web 服务器
- 配置 Apache Web 服务器
- 启动和停止服务器
- 监控服务器活动

Web 是互联网增长最快的部分。根据 Netcraft 的数据，2004 年 5 月互联网上有 5000 万 Web 站点。电子商务为企业提供了新的虚拟商店。

随着计算能力的提高、价格的下降、Linux 等免费操作系统以及 Apache 和 TUX 等免费 Web 服务器的出现，任何人建立存在变得更容易。

本章介绍了如何安装和配置 Apache Web 服务器。服务器的每个配置文件都得到了详细描述和解释。你学习了启动和停止服务器的各种选项，以及如何监控 Web 服务器的活动。安全是一个贯穿始终的问题。

> 注意：当前的 Fedora 版本带有 Apache 2.0 版本。Apache 2.0 包含了新的 Apache 应用程序接口、Unix 线程（用于多处理）、互联网协议版本 6 (`IPv6`) 以及多种协议。版本 2.0 还增加了一些模块，包名 `apache` 和 `apache-manual` 更改为 `httpd` 和 `httpd-manual`。

# 第四部分：Fedora 网络服务器设置
