
## 通过命令行进行远程访问

虽然现代图形用户界面（GUI）可用于连接远程系统，但使用命令行工具通常更简单快捷。常用的工具包括 `telnet`、`curl` 和 `wget`。`telnet` 是一种运行在 23 端口的网络协议，属于客户端-服务器协议。`telnet` 起源于 1969 年，是最早的互联网标准之一。`telnet` 的安全性较差，因为它不会加密连接上的任何数据，并以明文形式在线路上传输认证数据。基本命令为 `telnet hostname|IP address`，该命令将连接到指定主机名或 IP 地址的 `telnet` 服务器。

另外两个工具 `curl` 和 `wget` 功能相似，它们都使用 HTTP、HTTPS 和 FTP 检索文件。`curl` 支持的协议比 `wget` 更多。若要使用 `wget` 下载 URL，可以使用以下代码：

```bash
wget http://www.shell.com
```

该命令的输出如下所示：

```text
$ wget www.shell.com
--2009-06-22 16:51:43--  http://www.shell.com/
Resolving www.shell.com... 134.146.83.23
Connecting to www.shell.com|134.146.83.23|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 26594 (26K) [text/html]
Saving to: `index.html.1'

100%[===================================>] 26,594  86.4K/s in 0.3s

2009-06-22 16:51:44 (86.4 KB/s) - `index.html.1'
saved [26594/26594]
```

该工具可以使用以下格式通过 FTP 下载文件：

```bash
wget ftp://www.syngress.com/*.jpg
```

对于拥有 FTP 用户名和密码的网站，可以在命令行中指定这些凭据，例如 `--ftp-user=user`。由于该命令是非交互式的，可以将其集成到脚本中以实现流程自动化。

另一个工具 `curl` 可以使用广泛的协议（包括 `telnet`）传输数据。它被设计为无需用户交互即可工作，以便于在脚本中使用。它可以用于包含用户认证、支持代理以及恢复数据传输。其使用方法与上述 `wget` 类似。选项列表过长，此处不予列出，可以通过 `man curl` 查看。例如，假设您想要下载 www.shell.com 上的网页。

`curl http://www.shell.com`

输出的前两行如下所示（经过大量删减）：

```html
$ curl www.shell.com
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
  xml:lang="en" lang="en">
<head>
```

## Apache (HTTP) 和 Tomcat

Linux 上有许多不同的 Web (HTTP) 服务器可用，但其中最常见的是由 Apache 软件基金会开发和维护的 Apache Web 服务器，其主页位于 www.apache.org/。Apache Web 服务器可能是当今互联网上最受欢迎的 Web 服务器。虽然我们只关注 HTTP 服务器，但该基金会还有许多其他一直在推进的项目，这些项目都在其主页上有描述。

Apache HTTP 服务器是一款开源服务器，已为包括 Linux、UNIX 和 Microsoft Windows 在内的多种操作系统开发。虽然服务器代码通常包含在 Linux 发行版中，但通常会在一定程度上过时。如果服务器将用于向互联网提供页面，则应从 http://apache.org 网站下载最新版本，该版本将包含所有最新的安全修复。Apache 的默认安装路径为 /usr/local/apache2，但用户可以在安装时进行配置。安装将占用约 50 MB 的磁盘空间，其中包括一些选项。任何用户页面都会增加所需的磁盘空间。其他软件包的安装方法类似：下载、解压、配置 makefile、编译、安装以及进行额外的配置更改。以下章节将介绍如何配置服务器以满足您的特定需求。

### Apache 配置

安装前缀是配置任务的一部分，使用 `--prefix=PREFIX` 选项更改默认值，其中 PREFIX 定义为安装目录。该目录被称为 ServerRoot。

### apachectl

在 Linux 系统上，Apache 服务器作为 httpd 守护进程运行，通常会在启动时开始。有一个名为 apachectl 的控制脚本，应使用它来调用 httpd 守护进程。该脚本确保在调用 httpd 之前设置了正确的环境变量。如有必要，该脚本会将任何命令行参数传递给 httpd，或者可以编辑该脚本（如果您愿意的话），以确保始终将特定参数传递给 httpd。控制脚本语法为 `apachectl [http-argument]`，主要参数如表 9.4 所示，即 apachectl 参数。

启动 Apache 服务器后，使用 Web 浏览器连接到服务器将显示默认启动页面，如图 9.1 所示。

**表 9.4 apachectl 参数**

| 参数 | 描述 |
| :--- | :--- |
| start | 启动 httpd 守护进程，如果已在运行则显示错误 |
| stop | 停止 httpd 守护进程 |
| restart | 重启 httpd 守护进程（如果未运行则启动它） |
| status | 显示状态报告 |

![](img/95b3ebd6248b36778ccf73988aaab2f2_280_0.png)

### httpd

启动时，httpd 读取其配置文件 httpd.conf，默认情况下该文件相对于 ServerRoot 存储在 conf/httpd.conf 中。启动后，它将创建一个进程池来处理在服务器上生成的所有请求。主要选项如表 9.5 所示，即 httpd 参数。

### Apache 模块

Apache 服务器可以通过模块进行定制，Web 上有许多可用的模块——特别是在 http://modules.apache.org/，那里有接近 500 个可供下载的模块。这些模块可以为 Apache 服务器增加各种功能，如带宽管理、CGI 或身份认证。可以使用以下命令列出当前加载的模块：

```bash
apache2 -l # 显示编译进代码的模块
apache2 -t -D DUMP_MODULES # 显示所有已加载的模块
```

可以使用 a2enmod 和 a2dismod 命令启用和禁用模块。

### Apache 容器

在 Apache 配置文件中包含一些容器，它们是包含指令的独立单元，这些指令会改变 Apache 服务器的配置。两个主要的容器是文件系统容器和 Web 空间容器。文件系统容器包含所有关于目录和文件的指令；例如，位置和访问权限。Web 空间容器包含所有关于您正在开发的网站的信息；例如，URL 名称。

作为一个例子，要为 /var/web/dir 目录启用目录索引，应包含以下内容：

```apache
<Directory /var/web/dir>
Options +Indexes
</Directory>
```

**表 9.5 httpd 参数**

| 选项 | 描述 |
| :--- | :--- |
| -d ServerRoot | 如果与默认值不同，则设置 ServerRoot 的值 |
| -k start \| stop \| restart | 启动或停止守护进程 |
| -v | 显示当前版本 |
| -X | 以调试模式运行 |

当您从同一台机器提供多个主机时，可以使用虚拟主机容器。这将允许为每个虚拟主机应用不同的配置选项。虚拟主机可以是基于 IP 的（每个网站一个 IP）或基于名称的（单个 IP 地址上有多个名称）。

### 考试警示

您应该知道 Apache Web 文件位于 httpd.conf 文件中指定的 DocumentRoot 指令所指定的目录中。

### .htaccess 文件

.htaccess 文件允许 Apache 服务器对其 Web 树进行去中心化管理。该文件在一个纯文本配置文件中包含指令。这些指令将应用于 .htaccess 文件所在的目录，并在每次访问时读取；因此任何更改都会立即生效。如果 .htaccess 文件包含选项，则必须将 Apache 配置文件配置为设置 AllowOverride Options。

## 练习 9.2：停止和启动 Apache HTTP 服务器

在本练习中，您将学习如何停止和启动 Apache HTTP 服务器守护进程。如果您更改配置细节或添加某些功能，通常需要这样做。许多这些更改往往只在 Apache 服务器启动时读取。

- 您希望妥善停止 Apache 服务器守护进程 [允许进程在有时间时完成]，因此您需要执行命令 `apachectl -k graceful-stop`。
- 当所有进程停止后，您可以使用命令 `apachectl -k restart` 重启服务器。

## PHP

PHP 是一种用于 Web 开发的通用脚本语言。当您需要创建动态 Web 页面时主要使用它，一旦创建，其外观就像任何其他 HTML 页面一样。它通常作为 LAMP 环境（Linux、Apache、MySQL 和 PHP）的一部分安装，XAMPP 就是一个很好的例子，可以在 www.apachefriends.org/en/xampp.html 下载。当 PHP 启动时，它读取其配置文件 php.ini，该文件通常位于 /usr/local/lib/php 目录下。当

