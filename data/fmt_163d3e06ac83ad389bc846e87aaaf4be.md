
| `$JPCACHE_DIR` | `/tmp/jpcache` | JPCache 存储其基于文件的缓存数据的目录由这个变量设置。JPCache 存储缓存文件的位置需要由 Apache 进程用户可写。 |
| `$JPCACHE_FILEPREFIX` | `jpc-` | 当 JPCache 在磁盘缓存中创建缓存文件时，它可以使用在此指定的文件名前缀，以避免与现有文件冲突。 |
| `$JPCACHE_DB_HOST` | `localhost` | 当使用数据库作为缓存存储位置时，您需要为 JPCache 设置用于连接和使用数据库的变量。此变量设置 JPCache 将连接的数据库主机。 |
| `$JPCACHE_DB_DATABASE` | `jpache` | 此变量设置存储缓存数据的 MySQL 数据库的名称。 |
| `$JPCACHE_DB_USERNAME` | `sqluser` | 要设置存储数据库中的缓存信息时使用的用户名，请设置 `$JPCACHE_DB_USERNAME`。 |
| `$JPCACHE_DB_PASSWORD` | `passwd` | 与 `$JPCACHE_DB_USERNAME` 配合使用，此变量设置数据库连接密码。 |
| `$JPCACHE_DB_TABLE` | `CACHEDATA` | JPCache 缓存数据存储在 `$JPCACHE_DB_TABLE` 指定的表中。要创建表，您可以在 MySQL Monitor 或您首选的 MySQL 管理工具中执行以下命令： `CREATE TABLE CACHEDATA ( CACHEKEY varchar (255) NOT NULL, CACHEEXPIRATION int(11) NOT NULL, GZDATA blob, DATASIZE int (11), DATACRC int (11), PRIMARY KEY (CACHEKEY) )` 当然，您需要更改数据库表的名称以匹配您在 `$JPCACHE_DB_TABLE` 中指定的值，反之亦然。 |
| `$JPCACHE_OPTIMIZE` | 1 (执行 OPTIMIZE TABLE) | 垃圾回收周期完成后，您可以指示 JPCache 对 `$JPCACHE_DB_TABLE` 中指定的表执行自动的 MySQL OPTIMIZE TABLE 命令。 |

### 移除 JPCache

要移除 JPCache，您需要搜索所有 PHP 脚本并删除任何对 `jpcache.php` 文件的 `include` 或 `require` 引用。删除引用后，您可以安全地删除 JPCache 目录。

有关 JPCache 的更多信息，请访问 `http://www.jpcache.com`。

## memcached

与 APC、e_Accelerator 和 JPCache 提供的输出缓存系统不同，memcached 系统依赖于后端对象的缓存来提供速度提升。memcached 是由 Danga Interactive（负责 LiveJournal.com 的团队）创建的一个分布式内存对象缓存系统。memcached 不缓存页面输出或编译后的 PHP 操作码，而是缓存各种代码对象，最重要的是数据库结果对象和数据模型实体。

这种缓存解决方案与本章节中的其他系统略有不同——memcached 实际上需要始终运行其自身的守护进程。然后，PHP 可以使用其 memcached 函数集来访问和使用内存对象缓存。

### 安装 memcached

要安装 memcached，首先从 `http://www.danga.com/memcached/` 获取守护进程源代码的副本。

然后解压缩 tar/gzip 归档文件，并更改目录到新创建的文件夹：

```bash
tar -xvzf memcached-1.1.12.tar.gz
cd memcached-1.1.12
```

接下来配置和构建源代码。如果 configure 报告任何缺失的库（例如 libevent），请根据各自的说明下载并安装它们；然后重新运行 configure 脚本，再构建 memcached。

```bash
./configure
make
```

然后，以 root 身份安装 memcache 守护进程：

```bash
make install
```

最后您需要做的是实际启动守护进程。以下命令使用 128MB 内存启动守护进程，在 IP 127.0.0.1 上监听端口 11211：

```bash
/usr/local/bin/memcached -d -m 128 -l 127.0.0.1 -p 11211
```

## 缓存引擎

如果你决定永久使用 memcached，请确保将启动 memcached 的命令添加到你偏好的启动设施或脚本中，以便机器每次启动时都能自动加载。

现在，既然 memcached 守护进程已经运行，你需要准备 PHP 以使用该缓存系统。请从 `http://pecl.php.net/package/memcache` 下载 memcached PECL 模块。

解压归档文件并进入新目录：

```
tar -xzvf memcache-1.4.tgz
cd memcache-1.4
```

运行 `phpize`，然后配置并编译 DSO：

```
phpize
./configure
make
```

以 root 用户身份安装该模块：

```
make install
```

最后，将以下行添加到你的 php.ini 中，并重启 Apache：

```
extension="memcache.so"
```

### 使用 memcached

为了使用 memcached，你安装的 PHP DSO 为 Memcache 对象提供了以下方法：

- `Memcache::add`

  `bool Memcache::add ( string key, mixed var [, int flags [, int expire]] )`

  此方法将一个变量或对象添加到内存缓存中，由标记 `key` 标识。如果内存缓存中已经存在具有相同 `key` 的值，则返回 `FALSE`。如果你希望在将值放入内存缓存之前对其进行压缩，请提供 `MEMCACHE_COMPRESSED` 作为标志，否则可以省略或设置为 0。为 `expire` 提供的任何值都告诉 memcached 何时应该从缓存中移除该项。`expire` 的值为 0 表示该值应该被无限期缓存。

  只有变量和对象可以存储在内存缓存中，而资源不可以。

- `Memcache::close`

  `bool Memcache::close ( void )`

  此方法关闭与 memcached 服务器的任何非持久连接。如果在关闭连接时发生错误，则返回 `FALSE`。

- `Memcache::connect`

  `bool Memcache::connect ( string host [, int port [, int timeout]])`

  此方法创建并打开到运行在 host 上的 memcached 服务器的连接。port 参数指定 memcached 使用的 TCP 端口，默认为 11211，而 timeout 指定在尝试连接时等待多长时间才返回 FALSE。成功时返回 true，失败时返回 FALSE。

- `Memcache::decrement`

  `int Memcache::decrement ( string key [, int value])`

  当在内存缓存中存储简单数值时，你可以实际使用 decrement() 方法将通过 key 匹配的值减少指定的 value。如果未指定递减值，则缓存的值减少 1。此方法在失败时返回 FALSE，或在成功时返回该项的新值。

- `Memcache::delete`

  `bool Memcache::delete (string key [, int timeout])`

  此方法从内存缓存中删除由 key 标识的项。为 timeout 提供值会导致该项在指定的秒数后被删除。失败时返回 FALSE，成功时返回 TRUE。

- `Memcache::flush`

  `bool Memcache::flush ( void )`

  此方法告诉 memcached 立即设置缓存中所有项的过期时间。一旦调用此方法，缓存中的任何项都可以被新键覆盖，但在发生这种情况之前，内存不会被释放。此方法在成功时返回 TRUE，或在失败时返回 FALSE。

- `Memcache::get`

  `string Memcache::get ( string key )`

  `string Memcache::get ( array keys )`

  此方法检索存储在内存缓存中的项或各项，与给定的 key 或 key 数组匹配。根据提供的匹配 key 的数量，它在成功时返回字符串或数组，如果未找到匹配输入参数的 key，则返回 FALSE。

- `Memcache::getStats`

  `array Memcache::getStats ( void )`
