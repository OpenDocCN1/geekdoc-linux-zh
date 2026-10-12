

## 安装 APC

首先，从 PECL 网站获取最新版本的 APC 源代码副本：`http://pecl.php.net/package/APC`。

一旦你获得了 tar/gzip 格式的源代码副本，解压该包并进入新创建的源代码文件夹：

```bash
tar -xvzf APC-3.0.5.tgz
cd APC-3.0.5
```

接下来，在源代码文件夹中运行 phpize。请务必使用安装 PHP 时附带的 phpize 的正确路径：

```bash
/usr/local/bin/phpize
```

当 phpize 运行时，你应该看到类似于以下内容的输出：

```text
Configuring for:
PHP Api Version:     20031224
Zend Module Api No:  20041030
Zend Extension Api No:       220040412
```

phpize 完成后，运行以下 configure 脚本，同样替换为你自己的 php-config 和 apxs 程序的正确路径：

```bash
./configure \
--enable-apc \
--enable-apc-mmap \
--with-apxs=/usr/local/apache2/bin/apxs \
--with-php-config=/usr/local/bin/php-config
```

然后，构建共享对象：

```bash
make
```

构建完成后，安装 DSO（以 root 身份运行）：

```bash
make install
```

此时，你的 PHP 扩展文件夹中应该有一个 apc.so 的副本。

要完成安装，将以下内容添加到 php.ini 文件的 extensions 部分，然后重启 Apache：

```ini
extension="apc.so"
```

## 配置 APC

在大多数情况下，APC 使用的默认配置应该就足够了，但如果你想要调整缓存以适应你的需求或系统，可以使用 php.ini 中的以下指令：

### 缓存引擎

| 指令 | 默认值 | 设置位置 | 描述 |
|---|---|---|---|
| `apc.enabled` | `1` (启用) | php.ini, httpd.conf, .htaccess, 和用户脚本 | 使用值 `1` 或 `0` 相应地启用或禁用 APC。在 php.ini 中，此设置只有在 APC 被静态编译到 PHP 中时才真正有用——当你像之前那样安装 APC 时，你可以简单地注释掉 `extension="apc.so"` 这一行。然而，此设置在用户脚本和 .htaccess 文件中是可修改的，因此你可以使用它在单个脚本和目录中启用/禁用缓存引擎。 |
| `apc.shm_segments` | `1` | php.ini 和 httpd.conf | 使用数值，你可以指定 APC 使用的共享内存段数。许多操作系统对每个共享内存段可以变得多大都有一个限制，通常很低。如果 APC 内存不足，增加此值将导致 APC 使用更多段，以帮助绕过操作系统限制。 |
| `apc.shm_size` | `30` | php.ini 和 httpd.conf | APC 共享内存段的大小，以 MB 为单位。根据操作系统不同，可能存在大小限制，通常较低。查阅你的操作系统文档以获取有关其共享内存段大小的更多信息。 |
| `apc.optimization` | `0` (关闭) | php.ini, httpd.conf, .htaccess, 和用户脚本 | 这是一个实验性设置，该指令控制 APC 内置的优化器。此设置的值越大，优化器的激进度越高。值 `0` 完全禁用优化。 |
| `apc.num_files_hint` | `1000` | php.ini 和 httpd.conf | 此设置向 APC 提供关于你的网站通常提供多少个独立源文件的提示。 |
| `apc.ttl` | `0` | php.ini 和 httpd.conf | 定义每个缓存条目在缓存中允许存在的时间（以秒为单位），在此之后允许新条目覆盖它。如果保持为 `0`，缓存可能会填满过时的条目，阻止新条目被缓存。 |
| `apc.gc_ttl` | `3600` | php.ini 和 httpd.conf | 定义每个缓存条目在垃圾收集列表中保留的时间（以秒为单位）。作为在服务器进程死亡，导致缓存文件滞留在缓存中的情况下的故障安全机制。值 `0` 禁用此功能。 |
| `apc.cache_by_default` | On | `php.ini` 和 `httpd.conf` | 控制所有文件的缓存。使用此指令来禁用默认的所有脚本缓存，允许你使用下面的 `apc.filters` 指令来更精细地控制哪些文件实际上被缓存。 |
| `apc.filters` | `""` (空字符串) | `php.ini` 和 `httpd.conf` | 允许你定义一个由逗号分隔的正则表达式列表，用于过滤哪些文件被缓存。使用 POSIX 扩展正则表达式——类似于 PHP 的 `ereg` 函数——你指定一个正则表达式列表以将某些脚本排除在缓存之外。任何匹配列表中模式的文件名将不会被缓存，除非该模式以 `+` 开头，在这种情况下它们将由 APC 缓存。在创建正则表达式时，假设是相对文件路径，而不是绝对路径。 |
| `apc.slam_defense` | 0 (禁用) | `php.ini` 和 `httpd.conf` | 使用 0 到 100 的数字定义，该指令指定服务器进程跳过缓存之前未缓存文件的概率。主要用于极其繁忙的 Web 服务器，`apc.slam_defense` 用于对抗多个服务器线程试图在同一时间缓存同一文件时的竞态条件。 |

## 移除 APC

如果你安装 APC 后不再需要它，可以遵循这些简单步骤将其从你的 PHP 安装中移除。

首先，在 `php.ini` 文件中查找并删除 `extension="apc.so"` 行。或者，你可以只将其注释掉：

```ini
;extension="apc.so"
```

此时，你可以重启 Apache，APC 将不再在 PHP 中激活。如果你想要彻底从机器上清除 DSO，可以在 Apache 重启后删除 PHP 扩展目录中的 `apc.so` 文件。

## eAccelerator

eAccelerator 是另一个编译状态 PHP 缓存引擎，类似于 APC。eAccelerator 是流行的 PHP4 TurckMMCache 缓存引擎的分支，是一个免费的编码器和优化器，目前由 Frank Alcantara 和 SourceForge 程序员团队维护。

除了作为 PHP 优化器和缓存引擎外，你还可以使用 eAccelerator 对你的 PHP 脚本进行编码，这样你可以将编码后的版本重新分发到安装了 eAccelerator 的客户端，而不用担心源代码被窥探。

> 与其他 PHP 编码解决方案一样，当文件使用 eAccelerator 编码时，几乎不可能使用标准工具对其进行解密。然而，可以使用 PHP 引擎本身的调试器和反汇编器进行逆向工程，但通常这种努力并不值得可能的回报。

## 安装 eAccelerator

与 APC 一样，eAccelerator 可以作为一个 DSO 安装，使用以下过程。首先，下载源代码副本，可在 http://eaccelerator.net/ 获取。

> 不幸的是，目前 eAccelerator 与 PHP 的 CGI 二进制版本不兼容。如果你运行 CGI 二进制版本，本节仅作为参考信息。

解压你下载的 tarball，然后进入新创建的目录：

```bash
tar -xvzf eaccelerator-0.9.3.tar.gz
cd eaccelerator-0.9.3
```

在此目录中运行你的 phpize 副本（再次，相应更改路径）：

```bash
/usr/local/bin/phpize
```

然后，配置源代码并构建二进制文件：

```bash
./configure \
--enable-eaccelerator=shared \
--with-php-config=/usr/local/bin/php-config
make
```

构建完成后，以 root 身份安装 DSOs：

```bash
make install
```

接下来，你需要为 eAccelerator 放置临时文件提供一个位置。在 /tmp 文件夹中创建一个 eaccelerator 目录：

```bash
mkdir /tmp/eaccelerator
chmod 0777 /tmp/eaccelerator
```

最后，将以下内容添加到 php.ini，然后重启 Apache：

```ini
extension="eaccelerator.so"
```

## 配置 eAccelerator

与 APC 类似，默认选项在大多数情况下可能就足够了，但如果不足，你可以访问以下 php.ini 指令：

