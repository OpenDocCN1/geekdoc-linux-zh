
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

如本章前面所述，PHP 允许一种称为“魔术引号”的特殊数据处理机制。当启用魔术引号时，PHP 会自动转义任何特殊字符——单引号、双引号、NULL——通过在它们前面添加反斜杠，以防止在数据库中使用字符串时出现问题。

实际上，PHP 可以在两个地方自动转义字符串：来自 Web 表单或请求的输入数据，或者来自任何返回任何数据的函数的自动转义。每个替换操作都由其自身的配置指令控制。输入数据的自动转义由 `magic_quotes_gpc` 指令控制，而任何函数的转义则由 `magic_quotes_runtime` 设置控制。

由于这两者都是关键操作，如果忽视可能会导致数据“污染”，PHP 提供了两个函数来快速确定每个设置的当前状态：`get_magic_quotes_gpc()` 用于输入数据，`get_magic_quotes_runtime()` 用于函数处理。这两个函数都不需要参数，如果设置已启用则返回 1，如果禁用则返回 0。运行这段代码：

```php
<?php

echo "Magic quotes GPC: " . get_magic_quotes_gpc() . "\n"
     "Magic quotes runtime: " . get_magic_quotes_runtime() . "\n";

?>
```

根据你的当前配置，你会看到类似以下内容：

```
Magic quotes GPC: 0
Magic quotes runtime: 0
```

## 动态更改配置

你现在可以在代码中实时检查配置设置和扩展属性，但如果某些地方不符合你的喜好，你会怎么做？通过一些内置的 PHP 函数，你可以更改 PHP 在某些情况下的行为。

### 不那么神奇的引号

如果你像我一样，可能不喜欢启用 `magic_quotes_runtime`，因为它会破坏所有函数的输出。虽然它可以被视为一种便利，但通常它只会碍事，并迫使你到处使用 `stripslashes()` 或 `addslashes()`。要更改此设置，可以使用 `set_magic_quotes_runtime()`。参数“1”开启自动替换；值“0”关闭它：

```php
<?php

// Turn on magic_quotes_runtime
set_magic_quotes_runtime(1);

// Turn off magic_quotes_runtime
set_magic_quotes_runtime(0);

?>
```

不幸的是，对于 `magic_quotes_gpc` 不能这么说——你不能在运行时更改其值（这一点稍后会有更多说明）。

### 移除时间限制

如果你发现自己处于脚本运行时间稍长于 PHP 允许的情况，你有两个选择：优化代码使其更快，或者告诉 PHP 更有耐心一些。也许你已经尽可能优化了代码，但默认的 30 秒超时仍然太快了。

是时候让 PHP 在超时之前再等待一会儿了。要做到这一点，使用 `set_time_limit()`，并简单指定允许脚本运行的秒数：

```php
<?php

// Set the timeout at one minute
set_time_limit(60);
?>
```

如果你无法准确猜测脚本需要多长时间，并且绝对确定没有无限循环，你可以通过将值设置为零来完全移除超时：

```php
<?php

// Will run forever if you're not careful
set_time_limit(0);
?>
```

当你使用 `set_time_limit()` 时，有两件事需要注意。首先，如果你的服务器在安全模式下运行 PHP，使用 `set_time_limit()` 将不起作用。你必须禁用安全模式，或者更改 `php.ini` 中的全局值。其次，每当调用 `set_time_limit()` 时，它会内部计时器重置为 0。如果脚本已运行了 15 秒，你将超时设置为 20 秒，它不会在再 5 秒后退出——它将计数器重置为 0，并重新计数 20 秒，总共 35 秒。

### 更改指令

如果你只想更改任何随机的运行时配置设置怎么办？要做到这一点，可以使用函数 `ini_set()`。使用 `ini_set()`，只需传入设置名称和新值即可。如果函数成功，它将返回旧值；如果不成功，它将返回 `false`。运行这段代码：

```php
<?php

echo "Setting error_reporting to E_STRICT...\n";

$old = ini_set('error_reporting', E_STRICT);

echo "Old value was: " . $old . "\n";
?>
```

你应该看到以下内容：

```
Setting error_reporting to E_STRICT...
Old value was: 2047
```

如果你决定不再想要更改后的值，可以使用 `ini_restore()` 来恢复脚本开始执行时的原始值：

```php
<?php

echo "Setting error_reporting to E_STRICT...\n";

$old = ini_set('error_reporting', E_STRICT);

echo "Old value was: " . $old . "\n" .
        "New value is: " . ini_get('error_reporting') . "\n";

ini_restore('error_reporting');

echo "The value is once again: " . ini_get('error_reporting') . "\n";

?>
```

这次运行代码时，它应该能成功恢复旧值：

```
Old value was: 2047
New value is: 2048
The value is once again: 2047
```

在你开始随意更改设置之前，你需要意识到在脚本执行期间可以更改的设置是有限制的。如果你还记得之前展示 `ini_get_all()` 时，每个配置指令的数组返回了三个值：

```
... 
[allow_call_time_pass_reference] => Array
    (
        [global_value] =>
        [local_value]  =>
        [access]   => 6
    )
...
```

第三个值 `access` 指示该配置指令实际可以在哪里更改。提供给 `access` 的数字实际上是以下任何值的总和：

| 值 | 含义 |
| :--- | :--- |
| 1 | 该指令可以在用户脚本中设置。 |
| 2 | 该指令可以在 php.ini、.htaccess 或 httpd.conf 中设置。 |
| 4 | 该指令可以在 php.ini 或 httpd.conf 中设置。 |
| 7 | 该条目可以在任何地方设置。 |

在上面的示例中，`allow_call_time_pass_reference` 的 access 值为 6，意味着该指令只能在 `php.ini`、`.htaccess` 或 `httpd.conf` 中更改。需要记住的关键点是，如果设置的 access 值为 2、4 或 6，则不能在脚本执行期间更改。任何此类尝试都会自动返回 `false`。

