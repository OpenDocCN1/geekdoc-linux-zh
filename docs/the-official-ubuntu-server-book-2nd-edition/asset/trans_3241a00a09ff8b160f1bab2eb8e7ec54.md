
在 Ubuntu 中，我将一步一步地引导您完成一个常见的 LAMP 部署——安装 WordPress。WordPress 是广受欢迎的博客软件，由 Ubuntu 打包，为单个或多个博客提供了一个良好的、功能丰富的平台。

## 安装 WordPress

在本示例中，我在同一台主机上同时运行 Web 服务器和 MySQL 数据库，该主机名为 blog.example.net，因此在安装过程中我选择了 LAMP Server 任务。我还已经确保在 DNS 服务器中将 blog.example.net 设置为指向此特定 Web 服务器。接下来，我使用包管理器安装 WordPress 软件包，它会连同所需的额外库一起下载 WordPress 软件：

```
$ sudo apt-get install wordpress
```

## 配置 Apache

有几种不同的方式可以配置 Apache 以用于 WordPress，位于 /usr/share/doc/wordpress/example/apache.conf 的随附 Apache 示例文件提供了您所需的主要选项。文件中的第一个示例提供了最佳的全面方案，因为它使得在同一站点上托管多个 WordPress 博客变得容易。请将以下配置保存到 /etc/apache2/sites-available/wordpress：

```
NameVirtualHost *:80

<VirtualHost *:80>
UseCanonicalName Off
VirtualDocumentRoot /var/www/%0
Options All
</VirtualHost>
```

配置文件就绪后，我使用 a2ensite 启用站点，并使用 a2dissite 禁用可能存在的任何默认站点：

```
$ sudo a2ensite wordpress
$ sudo a2dissite default
```

由于配置使用了 VirtualDocumentRoot 选项，我需要确保 vhost_alias 模块已启用，因此我使用 a2enmod 命令：

```
$ sudo a2enmod vhost_alias
```

> 注意：我怎么知道 VirtualDocumentRoot 需要 vhost_alias 模块？首先，如果没有该模块而尝试重新加载 Apache，Apache 会报错提示未知配置选项。此时，在 Web 上快速搜索 VirtualDocumentRoot，就能找到提供该功能的 vhost_alias 模块。

现在，我需要为我的网站在 /var/www 下创建一个符号链接，并将其指向包含所有 PHP 文件的 WordPress 根目录。如果我想托管多个 WordPress 站点，可以在这里创建多个符号链接。

```
$ sudo ln -s /usr/share/wordpress /var/www/blog.example.net
```

现在我可以重新加载 Apache：

```
$ sudo apache2ctl graceful
```

## 配置 MySQL

WordPress 在 /usr/share/doc/wordpress/examples/setup-mysql 下提供了一个简单脚本，该脚本将为指定的 MySQL 用户和网站域名设置 WordPress 的 MySQL 配置：

```
$ sudo bash /usr/share/doc/wordpress/examples/setup-mysql \
-n wordpress blog.example.net
```

就这样，博客已经可以使用了。此时我只需要在 Web 浏览器中打开 http://blog.example.net，就会看到如图 5-2 所示的 WordPress 安装网页。最后一步是在提供的字段中输入站点名称和电子邮件地址，然后点击标有“Install WordPress”的大按钮。随后，系统将为您的站点设置数据库，并加载一个新页面，列出您的管理员用户名和临时密码，以及登录博客的链接。至此，其余配置由您自行决定。您可以更换主题、创建“Hello World”文章、安装插件，或者更好的做法是，将密码改成您能记住的。

![](img/304f637afcecc491b152ee8ac5afadee_200_0.png)

## 图 5-2 WordPress Web 安装页面

## 邮件服务器

与 Web 一样，电子邮件可能是人们想到互联网时最常想到的服务。与 Web 服务器一样，邮件服务器传统上相当难以配置，且有很多关于该主题的指南和书籍。不过，您会发现，在 Ubuntu 下配置和使用邮件服务器相当容易。有很多不同的邮件服务器可供选择，但在本节中，我将讨论 Postfix。原因之一是，当您在 tasksel 中选择“邮件服务器”时，它是 Ubuntu 使用的默认邮件服务器。其次，它是一个优秀、安全、易于管理的邮件服务器。

## 安装 Postfix

Postfix 可以使用我在本章中提到的许多其他服务所用的相同方法来安装。您可以在初始安装时或运行 tasksel 程序时选择“邮件服务器”，或者也可以输入

```
$ sudo apt-get install postfix
```
