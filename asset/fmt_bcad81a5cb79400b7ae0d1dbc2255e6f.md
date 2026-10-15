
> The current version of PHP installed is: 5.0.4

### 检索配置设置

有时候，简单的版本检查提供的信息不够，你需要更多关于 PHP 配置方式的信息，但你无法直接访问 `php.ini`。要查找运行时配置设置，你有三个主要选择：`ini_get()`、`get_cfg_var()` 和 `ini_get_all()`。

第一个选项 `ini_get()` 将给定字符串与当前运行时配置进行检查。如果设置匹配，则返回该设置的值；如果未找到匹配项，则返回空字符串：

```php
<?php
echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     "Nonexistant setting: " . ini_get('nonexistant') . "\n";
?>
```

运行此代码应产生类似以下内容的输出：

```
Error reporting: 2047
Register globals:
Nonexistant setting:
```

请注意，在这种情况下，错误报告的值实际上是常量 `E_ALL` 的数值等价物。但 `register_globals` 的值在哪里呢？当 `ini_get()` 返回 `php.ini` 认为的布尔值（`off` 或 `on`，`0` 或 `1`，`yes` 或 `no`）时，它会自动转换它们。任何“off”或“no”的值自动转换为“0”；任何“yes”或“on”的值自动变为“1”。

检索配置设置的第二个选项 `get_cfg_var()` 的行为与 `ini_get()` 几乎相同，除了它直接从 `php.ini` 拉取值，而不是当前的运行时环境。除非你在代码中更改了配置变量（稍后会有更多说明），否则值通常应与 `ini_get()` 返回的值匹配。例如，请考虑以下代码：

```php
<?php
echo 'Error reporting: ' . get_cfg_var('error_reporting') . "\n" .
     'Register globals: ' . get_cfg_var('register_globals') . "\n" .
     "Nonexistant setting: " . get_cfg_var('nonexistant') . "\n";
?>
```

除非某个设置在活动脚本中被更改，否则此代码将产生与以下内容相同的输出：

```php
<?php
echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     "Nonexistant setting: " . ini_get('nonexistant') . "\n";
?>
```

获取配置信息的第三种方法 `ini_get_all()` 像放大版的 `ini_get()`。它不再指定单个值来查找，而是 `ini_get_all()` 返回一个包含所有已注册配置选项的数组。它返回的值也不仅限于当前设置——`ini_get_all()` 返回在 `php.ini` 中设置的全局值、当前时刻存在的本地值以及更改设置所需的访问级别。

看看这个简单的例子：

```php
<?php
print_r(ini_get_all());
?>
```

执行此代码，你会得到类似以下内容的结果：

```
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
)
```

请注意，此输出已被大幅简略——实际返回的数组包含超过 150 个不同的项。另外请注意，某些值是空字符串，例如 `allow_call_time_pass_reference` 的全局和本地值。当 `ini_get_all()` 返回每个设置时，它使用与 `ini_get()` 执行的值转换相同的方式，涉及 `off`/`on` 值。

## 扩展信息

既然你已经能够获取关于运行时设置的信息，现在是时候学习如何检查扩展及其属性了。PHP 为你提供了三个内置函数来查找已加载扩展的相关信息。

第一个函数是 `extension_loaded()`，它仅用于检查给定的扩展是否已加载。你只需提供扩展的名称，它会返回一个布尔值，指示该扩展是否可用，如下所示：

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

当你运行这段代码时，你应该会看到以下内容：

```
MySQL is available.
Fake SQL is NOT available.
```

如果你需要同时了解多个扩展的状态，PHP 提供了 `get_loaded_extensions()`。与 `ini_get_all()` 类似，`get_loaded_extensions()` 返回一个包含所有已加载扩展的数组。请考虑以下代码：

```php
<?php

print_r(get_loaded_extensions());

?>
```

根据你的当前配置，这应该会产生类似以下的输出（可能或多或少有几个扩展）：

```
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
    [9] => pgsasl
    [10] => pcre
    [11] => mysql
    [12] => mysqli
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

一旦你知道某个扩展可用，你可能希望了解更多关于该特定模块的信息。要获取扩展提供的所有函数的列表，请使用 `get_extension_funcs()`。与之前的一些信息性命令类似，它返回一个可用值的数组，但在这种情况下，它提供的是给定扩展的函数列表。例如：

```php
<?php
print_r(get_extension_funcs('simplexml'));
?>
```

运行这段代码应该给出 SimpleXML 扩展提供的所有函数列表：

```
Array
(
    [0] => simplexml_load_file
    [1] => simplexml_load_string
    [2] => simplexml_import_dom
)
```

## 魔术引号
