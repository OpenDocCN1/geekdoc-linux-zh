
如果你选择标准配置，将假设许多默认值。例如，你的文档根目录假设为 `/usr/local/apache2/htdocs`，你的 `cgi-bin` 目录假设为 `/usr/local/apache2/cgi-bin`，这在大多数情况下应该是没问题的。

一旦服务器安装完成，你需要使用 `apachectl` 命令启动它。

```
/usr/local/apache2/bin/apachectl
```

你通过 `stop` 选项而不是 `start` 选项来停止——但我打赌你已经知道了。要测试你的安装，启动你喜欢的浏览器——Netscape、Lynx 或 Konqueror——并指向你的新服务器。假设你刚刚安装在一个名为 `your_server` 的服务器上，请使用此 URL：

```
http://your_server
```

## 转向 Linux 商务桌面

你应该会看到一个看起来非常像图 17-1 的页面。

![](img/c69138fb82b7e78233ca21acbdb2739f_363_0.png)

图 17-1 新安装 Apache 的界面。

此时，你实际上可以开始将网页（HTML 文档）放入服务器的文档根目录。使用我从源码构建的示例，那就是 `/usr/local/apache2/htdocs` 目录。

如果你查看正在运行的进程，服务器本身通常显示为 `httpd`。如果你的 Web 服务器是作为 Debian `apt-get` 或基础安装的一部分安装的，很有可能执行文件的名称实际上是 `apache` 而不是 `httpd`。你可以通过此命令列出 `apache` 软件包文件来验证这一点：

```
dpkg -L apache | more
```

# 简访 PHP 之乡

在我深入研究配置选项之前，我想请你考虑编译 PHP（或从你的 CD 软件包中安装它）。在写本文时，最新版本是 `php-4.3.6`，这也是我在下面的示例中使用的版本。再次强调，这是你可以使用发行版提供的包来完成的工作。尽管如此，从源码编译包确实让你在功能和安全性方面获得最新、最强大的特性。虽然这大部分是我在第 7 章“安装新应用程序”中描述的提取和构建过程的另一个示例，但有一些与你刚刚创建的 Apache 服务器相关的配置标志。

```
tar -xvf php-4.3.6.tar.gz

cd php-4.3.6

./configure --with-apxs2=/usr/local/apache/bin/apxs --with-mysql --with-pgsql

make

make install
```

两个最流行的开源数据库无疑 PostgreSQL 和 MySQL。上面的 `configure` 语句构建了支持这两种者的 PHP。一旦 `make` 完成，你可能想修改 `php.ini` 配置文件中的一两个参数。在大多数预包安装中，该文件将位于 `/etc`。假设你是从源码编译的，默认将是 `/usr/local/etc`。

现在，为了让你的 Apache 服务器支持 PHP 页面，你需要向 `httpd.conf` 中添加此指令：

```
AddType application/x-httpd-php .php .phtml
```

最后，我们希望在访问 Web 服务器上的目录时，名为 `index.php` 的页面能自动加载，就像名为 `index.html` 的页面自动加载一样。在 `httpd.conf` 中查找此行：

```
DirectoryIndex index.html index.html.var
```

如果因为你是从源码编译的导致该行不存在，请添加 `index.php` 使该行看起来像这样：

```
DirectoryIndex index.html index.html.var index.php
```

# Apache Apache 配置

大部分配置信息都在一个文件中：`httpd.conf` 文件。如果你是从零开始构建，你将在 `/usr/local/apache2/conf` 中找到配置文件。

## 转向 Linux 商务桌面

在我预装的 Debian Apache 服务器上，`httpd.conf` 文件位于 `/etc/apache` 目录，而在我的 Red Hat 系统上，它位于 `/etc/httpd.conf`。查看 `httpd.conf` 文件寻找你可能想要更改的参数是一个好主意。其中最重要的是 `ServerName`。这是你的服务器响应的域名。如果你还没有域名，Apache 默认设置为 `localhost`。

```
ServerName localhost
```

另一个重要的参数是 Apache 运行的用户名和组 ID。在 `httpd.conf` 中找到这些行：

```
User apache

Group apache
```

有时，当文档出现问题时，服务器会生成一个错误提示，联系管理员。该信息在 `ServerAdmin` 参数中维护。管理员可以是服务器的某个地址。找到并修改该行使其像这样：

```
ServerName webmaster@yourdomain.com
```

你可能想修改其中的一两个参数。在大多数预包安装中，该文件将位于 `/etc`。假设你是从源码编译的，默认将是 `/usr/local/etc`。

# 常见更改

查看 `httpd.conf` 文件寻找你可能想要更改的参数是一个好主意。其中最重要的是 `ServerName`。这是你的服务器响应的域名。如果你还没有域名，Apache 默认设置为 `localhost`。

```
ServerName localhost
```

另一个重要的参数是 Apache 运行的用户名和组 ID。在 `httpd.conf` 中找到这些行：

```
User apache

Group apache
```

有时，当文档出现问题时，服务器会生成一个错误提示，联系管理员。该信息在 `ServerAdmin` 参数中维护。管理员可以是服务器的某个地址。找到并修改该行使其像这样：

```
ServerName webmaster@yourdomain.com
```

你可能想修改其中的一两个参数。在大多数预包安装中，该文件将位于 `/etc`。假设你是从源码编译的，默认将是 `/usr/local/etc`。

# 转向 Linux

现在你已经有了一个运行 PHP 的 Apache 服务器，让我们来做一些与运行网站无关的实际操作。为你的公司提供免费的电子邮件听起来怎么样？

# SquirrelMail

有多少人拥有单独的 hotmail 或 Yahoo 电子邮件账户，以便在路上无法访问电子邮件时使用？这简直太疯狂了，如果你运行自己的服务器，完全没有理由不访问自己的电子邮件。这就是 SquirrelMail 的用武之地。

被誉为“傻瓜 Webmail”，这是一个你需要查看的软件包。SquirrelMail 使用 PHP 编写，完全支持 IMAP。它是可主题的、自定义的，包含地址录、支持 MIME 等。最棒的是它根据 GPL 免费发布。你可以在 `squirrelmail.org` 获取 SquirrelMail。

在我介绍如何安装 SquirrelMail 之前，你需要确保系统上安装并运行了 IMAP。IMAP 服务是处理 POP3 的同一个软件包的一部分。（我在第 15 章“电子邮件”中在讨论设置 Postfix 电子邮件服务器时提到过这一点）在任何现代 Linux

## 迁移到 Linux 桌面

对于使用 `xinetd` 处理网络服务的发行版，请编辑你的 `/etc/xinetd.conf/imap` 文件。它看起来应该是这样的：

```
service imap

{

    socket_type      = stream

    wait             = no

    user             = root

    server           = /usr/sbin/imapd

    log_on_success  += DURATION USERID

    log_on_failure  += USERID

    disabled         = no

}
```

确保 `disable` 被设置为 `no`。要使更改生效，请运行 `inetd`（或 `xinetd`）：

```
kill -HUP `cat /var/run/xinetd.pid`
```

记住，命令中使用的是反引号。
与 SquirrelMail 安装相关的所有操作都发生在同一个目录下。一旦你下载了源码，请切换到你 Apache 服务器的文档根目录。因为我我自己编译了 Apache 服务器，所以它位于 `/usr/local/apache2/htdocs`。在许多默认软件包安装中，文档根目录位于 `/var/www/html`。从文档根目录，解压 SquirrelMail 发行版并进行一些重命名。

```
cd /usr/local/apache2/htdocs

tar -xzf squirrelmail-1.4.2.tar.gz

mv squirrelmail-1.4.2 squirrelmail

cd squirrelmail
```
