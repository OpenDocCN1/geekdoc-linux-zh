
`make install`

最后，将以下行添加到你的 `php.ini` 中，并重启 Apache：

```ini
extension="memcache.so"
```

#### 使用 memcached

为了使用 memcached，你安装的 PHP DSO 为 Memcache 对象提供了以下方法：

- **Memcache::add**

  `bool Memcache::add ( string key, mixed var [, int flag [, int expire]] )`

此方法将一个变量或对象添加到内存缓存中，由 *key* 标识。如果具有相同 *key* 的值已存在于内存缓存中，则返回 *FALSE*。如果你希望在将值放入内存缓存之前对其进行压缩，请将 `MEMCACHE_COMPRESSED` 作为标志提供，否则可以省略或设置为 0。为 *expire* 提供的任何值都告诉 memcached 何时开始允许从缓存中移除该项。*expire* 的值为 0 表示该值应无限期缓存。

> *只有变量和对象可以存储在内存缓存中，而资源则不能。*

- **Memcache::close**

  `bool Memcache::close ( void )`

此方法关闭与 memcached 服务器的任何非持久连接。如果在关闭连接时发生错误，则返回 *FALSE*。

- **Memcache::connect**

  `bool Memcache::connect ( string host [, int port [, int timeout]] )`

此方法创建并打开到运行在 `host` 上的 memcached 服务器的连接。`port` 参数指定 memcached 使用的 TCP 端口，默认为 11211，`timeout` 指定在尝试连接时等待多长时间后返回 FALSE。成功时返回 true，失败时返回 FALSE。

- **Memcache::decrement**

  `int Memcache::decrement ( string key [, int value] )`

当在内存缓存中存储简单的数值时，你实际上可以使用 `decrement()` 方法将匹配 `key` 的值减少所提供的 `value`。如果未指定递减值，则缓存值减 1。此方法在失败时返回 FALSE，成功时返回该项的新值。

- **Memcache::delete**

  `bool Memcache::delete ( string key [, int timeout] )`

此方法从内存缓存中删除由 `key` 标识的项。提供 `timeout` 值会导致该项在提供的秒数后被删除。失败时返回 FALSE，成功时返回 TRUE。

- **Memcache::flush**

  `bool Memcache::flush ( void )`

此方法告诉 memcached 立即设置缓存中所有项的过期时间。一旦调用此方法，缓存中的任何项都可以被新键覆盖，但内存不会释放，直到这种情况发生。此方法在成功时返回 TRUE，在失败时返回 FALSE。

- **Memcache::get**

  `string Memcache::get ( string key )`
  `string Memcache::get ( array keys )`

此方法检索存储在内存缓存中的一项或多项，匹配给定的 `key` 或 `key` 数组。成功时，根据匹配输入参数提供的 `key` 数量，返回字符串或数组；如果没有找到匹配输入参数的 `key`，则返回 FALSE。

- **Memcache::getStats**

  `array Memcache::getStats ( void )`

这返回一个包含有关内存缓存状态各种信息（如当前和总连接数、缓存项数以及服务器正常运行时间）的数组。

- **Memcache::getVersion**

  `string Memcache::getVersion ( void )`

这返回一个包含 memcached 服务器版本号字符串，或者在发生错误时返回 FALSE。

## 缓存引擎

- **Memcache::increment**

  `int Memcache::increment ( string key [, int value ] )`

与 `decrement()` 方法类似，`increment()` 允许你轻松地在内存缓存中直接更改简单的数值——在此情况下，将存储的变量增加 `value`，如果未提供值则增加 1。成功时返回新值，失败时返回 FALSE。

- **Memcache::pconnect**

  `bool Memcache::pconnect ( string host [, int port [, int timeout]] )`

此方法创建并打开到 memcached 服务器的持久连接，类似于 MySQL 持久连接。参数与 `connect()` 相同：`host` 指定 memcached 服务器的主机名或 IP 地址，`port` 指定 memcached 的监听端口，`timeout` 指定连接超时时间。

- **Memcache::replace**

  `bool Memcache::replace ( string key, mixed var [, int flag [, int expire]] )`

此方法在缓存对象中搜索与 `key` 匹配的项，如果找到，则用值 `var` 替换它。与 `add()` 和 `set()` 一样，`replace()` 可以提供标志以请求在存储值时进行压缩，并且还可以为新值提供可选的过期时间。此方法在成功时返回 TRUE，在失败时返回 FALSE。

- **Memcache::set**

  `bool Memcache::set ( string key, mixed var [, int flag [, int expire]] )`

此方法将值 `var` 存储在内存缓存中，即使存在与 `key` 匹配的现有项。参数与 `add()` 和 `replace()` 相同。成功时返回 TRUE，失败时返回 FALSE。

你可以以与 MySQLi 方法类似的方式使用这些方法——你连接到 memcached 服务器，将数据输入缓存并进行处理，然后断开连接。以下简单示例将一个 `Circle` 对象存储在内存缓存中：

```php
<?php

class Circle
{
    public $radius;
    public function area()
    {
        return pi() * pow($this->radius, 2);
    }
}

$memc = new Memcache();
$memc->connect('10.0.0.20', 11211);
$c = new Circle();
$c->radius = 15;
$memc->set('circle1', $c);
$stats = $memc->getStats();
$memc->close();

print_r($stats);
?>
```

如果你运行此脚本，它将打印一个包含当时内存缓存统计信息的数组。如果是你第一次运行该脚本，或者是你服务器上第一次使用 memcached，你的 `curr_items` 值应为 1，反映新添加的 `Circle` 对象。

```text
Array
(
    [pid] => 1379
    [uptime] => 4148
    [time] => 1124758570
    [version] => 1.1.12
    [rusage_user] => 0.030000
    [rusage_system] => 0.010000
    [curr_items] => 1
    [total_items] => 8
    [bytes] => 77
    [curr_connections] => 1
    [total_connections] => 9
    [connection_structures] => 2
    [cmd_get] => 0
    [cmd_set] => 8
    [get_hits] => 0
    [get_misses] => 0
    [bytes_read] => 605
    [bytes_written] => 1856
    [limit_maxbytes] => 134217728
)
```
