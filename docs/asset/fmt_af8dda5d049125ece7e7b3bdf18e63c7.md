
然而，在大多数服务器配置中，这不是一个好主意。事实上，有一些文件类型从压缩中无法受益，有些文件在压缩后甚至会导致最终用户的数据损坏。在大多数情况下，没有必要压缩图像格式，因为最常用的 Web 格式已经内置了某种形式的压缩。此外，PDF 也是压缩过的，绝对不应该通过 `mod_deflate` 进行过滤，否则它们将在 Acrobat Reader 中变得无法阅读。

> 需要注意的是，Netscape Navigator 4.x 版本无法可靠地解压除 `text/html` 以外的任何文件类型，且特定版本的 Netscape Navigator 4.x 根本无法解压任何文件类型。

为了进一步调整你选择的文件类型的压缩，`mod_deflate` 提供了以下部分描述的配置指令。

### DeflateCompressionLevel

`DeflateCompressionLevel` 设置用于缩小文件的压缩级别，范围从 1 到 9。压缩级别 1 提供最快的压缩速度，压缩率最低（文件较大），而压缩级别 9 使用最慢的压缩速度，但生成的文件大小小得多。在决定使用哪个级别时，你必须确定对你来说哪个更重要——节省处理器周期还是节省下载时间。默认的压缩级别 6 通常是两者之间的良好折中方案。

### DeflateFilterNote

如果你希望日志文件显示访问日志中每个请求文件的压缩比，请使用 `DeflateFilterNote`。`DeflateFilterNote` 接受一个日志标记名称作为其值——使用 `DeflateFilterNote` 给出的命名标记可用于使用 Apache 的 `LogFormat` 指令自定义日志输出。

### DeflateWindowSize

这指定了用于压缩文件的 zlib 压缩窗口大小。值范围为 1 到 15，1 提供较少的压缩，15 提供最多的压缩。`DeflateWindowSize` 的默认值为 15。

### mod_deflate 的效果如何？

为了查看 `mod_deflate` 的节省字节的能力，此示例使用 Apache 提供了一个中等大小的 HTML 页面，分别在有和没有启用 `mod_deflate` 的情况下进行测试。在此示例中，用于 Wrox P2P 社区论坛（位于 `http://p2p.wrox.com`）的首页。该页面的原始 HTML 标记——仅指 HTML——重达 47172 字节。请查看下表，了解它在三种不同压缩级别下通过 `mod_deflate` 后的表现：

| 压缩级别 | 传输字节数 | 占原始大小百分比 | 近似下载时间 (56k) |
| :--- | :--- | :--- | :--- |
| 原始 | 47172 字节 | 原始 100% | 11.7 秒 |
| 默认 (6) | 7621 字节 | 原始 16.2% | 3.8 秒 |
| 级别 1 | 9050 字节 | 原始 19.2% | 4.1 秒 |
| 级别 9 | 7581 字节 | 原始 16.1% | 3.8 秒 |

如你所见，使用 `mod_deflate` 显然比提供未压缩的原始 HTML 更有优势——它可以消除通过连接发送的文件大小的近 84%。还要注意，使用最大压缩级别 9 仅比默认级别 6 略胜一筹，因此在这种情况下，坚持使用默认压缩级别 6 来为处理器节省几个周期可能是安全的。

许多网站混合了 HTML、媒体和相关脚本文件，因此像摄影博客或在线购物商城这样的网站可能无法在每个提供的文件上都获得巨大的文件节省，但每节省一个字节在月底都可能转化为巨大的带宽节省。以文本为主的网站，如博客和新闻门户，将真正受益于内容压缩，因为这些网站利用的大部分带宽都是纯文本——这些文本会通过 `mod_deflate`。

#### 为 PHP 脚本启用压缩

你可能在问 PHP 文件怎么办？在许多情况下，没有必要对 PHP 文件使用压缩，在某些情况下，这对输出甚至有害。

如果你的 PHP 脚本输出实际的图像或 PDF，例如，你不会希望 Apache 盲目地压缩输出，仅仅因为文件扩展名碰巧是 `.php`。

在某些情况下，输出缓冲和压缩可能已针对所有 PHP 脚本启用。要确定这一点，请检查配置变量 `output_handler` 的值，或者在 `php.ini` 中查找 `output_handler` 和 `zlib.output_compression` 的值。

要在 PHP 中启用输出压缩，请执行以下操作：

- 如有必要，请在您的机器上安装 `zlib` 库。
- 根据需求配置 PHP 源代码，确保包含 `--with-zlib`，然后正常进行 `编译`/`安装`。
- 修改您的 `php.ini` 以包含以下内容：

```text
output_buffering = Off
output_handler =
zlib.output_compression = On
```

- 重启 Apache 以使新的更改生效。

## 将 MySQL 与 Apache 结合使用

到目前为止，您已经使用 Apache 和基础身份验证创建了一个或两个安全区域，对于大多数情况而言，这可能已经足够。然而，您可能会发现，虽然 Apache 的基础身份验证很简单，但您可以纳入的控制和自定义程度有点过于有限。对于许多此类情况，您可以实际使用 Apache 基础身份验证与通过 MySQL 使用关系数据库功能性的组合。为了实现这种目的，存在 `mod_auth_mysql` Apache 模块。

与标准的 Apache 基础身份验证类似，`mod_auth_mysql` 可以按目录控制访问权限，并且可以配置在 `.htaccess` 文件内部以及 `httpd.conf` 中的 `<Directory>` 部分内。与标准的 Apache 基础身份验证不同，所有用户凭据存储在数据库中，而不是存储在平面文件中。

### 设置数据库

安装和配置 `mod_auth_mysql` 涉及几个步骤，第一步是创建必要的数据库结构以容纳用户数据。首先，打开您喜欢的 MySQL 客户端，并创建数据库。例如：

```sql
CREATE DATABASE apacheauth;
```

接下来，创建一个供 Apache 访问凭据使用的用户：

```sql
GRANT SELECT ON apacheauth.* TO apache@localhost IDENTIFIED BY 'apachepass';
```

现在数据库用户已创建，是时候添加一个表来存储登录信息了。暂时从一个仅包含用户名和密码的简单表开始：

```sql
USE apacheauth;
CREATE TABLE user_info (
user_name varchar(50) NOT NULL,
user_password varchar(50) NOT NULL,
PRIMARY KEY (user_info)
);
```

您可以随意命名表和列。在上面的示例中，`user_info` 用作表名，`user_name` 和 `user_password` 用作登录/密码组合，因为这些是 `mod_auth_mysql` 识别的默认名称。

> 在 `mod_auth_mysql` 的后续版本中，`password` 的默认列是 `user_password`，而不是模块文档中所述 的 `user_passwd`。

接下来，创建一个初始测试用户帐户，以便在后续测试身份验证时使用：

```sql
INSERT INTO user_info (user_name, user_password)
VALUES ('testuser', SHA1('testpass'));
```

> 请注意，语句中对密码使用了 `SHA1` 函数，而不是 `PASSWORD()` 函数。使用 `mod_auth_mysql` 时，您可以使用几种密码加密方法——本例碰巧使用的是 `SHA1`。

### 安装模块

一旦数据库表设置好，您需要实际下载 `mod_auth_mysql` 的源代码，可从 `http://modauthmysql.sourceforge.net` 获取。在撰写本文时，当前版本为 `2.9.0`，因此您应该下载 `mod_auth_mysql-2.9.0.tar.gz`。

下载模块源代码后，解压 tar 包：

```bash
tar -xvzf mod_auth_mysql-2.9.0.tar.gz
```

解压 tar 包后，更改目录到 newly created source folder（新创建的源文件夹）：

```bash
cd mod_auth_mysql-2.9.0
```

要从下载的源代码构建模块，您实际上将直接使用 Apache 的 `apxs` 命令。使用系统中 `apxs` 二进制文件的路径执行以下命令；此处使用的是默认 Apache 位置 `/usr/local/apache2/bin`：

```bash
/usr/local/apache2/bin/apxs -c -lmySQLclient -lm -lz mod_auth_mysql.c
```
