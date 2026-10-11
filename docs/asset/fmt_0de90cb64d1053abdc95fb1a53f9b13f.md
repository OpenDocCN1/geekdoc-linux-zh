
- `ServerName`，用于向外部世界标识服务器（此名称是 DNS 支持的注册域名）
- `ServerAdmin`，该虚拟主机管理员的电子邮箱地址
- `Redirect`，指定任何要重定向到其他 URL 的 URL
- `ErrorLog`，指定用于记录与该虚拟主机相关错误的文件
- `CustomLog`，指定记录该虚拟主机访问情况的文件

当服务器接收到对特定虚拟主机 `DocumentRoot` 目录下的文档请求时，它将使用该服务器 `<VirtualHost>` 块的配置参数来处理该请求。

这是一个设置虚拟主机 `www.lnsoft.com` 的典型 `<VirtualHost>` 指令示例。

```
<VirtualHost www.lnsoft.com>
  DocumentRoot /home/naba/httpd/htdocs
  ServerName www.lnsoft.com
  ServerAdmin webmaster@lnsoft.com
  ScriptAlias /cgi-bin/ /home/naba/httpd/cgi-bin/
  ErrorLog /home/naba/httpd/logs/error_log
  CustomLog /home/naba/httpd/logs/access_log common
</VirtualHost>
```

这里 `CustomLog` 指令中的名称 `common` 指的是早在 `httpd.conf` 文件中通过 `LogFormat` 指令定义的格式名称，如下：

`LogFormat "%h %l %u %t %r" %s %b"`

该日志字符串产生的日志文件行看起来如下：

```
dial236.dc.psn.net - [13/Jul/2004:18:09:00 -0500] "GET /
HTTP/1.0" 200 1243
```

该格式字符串包含两个以百分号（`%`）开头的字母标记。这些标记的含义见表 2-1。

| 表 2-1 LogFormat 标记 |
| :--- | :--- |
| 标记 | 含义 |
| `%b` | 发送到客户端的字节数，排除标头信息 |
| `%h` | 客户端机器的主名 |
| `%l` | 用户的身份标识（如果可用） |
| `%r` | 来自客户端的 HTTP 请求（例如，GET /HTTP/1.0） |
| `%s` | Web 服务器的响应状态码 |
| `%t` | 当前日期和时间 |
| `%u` | 用户提供的用户名（仅当访问控制规则要求用户名/密码认证时） |

## 第 3 章：设置 FTP 服务器

### 本章内容

- 安装 FTP 服务器
- 配置 FTP 服务器

文件传输协议（FTP）是一种用于从一个系统传输文件到另一个系统的流行互联网服务。匿名 FTP 是另一种用于分发文件的流行互联网服务。匿名 FTP 的奇之处在于远程系统支持匿名 FTP，任何人都可以匿名用户 ID 使用 FTP 并从该系统下载文件。虽然匿名 FTP 对于分发数据很有用，但如果设置不当，会带来安全风险。

Linux 发行版通常带有几个 FTP 客户端和由 Chris Evans 编写的`safety FTP`守护进程（`vsftpd`）。FTP 服务器包含了支持匿名 FTP 所需的文件。在本章中，我将向如何通过文本配置文件配置 `vsftpd` FTP 服务器，以及如何控制对 FTP 服务器的访问。

## 安装 FTP 服务器

根据你在 Linux 安装期间做出的选择，FTP `vsftpd` 及其配置文件可能已在你的系统中。如果没有安装 `vsftpd`，你可以轻松安装它。

在 Debian 和 Xandros 中，使用 `dpkg -l` 查看是否安装了 FTP 服务器。在 Fedora Core 和 SUSE 中，使用 `rpm -qa | grep vsftpd` 查看软件包是否已安装。在 Debian 中，使用 `apt-get install vsftpd`。在 Fedora Core 中，使用 `rpm -ivh vsftpd`。在 SUSE 中，使用 YaST 控制中心查找并安装。在 Xandros 中，使用 `apt-get install vsftpd`。

## 配置 FTP 服务器

### 配置 FTP 服务器

安全性 FTP 守护进程（`vsftpd`）使用 `/etc` 目录下的若干配置文件（在 Fedora Core 中位于 `/etc/vsftpd` 目录）。默认情况下，`vsftpd` 是禁用的——如果你想使用 FTP 服务器，首先必须启用它。在本节中，我将展示如何操作。

`vsftpd` 服务器可以配置为独立模式运行或由 `xinetd` 控制。在 Debian 和 Fedora Core 中，`vsftpd` 由 `xinetd` 控制。在 Debian 和 Fedora Core 中，你可以通过输入 `/etc/init.d/vsftpd start` 来启动 `vsftpd`。在 SUSE 中，编辑文件 `/etc/xinetd.d/vsftpd` —— 确保没有 `disable = yes` —— 然后重启。

要在系统启动时启动 `vsftpd`，在 Debian 中输入 `update-rc defaults`。通过输入 `chkconfig --level 3 vsftpd` 设置自动启动。

启动 `vsftpd` 服务器后，默认设置足以让服务器可用。因此，其他 FTP 客户端现在可以连接到你的 FTP 服务器并请求文件。然而，你需要了解配置文件，以防需要对其进行自定义。

### vsftpd 配置文件

`vsftpd` 服务器读取 `vsftpd.conf` 文件（在 Debian、SUSE 和 Xandros 中位于 `/etc`，在 Fedora Core 中位于 `/etc/vsftpd` 目录——记住在 Xandros 中你必须先安装 `vsftpd`）。配置文件可能会引用 `/etc` 目录下的其他文件。`vsftpd.conf` 控制 FTP 服务器的许多方面，例如，它允许匿名登录、允许文件上传等。`vsftpd` 的关键配置文件包括：

- `/etc/vsftpd.conf` 或 `/etc/vsftpd/vsftpd.conf` 控制 `vsftpd` 服务器如何工作（例如，它允许匿名登录、允许文件上传等）。
- `/etc/vsftpd.ftusers`，如果存在，列出无法访问 FTP 服务器的用户名。
- `/etc/vsftpd.user_list`，如果存在，列出哪些被拒绝访问的用户名（甚至不会提示密码）。然而，如果在 `/etc/vsftpd/vsftpd.conf` 中将 `userlist_deny` 选项设置为 `NO`，则这些用户被允许访问 FTP 服务器。

## 配置 FTP 服务器 575

在 Debian、SUSE 和 Xandros 中，`vsftpd` 使用单个配置文件 — `/etc/vsftpd.conf`。在 Fedora Core 中，`vsftpd` 的默认安装程序使用 `/etc/vsftpd/vsftpd.conf` 文件，以及 `/etc/vsftpd.fusers` 和 `/etc/vsftpd.user_list`。

通常情况下，你可以让大多数 `vsftpd` 配置文件保持默认设置。但是，以防你可能需要更改某些设置以使 `vsftpd` 符合你的需求，我将在接下来的章节中简要说明这些配置文件。

## vsftpd.conf 文件

要了解 `vsftpd.conf` 文件中包含哪些内容以及这些行如何影响 `vsftpd` 的运行，请从查看默认安装的 `vsftpd.conf` 文件开始。文件中的注释会告诉你每个选项的作用。

默认情况下，`vsftpd` 几乎不允许任何操作。通过编辑 `vsftpd.conf` 中的选项，你可以放宽用户使用 FTP 的限制。你可以决定具体的设置。

以下是你可以在 `vsftpd.conf` 中设置的一些选项：

- `anon_mkdir_write_enable=YES` 允许匿名 FTP 用户创建新目录。此选项是有风险的，因为恶意用户可能会通过创建许多目录来占用你所有的硬盘空间。因此，即使你允许匿名用户上传文件，可能也将此选项设置为 `NO`。
- `anon_upload_enable=YES` 意味着匿名 FTP 用户可以上传文件。只有当 `write_enable` 已设置为 `YES` 且目录对所有人都有写权限时，此选项才会生效。记住：允许匿名用户在你的系统上写入是非常危险的，因为用户可能会填满磁盘或将你的磁盘用于他们的个人存储。
- `anonymous_enable=YES` 启用匿名 FTP。（用户可以使用用户名 `anonymous` 登录，并提供其电子邮件地址作为密码。）如果你不需要匿名 FTP，请注释掉此行。
- `ascii_download_enable=YES` 启用 ASCII 模式下的文件下载。遗憾的是，恶意的远程用户可以可以使用文件名发布 `SIZE` 命令，从而地导致 FTP 服务器浪费大量资源来打开文件并确定其大小。这种技术被用于拒绝服务（DoS）攻击。关于拒绝服务 [DOS] 攻击的更多信息，请参阅第六本书第 1 章。
