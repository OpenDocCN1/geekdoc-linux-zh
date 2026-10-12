

用户，并且不会建立连接。若要使用此功能，您需要自行创建该文本文件。

## 限制匿名和来宾登录的主机访问

您可以使用 `guestserver` 参数来限制哪些主机被允许使用匿名或来宾登录来访问您的服务器。示例如下：

```
guestserver maple,pine,snowbird
```

在此示例中，来宾和匿名登录仅限于来自名为 maple、pine 或 snowbird 的主机的连接。来自其他计算机的此类登录将被拒绝。如果仅使用 `guestserver` 参数而不指定任何主机名，则所有来宾和匿名登录请求都将被拒绝。

## 拒绝真实用户访问

您可以通过将用户名添加到 `/etc/ftpusers` 文件来拒绝来自真实用户（即在 `/etc/passwd` 系统中拥有用户账户的用户）对您的 FTP 服务的访问。这样做的一个主要原因是防止人们试图通过管理账户闯入您的系统。拒绝管理用户访问可能看似不合逻辑，但可以防止潜在的安全漏洞。此文件默认包含的用户名有：

- root
- daemon
- adm
- ip
- sync
- shutdown
- halt
- mail
- news
- uucp
- operator
- games
- nobody

如果这些行政级真实用户账户可以访问您的 FTP 服务器，那么黑客可能会通过 FTP 闯入您的系统。这可能会使他们获得对您整个 Red Hat Linux 系统的访问权限——而不仅仅是 /var/ftp 目录结构。

## 通过 UID 和 GID 拒绝/允许用户访问

您可以拒绝那些尝试以特定用户或组名称或编号登录的用户的访问权限。`deny-uid` 和 `deny-gid` 功能可用于替代前面描述的 `/etc/ftpusers` 文件。`allow-uid` 和 `allow-gid` 功能可用于允许使用在 `/etc/ftpusers` 文件中被拒绝的服务权限。

您可以通过编号或名称来识别用户和组。如果使用编号，这些编号前必须加上百分号（%）。以下是一些示例：

```
deny-gid      %-110
deny-uid      %-110
allow-uid     uucp news
```

在这些示例中，所有管理登录以及其他用户 ID 和组 ID 小于 110 的用户都被拒绝访问您的 FTP 服务。然而，`allow-uid` 行会覆盖对 `uucp` 和 `news` 登录的服务拒绝。

## 启动和关闭 WU-FTPD 服务

一旦配置好 FTP 服务器，您就可以准备启动它。WU-FTPD 的启用或禁用基于 `/etc/xinetd.d/wu-ftpd` 文件中的信息。若要暂时关闭 WU-FTPD 服务，您可以使用 `ftpsut` 命令。

### 启动 WU-FTPD

默认情况下，WU-FTPD 是禁用的。若要启用 WU-FTPD，您需要修改 `/etc/xinetd.d/wu-ftpd` 文件中的 `disable = yes` 条目。请以 root 用户身份使用任意文本编辑器打开该文件，并将该行更改为如下内容：

```
disable = no
```

接下来，您需要重启 `xinetd` 守护进程，以便应用新的更改。您可以以 root 用户身份输入以下内容来完成此操作：

```
# /etc/init.d/xinetd restart
Stopping xinetd:        [   OK   ]
Starting xinetd:        [   OK   ]
```

现在，尝试使用 `ftp` 命令或其他 FTP 客户端连接到您的 WU-FTPD 服务器。

### 关闭 WU-FTPD

`ftpsut` 命令用于关闭 FTP 服务。任何当前连接到 FTP 服务的用户将被断开连接。当他们输入 FTP 命令时，他们会看到诸如“FTP server shut down -- please try again later”（FTP 服务器已关闭 —— 请稍后再试）或仅显示“Not connected”（未连接）的消息。

使用 `ftpsut` 命令，您可以选择立即关闭服务器，或设置在未来某个时间关闭。若要立即关闭服务，请输入以下内容：

```
# ftpsut now
```

您可以通过添加从现在起希望服务器关闭的分钟数，或输入未来某个特定时间来设置服务器在特定时间关闭。以下是一些示例：

```
# ftpshut 20:18
# ftpshut -1 20 -d 3
```

在第一个示例中，服务器被设置为在 20:18 关闭（在 12 小时制时钟下即晚上 8:18）。在第二个示例中，-1 选项指定服务器关闭前剩余的分钟数（在此示例中为 20 分钟）。-d 选项指定在 FTP 服务关闭前多少分钟将用户从服务器断开连接。（如果未指定 -d 选项，则用户将在服务器关闭前五分钟被断开连接。）

为了使关闭 FTP 服务的过程更有人情味，发送一条警告消息让用户知道 FTP 即将停止运行是个不错的主意。以下是关闭 FTP 服务器时发送关闭警告消息的一个示例：

```
ftpshut 20:15 "FTP will go down soon. Finish and disconnect."
```

### 重启 FTP

运行 `ftpshut` 后，它会在 `/etc` 和 `/var/ftp/etc` 目录中创建一个名为 `shutmsg` 的文件。当您的 FTP 服务器关闭时，它会保持关闭状态，直到这些文件被移除。因此，要重启您的 FTP 服务器，您只需执行以下操作（以 root 用户身份）：

```
# rm /etc/shutmsg /var/ftp/etc/shutmsg
```

上述命令移除了这些文件。此时，用户可以立即重新连接到您的 FTP 服务器。另一种可用于重启 FTP 服务器的命令是 `ftprestart` 命令。

## 监控 WU-FTP 服务器

每当您从计算机设置供公众使用的服务时，密切关注它是个好主意。您可以使用许多通常用于监控计算机文件系统的相同技术来监控您的 FTP 服务器（例如，各种用于监视磁盘空间消耗的工具）。不过，为了跟踪用户在您的 FTP 系统上的活动，FTP 提供了日志记录功能。

### 记录连接

当 `ftpd` 守护进程被启用（基于 `/etc/xinetd.d/wu-ftpd` 文件中的条目）时，-l 选项会被添加到命令行中。此选项会导致每个 FTP 会话被记录到 syslog 设施中。因此，提供以下部分关于 FTP 活动信息的消息将发送到您的 `/var/log/messages` 文件：

- 尝试连接您 FTP 服务的用户的用户名、主机名和 IP 地址。
- 登录时使用的用户名（如 anonymous 等）。
- FTP 服务针对该用户断开连接的方式和时间。

您可以使用这些信息来监控服务器上的活动。例如，如果有人试图闯入您的系统，您可以看到多次失败的登录尝试。您还可以查看是否收到的匿名 FTP 请求超出了您的处理能力。

### 记录文件传输

如果会话期间有文件传输，它们会被记录到 /var/log/xferlog 中。在该文件中，您可以看到传入和传出的文件传输。以下是 /var/log/xferlog 文件中两个日志条目的示例：

```
Sat Aug 23 21:26:20 2003 1 oak 1625 /in/log b i r mike ftp 1 root c
Sat Aug 23 21:27:23 2003 1 pine 124 /pub/a.txt a o r mike ftp 1 root c
```

在第一个示例中，传输发生在 2003 年 8 月 23 日星期六的 21:26:20。传输时间仅为 1 秒。远程主机名为 oak，文件大小为 1625 字节。传输的文件名为 log，并被放入 FTP 服务器上的 /in 目录。传输类型为二进制（b）。下划线 (_) 表示未采取任何特殊操作（如文件压缩或解压缩）。i 表示这是一个传入传输。用户是一个名为 mike 的真实用户（r）。调用的服务是 ftp。认证是使用 RFC931 认证（1）完成的。认证方法返回的用户 ID 为 root。c 表示传输已完成。

在第二个示例中，有几种项目值得关注。远程计算机名称为 pine。文件使用 ASCII 传输方法（a）进行传输。文件 /pub/a.txt 从文件服务器传输（o）。

## 获取有关 FTP 服务器的更多信息

有许多资源可用于获取更多关于 FTP 服务器的信息。以下是您的一些选择：

- **FAQ** — WU-FTPD 常见问题列表的最新版本可从 www.wu-ftpd.org/wu-ftpd-faq.html 获取。若要查看 vsFTPd FAQ，请访问 /usr/share/doc/vsftpd\*/FAQ。
- **RFCs** — 请求评论（Requests for Comments）是定义互联网使用标准协议的文档。FTP 的主要 RFC 是 RFC959。您可以从互联网上的多个位置获取 RFC，包括 Internet RFC/FYI/STD/BCP Archives: www.faqs.org/rfcs。
- **CERT** — 该组织提供了有关设置 FTP 服务器的有用文档。《匿名 FTP 滥用》描述了如何应对和恢复 FTP 服务器滥用。它还说明了如何处理软件盗版问题。《匿名 FTP 配置指南》提供了设置 FTP 区域的一般指导，以及设置可写 FTP 区域的具体挑战。这两份文档均可从 CERT Tech Tips 页面 (www.cert.org/tech\_tips) 获取。

