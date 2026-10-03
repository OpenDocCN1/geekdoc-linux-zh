
- `variables_order = 'GPCS'`: `variables_order` 通常包含环境变量——即生成 `$ENV` 变量设置为 `GPCS`。这仅是出于性能考虑，如果你仍然需要访问变量，可以使用 `getenv()` 函数。

- `allow_call_pass_reference = off`: 此指令可能不会影响所有代码，但它可以防止你的代码在未来的 PHP 版本中过时。`allow_call_pass_reference = off` 禁止强制通过引用传递函数参数。如果你在设置为 `off` 时通过引用传递参数（使用 `&` 前缀），将生成警告。虽然目前对生产服务器不是关键问题，但使用标准的 PHP 标签以确保与未来的版本兼容是很好的做法。

- `asp_tags = off`: 将应用程序迁移到 `asp_tags` 设置不同的服务器时，asp 类型标签（`<?php ?>`）可能会出现问题。虽然这在大多数设置中不正常，但在开发期间将 `asp_tags` 设置为 `off` 是一个好主意，以避免兼容性问题。

- `short_open_tag = off`: 与将 `asp_tags` 设置为 `off` 一样，将 `short_open_tag` 设置为 `off` 也能确保你的应用程序在不同的服务器上通用，而不会因为简单的配置差异而损坏。

如果你可以使用 `<?xml?>` 语句或 XML 文档开头，那么使用 `short_open_tag = off` 有另一个益处。如果 `short_open_tag` 被设置为 `on` 且你尝试使用 `<?xml`，它将尝试将 `<??` 括号内的任何内容作为 PHP 解析，然后抛出错误。

`zlib.output_compression = on`: 将 `zlib.output_compression` 设置为 `on` 可以使用 zlib 库在向终端发送数据之前压缩输出数据。这与在 Apache 中使用 `mod_gzip` 或 `mod_deflate` 的效果类似：减少了输出字节，从而缩短了互联网传输时间。

## 新 PHP5

除了 PHP5 中引入了极大改进的对象外，还增加了一些新的配置设置。PHP5 新增的内容包括：

- `mail_force_extra_parameters`
- `register_long_arrays`
- `session.hash_function`
- `session.hash_bits_per_character`
- `zend.zend_compatibility_mode`

后续章节描述了这些新指令。

## mail_force_extra_parameters

该指令允许你在调用 `mail()` 函数时，指定传递给 Sendmail 的特定值。通常使用 `mail()` 函数时，你可以传递第五个参数来为 Sendmail 设置额外的命令行参数。当设置此指令时，`mail()` 第五个参数中指定的任何 Sendmail 命令行参数都会被 `mail_force_extra_parameters` 设置的值自动覆盖。

> 在发送邮件时，`mail_force_extra_parameters` 设置的任何值始终有效——在安全模式下，`mail()` 的第五个参数是不允许使用的。

## register_long_arrays

当网站上提交表单时，PHP 会获取表单每个字段的值，并将它们放在两个大数组中，根据表单的方法（GET 或 POST）命名。如果表单通过 GET 提交，则数组 `$_GET_VARS` 将填充了这些值，每个字段在数组中都有一个对应的命名索引，此外还有一个名为 `$_GET` 的相同数组，具有相同的值。这种重复主要是为了向后兼容——超全局变量 `$_GET` 和 `$_POST` 直到 PHP 4.1.0 才引入，因此许多旧应用程序仍使用旧的 `$_HTTP_VARS` 数组。

如果你的应用程序完全不使用旧风格的数组，出于性能考虑，你应该将其设置为 `off`。

# 第 5 章

## session.hash_function

在过去，当 PHP 为用户创建新的 session 和 session ID 时，你无法控制使用哪种算法来创建 session。通过 `session.hash_function`，你可以在用于创建 session 的两种哈希算法之间进行选择。

将其设置为 0 告诉 PHP 使用 MD5 对 session ID 进行哈希处理（128 位）。如果你想使用 SHA-1（160 位），则将值设置为 1。

## session.hash_bits_per_character

为了配置 session ID，你可以使用 `session.hash_bits_per_character` 来指定在将 session ID 转换为可读值时，session ID 的每个字符中存储多少位。选项如下：

- 4: 0-9

## zend.zend_compatibility_mode

最后一个新配置设置 `zend.zend_compatibility_mode` 仅用于指定你想要不要启用与 Zend Engine 1 (PHP4) 的兼容性。

## 运行时的 PHP 配置

直接检查和更改 `php.ini` 中指令的设置通常是监控和修改安装的一种快速简便的解决方案，但许多时候你无法停止服务器来做出更改，或者你需要在脚本运行时知道某项设置。本章这部分的技巧将帮助你在服务器仍在运行时进行修改。

## 获取当前运行时设置

如果你需要知道已安装的 PHP 精确版本，PHP 提供了 `phpversion()` 函数，它返回一个字符串列表，告知完整的安装版本信息。例如：

```php
<?php
echo "The current version of PHP installed is: " . phpversion();
?>
```

这将输出类似以下的内容：

The current version of PHP installed is: 5.0.4

## 获取配置设置

有时，简单的版本检查提供的信息是不够的，你需要更多关于 PHP 配置方式的细节，但你又无法直接访问 `php.ini`。要查找运行时配置设置，你有三个选择：`ini_get()`、`get_cfg_var()` 和 `ini_all()`。

第一个选项 `ini_get()` 检查字符串与当前的运行时配置。如果设置匹配，它会返回该设置的值；如果未找到匹配项，则返回一个空字符串：

```php
<?php
echo "Error reporting: " . ini_get('error_reporting') . "\n";
echo "Register globals: " . ini_get('register_globals') . "\n";
echo "Nonexistent setting: " . ini_get('nonexistent') . "\n";
?>
```

运行此代码将产生类似下面的输出：

```
Error reporting: 2047
Register globals:
Nonexistent setting:
```

注意，error reporting 的值实际上是常量 `E_ALL` 对应的数值等效值。但 `register_globals` 的值呢？当 `ini_get()` 返回 `php.ini` 认为是布尔值（或 0 或 1，是的）时，它会自动进行转换。任何 "off" 或 "no" 的值会自动转换为 "0"；任何 "yes" 或 "on" 的值会自动转换为 "1"。获取配置设置的第二个选项 `get_cfg_var()` 行为与 `ini_get()` 相同，不同之处在于直接从 `php.ini` 获取值，而不是从当前的运行时环境。除非你在代码中（或之后）更改了变量，否则返回的值与 `ini_get()` 返回的相同。例如，以下代码：

```php
<?php
echo "Error reporting: " . get_cfg_var('error_reporting') . "\n";
echo "Register globals: " . get_cfg_var('register_globals') . "\n";
echo "Nonexistent setting: " . get_cfg_var('nonexistent') . "\n";
?>
```

除非在活动脚本中更改了某个设置，否则此代码产生的输出与以下相同：

```php
<?php
echo "Error reporting: " . ini_get('error_reporting') . "\n";
echo "Register globals: " . ini_get('register_globals') . "\n";
echo "Nonexistent setting: " . ini_get('nonexistent') . "\n";
?>
```

# 第 5 章

获取配置信息的第三种方法 `ini_all()` 行为类似于 `ini_get()`。由于不是指定单个值，`ini_all()` 返回一个包含所有设置的数组。看这个示例：

```php
<?php
print_r(ini_all());
?>
```

执行它，你将得到类似下面的的内容：

```
Array(
    [allow_urlinclude] => Array(
        [global_value] => 
        [local_value] => 
    )
    [always_populate_post_data] => Array(
        [global_value] => 0
        [local_value] => 0
    )
    [arg_separator.input] => Array(
        [global_value] => &
        [local_value] => &
    )
...
```

此输出已经经过大幅缩减——实际返回的数组有 150 项。此外注意，`allow_urlinclude` 的全局和本地值为空字符串。当 `ini_all()` 返回每个设置时，它使用了 `ini_get()` 执行的 off/on 取值转换。

## PHP 配置

现在你已经获取运行时设置的信息，是时候学习如何检查扩展及其属性了。PHP 提供了三个内置函数来查找已加载的扩展。

第一个 `extension_loaded()` 仅检查给定的扩展是否加载。你只需要提供扩展的名称，它将返回一个指示其是否用的布尔值。

```php
<?php
if (extension_loaded('mysql'))
{
    echo "MySQL is available.\n";
} else {
    echo "MySQL is NOT available.\n";
}
if (extension_loaded('fakesql'))
{
    echo "Fake SQL is available.\n";
} else {
    echo "Fake SQL is NOT available.\n";
}
?>
```

运行此代码时，你应该看到：

MySQL is available.

Fake SQL is NOT available.

如果你需要一次知道多个扩展的状态，PHP 给了你 `get_loaded_extensions()`。像 `ini_all()` 一样，`get_loaded_extensions()` 返回已加载扩展的数组。考虑以下代码：

```php
<?php
print_r(get_loaded_extensions());
?>
```

根据你当前的设置，这应该产生类似下面的输出，可能多出几个扩展：

```
Array(
    [0] => xml
    [1] => tokenizer
    [2] => standard
    [3] => SQLite
    [4] => SPL
    [5] => sockets
    [6] => SimpleXML
    [7] => session
    [8] => posix
    [9] => pgsql
    [10] => pcre
    [11] => mysqli
    [12] => mysql
    [13] => iconv
    [14] => gd
    [15] => exif
    [16] => dom
    [17] => ctypes
    [18] => calendar
    [19] => bz2
    [20] => bcmath
    [21] => zlib
    [22] => openssl
    [23] => libxml
)
```

一旦知道某个扩展可用，你可能想进一步了解该特定模块。要获取扩展提供的所有函数列表，请使用 `get_extension_funcs()`。与之前的某些信息通道不同，它返回一个可用值的数组，在这种情况下，它提供的是给定扩展的函数列表。例如：

```php
<?php
print_r(get_extension_funcs('simplexml'));
?>
```

运行这段代码将为你提供 SimpleXML 扩展提供的所有函数列表：

```
Array
(
    [0] => simplexml_load_file
    [1] => simplexml_load_string
    [2] => simplexml_import_dom
)
```

# 魔幻引号 (Magic Quotes)

如本章节前面提到的，PHP 允许一种特殊数据处理机制“魔幻引号”。启用引号时，PHP 会自动转义任何特殊字符——单引号、双引号、NULL——在它们前面加上反斜杠，以防止在数据库中使用字符串时出现问题。

PHP 实际上有两个自动转义字符串的地方：来自 Web 表单或请求的输入数据，或者来自任何返回数据的函数的自动处理。每个替换都由自己的

## PHP 配置

输入数据的自动转义由 `magic_quotes_gpc` 指令控制，而任何函数的转义由 `magic_quotes_runtime` 设置控制。

由于这些可能会“污染”你数据的关键操作，PHP 提供了函数来快速确定每个设置当前的状态：`get_magic_quotes_gpc()` 用于输入数据，`get_magic_quotes_runtime()` 用于函数处理器。这两个函数都不需要参数，如果设置已启用则返回 1，如果禁用则返回 0。运行这个：

```php
<?php
echo "Magic quotes GPC: " . get_magic_quotes_gpc() . "\n";
echo "Magic quotes runtime: " . get_magic_quotes_runtime() . "\n";
?>
```

根据你当前的配置，你将看到类似的内容：

Magic quotes GPC: 0

Magic quotes runtime: 0

## 动态更改配置

现在可以在代码中实时检查配置设置和扩展属性，但如果某些地方你不满意，该怎么办？通过一些内置 PHP 函数，你可以改变 PHP 在某些情况下的行为。

## 并不那么魔幻的引号

如果你和我一样，你不喜欢 `magic_quotes_runtime` 被启用，因为它破坏了每个函数的输出。虽然这可以被视为一种便利，但它通常只会产生干扰，并迫使你到处使用 `stripsslashes()` 或 `addslashes()`。要更改它，你可以使用 `set_magic_quotes_runtime()`。参数 "1" 开启自动替换；值 "0" 则关闭：

```php
<?php
// 开启 magic_quotes_runtime
set_magic_quotes_runtime(1);

// 关闭 magic_quotes_runtime
set_magic_quotes_runtime(0);
?>
```

遗憾的是，`magic_quotes_gpc` 的情况并非如此——你不能在运行时更改它的值（稍后讨论）。

## 移除时间限制

如果你发现脚本运行时间略微超过了 PHP 允许的范围，你有两个选择：优化你的代码让它运行更快，或者告诉 PHP 更有耐心一点。也许你已经尽可能地优化了代码，但默认的 30 秒超时仍然太快了。

113

# 第 5 章

是时候让 PHP 在超时之前多等一会儿了。要做到这一点，你使用 `set_time_limit()`，只需指定你的脚本允许运行的秒数即可：

```php
<?php
// 设置超时时间为分钟
set_time_limit(60);
?>
```

如果你无法准确判断脚本需要多长时间，并且完全确定你没有无限循环，你可以通过将值设置为零来完全移除超时：

```php
<?php
// 如果不小心，它将永远运行
set_time_limit(0);
?>
```

当你使用 `set_time_limit()` 时，有两点需要记住。首先，如果你的服务器在安全模式下运行 PHP，使用 `set_time_limit()` 将不起作用。你必须禁用安全模式，或者更改 `php.ini` 中的全局值。其次，无论调用 `set_time_limit()` 时，都会将内部计时器重置为 0。如果你的脚本运行了 15 秒，而你将超时时间设置为 20 秒，它不会在 5 秒后退出——它会将计数器重置为 0 并重新计算 20 秒。

配置检查器中的下一个文件是 `class.ConfigManager.php`，它是脚本的中央控制点：
