

![](img/577d3bff979ee86b07f9836e0df274ce_423_0.png)

许多系统（包括 Ubuntu 和 openSUSE）将 Apache Web 服务器配置拆分为多个文件，以帮助使功能更加模块化。查看主配置文件 `httpd.conf` 中的 `Include` 指令行，以了解哪些其他文件包含 Apache Web 服务器配置设置。如果 `Include` 指令指向一个文件夹，Apache 服务器将读取该文件夹中所有以 `.conf` 结尾的文件，以查找指令。

## 定义 Web 文件夹位置

Apache Web 服务器的主要职责是向远程客户端提供文件。然而，你并不希望任何人都能检索你系统中的任意文件！为了限制 Apache 服务器提供的文件，你必须将其限制在系统中的特定文件夹区域。

你使用 `DocumentRoot` 指令来设置 Apache Web 服务器提供文件的文件夹：

```
DocumentRoot /var/www/html
```

在 Linux 环境中，`html` 文件夹已成为 Apache Web 服务器的常见默认值，Ubuntu 也使用此设置。对于 openSUSE，它使用 `/srv/www/htdocs`。

![](img/577d3bff979ee86b07f9836e0df274ce_423_1.png)

如果你选择将 `DocumentRoot` 文件夹移动到服务器上的另一个位置，请确保运行 Apache Web 服务器的用户账户有权读取该文件夹中的文件。

## 设置默认 TCP 端口

Apache Web 服务器使用两个不同的默认 TCP 网络端口来监听来自客户端浏览器的传入连接：

- 用于 HTTP 请求的 TCP 端口 80
- 用于 HTTPS 请求的 TCP 端口 443

HTTPS 请求使用加密来保护浏览器和服务器之间的通信。这种方法正在迅速成为互联网上所有 Web 服务器的标准。

## 使用加密

要建立安全的 HTTPS 连接，你的 Apache Web 服务器必须拥有一个有效的*由证书颁发机构签署的加密证书*。证书颁发机构确认你的网站是有效的，并保证你的真实性。这使得你的网站访问者能够相信你是你说的那个人，并且你的 Web 服务器是它声称的那个服务器。

不幸的是，签署的证书必须购买，而且可能有点昂贵。对于开发工作，你可以使用*自签名证书*。自签名证书就是字面意思——你自己签署你的证书。这不会给你的网站访问者带来任何信任，因此不要在生产网站上使用自签名证书；仅将其用于开发。你可以使用 OpenSSL 包创建自签名证书。

你使用 `Listen` 指令来设置 Apache Web 服务器接受传入请求的端口：

```
Listen 80
Listen 443
```

你可以在配置文件中使用多个 `Listen` 指令来监听多个 TCP 端口。

# 与 PHP 服务器交互

Apache Web 服务器必须知道如何将包含 PHP 代码的文件传递给 PHP 服务器进行处理。这是一个两步过程。

首先，Apache Web 服务器必须加载 PHP 服务器模块，以便它可以在 Apache 和 PHP 服务器之间建立链接。它使用 `LoadModule` 指令来做到这一点：

```
LoadModule php7_module /usr/lib/apache2/modules/libphp7.4.so
```

在 Apache 加载 PHP 模块后，它必须知道将哪种类型的文件发送到 PHP 服务器。它使用 `SetHandler` 指令来实现这一点：

```
<FilesMatch "\.(ar|pl|tml)$">
  SetHandler application/x-httpd-php
</FilesMatch>
```

该指令告诉 Apache Web 服务器将所有具有 `.phar`、`.php` 或 `.phtml` 文件扩展名的文件转发给 PHP 模块，然后该模块将文件转发给 PHP 服务器进行处理。

![](img/577d3bff979ee86b07f9836e0df274ce_425_0.png)

将所有 `.html` 文件直接转发给 PHP 服务器可能会很有吸引力，因为 PHP 服务器会直接将任何 HTML 代码传递给客户端浏览器。然而，你的静态网页加载时间会更长，从而导致 HTML 页面出现性能问题。

# 跟踪错误

在开发环境中工作时，能够跟踪应用程序中发生的任何错误总是很有帮助的。Apache Web 服务器支持九个不同级别的错误消息，如表 21-1 所示。

**表 21-1 Apache Web 服务器错误级别**

| 错误级别 | 描述 |
|---|---|
| `emerg` | 导致 Apache Web 服务器停止的致命错误 |
| `alert` | 对应用程序产生不利影响且需要立即解决的严重错误 |
| `crit` | 导致操作失败的关键状况，例如无法访问网络 |
| `error` | 会话中发生的错误，例如无效的 HTTP 标头 |
| `warn` | 会话中发生的小问题，但没有阻止其继续 |
| `notice` | 发生了异常情况 |
| `info` | 关于应更改的设置或应加载的模块的信息消息 |
| `traceN` | 跟踪级别，其中 N 为 1–8，用于跟踪服务器中的活动 |
| `debug` | 解释服务器处理请求每一步的低级别消息 |

你使用 `LogLevel` 指令定义错误跟踪级别，使用 `ErrorLog` 指令定义错误日志的位置：

```apache
LogLevel warn
ErrorLog ${APACHE_LOG_DIR}/error.log
```

在 Linux 系统中，APACHE_LOG_DIR 通常设置为 /var/log/apache2 文件夹。调试日志级别在排查问题时可能很有用，但不建议用于常规活动，因为它会产生大量输出！

# 步骤 6：检查 MySQL（或 MariaDB）服务器

MySQL 系列服务器使用 /etc/mysql 文件夹来存储配置文件。MySQL 服务器的主配置文件是 mysql.conf。

关于 MySQL 服务器更令人困惑的功能之一是，指定配置设置有三种方法：

- 可以从源代码编译时编译到可执行服务器程序中。
- 可以在服务器启动时作为命令行选项指定。
- 可以在 MySQL 配置文件中设置。

大多数 MySQL 服务器安装使用一种组合方式，将一些基本设置编译到可执行服务器程序中，并为其余设置创建一个基本配置文件。配置文件中设置的值覆盖编译到可执行服务器程序或命令行中设置的任何内容。

与 Apache Web 服务器一样，MySQL 数据库服务器有许多选项可以在配置文件中更改，以微调工作方式。话虽如此，在正常设置中，你只需要调整几个项目。以下部分将讲解你应该熟悉的一些设置。

# 核心服务器设置

核心服务器设置定义了 MySQL 服务器运行的基本方式。这些设置看起来像这样：

```ini
[mysql]
port = 3306
socket = /var/run/mysql/mysql.sock
tmpdir = /tmp
datadir = /var/lib/mysql
log_error = /var/log/mysql/error.log
```

**port** 设置定义了 MySQL 服务器监听传入请求的 TCP 端口。**socket** 设置定义了本地客户端可以使用的套接字文件的位置，以便在不使用网络的情况下与 MySQL 服务器通信。

**tmpdir** 和 **datadir** 设置定义了 MySQL 用于存储其工作文件的服务器上的位置。**datadir** 设置定义了 MySQL 存储实际数据库文件的位置。

# 处理 InnoDB 存储引擎

InnoDB 存储引擎为 MySQL 服务器提供高级数据库功能。它拥有一套自己的配置设置，精确控制它的操作方式以及它如何处理使用该存储引擎的表中的数据。

你可能需要根据你的特定 MySQL 服务器安装调整两个主要配置设置：

```
innodb_data_home_dir = /var/lib/mysql
innodb_data_file_path = ibdata1:10M:autoextend
```

**innodb_data_home_dir** 设置定义了 MySQL 放置支持 InnoDB 存储引擎所需文件的位置。这允许你在需要时将这些文件与正常的 MySQL 数据库文件分离。

**innodb_data_file_path** 设置为存储引擎定义了三个信息部分：

- MySQL 用于主要 InnoDB 存储文件的文件名
- 存储文件的初始大小
- 当存储文件填满时会发生什么

为了帮助加快数据存储过程，InnoDB 存储引擎在系统硬盘上为数据库存储文件预分配空间。这样，对于插入表中的每条数据记录，存储引擎不需要向操作系统请求更多磁盘空间来添加到数据库文件中——它已经在那里了！这极大地提高了数据库性能。第二个参数定义了 InnoDB 存储引擎分配的初始磁盘空间量。

第三个参数是事情变得有趣的地方。它定义了当为存储文件分配的空间变满时，InnoDB 存储引擎的行为。

