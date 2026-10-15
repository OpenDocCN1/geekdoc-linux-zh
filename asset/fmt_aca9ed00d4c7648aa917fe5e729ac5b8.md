
要移除 Zend Optimizer，您必须先删除它为 `php.ini` 创建的符号链接。然后，将备份的原始 `php.ini` 文件恢复到其原来的位置。此时您可以重启 Apache，Zend Optimizer 将不再处于活动状态。如果您愿意，可以删除 Zend Optimizer 文件——它们的默认位置是 `/usr/local/Zend`。

## JPCache

内存/磁盘缓存方案领域的另一个条目是 JPCache。与 APC 和 eAccelerator 不同，JPCache 不需要编译为 DSO 或静态构建到 PHP 本身中。JPCache 实际上是用 PHP 编写的，并使用标准的 `include` 和 `require` 语句。

JPCache 通过将 PHP 脚本生成的输出存储到磁盘或 SQL 服务器中，而不是保存每个脚本的编译状态来工作。通过这种方式缓存输出，并结合 gzip 内容压缩，您可以实现 80% 或更多的带宽节省。

### 安装 JPCache

要开始使用 JPCache，您需要做的第一件事是在 <http://www.jpcache.com> 下载最新版本的副本。

接下来，解压缩 tar/gzip 归档：

```bash
tar -xvzf jpcache.v2.tgz
```

该目录的内容现在包含您使用 JPCache 所需的脚本。可以将此文件夹放置在您喜欢的任何位置，只要 Apache 运行的用户能够访问即可。记下该位置的完整路径，因为您在配置缓存时需要它。

在 JPCache 文件夹的根目录中，编辑 `jpcache.php` 文件。将以下行更改为指向您放置 jpcache 文件夹的位置：

```php
$includedir = "`path/to/jpcache-files`";
```

例如，如果您将解压后的 jpcache 文件夹移动到 `/www/jpcache`，您将使用以下值：

```php
$includedir = "/www/jpcache";
```

接下来，编辑 `jpcache-config.php` 文件。最重要的是，您需要取消注释一行，指示您希望使用哪种类型的缓存存储（文件或 MySQL）。对于本例，取消基于文件的存储选项的注释：

```php
$JPCACHE_TYPE = "file";
```

## 缓存引擎

需要更改的另一个设置是 `$JPCACHE_USE_GZIP` 值。此值用于启用 gzip 内容压缩，但不幸的是，由于最近版本的 JPCache 中存在一个 bug，在某些浏览器中输出可能会损坏。为了安全起见，请将此值设置为 0：

```
$JPCACHE_USE_GZIP=0;
```

还请注意控制文件缓存位置的设置 `$JPCACHE_DIR`，其默认值为 `/tmp/jpcache`。你需要实际创建 `$JPCACHE_DIR` 设置中列出的文件夹，因此在命令提示符下执行以下操作：

```
mkdir /tmp/jpcache
chmod 0777 /tmp/jpcache
```

最后，使用以下 PHP 脚本测试缓存系统，使用合适的路径指向你放置 JPCache 文件夹的位置：

```
<?php
require "/path/to/jpcache.php";
echo time();
phpinfo();
?>
```

注意页面顶部的 UNIX 时间戳。每次重新加载页面时，它应该保持不变——JPCache 正在提供缓存版本，而不是每次重新处理脚本。

### 配置 JPCache

除了前面提到的三个配置选项外，你还有十四个额外的配置变量可以根据需要进行修改。完整的配置选项列表如下：

| 配置选项 | 默认值 | 描述 |
| :--- | :--- | :--- |
| `$JPCACHE_TYPE` | 无——你*必须*在使用 JPCache 之前设置此变量。 | 要告诉 JPCache 使用基于文件或基于数据库的存储来存储缓存数据，你使用 `$JPCACHE_TYPE`。值 `file` 告诉 JPCache 使用磁盘存储，而值 `mysql` 使缓存数据存储在一个 MySQL 数据库中。 |
| `$JPCACHE_TIME` | 900 | 使用数值定义，此变量告诉 JPCache 在缓存中保留页面多长时间（以秒为单位）。负值将完全禁用页面缓存，而值 0 告诉 JPCache 永久保留缓存页面。 |
| `$JPCACHE_DEBUG` | 0 (关闭) | 使用 `0` 表示关闭，`1` 表示开启，`$JPCACHE_DEBUG` 控制是否启用调试。 |
| `$JPCACHE_IGNORE_DOMAIN` | 1 (忽略域名) | 如果你的 Web 服务器只提供一组内容，你可以将此值设置为 1 (开启)，让 JPCache 忽略文件名的任何域名前缀。当关闭时，JPCache 搜索与完整 URL 匹配的文件，包括域名。 |
| `$JPCACHE_ON` | 1 (启用) | 此变量仅控制是否启用 JPCache。 |
| `$JPCACHE_USE_GZIP` | 1 (开启) | 要启用 GZIP 输出压缩，类似于 Apache 的 `mod_deflate` 或 PHP 自身的 GZIP 输出缓冲，请设置此值为 1。请注意，由于最近版本的 JPCache 中的一个 bug，在使用 JPCache 的 GZIP 压缩时，某些浏览器中的输出可能会损坏。如果你的脚本在此设置启用时返回乱码或缺失的内容，请尝试禁用此设置，看看情况是否得到纠正。 |
| `$JPCACHE_POST` | 0 (禁用) | 此变量控制 JPCache 中的 HTTP POST 缓存。设置为 `0` 以禁用，`1` 以启用。 |
| `$JPCACHE_GC` | 1 | 要控制 JPCache 垃圾回收例程的积极性，你可以为 `$JPCACHE_GC` 分配数值。值范围为 `0` 到 `100`，表示对缓存项执行垃圾回收的概率百分比。 |
| `$JPCACHE_GZIP_LEVEL` | 9 (最大压缩) | 当使用 JPCache 内置的 GZIP 输出压缩时，你可以使用此变量来控制输出流的压缩级别。值范围从 `9`，表示高压缩率和较小的输出大小，到 `1`，表示低压缩率和较大的传输大小。 |
| `$JPCACHE_CLEANKEYS` | 1 (哈希存储键) | 当 JPCache 创建脚本输出的缓存副本时，它使用每个脚本的唯一键将输出存储在文件名或数据库记录中。默认情况下，JPCache 对标识符进行哈希处理，以使其难以确定给定缓存条目的来源，例如 "`JPC-be45886d86b822858023b8f6061401a2`" 。如果需要，你可以告诉 JPCache 不哈希每个脚本的缓存标识符，以便你轻松确定每个缓存脚本的身份。禁用哈希后，脚本标识符将看起来更像 `directory_file_name_extension_HTTPMethod=n_n__`。 |
| `$JPCACHE_DIR` | /tmp/jp-cache | 使用此变量设置 JPcache 存储其基于文件的缓存数据的目录。JPcache 存储缓存文件的目录需要可由 Apache 进程用户写入。 |
| `$JPCACHE_FILEPREFIX` | jpc- | 当 JPcache 在磁盘缓存中创建缓存文件时，它可以在此指定一个文件名前缀，以避免与现有文件发生冲突。 |
| `$JPCACHE_DB_HOST` | localhost | 当使用数据库作为缓存存储位置时，你需要设置变量以便 JPcache 连接和使用数据库。此变量设置 JPcache 将连接到的数据库主机。 |
| `$JPCACHE_DB_DATABASE` | jp-cache | 此变量设置存储缓存数据的 MySQL 数据库的名称。 |
| `$JPCACHE_DB_USERNAME` | sqluser | 要设置存储在数据库中缓存信息时使用的用户名，请设置 `$JPCACHE_DB_USERNAME`。 |
| `$JPCACHE_DB_PASSWORD` | passvd | 与 `$JPCACHE_DB_USERNAME` 配合使用。此变量设置数据库连接密码。 |
| `$JPCACHE_DB_TABLE` | CACHEDATA | JPcache 缓存数据存储的表的名称在 `$JPCACHE_DB_TABLE` 中。要创建该表，你可以在 MySQL Monitor 或你首选的 MySQL 管理工具中执行以下命令：`CREATE TABLE CACHEDATA ( CACHEKEY varchar(255) NOT NULL, CACHEEXPIRATION int(11) NOT NULL, GZDATA blob, DATASIZE int(11), DATAARC int(11), PRIMARY KEY (CACHEKEY) );` 当然，你需要更改数据库表的名称，使其与你在 `$JPCACHE_DB_TABLE` 中指定的值相匹配，反之亦然。 |
