
RewriteCond 的另一个功能是将多行链联在一起。当连续列出多个 `Cond` 语句时，每个语句都被视为一个逻辑上的 AND（与）——只有当所有的 `RewriteCond` 都返回 true 时，末尾 `RewriteRule` 才会处理。之前的规则可以使用多个 `RewriteCond` 语句重写，如下：

```
RewriteCond %{HTTP_ACCEPT} application/xhtml+xml
RewriteCond %{SCRIPT_FILENAME} \.html$
RewriteRule . ~ [application/xhtml+xml]
```

```
<CondPattern
>CondPattern
=CondPattern
```

# 第 6 章

这些检查项分别检查输入字符串是否小于、大于或等于 `CondPattern`。例如，如果你想在特定年份后禁止网站的某个区域，可以使用以下代码：

```
RewriteCond %{TIME_YEAR} >2005
RewriteRule .* -F
```

除了这些比较运算符外，你还可以使用另外六个条件检查，它们用于评估文件和目录的状态：

| 比较运算符 | 含义 |
|---|---|
| `-d` (directory) | 检查是否存在匹配测试字符串的目录 |
| `-f` (is regular file) | 检查是否存在匹配测试字符串的普通文件 |
| `-s` (is regular file size) | 检查是否存在匹配测试字符串的普通文件，且大小大于 0 字节 |
| `-l` (is symbolic link) | 检查是否存在匹配测试字符串的符号链接 |
| `-F` (is existing file via subrequest) | 在考虑所有服务器访问控制后，检查文件是否可访问；使用内部子请求进行检查（会影响性能） |
| `-U` (is existing URL via subrequest) | 在考虑所有服务器访问控制后，检查 URL 是否可访问；使用内部子请求进行检查（会影响性能） |

例如，要检查图像是否存在且实际上包含某些数据，你可以使用以下代码：

```
RewriteCond %{REQUEST_FILENAME} \.jpg$
RewriteCond %{REQUEST_FILENAME} !-s
RewriteRule . -F
```

第一个条件检查文件是否存在，第二个条件检查它是否为空。注意，使用感叹号会否定该条件。

## RewriteCond 标志 (Flags)

要控制 `RewriteCond` 的行为，你可以使用标志（flags）。这里是一些常用的标志：

| 标志 | 含义 |
|---|---|
| `[NC]` | 使模式匹配不区分大小写。 |
| `[OR]` | 如果上一个条件满足，则当前条件也满足。 |
| `[L]` | 如果条件满足，则停止处理后续规则。 |
| `[R]` | 如果条件满足，则重定向请求。 |
| `[QSA]` | 启用查询字符串追加。 |

## RewriteBase

`RewriteBase` 指令用于设置所有相对 URL 路径的基缀。当你的规则位于子目录时，该指令非常有用。

## Apache 技巧

要构建静态版本，请更改您的配置命令以包含 `mod_speling`，如下所示：

```
./configure \
--enable-speling \
# ...以及您使用的任何其他配置设置
```

如果您倾向于使用动态模块，只需在 `mod_speling` 行后面添加 `=shared` 即可：

```
./configure \
--enable-speling=shared \
# ...以及您使用的任何其他配置设置
```

在运行配置脚本之后，使用 `make` 和 `make install` 来构建并安装新的二进制文件和模块就是很简单的事。如果您选择使用动态模块的 `mod_speling`，您将需要额外执行一个步骤。要将 `mod_speling` 启用为动态模块，请在您的 `httpd.conf` 文件中取消注释或添加该行：

```
LoadModule Apache_speling modules/mod_speling.so
```

完成更改后，重启 Apache。如果 Apache 错误日志中没有显示错误，则说明您已成功为服务器添加了 `mod_speling` 功能。

要激活拼写检查，请将以下指令添加到全局服务器配置部分、您的虚拟主机部分、`<Directory>` 部分或简单的 `.htaccess` 文件中：

```
CheckSpelling on
```

配置 `mod_speling` 仅涉及 `CheckSpelling` 指令——值 "on" 启用拼写检查，值 "off" 禁用任何检查（这是默认行为）。

要查看 `mod_speling` 的效果，请在您选择的目录中启用 `CheckSpelling`，在该目录下创建一个名为 `info.php` 的脚本：

```php
<?php phpinfo(); ?>
```

现在您应该认出这是标准的 PHP 信息输出了，但请不要使用正确的 `info.php` URL 加载文件，而是尝试使用一个拼写稍错误的名称，如 `iofn.php`。在启用 `mod_speling` 的情况下，Apache 会执行一个快速的 HTTP 301 重定向到它对您意图的最优猜测，而不是返回一个冰冷的 404 Not Found 错误。

## 内容压缩

如果我们告诉您，只需几分钟的 Apache 配置，就能节省大量的每月带宽流量？您可能会认为这是谎言，但事实确实如此——您需要的只是内容压缩和几个配置指令。

什么是内容压缩？当通过互联网下载网页页面时，默认情况下，构成页面标记、图像、脚本和其他内容的位和字节处于未压缩状态。您编写的 HTML 会在您保存时直接发送，包括所有空白符。内容压缩允许您透明地压缩页面标记，并将其通过互联网发送到用户的浏览器，在渲染到屏幕之前，它会在那里静默地解压缩。另一种思考方式是与通过电子邮件发送压缩文件相比。您可以很轻松地将一个大型媒体文件文档作为普通附件发送到电子邮件，但很多时候您在发送之前会将文件压缩成 `.zip` 或 `.tar.gz` 归包，以帮助缩短下载消息和附件的时间。

在 Apache 中使用压缩非常简单。您只需要 `mod_deflate`，它随 Apache 源代码一起提供，并在构建 Apache 时可以轻松编译为模块。

## 使用 mod_deflate

与之前过的模块一样，您首先需要检查的是该模块是静态可用于 Apache 还是作为模块可用：

```
/path/to/httpd -l
ls /path/to/apache/modules/
```

如果您在第一条命令的输出中看到 `mod_deflate.c`，或者在第二条命令的输出中看到 `mod_deflate.so`，说明您已经可以访问 `mod_deflate`，可以跳过重新构建 Apache 的步骤。

如果您在两个命令结果中都没有看到 `mod_deflate`，则需要在从源码编译时将其静态启用到 Apache 二进制文件中：

```
./configure \
--enable-deflate
```

如果您想使用动态可加载模块，只需在启用 `mod_deflate` 的行末尾添加 `=shared` 或 `--enable-deflate=shared`：

```
./configure \
--enable-deflate=shared \
# 以及您使用的任何其他配置设置
```

如果您将 `mod_deflate` 构建为动态模块，您将需要通过以下方式启用 `httpd.conf`：

```
LoadModule deflate_module modules/mod_deflate.so
```

然后重启 Apache 使更改生效。在构建并启用 `mod_deflate` 后，告诉 Apache 使用 `mod_deflate` 以及压缩哪些文件类型就是简单的事了。要做到，您需要编辑 `httpd.conf`，或者在您使用的目录中创建一个 `.htaccess` 文件——如果可用，这是首选方法。

## Apache 技巧

要在 Apache 中全局启用压缩，请向 `httpd.conf` 添加以下内容：

```
AddOutputByType DEFLATE text/*
AddOutputByType DEFLATE application/ms*
AddOutputByType DEFLATE application/vnd*
AddOutputByType DEFLATE application/postscript
```

然后您只需要重启 Apache，压缩就会开始运行。

这些配置指令到底意味着什么？这非常直观——在 Apache 2.x 中，`AddOutputByType` 指令的作用正如其名所示：它告诉 Apache 在输出到达端用户浏览器之前，通过 `mod_deflate` 过滤器处理任何 Microsoft 文档（如 Word 或 Excel 文件）以及 postscript 文件（如 Adobe Illustrator 绘图）。只需通过使用 MIME 类型和通配符的组合（类似于示例），即可将任何文档类型添加到 `mod_deflate` 的过滤列表中。

如果您只想压缩纯文本和 HTML 文件，请使用：

```
AddOutputByType DEFLATE text/plain
AddOutputByType DEFLATE text/html
```

如果您想让特定的文件被压缩，请使用：

```
AddOutputByType DEFLATE application/pdf
AddOutputByType DEFLATE application/zip
```

如果您想压缩所有类型的文件，请使用：

```
AddOutputByType DEFLATE */*
```

在某些情况下，所有 PHP 脚本可能已经启用了输出缓冲和压缩。要确定这一点，请检查配置变量 `output_handler` 的值，或者在 `php.ini` 中查看 `output_handler` 和 `zlib.output_compression` 的值。

要在 PHP 中启用输出缓冲，请执行以下操作：

1. 在您的机器上安装所需的 zlib 库。
2. 根据需要配置 PHP 源码，确保包含 `--with-zlib`，然后根据需要进行编译/安装。
3. 修改您的 `php.ini` 以包含以下行：

```
output_buffering = Off
output_handler =
zlib.output_compression = On
```

4. 重启 Apache 使新更改生效。

## 结合 Apache 的 MySQL

到此时，你已经创建了安全区域或正在使用 Apache 和基本认证，对于大多数情况，这可能就是你需要的所有。你可能会发现，Apache 的基本认证虽然简单，但在控制和自定义方面略有局限。对于这种情况，你实际上可以使用 Apache 基本认证与通过 MySQL 实现的关系型数据库的力量相结合。为了实现这一目的，存在 `mod_auth_mysql` Apache 模块。

与标准的 Apache 基本认证一样，`mod_auth_mysql` 可以控制按目录访问，并可以在 `.htaccess` 文件和 `httpd.conf` 内部的 `<Directory>` 中进行配置。与标准的 Apache 基本认证不同，所有凭据都存储在数据库中，而不是文件中。

## 设置数据库

安装和配置 `mod_auth_mysql` 涉及几个步骤，其中一步是创建必要的数据库结构来存储用户数据。首先加载您的 MySQL 客户端并创建数据库。例如：

```
CREATE DATABASE apacheauth;
```

接下来，创建一个将供 Apache 访问凭据的用户：

```
GRANT SELECT ON apacheauth.* TO apache@localhost IDENTIFIED BY 'apachepass';
```

现在数据库用户已经创建，是时候添加一个表来存储登录信息了。现在从一个只包含用户名和密码的示例表开始：

```
USE apacheauth;
CREATE TABLE user_info (
user_name varchar(50) NOT NULL,
user_password varchar(50) NOT NULL,
PRIMARY KEY (user_info)
);
```

你可以按照喜意命名表和列。在先前的示例中，`user_info` 被用表名，`user_name` 和 `user_password` 用于登录/密码组合，因为这些是 `mod_auth_mysql` 识别的默认名称。

在 `mod_auth_mysql` 的后续版本中，密码的默认列是 `user_password`，而不是模块文档中提到的 `user_passwd`。

创建一个初始测试账户，以便你在测试认证时使用它：

```
INSERT INTO user_info (user_name, user_password)
VALUES ('testuser', 'testpass');
```

注意语句中对密码使用了 `SHA1` 函数，而不是 `PASSWORD()` 函数。通过 `mod_auth_mysql`，你可以对密码使用多种加密方法——这里只是恰好使用了 SHA1。

## 安装模块

一旦设置好数据库表，你将需要实际下载 `mod_auth_mysql` 的源码，地址为：http://modauthmysql.sourceforge.net。在编写本文时，当前版本为 2.9.0，因此你需要下载 `mod_auth_mysql-2.9.0.tar.gz`。

下载模块源码后，解压 tar 包：

```
tar -xzvf mod_auth_mysql-2.9.0.tar.gz
```

解压存档后，切换到新创建的文件夹：

```
cd mod_auth_mysql-2.9.0
```

要从下载的源码构建模块，你实际上将使用 Apache 的 `apxs` 来执行以下命令，并使用你系统中 `apxs` 二进制文件的路径；这里使用了 Apache 的默认位置 `/usr/local/apache2/`：

```
/usr/local/apache2/bin/apxs -c -mysqlclient -lm mod_auth_mysql.c
```

如果构建成功，你将得到编译文件 .h 且没有错误。如果你在构建 `mysql.h` 文件时遇到错误以及 MySQL 相关的错误，你可能需要手动指定 MySQL 库和包含文件的路径。使用 MySQL 的默认位置，你的命令可能如下：

```
/usr/local/apache2/bin/apxs -c -mysqlclient -lm -lz \
-L /usr/local/mysql/lib/mysql \
-I /usr/local/mysql/include/mysql \
mod_auth_mysql.c
```

## Apache 技巧

要安装新编译的模块，你需要以 root 身份执行以下命令。像往常一样，更改 `apxs` 路径指向你的 `apxs` 二进制文件：
