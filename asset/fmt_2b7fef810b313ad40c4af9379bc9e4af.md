
使用 `xferlog_file` 选项指定你想要使用的日志文件。默认值所示：

```
xferlog_file=/var/log/vsftpd.log
```

## vsftpd 访问控制

某些选项控制对 FTP 站的访问。如所述，`anonymous_enable` 选项允许匿名用户访问，而 `local_enable` 允许本地用户登录其账户（如果使用 `/etc/vsftpd`，会对文件使用前缀）。

## 第 4 部分：网络服务

### 拒绝访问

`deny_email_enable` 选项允许你拒绝匿名用户的访问，`banned_email` 文件选项指定持有这些用户电子邮件地址的文件（通常为 `vsftpd.banned`）。`vsftpd.ftusers` 文件列出了那些永远无法访问的用户。这些通常是如 root、mail 和 nobody 这样的系统用户。请参阅表 21-3 以获取 vsftpd 文件列表。

| 文件 | 描述 |
| --- | --- |
| vsftpd.ftusers | 始终被拒绝访问的用户 |
| vsftpd.user_list | 指定被拒绝访问的用户（如果 `userlist_deny` 为 NO 则允许访问） |
| vsftpd.chroot_list | 允许访问的本地用户（如果 `chroot_local_user` 开启则拒绝访问） |
| /etc/vsftpd/vsftpd.conf | vsftpd 配置文件 |
| /etc/pam.d/vsftpd | PAM vsftpd 脚本 |
| /etc/init.d/vsftpd | vsftpd 服务器服务脚本，独立运行 |
| /etc/xinetd.d/vsftpd | Xinetd vsftpd 服务器脚本 |

表 21-3：vsftpd 文件

### 用户访问

`userlist_enable` 选项控制用户的访问，拒绝列在由 `userlist_file` 指定文件（通常为 `vsftpd.user_list`）中的用户访问。如果，如果你想限制对某些特定选定用户的访问，可以更改 `vsftpd.user_list` 文件的含义和用法，以指示仅允许哪些用户访问，而不是哪些哪些用户被拒绝访问。要实现这一点，请将 `userlist_deny` 选项设置为 NO（默认是 YES）。只有列在 `vsftpd.user_list` 文件中的用户才会被授予 FTP 站的访问权限。

### 用户限制

`chroot_list_enable` 选项控制本地用户的访问，让他们仅访问自己的家目录，同时限制对系统的访问。`chroot_list_file` 选项指定列出允许访问的用户的文件（通常为 `vsftpd.chroot`）。你可以通过 `chroot_local_user` 选项允许所有本地用户访问。

```
chroot_local_users=YES
```

如果设置了此选项，由 `chroot_list_file` 指定的文件将有一个反向列表，列出不允许访问的用户。在以下示例中，本地用户的访问限制为列在 `vsftpd.chroot` 中的用户：

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list
```

在 Fedora 上，使用 `secure_chroot_dir` 选项来指定一个非安全的根目录。

```
secure_chroot_dir=/var/run/vsftpd
```

## 第 21 章：FTP 服务器 527

### 用户身份验证

vsftpd 服务器利用 PAM 服务来验证通过 FTP 远程访问其账户的本地用户。在 `vsftpd.conf` 文件中，使用 `pam_service_name` 选项指定用于服务器的 PAM 脚本。

```
pam_service_name=vsftpd
```

在 `etc/pam.d` 目录下，你会找到一个名为 `vsftpd` 的 PAM 文件，其中包含控制 vsftpd 服务器访问的条目。PAM 目前配置为验证有效账户的用户，并拒绝对 `/etc/vsftpd.ftupers` 中用户的访问。默认的 `etc/pam.d/vsftpd` 文件所示：

```
## PAM-1.0
session optional pam_keyinit.so force revoke
auth required pam_listfile.so item=user den=deny	file=/etc/vsftpd.ftupers onerr=succeed
auth required pam_shells.so
auth include system-auth
account include system-auth
account include system-auth
session required pam_login.so
```

### 命令访问

命令在 vsftpd 中受到严格限制。仅支持星号匹配操作。要启用子目录的递归列表，你需要通过将 `recurse_enable` 选项设置为 YES 来启用 `-R` 选项。某些客户端（如 ncpft）会假设递归选项已启用。

### vsftpd 虚拟主机

## 22. Web 服务器

- Apache Web 服务器
- Linux Apache 安装
- Apache 配置
- 使用 system-config-httpd 配置 Apache
- Apache 配置指令
- 日志文件
- Apache 上的虚拟主机
- 服务器包含 (SSI)
- PHP
- Apache 配置工具 - system-config-httpd
- Web 服务器安全：SSL

Fedora 的主要 Web 服务器是 Apache，它几乎成为所有 Linux 发行版的标准 Web 服务器。这是一个非常强大、稳定且相当容易配置的系统。Fedora 为 Apache 提供了默认配置，使其安装后即可使用。此外还有 lightttppd，这是一个轻量级、快速且系统要求的要求的 Web 服务器；以及 cherokee 和 thttpd，它们都是极小且极快的 Web 服务器。表 22-1 列出了各种 Web 服务器网站站点。

此外，Fedora 仓库中还包含了用于 Web 开发的 Zope 应用服务器。Zope 应用服务器 (www.zope.org) 是一个集成了安全性、Web 端管理和数据库接口功能的开放 Web 服务器。它由 Zope 公司开发，该公司还开发了 Python 编程语言。

| 网站 | 描述 |
| --- | --- |
| www.apache.org | Apache 软件基金 |
| http://httpd.apache.org | Apache HTTP Server 项目 |
| http://jakarta.apache.org | Jakarta Apache 项目 |
| www.lighthttppd.net | Lighthttppd Web 服务器 |
| www.cherokee-project.com | cherokee Web 服务器 |
| www.lighthttppd.net | lighthttppd 服务器 |
| www.acme.com/software/thttpd/ | thttpd 微型 HTTP 服务器 |
| www.php.net | PHP 超文本预处理器，嵌入式 Web页面编程语言 |
| www.zope.org | Zope 应用服务器 |

表 22-1：Web 服务器网站

### Lighthttpd Web 服务器

Lighthttpd Web 服务器是一个非常快速且轻量级的 Web 服务器。Lighthttpd 网站地址为 http://www.lighthttpd.net。在该网站上，你可以访问包含教程和详细说明的文档。

httpd 使用 Web 服务器目录下的 lighthttpd 目录，即 `/var/www/lighthttpd`。其配置文件位于 `/etc/lighthttpd`。服务器变量未在 `/etc/sysconfig/lighthttpd` 文件中设置。你可以使用 `/etc/init.d/lighthttpd` 服务脚本来启动和停止服务器，该脚本也可以通过 system-config-services 作为 lighthttpd 进行管理（系统 | 管理 | 服务）。

```
service lighthttpd start
```

就像 Apache 一样，你可以使用端口 80 的 localhost URL 访问 Web 服务器。

http://localhost:80
