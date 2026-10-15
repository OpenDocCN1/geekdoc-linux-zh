
> **提示 (TIP)** 确保以用户身份运行！如果你从源码编译 Apache，示例配置文件（`httpd.conf`）期望 Web 服务器以用户守护进程身份运行。虽然这在几乎所有 Linux 发行版中都存在，但如果在此过程中出现某些问题，你可能需要检查用户数据库（`/etc/passwd`）以确保用户守护进程确实存在。

## 启动和关闭 Apache

在大多数 Linux 发行版上启动和关闭 Apache 很容易。

若要在任何将 Apache 称为 `httpd` 且使用 `service` 工具的发行版上启动 Apache，请使用此命令：

在运行 `systemd` 的发行版上，你可以使用 `systemctl` 命令来启动 Apache：

若要在任何将 Apache 称为 `httpd` 且使用 `service` 工具的发行版上启动 Apache，请使用此命令：

要关闭 Apache，请使用此命令：

## 第 18 章 Apache 服务器 485

> **提示 (TIP)** 确保以用户身份运行！如果你从源码编译 Apache，示例配置文件（`httpd.conf`）期望 Web 服务器以用户守护进程身份运行。虽然这在几乎所有 Linux 发行版中都存在，但如果在此过程中出现某些问题，你可能需要检查用户数据库（`/etc/passwd`）以确保用户守护进程确实存在。

## 启动和关闭 Apache

在大多数 Linux 发行版上启动和关闭 Apache 很容易。

若要在任何将 Apache 称为 `httpd` 且使用 `service` 工具的发行版上启动 Apache，请使用此命令：

在运行 `systemd` 的发行版上，你可以使用 `systemctl` 命令来启动 Apache：

若要在任何将 Apache 称为 `httpd` 且使用 `service` 工具的发行版上启动 Apache，请使用此命令：

要关闭 Apache，请使用此命令：

## 第 18 章 Apache Web 服务器

489

要访问 Web 服务器，只需在 Web浏览器的地址栏中输入 `http://localhost`（或其 IPv6 等效地址 `http://[::1/`）。如果你看到一个显示类似于“Apache HTTP 服务器在您的站点上运行正常”的页面，说明安装成功了。如果没有看到，请回溯你的 Apache 安装步骤，确保在此过程中没有遇到错误。另一个需要检查的项目是，如果你看到了默认网页，请确保没有类似基于主机的防火墙（如 Netfilter；iptables 或 nftables；见第 13 章）阻止对 Web 服务器的访问。

## 配置 Apache

Apache 支持丰富的配置选项，这些选项非常合理且易于遵循。这使得在各种配置下设置 Web 服务器成为一项简单任务。

本节将介绍一种基础配置。默认配置非常好且开箱即用，因此如果你对默认设置可以接受，只需开始创建你的 HTML 文档即可！Apache 允许几种常见的自定义。在我们完成创建一个简单网页之后，你将看到如何在 Apache 配置文件中进行这些常见的自定义。

## 创建简单的根级页面

如果你愿意，可以立即在 `/var/www/html/` 目录中为 Apache 添加文件以创建顶级页面（对于源码安装，该目录将是 `/usr/local/httpd`）。只需记住确保放置在该目录中的任何文件或目录都是 world可读的。

如前所述，Apache 的默认网页是 `index.html`。让我们创建并更改默认主页，使其内容为“Welcome to webserver.example.org.”。以下是命令：

```
[rootserver ~]# cd /var/www/html/
[rootserver ~]# echo "Welcome to webserver.example.org" >> index.html
[rootserver ~]# chmod 644 index.html
```

你也可以使用 `vi`、`pico` 或 `emacs` 等编辑器来编辑 `index.html` 文件，使其更有趣。

## Apache 配置文件

Apache 的配置文件位于 Fedora 或 Red Hat Linux (RHEL) 系统的 `/etc/httpd/conf/` 目录中，对于我们的示例安装，路径将为 `/usr/local/httpd/conf/`。在 Fedora 等 Red-Hat 发行版中，主配置文件通常命名为 `httpd.conf`。

在 Debian 类系统上，Apache 的主配置文件名为 `/etc/apache2/apache2.conf`。

熟悉并进一步了解配置文件的一种好方法是阅读 `httpd.conf` 文件。默认配置包含大量的注释，解释了每个条目、其作用以及你可以看到的参数。

## 常用配置选项

默认配置设置开箱即用且运行良好，对于基本需求，它们可能不需要进一步修改。尽管如此，站点管理员可能需要进一步自定义他们的 Web 服务器和/或网站。

本节讨论了 Apache 配置文件中一些常用指令或选项。

### ServerRoot

此项用于指定 Web 服务器的基础配置目录。在 Fedora、RHEL 和 CentOS 发行版中，该值默认认为 `/etc/httpd` 目录。在 Ubuntu、openSUSE 和 Debian Linux 发行版中，其默认值为 `/etc/apache2/`

```
Syntax: ServerRoot directory-path
```

### Listen

这是 Web 服务器监听连接请求的端口。它指的是著名的 80 端口（HTTP），因为互联网上所有好或坏的事都是众所知的！

`Listen` 还可以用于指定 Web 服务器接受连接的特定 IP 地址。对于非安全 Web 通信，其默认值为 80。

```
Syntax: Listen [IP-address:] portnumber
```

例如，要设置 Apache 在端口 80 上监听其 IPv4 和 IPv6 接口，你会将 `Listen` 指令设置为：

```
Listen 80
```

要设置 Apache 在端口 8080 上监听特定的 IPv6 接口（如 2002:c0a8:1::），你会将 `Listen` 指令设置为：

```
Listen [2002:c0a8:1::]:8080
```

在像 Ubuntu 这样的 Debian 类系统中，此此默认值位于 `/etc/apache2/ports.conf` 文件之外。该值通常设置在

### ServerName

此指令定义了服务器用于识别自身的主机名和端口。在许多站点中，单个（通常未充分利用的）服务器可能满足多个用途并托管多个服务。例如，在某种情况下，一个没有频繁使用的内网 Web 服务器，将计算机名设为“www”（完全限定域名，或 FQDN=www.example.org）并不是一个好的选择，因为这暗示该机器只有一个用途。

第 18 章 Apache 服务器 491

最好给服务器起一个中性名称，然后在 `/etc/hosts` 文件中建立域名系统 (DNS) 规范名称 (CNAME) 条目或多个主机名条目。换句话说，从用户的角度，你可以为访问服务器或服务定义多个名称。

假设你的真实主机名是 `dioxin.example.org`。这台服务器也兼任 Web 服务器。然而，你可能想给它起一个主机名别名 `www.sales.example.org`，但是由于 `dioxin` 只知道自己是 `dioxin`，访问 `www.sales.example.org` 的用户可能会在浏览器中看到服务器是 `dioxin` 而感到困惑。

### ServerAdmin

这是服务器在发送给客户端的错误消息中包含的电子邮件地址。出于几个原因，这是一个好主意，可能有多个管理员。通过别名，可以扩展到其他电子邮件地址。

Syntax: ServerAdmin email_address

### DocumentRoot

此项定义了提供 HTML 文件的主要目录。在 Fedora 发行版和其他红帽类系统中，其默认值为 `/var/www/html/`。在 openUSE 和 SLE 中，其默认值为 `/srv/www/htdocs`。

```
Syntax: DocumentRoot directory-path
```

提示：对于预计托管大量 Web内容的服务器，`DocumentRoot` 中指定的目录系统应该有足够的空间。

### MaxRequestWorkers

此项设置了 Web 服务器服务的并发请求数量限制。

```
Syntax: MaxRequestWorkers number
```

492## Linux 管理：学者指南

### LoadModule

此项用于将模块加载到 Apache 配置中。
它将指定的模块添加到活动模块列表中。

```
Syntax: LoadModule module filename
```
