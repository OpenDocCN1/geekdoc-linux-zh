
通过取消这些行的注释，你可以将这些攻击重定向到 `phf.apache.org` 上的日志脚本。或者你也可以使用 `support/phf_abuse_log.cgi` 脚本来自己记录这些攻击。

```apache
<Location /cgi-bin/phf>
deny from all
ErrorDocument 403 http://phf.apache.org/phf_abuse_log.cgi
</Location>
```

Debian 策略假设 `/usr/doc/*` 至少来自本地主机（`localhost`）。

```apache
<Directory /usr/doc>
Options Indexes FollowSymLinks
AllowOverride None
order allow,deny
allow from all
</Directory>
```

这设置了 `mod_throttle` 状态显示可的位置。

```apache
# <Location /throttle-info>
# SetHandler throttle-info
# </Location>
```

不允许用户通过符号链接浏览其私有网页 `public_html` 中的外部文件。注意：如果你修改了 `UserDir`-Option，则应修改此项。我们非常想使用 `LocationMatch`，但我们想要的 `Option` 在该指令下会被忽略。

```apache
<DirectoryMatch /home/*/*/public_html>
Options SymLinksIfOwner Indexes
AllowOverride None
</DirectoryMatch>
```

你可以在此之后放置任何其他希望获取访问信息的目录或位置。

## 控制守护进程

在对任何配置文件进行任何更改后，你必须重启服务器。与所有 Linux 守护进程一样，你可以在不重启电脑的情况下重启服务器进程。此外，为了方便起见，Debian 发行版带了一个专门为此功能的脚本——`apachectl`。只需执行停止和启动服务器的命令即可运行此脚本：

```bash
apachectl stop
```

和

```bash
apachectl start
```

服务器每次启动时，都会读取配置文件以实施。Apache 守护进程的另一种方法是通过启动脚本 `/init.d/apache`。该命令的选项——如 `start`、`stop`、`reload` 和 `restart`——为你提供了控制守护进程的选择。

```bash
/init.d/apache restart
```

在你对其中一个配置文件进行更改后，这将重启 Apache 守护进程。如果你不重启 Apache，这些更改就不会生效。

## 监控 Web 服务器

与运行在任何计算机上的其他服务一样，必须进行某些监控，以便在某些运行不正常时获得警告信号。这是通过日志文件实现的。所有的日志文件都位于 `/var/log/apache` 目录。日志提供了攻击迹象，帮助诊断不当的配置设置，并提供有关网站流量的宝贵信息。

使用 `tail` 命令可以快速查看文件。该命令显示文件的末尾，其中包含了最后几行活动记录。在追踪问题或寻找最近的嫌疑活动时，最后几行非常重要。某些日志文件可能巨大，需要一些时间才能打印到屏幕。`tail` 只显示文件的末尾。以下是你如何使用 `tail` 查看 `access.log` 的最后几行的：

```bash
$ /var/log/apache/access.log
```

已经开发了一些工具来创建站点统计数据。其中一个应用 `Webalizer` 可以在从日志文件编译的网站上以图形化方式列出服务器活动（如图 21-2 所示）。你可以安装 `webalizer` 的 Debian 软件包。它匹配 Debian Apache 的安装位置。如果你需要对 Apache 进行更改，请双击 `/etc/webalizer.conf` 以确保默认路径匹配。

![](img/0d314422de05113fe6acc6b5e7b494ff_490_0.png)

**图 21-2：** `Webalizer` 根据日志文件数据创建图形化图表，此图显示了一个月的使用情况。

如果你管理多个域名或有多个配置文件，你可以设置 `Webalizer` 从多个配置文件中工作。使用 `-c` `conf.file`，`name` 允许你为每个日志文件使用自定义的配置文件。事实上，你可以使用选项来临时覆盖配置文件中的设置。

## 网页的安全控制

有时，更改特定目录的 Web 服务器功能是重要的。你可能希望在访问目录、页面或站点时需要密码。取决于你如何设置，访问整个站点可能都需要密码。限制整个域名的访问可能有点极端；限制一个目录要实用得多。

要实现这一点，你必须在 `srm.conf` 文件中通过指定文件名（默认为 `.htaccess`）启用 `AccessFileName` 指令。然后在 `access.conf` 文件中，为特定目录添加 `AllowOverride` 指令以提供限制（或取消限制）。这一切都是为了向建议的目录中添加 `.htaccess` 文件做准备。

虽然允许授权所需的模块默认已加载，但双重检查一下也无害。该模块 `auth_module` 在 `httpd.conf` 文件中加载。

记住，每当你对任何配置文件进行任何更改时，都需要重启 Apache。

## .htaccess

你可以通过使用 `.htaccess` 文件中的几乎任何指令来自定义目录。只需在你希望添加指令的目录创建一个名为 `.htaccess` 的文件。然后添加全局文件中未涵盖的指令。这为每个目录设置了单独的 Apache 配置。你可以使用 `apachectl` 命令随时重启服务器。

你可以使用此文件调整目录的 `Options`。以下是为站点设置的示例，在 `access.conf` 中添加以下内容：

```apache
<Directory /home/userID/public_html>
AllowOverride Options FileInfo AuthConfig Limit
</Directory>
```

这允许开发者通过 `.htaccess` 文件覆盖选项、文档类型、授权和访问限制。

Apache 服务器的一个功能允许使用密码访问 Web 页面。这种设置意味着文档或目录必须有授权 `.htaccess` 文件。当你安装 Apache 时，`htpasswd` 文件也会一起安装。此程序允许你创建包含用户 ID 和加密密码的文件。

在首次设置密码文件时，使用创建选项。你还需要提供文件名和第一个用户名。提供文件名时，可以使用完整路径。以下是你使用的语法：

```bash
htpasswd -c /etc/filename username
```

> 我建议将密码文件存储在安全区域，例如 `/etc` 或 `apache` 目录。永远不要在公共访问目录中存储这些文件。尽管密码经过了加密，仍然仍然复制、破坏或解密。理想情况下，由系统管理员控制文件以添加、更改和删除 ID 以确保安全。

这创建一个名为 `/etc/filename` 的密码文件，并将用户名作为初始 ID。Web 浏览器会提示该用户 ID 的密码。你可以通过类似的方法继续在此文件中添加 ID，但不使用创建选项。否则，现有文件会被覆盖。要添加任何其他用户 ID，使用以下语法，其中 `username2` 是另一个 ID：

```bash
htpasswd /etc/filename username2
```

![](img/0d314422de05113fe6acc6b5e7b494ff_492_0.png)

**图 21-3：** 基础对话框，授权访问网站

## 启用虚拟主机

作为家庭或小型企业的单台服务器，你可能不需要为了单个域名更改默认的 Web 服务器。然而，当你观察整个互联网时，一台机器会为许多域名发布 Web 页面。这意味着在某处，一台机器托管的内容不仅限于一个域名。这种术语被称为虚拟主机（`virtual hosting`）或多主机托管（`multihomed hosting`）。无论哪种，你都可以配置服务器为多个域名发布 Web 页面。未与真实网络或机器关联的域名被视为虚拟域名。

有几种方法可以在 Web 服务器上启用虚拟域名。第一种是在域名服务器（DNS）中为每个虚拟域名分配一个 IP 地址，并将该地址分配给 Linux 机器。（你可以找到更多关于向机器添加 IP 地址的信息）对于互联网使用，这些域名和 IP 数字必须经过注册且真实。虚造名称或 IP 数字是无效的。另一种方法是在 DNS 中将域名分配为别名（`CNAME`）。

在 IP 地址的情况下，你需要在 `httpd.conf` 文件中添加有关虚拟服务器的信息。以下是如何在配置文件中设置指令的示例。当请求指向此虚拟域名时，这些指令将覆盖服务器的全局指令。
