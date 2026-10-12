

## 第 12 章

### 缓存引擎

| 指令 | 默认值 | 设置位置 | 描述 |
| --- | --- | --- | --- |
| eaccelerator.shm_size | 0 | php.ini 和 httpd.conf | 定义 eAccelerator 用于缓存脚本的共享内存量（以兆字节为单位）。值为 0 时，表示 eAccelerator 将使用操作系统的默认值。 |
| eaccelerator.cache_dir | /tmp/eaccelerator | php.ini 和 httpd.conf | 指定磁盘缓存目录，如果 eAccelerator 配置为使用磁盘缓存。 |
| eaccelerator.enable | 1 (启用) | php.ini、.htaccess 和用户脚本 | 允许相应地使用数值 1 和 0 来启用或禁用 eAccelerator。此设置可以在用户脚本和 .htaccess 文件中更改，因此你可以使用它在单个脚本和目录中启用/禁用缓存引擎。 |
| eaccelerator.optimizer | 1 (启用) | php.ini、httpd.conf、.htaccess 和用户脚本 | 启用 eAccelerator 的内部代码优化引擎。值为 1 时启用优化器，值为 0 时禁用。此设置可以在用户脚本和 .htaccess 文件中更改，因此你可以使用它在单个脚本和目录中启用/禁用优化引擎。 |
| eaccelerator.debug | 0 (关闭) | php.ini 和 httpd.conf | 切换调试日志的开启和关闭。 |
| eaccelerator.check_mtime | 1 | php.ini 和 httpd.conf | 此设置控制 eAccelerator 是否检查文件的修改时间以判断其是否已更改。启用的值 1 指示 eAccelerator 如果 PHP 脚本已更改，则自动重新编译该脚本。 |
| eaccelerator.filter | "" (空字符串) | php.ini、httpd.conf、.htaccess 和用户脚本 | 此指令允许你指定一个以空格分隔的列表，指示哪些文件应处理以及哪些文件不应由 eAccelerator 处理。该列表由带有通配符匹配的文件名组成（例如，*.php *.pht）。若要忽略特定的匹配项，请在相关模式前加上感叹号。 |

| 指令 | 默认值 | 设置位置 | 描述 |
| :--- | :--- | :--- | :--- |
| `eaccelerator_shm_max` | `0` (无限制) | `php.ini` 和 `httpd.conf` | 指定使用 `eaccelerator_put()` PHP 函数放入共享内存的数据的最大大小。数值以字节为单位指定，值为 0 表示禁用限制。 |
| `eaccelerator_shm_ttl` | `0` (从不删除过时脚本) | `php.ini` 和 `httpd.conf` | 定义脚本在 `eAccelerator` 共享内存中保持缓存状态的秒数，超过该时间后允许为了新请求而从缓存中移除。值为 0 表示不应移除项目，这可能导致共享内存缓存最终填满，从而阻止对新请求进行缓存。 |
| `eaccelerator_shm_prune_period` | `0` (从不删除过时项目) | `php.ini` 和 `httpd.conf` | 类似于 `shm_ttl` 设置，此指令控制从共享内存缓存中收集过时脚本。与作为缓存中单个脚本的超时不同，`shm_prune_period` 通过仅在 `shm_prune_period` 中定义的时间经过后移除过时项目来工作。此值以秒数表示，值为 0 指示 `eAccelerator` 不要尝试移除过时项目。 |
| `eaccelerator_shm_only` | `0` (两者都使用) | `php.ini` 和 `httpd.conf` | 启用和禁用（0 或 1）磁盘缓存。值为 0 指示 `eAccelerator` 同时使用共享内存和基于文件的磁盘缓存，而值为 1 指示 `eAccelerator` 仅使用共享内存。 |
| `eaccelerator_compress` | `1` (启用压缩) | `php.ini`、`httpd.conf`、`.htaccess` 和用户脚本 | 此指令启用和禁用输出内容压缩，类似于 Apache 的 `mod_deflate` 或 PHP 的 `gzip` 输出缓冲。 |
| `eaccelerator_compress_level` | `9` (最大压缩) | `php.ini`、`httpd.conf`、`.htaccess` 和用户脚本 | 此设置控制使用 `eaccelerator_compress` 中启用的输出压缩时所使用的压缩级别。最大值 9 使用高压缩，导致传输的文件大小更小，而较低的值会降低压缩并增加传输大小。 |

| 指令 | 默认值 | 设置位置 | 描述 |
|---|---|---|---|
| eaccelerator.sessions eaccelerator.content | | php.ini 和 httpd.conf | 你可以使用此指令告诉 eAccelerator 你希望它存储会话数据和内容的位置。值为 shm_and_disk 指示缓存引擎在共享内存和磁盘位置存储会话数据和内容。将其设置为 shm，它将使用共享内存作为主要存储位置，如果共享内存已满，则回退到磁盘存储。shm_only 表示你希望仅使用共享内存且从不使用磁盘回退。值 disk_only 的行为完全相反：它表示你希望仅使用磁盘存储而不使用共享内存。 |

### 移除 eAccelerator

移除 eAccelerator 非常简单，只需删除或注释掉 php.ini 中相应的扩展行，如下所示：

```php
;extension="accelerator.so"
```

若要永久从系统中移除 eAccelerator，请从 PHP 扩展目录中删除 eaccelerator.so 文件。

> 有关 eAccelerator 的更多信息，请访问 http://eaccelerator.net。

### Zend 优化器

不逊于可用的少数免费 PHP 缓存解决方案，Zend——驱动 PHP 的 Zend 引擎的创建者——发布了它们自己的代码优化器，而且是免费的。Zend 优化器的作用与 APC 和 eAccelerator 类似：它缓存 PHP 脚本的编译状态，从而在后续请求中实现更快的执行。

除了加速 PHP 脚本的性能外，Zend 优化器还允许你在服务器上运行由 Zend Encoder 或 Zend SafeGuard Suite 编码的脚本。

### 安装 Zend 优化器

与大多数竞争缓存解决方案相比，安装 Zend 优化器稍显容易，因为它附带了一个方便的身份配置和设置向导。

首先，从 http://zend.com/store/products/zend-optimizer.php 下载适合你系统的软件包。

然后，解压存档，并进入新创建的目录：

```bash
tar -xvzf ZendOptimizer-2.5.10a-linux-glibc21-i386.tar.gz
cd ZendOptimizer-2.5.10a-linux-glibc21-i386
```

以 root 身份运行安装向导：

```bash
./install.sh
```

运行向导，在提示时指定必要的路径。通常提供的默认值就足够了。确保在询问时选择正确版本的 Apache（本书撰写时基于 Apache 2）。

向导会对你的 php.ini 文件进行备份，并创建一个指向 Zend 修改后的 php.ini 文件的新符号链接。

在向导结束时，你可以选择自动重启 Apache，或者按你的选择退出向导并手动重启 Apache。

### 配置 Zend 优化器

与 APC 和 eAccelerator 一样，你有几个指令可用于调整 Zend 优化器的运行：

| 指令 | 默认值 | 设置位置 | 描述 |
| --- | --- | --- | --- |
| zend_optimizer.optimization_level | 15 (所有优化) | php.ini 和 httpd.conf | 确定由 Zend 优化器执行的优化级别。优化器可以对每个脚本执行四次不同的传递，通过组合以下值来控制：<br>0: 无传递 <br>1: 传递 1 <br>2: 传递 2 <br>4: 传递 3 <br>8: 传递 4 <br>你只需将每次传递的数字相加即可得到你的优化传递设置。例如，值 11 将执行传递 1、传递 2 和传递 4 (1+2+8)。 |
| zend_optimizer.enable_loader | 1 (启用) | php.ini 和 httpd.conf | 你可以使用此指令在不卸载的情况下启用或禁用 Zend 优化器。值为 0 禁用优化器；1 启用它。 |

### 移除 Zend 优化器

要移除 Zend 优化器，你首先必须删除其为 php.ini 创建的符号链接。然后，将备份的原始 php.ini 文件恢复到其原位置。此时你可以重启 Apache，Zend 优化器将不再处于活动状态。如果你愿意，你可以删除 Zend 优化器文件——其默认位置是 /usr/local/Zend。

### JPCache

内存/磁盘缓存解决方案领域的另一个条目是 JPCache。与 APC 和 eAccelerator 不同，JPCache 无需编译为 DSO 或静态构建到 PHP 本身。JPCache 实际上是用 PHP 编写的，并使用标准 *include* 和 *require* 语句使用。

JPCache 通过将 PHP 脚本生成的输出存储到磁盘或 SQL 服务器中工作，而不是保存每个脚本的编译状态。通过以此方式缓存输出，并结合 gzip 内容压缩，你可以实现高达 80% 或更多的带宽节省。

### 安装 JPCache

要开始使用 JPCache，你需要做的第一件事是从 http://www.jpcache.com 下载最新版本的副本。

接下来，提取 tar/gzip 存档：

```bash
tar -xzvf jpcache.v2.tgz
```

此目录的内容现在包含你使用 JPCache 所需的脚本。将此文件夹放在任何你喜欢的位置，只要 Apache 运行的用户可以访问即可。记下该位置的完整路径，因为配置缓存时你需要它。

在你的 JPCache 文件夹的根目录中，编辑 jpcache.php 文件。更改以下行以指向你放置 jpcache 文件夹的位置：

```php
$includedir = '/path/to/jpcache-files';
```

例如，如果你将提取的 jpcache 文件夹移动到 /www/jpcache，你将使用以下值：

```php
$includedir = '/www/jpcache';
```

接下来，编辑 jpcache-config.php 文件。最重要的是，你需要取消注释指示你希望使用什么类型的缓存存储（文件或 MySQL）的行。对于此示例，取消注释基于文件的存储选项：

```php
$JPCACHE_TYPE = 'file';
```

