
## 什么是 FTP 服务器？

FTP 服务器只是一种能够响应 FTP 请求的软件，就像 Web 服务器是一台在 80 端口监听并响应 HTTP 请求的计算机一样。对于 FTP 服务器，软件必须在 21 端口监听 FTP 请求。微软的 Internet Information Server 软件包中包含一个 FTP 服务器。它基本上允许用户将文件上传到计算机中。请记住，这可能会成为重大安全风险来源。如果您允许用户上传任意他们喜欢的文件到您的 Web 站点，那么有人可能会向您的系统上传有害软件。最好在运行 FTP 服务器之前，访问您首选的 FTP 服务器网站并阅读其所有文档。本章旨在为您提供该主题的入门介绍，并展示如何设置基本配置选项。

### VSFTP

我们将从一个最容易配置的 FTP 服务器开始。VSFTP 非常容易配置，并且随 Red Hat 9.0 附带提供。这意味着您应该已经拥有它了。请回想一下第 14 章“杂项 Linux 应用程序”中如何查看软件包并确保该应用程序已正确安装在您的计算机上。安装完成后，您就可以准备进行配置和运行了。只需遵循几个简单的步骤即可。

- 找到文件 `/etc/vsftpd/vsftpd.conf`。这如 **图 16.1** 所示。

![](img/12d790664598bbf390261087fbe55bbc_343_0.png)

**图 16.1：** 查找 VSFTP 的配置文件。

- 检查并确保设置了以下属性：
  - 将 `disabled` 设置为 `no`。
  - 确保设置了 `local_enabled = yes`。
  - 确保设置了 `allow_anonymous = yes`。这如 **图 16.2** 所示。

![](img/12d790664598bbf390261087fbe55bbc_344_0.png)

- 找到 `/etc/hosts.allow` 文件。您可以在图 16.3 中看到它。其中应包含设置 `vsftp: ALL`。这如图 16.4 所示。

![](img/12d790664598bbf390261087fbe55bbc_344_1.png)

![](img/12d790664598bbf390261087fbe55bbc_345_0.png)

**图 16.4：** hosts.allow 设置。

- 在 shell 中输入 `chkconfig --add xinetd`。然后输入 `/etc/init.d/xinetd start`。这如图 16.5 所示。

![](img/12d790664598bbf390261087fbe55bbc_345_1.png)

**图 16.5：** 启动您的 FTP 服务器。

您的 shell 命令所做的操作是将您的 VSFTP 服务器添加到 xinetd 进程中。该进程管理互联网和网络连接。第二行命令启动了您的 FTP 服务器。现在您的 FTP 服务器正在运行。您应该能够进入任何其他机器并使用任何 FTP 客户端登录。请记住，FTP 协议不依赖于操作系统。您可以进入一台 Windows 机器并使用 FTP 连接到您的 Linux FTP 服务器。登录的最简单方式是匿名登录：

```
username = anonymous
password = anye-mail@anywhere.com
```

如果您为 VSFTP 分配了任何用户名和密码，那么您可以使用它们登录。如果您查看了 VSFTP 的配置文件，您可能注意到还有几个可以更改的其他设置。VSFTP 的基本设置如表 16.1 所示，并附有简要说明。

**表 16.1：** VSFTP 设置

| 设置 | 用途 |
| :--- | :--- |
| `anonymous_enable` | 确定是否允许匿名用户登录。 |
| `local_enable` | 确定本地用户是否可以登录。 |
| `write_enable` | 连接的用户是否可以在执行写操作？ |
| `dirmessage_enable` | 当用户连接到特定目录时，是否希望显示消息？ |
| `ascii_upload_enable` | 是否允许上传 ASCII 文件？ |
| `ascii_download_enable` | 是否允许下载 ASCII 文件？ |
| `ftpd_banner` | 用户首次登录时是否希望显示横幅？ |

还有一个您可能需要考虑检查的文件。该文件是 `/etc/vsftpd.users`，其中包含一个用户列表，这些用户在任何情况下都不允许登录 FTP 服务器。将用户名添加到此列表中会阻止该用户永远无法登录您的 FTP 服务器。如果您有一个特定的用户无法登录，您可以考虑检查此文件以查看他是否因为某种原因出现在其中。默认情况下列出了几个用户。此文件的默认列表如图 16.6 所示。

![](img/12d790664598bbf390261087fbe55bbc_346_0.png)

**图 16.6：`vsftpd.users` 文件。**

这只是 VSFTP 的基本设置。它将运行并允许人们上传和下载。建议在本章结束后，挑选一个您觉得最喜欢的 FTP 服务器，并花些时间更深入地学习它。一个很好的开始方式是针对该 FTP 服务器进行简单的网络搜索。

### ProFTPD

ProFTPD 不随 Red Hat 安装 CD-ROM 附带，但它是流行的 FTP 服务器，因此不在此讨论它将是错误的。可以从 http://proftpd.linux.co.uk/ 获取。

最常用的服务器是 WU-FTPD。然而，ProFTPD 的设计者认为，虽然 WU-FTPD 提供了卓越的性能并且通常是一款不错的产品，但它缺少新版 Win32 FTP 中的某些功能。基于这种考虑，他们着手创建了一个针对 Unix 和 Linux 系统的 FTP 服务器，具备他们认为应该具备的功能。

安装 ProFTPD 相对简单。从网站下载该软件包后（之前提到的网站是一个不错的起点），您可以进入 shell，切换到软件包所在的目录，并输入 `rpm -install proftpd-{version}.rpm`。

这将把 ProFTPD 的配置文件放置在 `/usr/local/etc/proftpd.conf` 或 `/etc/proftpd.conf` 中。对于这以及任何不随 Red Hat 附带的软件，获取更多信息的最佳去处是该供应商的文档。我们在此列出的 FTP 服务器不包含在 Red Hat 安装中，是为了让您了解有哪些可用的替代方案。

### PureFTpd

PureFTpd 不随 Red Hat 附带，但它是一个非常有用的流行 FTP 服务器。您可以在 Web 地址 www.pureftpd.org/ 上找到它。然后您可以下载并安装在您的机器上。该 FTP 服务器的一个主要优点是它相当容易设置。

### WU-FTP

WU-FTP（华盛顿大学 FTP 服务器）随 Red Hat Linux 9.0 附带提供。它是 Linux 世界中最常用的 FTP 服务器之一。如果您遵循了第 2 章的说明，它应该已经安装在您的机器上了。您可以检查软件包，如果未安装，您可以添加它。配置此 FTP 服务器的第一步是找到配置文件。可以在 `/etc/xinetd.d/wu-ftpd` 找到。将 `disable = yes` 更改为 `disable = no`。

为了更改权限以使各种用户能够访问您的 FTP 服务器，您需要前往位于 `/etc/ftpaccess` 目录中的访问权限文件。要允许特定用户访问，您必须进行以下设置：`allow-uid ftp`（uid 是用户 ID） `allow-gid ftp`（gid 是组 ID）。

务必确保您添加的用户与系统中的实际用户相匹配。然后确保用户的家目录是您希望他们放置上传内容的地方。当您管理用户和组时，您会设置每个用户的家目录。这将是他通过 FTP 连接时首先看到的目录。如果您使用 FTP 允许 Web 服务器的客户上传页面，那么用户 `jdoe` 的家目录可能是类似 `/var/www/html/users/jdoe/` 的地方。

配置文件中以下条目并不关键，但查看它们可能是个好主意：

- `readme`: 此 `config` 文件中的设置标识了一个用户可以访问的 readme 文件。
- `e-mail root@localhost`: 这是管理员的电子邮件地址。
- `loginfails 5`: 失败前有多少次登录尝试？
- `message`: 这是您希望显示的欢迎消息文件。

现在您可以通过在 shell 中输入 `>/etc/init.d/xinetd restart` 来启动 WU-FTP。要停止 FTP 服务器，请输入 `ftpshtut now`。

您刚才看到的配置非常基础。建议您花些时间阅读 WU-FTP 网站上的文档。

最后，作为一个警告，您应该记住本章开头所说的内容。FTP 服务器可能构成重大的安全风险。如果本章是您第一次接触 FTP 服务器，那么建议您在未先阅读该 Web 服务器的所有文档之前，不要在商业或业务服务器上设置 FTP 服务器。访问该 Web 服务器的主页并阅读在线文档，特别关注安全注意事项。
