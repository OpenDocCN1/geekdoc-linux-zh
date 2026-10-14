
## 使用 IP 的虚拟主机

一旦在系统或主机上设置了 IP 别名，或者主机配置了多个网卡，就可以配置 Apache。为每个虚拟服务器指定单独的 VirtualHost 块：

```apache
<VirtualHost 192.168.1.20
ServerName www.example.com
DocumentRoot /srv/www/htdocs/example.com
ServerAdmin webmaster@example.com
ErrorLog /var/log/apache2/error.log
CustomLog /var/log/apache2/access.log
</VirtualHost>
```

```apache
<VirtualHost 192.168.1.21
ServerName www.other.com
DocumentRoot /srv/www/htdocs/other.com
ServerAdmin webmaster@other.com
ErrorLog /var/log/apache2/error.log
CustomLog /var/log/apache2/access.log
</VirtualHost>
```

VirtualHost 指令仅为原始域名（www.example.com）指定。在此示例中，原始域名和一个额外域名（www.other.com）被托管在同一台服务器上。

### 14.10.3 多个 Apache 实例

通过上述方法，一个 Apache 实例托管多个域名。在配置文件中，使用 Listen 指令来指定每个实例处理的 IP。对于上述示例，第一个实例的指令为：

```apache
Listen 192.168.1:80
```

对于其他实例：

```apache
Listen 192.168.1.20:80
Listen 192.168.1.21:80
```

### 14.11 安全

### 14.11.1 风险最小化

如果机器不需要 Web 服务器，请在运行级别中禁用它、卸载它，或者从根本上安装。这特别适用于作为防火墙的主机。

### 14.11.2 权限

默认情况下，DocumentRoot 目录（`/srv/www/htdocs`）和 CGI 目录属于 root 用户。你不应该更改此设置。如果目录对所有人可写，任何用户都可以其中放置文件。这些文件可能会以 wwwrun 的权限被执行。此外，Apache 对其交付的数据不应有写权限，因此这些不应属于 wwwrun。

为了允许用户在 Apache 目录中放置文件，不要让其对所有人可写。相反，创建一个对所有人可写的子目录（例如 `/srv/www/htdocs/miscellaneous`）。

## 从主目录发布文件

另一种确保用户可以在网络上发布文件的方法是在配置文件中为用户的主目录指定一个子目录。用户可以在该目录下放置任何网络演示文件（例如 `/public/html`）。这在 SUSE LINUX 中默认激活。详见第 351 页的第 14.7.2 节。

可以通过指定用户名来访问这些页面。URL 包含 `~username` 作为用户主目录下相应目录的快捷方式。例如，在浏览器中输入 http://localhost/~ux 来列出用户 tux 家目录下 public_html 中的文件。

### 14.11.3 保持更新

如果你运行 Web 服务器，特别是当该服务器公开访问时，请关注漏洞和潜在的安全风险。漏洞和修复的来源列在第 363 页的第 14.13.3 节中。

### 14.12 故障排除

如果出现问题，例如 Apache 不显示页面或显示不正确，可以通过以下步骤帮助找到问题。

- 首先，查看错误日志并检查消息中是否包含该错误信息。通用的错误日志位于 `/var/log/http/error_log` 或 `/var/log/apache2/error_log`。
- 一个经过验证的方法是在控制台中跟踪日志文件，以查看服务器对访问的响应。可以在 root 控制台中中输入 `tail -f /var/log/apache2/*_log` 来实现。
- 检查 http://bugs.apache.org/ 上的在线数据库。
- 阅读邮件列表和新闻组。用户邮件列表地址为 http://apache.org/userslist.html。推荐的新闻组有 comp.infosystems.www.servers.unix 和相关组。
- 如果这些都不都不提供解决方案，且你确定检测到了 Apache 的漏洞（bug），请在 http://www.suse.de/feedback/ 报告它。

### 14.13 更多信息

### 14.13.1 Apache

Apache 附带了详细的文档。该文档的安装说明见第 344 页第 14.6 节。安装完成后，通过 http://localhost/manual 访问文档。最新文档可以在 Apache 主页 http://apache.org 获取。

### 14.13.2 CGI

关于 CGI 的更多信息请见以下页面：

- http://apache.perl.org/
- http://perl.apache.org/
- http://www.modperl.com/
- http://www.modperlcookbook.org/
- http://www.fastcgi.com/
- http://www.boutell.com/cgic/

![](img/cd2fd97de988ee4c3e49ca563eaa9a48_382_0.png)

### 14.13.3 安全

SUSE 软件包的最新补丁发布在 http://www.suse.com/us/security/。请定期访问此 URL。在这里，你也可以订阅 SUSE 安全公告邮件列表以接收安全更新。

Apache 团队针对 Apache 中的漏洞推行开放信息政策。最新的漏洞报告和可能的漏洞点发布在 http://httpd.apache.org/security_report.html。

如果你检测到安全漏洞（请检查上述页面以确保该漏洞尚未被发现），请向 security@suse.de 或 security@apache.org 报告。

关于 Apache（以及其他互联网程序）安全问题的其他信息来源：

- http://www.cert.org/
- http://www.vnunet.com/
- http://www.securityfocus.com/

### 14.13.4 更多来源

如果你遇到困难，请查看 SUSE 支持数据库 http://sdb.suse.de/en/。一份关注 Apache 的在线报纸可以在 http://www.apacheweek.com 获取。

Apache 的历史信息可以在 http://httpd.apache.org/ABOUT_APACHE.html 查看。该页面还解释了为什么该服务器实际上被称为 Apache。

## 文件同步

今天，许多人使用多台电脑——家里一台，工作场所几台，在途中可能还带一台笔记本电脑或 PDA。所有这些电脑上都需要许多文件。你可能希望在所有电脑上工作并修改文件，随后随后在所有电脑上都获得最新版本的数据。

- 15.1 数据同步软件 . . . . . . . . . . . . . . . . 366
- 15.2 选择程序的决定因素 . . . . . . . . . . 368
- 15.3 InterMezzo 简介 . . . . . . . . . . . . . . . 372
- 15.4 Unison 简介 . . . . . . . . . . . . . . . . . . 375
- 15.5 CVS 简介 . . . . . . . . . . . . . . . . . . 376
- 15.6 mailsync 简介 . . . . . . . . . . . . . . . . . . 379

## 15.1 数据同步软件

对于通过快速网络永久连接的电脑来说，数据同步没有问题。在这种情况下，使用如 NFS 等网络文件系统并将文件存储在服务器上，允许所有主机通过网络访问相同的数据。如果网络连接较差或不是永久性的，这种方法是不可能的。当你带着笔记本电脑外出时，你需要在本地硬盘上保留所有需要文件的副本。然而，同步修改过的文件是必要的。当你在一台电脑上修改文件时，请确保所有其他电脑上的文件副本都已更新。对于偶尔的情况，可以使用 `scp` 或 `rsync` 手动完成。然而，如果涉及许多文件，该过程可能会变得复杂，并且非常小心以避免错误，例如用旧文件覆盖新文件。

## 注意

### 数据丢失风险

在开始使用同步系统管理数据之前，你应该充分熟悉所使用的程序并测试其功能。对于重要文件，备份是必不可少的。

## 注意

通过使用各种方法自动执行此工作的程序之一，可以避免手动同步数据这一耗时且容易出错的任务。以下摘要旨在传达对这些程序如何工作以及如何使用的通用理解。如果你计划使用它们，请阅读。

### 15.1.1 InterMezzo
