
使用这种语法，你用 <VirtualHost> 和 </VirtualHost> 来包裹一组仅适用于由 hostaddr 参数标识的特定虚拟主机的指令。hostaddr 可以是 IP 地址，也可以是虚拟主机的完全限定域名。

你可以在 <VirtualHost> 块内放置几乎任何 Apache 指令。至少，网站管理员会在 <VirtualHost> 块中包含以下指令：

- DocumentRoot，指定此虚拟主机文档的存储位置
- ServerName，向外部世界标识服务器（此名称是 DNS 支持的已注册域名）
- ServerAdmin，此虚拟主机网站管理员的电子邮件地址
- Redirect，指定要重定向到其他 URL 的 URL
- ErrorLog，指定记录与此虚拟主机相关的错误的文件
- CustomLog，指定记录对此虚拟主机访问的文件

当服务器收到针对特定虚拟主机的 DocumentRoot 目录中某个文档的请求时，它会使用该服务器 <VirtualHost> 块中的配置参数来处理该请求。

以下是一个典型的 <VirtualHost> 指令示例，用于设置虚拟主机 www.lnbssoft.com：

```
<VirtualHost www.lnbssoft.com>
 DocumentRoot /home/naba/httpd/htdocs
 ServerName www.lnbssoft.com
 ServerAdmin webmaster@lnbssoft.com
 ScriptAlias /cgi-bin/ /home/naba/httpd/cgi-bin/
 ErrorLog /home/naba/httpd/logs/error_log
 CustomLog /home/naba/httpd/logs/access_log common
 </VirtualHost>
```

在这里，CustomLog 指令中的名称 common 指的是先前在 httpd.conf 文件中由 LogFormat 指令定义的格式名称，如下所示：

```
LogFormat "%h %l %u %t "%>r" %s> %s" common
```

此日志格式字符串生成的日志文件中的行看起来像这样：

```
dial236.dc.psn.net - - [13/Jul/2003:10:09:00 -0500] "GET / HTTP/1.0" 200 1243
```

该格式字符串包含两个以百分号（%）开头的字母令牌。这些令牌的含义如表 2-1 所示。

表 2-1 LogFormat 令牌

| 令牌 | 含义 |
| --- | --- |
| %b | 发送给客户端的字节数，不包括头部信息 |
| %h | 客户端机器的主机名 |
| %l | 用户标识（如果可用） |
| %r | 来自客户端的 HTTP 请求（例如，GET / HTTP/1.0） |
| %s | 来自 Web 服务器的响应代码 |
| %t | 当前本地日期和时间 |
| %u | 用户提供的用户名（仅在访问控制规则要求用户名/密码身份验证时） |

## 第 3 章：配置 FTP 服务器

### 本章内容

- 安装 FTP 服务器
- 配置 FTP 服务器
- 设置匿名 FTP

**文件传输协议**（FTP）是一种用于在系统之间传输文件的流行互联网服务。**匿名 FTP** 是另一种用于分发文件的流行互联网服务。匿名 FTP 的优点在于，如果远程系统支持匿名 FTP，任何人都可以使用匿名用户 ID 通过 FTP 下载该系统的文件。尽管匿名 FTP 在分发数据方面很有用，但如果设置不当，它会带来安全风险。

Fedora Core 附带了多个 FTP 客户端和“非常安全”的 FTP 守护进程（vsftpd），由 Chris Evans 编写。Fedora Core 还包含一个名为 anonftp 的 RPM，它用于设置支持匿名 FTP 所需的文件。在本章中，我将向您展示如何通过文本配置文件来配置 FTP 服务器，以及如何控制对 FTP 服务器的访问。我还会介绍匿名 FTP——如何设置它以及如何确保其安全性。

### 安装 FTP 服务器

在 Fedora Core 安装过程中，您可以选择安装 FTP 服务器软件。要检查是否已安装 FTP 服务器，请输入以下命令：

```bash
rpm -q vsftpd
```

如果确实已安装该软件，您将看到类似以下输出：

```
vsftpd-1.2.1-2
```

如果您收到提示该包未安装的消息，您可以轻松地从随附的 DVD-ROM 上安装它。要安装 FTP 的 RPM 文件，请以 **root** 身份登录，并将 DVD-ROM 插入 DVD-ROM 驱动器。如果您使用的是 GNOME 或 KDE 桌面，DVD-ROM 会自动挂载。如果没有，请输入以下命令挂载 DVD-ROM：

```
mount /mnt/cdrom
```

然后输入以下命令更改目录：

```
cd /mnt/cdrom/Fedora/RPMS
```

该命令用于查找 FTP 的 RPM 文件。您可以使用以下 RPM 命令安装 FTP 服务器（包括匿名 FTP 设置）：

```
rpm -ivh vsftpd*
```

### 配置 FTP 服务器

Fedora Core 附带了由 Chris Evans 编写的“非常安全”的 FTP 守护进程（vsftpd）。vsftpd 的可执行文件为 /usr/sbin/vsftpd，它使用 /etc 和 /etc/vsftpd 目录中的多个配置文件。默认情况下，vsftpd 服务器是禁用的——如果您想使用 FTP 服务器，首先必须启用它。在本节中，我将向您展示如何做。

vsftpd 服务器被配置为独立运行，并且初始化脚本（或 init 脚本）——/etc/init.d/vsftpd——用于启动和停止服务器。要启动 vsftpd 服务器，请以 root 身份登录并输入以下命令：

```
service vsftpd start
```

您也可以以 root 身份输入以下命令，以便在系统启动时开启 vsftpd：

```
chkconfig --level 35 vsftpd on
```

启动 vsftpd 服务器后，默认设置就足以开始使用该服务器。这是因为其他 FTP 客户端现在可以连接并从您的 FTP 服务器请求文件。然而，您需要了解配置文件，以防将来需要自定义它们。

#### vsftpd 配置文件

vsftpd 服务器会参考位于 /etc 和 /etc/vsftpd 目录中的多个配置文件。这些目录控制 FTP 服务器的许多方面，例如它是独立运行、谁可以下载文件，以及是否允许匿名 FTP。vsftpd 的关键配置文件如下：

- `/etc/vsftpd/vsftpd.conf` 控制 `vsftpd` 服务器的工作方式（例如，是否允许匿名登录、允许文件上传等）。
- `/etc/vsftpd/ftpusers` 列出无法访问 FTP 服务器的用户名称。
- `/etc/vsftpd/user_list` 列出被拒绝访问的用户名称（甚至不会提示输入密码）。但是，如果在 `/etc/vsftpd/vsftpd.conf` 中将 `userlist_deny` 选项设置为 `NO`，则这些用户被允许访问 FTP 服务器。

通常情况下，您可以保留这些配置文件的大多数默认设置。然而，万一您需要更改某些内容以使 vsftpd 适合您的需求，我将在接下来的几节中简要解释这些配置文件。

#### /etc/vsftpd/vsftpd.conf 文件

要了解 `/etc/vsftpd/vsftpd.conf` 文件中可以包含哪些内容，以及这些行如何影响 vsftpd 服务器的操作，首先查看 Fedora Core 中默认安装的 `/etc/vsftpd/vsftpd.conf` 文件。该文件中的注释会告诉您每个选项的作用。

默认情况下，vsftpd 几乎不允许任何操作。通过编辑 `/etc/vsftpd/vsftpd.conf` 中的选项，您可以放宽限制，使用户能够使用 FTP。您可以决定设置的宽松程度。

以下是您可以在 `/etc/vsftpd/vsftpd.conf` 中设置的一些选项：

- `anon_mkdir_write_enable=YES` 允许匿名 FTP 用户创建新目录。此选项存在风险，即使您允许匿名用户上传文件，也建议将其设置为 `NO`。
- `anon_upload_enable=YES` 表示匿名 FTP 用户可以上传文件。此选项仅在 `write_enable` 已设置为 `YES` 且目录具有对所有用户的写入权限时才生效。**请记住**：允许匿名用户在您的系统上写入可能非常危险，因为有人可能会填满磁盘或将您的磁盘用作个人存储。
- `anonymous_enable=YES` 启用匿名 FTP（用户可以使用用户名 `anonymous` 登录，并提供其电子邮件地址作为密码）。如果您不想要匿名 FTP，请注释掉此行。

