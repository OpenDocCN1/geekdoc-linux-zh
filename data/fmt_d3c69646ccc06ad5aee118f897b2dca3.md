
- 从 Apache 官方网站 `http://www.apache.org` 或较近的镜像站点获取服务器源码。与 MySQL 软件一样，首先检查最新的 Apache 版本，然后参考镜像站点列表。将压缩包（例如 `apache_1.3.14.tar.gz`）保存在方便的位置（如 `/usr/src`），并使用以下命令解压压缩包：

```bash
# cd /usr/src
# tar xzvf apache_1.3.14.tar.gz
```

- 配置 Apache 服务器。对于第一阶段，必须运行 Apache 配置脚本。为此，输入以下命令：

```bash
# cd /usr/src/apache_1.3.14/
# ./configure --prefix=/usr/local/apache
```

使用 Apache、PHP、MySQL 和 `http://` 的 Linux Web 解决方案

- 卸载任何现有的 Apache 服务器。（如果你正在运行某一个 Linux 发行版，你可能已经有了 Apache 服务器。）如果你已经更改了配置，你可能想以新名称保存 Apache 文件。按照以下方法删除现有版本：

```bash
# rpm -qa | grep apache
apache-1.3.3-1
apache-devel-1.3.3-1
```

- 在安装了其他包的情况下，你将收到关于其他包依赖关系的警告。必须先删除它们。`RPM` 管理器提示使用 `"man rpm"` 获取关于使用该工具的信息。例如：

```bash
# rpm -e mod_perl-1.15-3 mod_php-2.0.1-5 mod_php3-3.0.5-2
# rpm -e apache-1.3.3-1 apache-devel-1.3.3-1
```

在下一步中，你将编译 PHP，并完成 Apache 安装的第二阶段。

### 3.1.3 安装 PHP3

导航到 PHP 的官方网站 `http://www.php.net/`。该网站提供了 PHP 源码包、手册、代码示例以及使用 PHP3 的其他开源包的指针。进入“Downloads”并从最近的镜像站点下载最新的 PHP3 源码包。将该包（例如 `php-3.0.17.tar.gz`）保存在方便的位置 `/usr/src/`，并使用以下命令解压该包：

- 获取源码，使用与之前命令中 Apache 切换时相同的 Apache src 目录。

```bash
# cd /usr/src/
# tar xzf php-3.0.17.tar.gz
```

> 注意：在下一步中，使用与之前命令中 Apache 切换时相同的 Apache src 目录。

- 编译 PHP3。PHP3 在编译为 Apache 模块并使用 MySQL 之前需要进行配置。

有许多你可能想要启的编译选项。常用的选项包括 IMAP 支持、用于动态创建图像的 GD、轻量级访问协议 (LDAP) 支持、WebDAV（HTTP 分布式授权与版本控制 (DAV)）支持以及 zlib（压缩库）。这些选项需要安装额外的包，并且超出了本文的范围。要编译 PHP3，输入以下命令：

```bash
# cd /usr/src/php-3.0.17/
# ./configure --with-mysql --with-apache=../apache_1.3.14 \
--enable-track-vars
```

- 使用以下命令安装 PHP3：

```bash
# make
# make install
```

### 3.1.4 重新配置 Apache 服务器（第二阶段）

此时，MySQL 数据库正在运行，Apache 服务器已部分就绪，PHP 库已安装。你将重新配置 Apache 服务器以使用 PHP。

- 返回 `apache_1.3.14` 目录，如下：

```bash
cd /usr/src/apache_1.3.14/
```

- 编译带有 PHP 模块的 Apache 服务器，以及 `mod-status` 和 `mod-info` 两个模块，你可以通过配置信息和服务器状态配置 Web 管理员。

```bash
#./configure --activate-module=src/modules/php/libphp3.a \
--enable-module-info --enable-module=status

# make

# install
```

- 编辑配置文件。

PHP 的默认配置是合理的，但你可以修改某些资源限制。默认情况下，任何 PHP 页面的最大执行时间 (`execution_time`) 为 30 秒。

将 PHP 的配置移动到系统目录，如下：

```bash
cp /usr/src/php3-3.0.17/php3.ini-dist /usr/local/lib/php3.ini
```

- 编辑 Apache 配置文件 `/usr/local/apache/conf/httpd.conf`，使其处理带有 `php3` 扩展的文件。删除以下行中的 `#` 字符：

```apacheconf
#AddType application/x-httpd-php3 .php3
#AddType application/x-httpd-php3-source .php
```

- 使用以下命令启动 Apache Web 服务器：

```bash
/usr/local/apache/bin/apachectl start
```

- 同样编辑你的系统启动脚本 `/etc/rc`，包含以下命令：

```bash
/usr/local/apache/bin/apachectl start
```

### 3.1.5 安装 htdig 搜索引擎

- 从官方网站 `http://www.htdig.org/` 获取 htdig 源码。

然后进入“Where to get it”页面并下载最新的源码包（编写时版本为 3.1.5）。

将该包（例如 `htdig-3.1.5.tar.gz`）保存在方便的位置如 `/usr/src/`，并使用此类命令解包：

```bash
cd /usr/src/
tar zxf htdig-3.1.5.tar.gz
cd /usr/src/htdig-3.1.5
```

编译 htdig。默认情况下，搜索引擎将文件放置在 `/opt/www/htdig` 目录。

构建该包非常简单：使用以下命令进行配置、编译和安装。注意设置 Apache 目录默认位置的开关。

```bash
# ./configure --with-cgi-dir=/usr/local/apache/cgi-bin \
--with-image-dir=/usr/local/apache/icons \
--with-search-dir=/usr/local/apache/htdocs
```

```bash
# make
# make install
```

重新配置 Apache 服务器，使其能够找到 htdig 使用的内容。为此，修改文件 `/usr/local/apache/conf/httpd.conf`。找到 aliases 部分并在末尾插入此行：

```apacheconf
Alias /htdig/ "/usr/local/apache/icons/"
```

由于你修改了 Apache 配置文件，你需要重启进程以启用此更改。以下命令将重启 Apache 服务器：

```bash
# /usr/local/apache/bin/apachectl restart
```

### 3.1.5.1 更改文件位置

由于数据库可能会变得很大，将数据库移动到具有足够剩余空间的分区是一个好主意。

注意：运行在 Intel 上的 Linux v2.x 最大大小为 2 GB。运行在 Alpha 上的 Linux 最大大小为 8 GB。

搜索数据库的存储需求各异。为了给预期搜索内容大小的两倍充分分配存储，索引增长比被索引的内容量略大。这种搜索不支持大量信息扩展。

要移动数据库，通过修改 `htdig.conf` 文件（通常位于 `/opt/www/htdig/config/`）来修改以下行：

```text
database_dir: /opt/www/htdig/db
```

### 3.1.5.2 更改搜索引擎查找内容的起点

这是一个由空格隔开的 URL 或文件位置列表。默认情况下，只跟随系统上的链接。例如，该行将 htdig 的起点更改为此 Web 服务器的名称。

```text
Start_url: http://www.isp.com/
```

### 3.1.5.3 将搜索方法从 HTTP 连接更改为通过文件系统进入

使用这种方法 htdig 直接遍历内容，这种方法大大减少了索引网站所需的时间以及 Web 日志中的混乱。

注意：此方法仅在 Web 服务器和搜索引擎位于同一系统上，或者它们可以通过 NFS 访问相同的磁盘时才有效。

为了演示这一点，在 `htdig.conf` 文件中添加一个 `local_urls` 条目，提供从 Web 空间到文件系统位置的映射。例如，如果 `http://www.isp.com` 位于 `/usr/local/apache/htdocs` 且 `http://www.isp.com/products` 的内容位于 `/home/data/`，你将拥有如下条目：
