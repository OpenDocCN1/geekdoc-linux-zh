
```text
The current version of PHP installed is: 5.0.4
```

## 检索配置设置

有时，简单的版本检查信息不够，你需要更多关于 PHP 配置方式的信息，但你无法直接访问 `php.ini`。要查找运行时配置设置，你有三个主要选择：`ini_get()`、`get_cfg_var()` 和 `ini_get_all()`。

第一个选项 `ini_get()`，将给定的字符串与当前运行时配置进行检查。如果设置匹配，则返回该设置的值；如果未找到匹配项，则返回空字符串：

```php
<?php
echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     'Nonexistent setting: ' . ini_get('nonexistent') . "\n";
?>
```

运行此代码应产生类似以下的输出：

```text
Error reporting: 2047
Register globals:
Nonexistent setting:
```

请注意，在这种情况下，错误报告的值实际上是常量 `E_ALL` 的数值等效值。但是 `register_globals` 的值在哪里呢？当 `ini_get()` 返回 `php.ini` 认为是布尔值（off 或 on，0 或 1，yes 或 no）时，它会自动转换它们。“off” 或 “no” 的值会自动转换为 “0”；“yes” 或 “on” 的值会自动变为 “1”。

检索配置设置的第二个选项 `get_cfg_var()`，其行为与 `ini_get()` 几乎相同，只是它直接从 `php.ini` 获取值，而不是来自当前运行时环境。除非你在代码中更改了配置变量（稍后详细介绍），否则值通常应与 `ini_get()` 返回的值匹配。例如，以下代码：

```php
<?php
echo 'Error reporting: ' . get_cfg_var('error_reporting') . "\n" .
     'Register globals: ' . get_cfg_var('register_globals') . "\n" .
     'Nonexistent setting: ' . get_cfg_var('nonexistent') . "\n";
?>
```

除非设置已在活动脚本中更改，否则此代码将产生与以下代码相同的输出：

```php
<?php
echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     'Nonexistent setting: ' . ini_get('nonexistent') . "\n";
?>
```

获取配置信息的第三种方式 `ini_get_all()`，像放大版的 `ini_get()`。它不是指定单个值来查找，而是返回一个包含所有已注册配置选项的数组。其返回值也不仅仅限于当前设置——`ini_get_all()` 返回在 `php.ini` 中设置的全局值、当前时刻存在的局部值，以及更改该设置所需的访问级别。

看看这个简单的例子：

```php
<?php
print_r( ini_get_all() );
?>
```

执行此代码，你会得到类似以下的输出：

```text
Array
(
    [allow_call_time_pass_reference] => Array
        (
            [global_value] =>
            [local_value] =>
            [access] => 6
        )

    [allow_url_fopen] => Array
        (
            [global_value] => 1
            [local_value] => 1
            [access] => 4
        )

    [always_populate_raw_post_data] => Array
        (
            [global_value] => 0
            [local_value] => 0
            [access] => 6
        )

    [arg_separator.input] => Array
        (
            [global_value] => &
            [local_value] => &
            [access] => 6
        )

    ...
```

请注意，此输出已大幅简略——实际返回的数组包含超过 150 个不同的项目。还要注意，一些值是空字符串，例如 `allow_call_time_pass_reference` 的全局值和局部值。当 `ini_get_all()` 返回每个设置时，对于 off/on 值，它使用与 `ini_get()` 执行相同的值转换。

# 第 5 章

## 扩展信息

既然你已经能够获取有关运行时设置的信息，现在是时候学习如何检查扩展及其属性了。PHP 提供了三个内置函数来查找已加载扩展的信息。

第一个是 `extension_loaded()`，它简单地检查给定的扩展是否已加载。你只需提供扩展的名称，它就会返回一个布尔值，指示该扩展是否可用，如下所示：

```php
<?php
if (extension_loaded('mysql'))
{
    echo "MySQL is available.\n";
}
else
{
    echo "MySQL is NOT available.\n";
}

if (extension_loaded('fakesql'))
{
    echo "Fake SQL is available.\n";
}
else
{
    echo "Fake SQL is NOT available.\n";
}
?>
```

运行此代码时，你应该看到以下内容：

MySQL is available.

Fake SQL is NOT available.

如果你需要一次知道多个扩展的状态，PHP 提供了 `get_loaded_extensions()`。与 `ini_get_all()` 类似，`get_loaded_extensions()` 返回所有已加载扩展的数组。考虑以下代码：

```php
<?php
print_r(get_loaded_extensions());
?>
```

根据你的当前配置，可能会增减几个扩展，这应该会生成类似以下的输出：

```text
Array
(
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
    [17] => ctype
    [18] => calendar
    [19] => bz2
    [20] => bcmath
    [21] => zlib
    [22] => openssl
    [23] => libxml
)
```

一旦你知道某个扩展可用，你可能想了解该特定模块的更多详细信息。要获取某扩展提供的所有函数列表，请使用 `get_extension_funcs()`。与前一些信息性命令一样，它返回一个可用值的数组，但在这种情况下，它提供的是给定扩展的函数列表。例如：

```php
<?php

print_r(get_extension_funcs('simplexml'));

?>
```

运行这段代码应该给出 SimpleXML 扩展提供的所有函数列表：

```text
Array
(
    [0] => simplexml_load_file
    [1] => simplexml_load_string
    [2] => simplexml_import_dom
)
```

## 魔术引号
