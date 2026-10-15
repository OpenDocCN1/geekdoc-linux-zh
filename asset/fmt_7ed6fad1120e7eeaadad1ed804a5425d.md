
在命令参数中放置任何用户提供的信息是非常危险的。用户可能会在表单字段中传递值，从而允许他们在你的 Web 服务器上执行他们自己的命令。如果你这样做，请先通过 `escapeshellcmd` 函数传递信息。

## 示例

```php
<?php
// 创建图片的头部
header("Content-type: image/gif");
passthru("counter");
?>
```

## 相关函数

`exec`, `system`

# `putenv(string variable)`

`putenv` 函数设置环境变量的值。

# Shell 命令

## 示例

```php
<?php
putenv("PATH=/local/bin;.");
?>
```

## 相关函数

`getenv`

# `string system(string command, integer return)`

`system` 函数的行为与 C 语言的 `system` 函数完全一致。它执行命令参数并将输出发送到浏览器。如果提供了 `return` 参数，它将被设置为命令的返回值。如果你不想让输出发送到浏览器，使用 `exec` 函数。

在命令参数中放置任何用户提供的信息是非常危险的。用户可能会在表单字段中传递值，从而允许他们在你的 Web 服务器上执行他们自己的命令。如果你这样做，请先通过 `escapeshellcmd` 函数传递信息。

## 示例

```php
<?php
// 列出目录文件
system("ls -l");
?>
```

## 相关函数

`exec`, `passthru`

# `boolean virtual(string filename)`

`virtual` 函数仅在 PHP 作为 Apache 模块时可用。它等同于写入 `!—#include virtual—>`，这是一个子请求。你可能希望参考 Apache 文档了解更多。如果你想解析 PHP 脚本，请使用 `include` 和 `require` 函数。出错时返回 False (0)。

## 示例

```php
<?php
virtual("ssi-example.html");
?>
```

## 相关函数

`include`, `require`

# HTTP 头部

HTTP 头部是浏览器接收到任何内容之前在浏览器和 Web 服务器之间发送的特殊命令。某些头部让服务器知道浏览器想要什么文件。其他头部可能指示浏览器即将收到的文件类型。要了解头部，请参考最初在 RFC 1945 中定义的 HTTP 规范。它和其他文档可以在 W3C 网站找到，那里有一个关于 HTTP 协议的章节（http://www.w3.org/Protocols/）。

# `array getallheaders()`

`getallheaders` 函数返回服务器和浏览器交换的所有头部。其中某些将被转换为环境变量，从而在你的 PHP 脚本中作为预填充变量变得可用。

## 示例

```php
<?php
$header = getallheaders();
print("<TABLE BORDER=\"1\">"
");
print("<TR>\"
");
?>
```

## HTTP 请求头

```php
print("<TH>Header</TH>\n");
print("<TH>Value</TH>\n");
print("</TR>\n");
for(reset($header)) {
    $index = key($header);
    $value = next($header);
    {
        print("<TR>\n");
        print("<TD>$index</TD><td$value</td>\n");
        print("<TD>$header[$index]</TD>\n");
        print("</TR>\n");
    }
}
print("</TABLE>\n");
```

## 相关函数

`header`

### `boolean header(string http_header)`

`header` 函数向浏览器发送 HTTP 请求头。它必须在向浏览器发送任何输出之前调用，无论是在 PHP 标签内部还是外部。否则，`header` 函数将被忽略。

## 示例

```php
<?php
// 将请求重定向到另一个地址
header("Location: http://www.php.net/");
?>
```

## 相关函数

`setcookie`

### `boolean setcookie(string name, string value, integer expire, string path, string domain, integer secure)`

使用 `setcookie` 在浏览器上设置 cookie。传入的 cookie 会转换为 PHP 变量。由于 cookie 是通过头部设置的，因此必须在向浏览器发送任何输出之前调用 `setcookie`。

如果调用 `setcookie` 时仅传递 `name` 参数，则将从浏览器数据库中删除 cookie。否则，将在客户端创建一个指定名称和值的 cookie。可选的 `expire` 参数设置了浏览器自动删除 cookie 的时间（自 Unix 纪以来的秒数）。如果省略 `expire`，浏览器将在话结束时删除 cookie。

`path` 和 `domain` 参数用于浏览器判断是否发送该 cookie。`secure` 参数用于告诉浏览器仅通过安全连接（套接层/SSL）发送 cookie。使用值 1 表示安全。

开发 cookie 的 Netscape 在标题为“持久化状态：HTTP Cookies”的文章中提供了关于 cookie 的更多信息。可以在 http://developer.mozilla.org/docs/manual/cookies.htm 找到。

## 示例

```php
<?php
/* 标记此站点在接下来 24 小时内已访问 */
setcookie("HasVisited", "Yes", time()+86400, "/");
```

## 相关函数

`header`

## 网络 I/O

网络 I/O 函数直接通过 Internet 协议发送信息，或获取有关主机的信息。

### `boolean checkdns(string host, string type)`

`checkdns` 函数检查主机的 DNS 记录。`type` 参数定义了要搜索的记录类型。有效类型列在图 8 中。如果省略，`checkdns` 将检查 MX 记录。你可能希望阅读命名 Internet 域名服务器守护进程的主页面。

图 8 DNS 记录类型

| 类型 | 说明 |
|---|---|
| A | IP 地址 |
| ANY | 任意记录 |
| CNAME | 规范别名 |
| MX | 邮件交换记录 |
| NS | DNS 服务器 |
| SOA | 区域授权起始 |

## 示例

```php
<?php
if(checkdns("php.net", "MX")) {
    print("php.net is a mail exchanger");
}
?>
```

## 相关函数

`getmxrr`, `gethostbyaddr`, `gethostbyname`

### `getmxrr(string host, array mxhost, array weight)`

`getmxrr` 函数获取主机的 DNS 记录。主机名将被添加到 `mxhost` 参数指定的数组中。可选的 `weight` 数组将为每个主机分配权重。返回值表示操作是否成功。

## 示例

```php
<?php
getmxrr("php.net", $mxrecord, $weight);
for($index=0; $index < count($mxrecord); $index++) {
    print($mxrecord[$index]);
    print(" - ");
    print($weight[$index]);
    print("\n");
}
?>
```

## 相关函数

`checkdns`, `gethostbyaddr`, `gethostbyname`

### `integer fsockopen(string hostname, integer port, integer error_number, string error_description)`

`fsockopen` 以文件流的形式开始一个网络连接，返回一个适用于 `fputs`、`fgets` 以及本章稍后讨论的其它流函数的文件描述符。它将尝试连接到指定端口的主机。主机名也可以是数字 IP 地址。

如果发生错误，则返回 false (0)，并设置可选的 `error_number` 和 `error_description` 参数。它们必须通过引用传递，这意味着在美元符号之前要添加连接符号 (&)。返回的错误代码为零，表示 PHP 在尝试连接时发生了错误。

## 示例

```php
<?php
// 浏览器不要渲染此内容
header("Content-type: text/plain");

// 尝试连接到 Web 服务器
$connection = fsockopen("www.php.net",
    80,
    &$error_number,
    &$error_description);

if($connection) {
    // 设置非阻塞模式
    set_socket_blocking($connection, false);

    // 设置等待时间
    set_socket_timeout($connection, 60);

    // 服务器我们想要根文档
    fputs($connection, "GET / HTTP/1.0");
    fputs($connection, "\r\n\r\n");

    // 获取输出
    fpassthru($connection);
    fclose($connection);
}
else {
    // $connect 为 false
    print("An error occurred!\n");
    print("Number: $error_number\n");
    print("Description: $error_description\n");
}
?>
```

*(注：由于提供的原文在后续出现大量重复截断，翻译已在您提供的最后一个有效逻辑结束)*

# 数据函数

### 本章主题

- 数据类型、常量和变量
- 数组
- 字符串
- 编码与解码
- 正则表达式

![](img/490647a2fc8fbc7034b6e56593c58845_181_0.png)

# 第9 章

本章中的函数用于处理数据。它们检查变量的值。它们将一种数据类型转换为另一种。它们还处理数组。你可能会发现回到第 2 章阅读关于数据类型和变量的讨论很有用。

## 数据类型、常量和变量

这些函数检查变量的状态、更改其类型或作为特定数据类型返回值。

```
boolean define(string constantname, string value, boolean non_case_sensitive)
```

`define` 函数创建一个常量，常量本质上是一个只能设置一次的变量。`value` 参数可以是字符串、整数或双精度浮点数。它不能是数组或对象。`non_case_sensitive` 参数是可选的。默认情况下，常量对大小敏感，这与变量不同。如果由于某些原因无法创建常量，将返回 false。

## 示例

```php
<?
define("MY_CONSTANT", "Hello");
define("ANOTHER_CONSTANT", 98.6);
print("MY_CONSTANT" . "\n");
print("ANOTHER_CONSTANT" . "\n");
?>
```

## 相关函数

`defined`

# `boolean defined(string constantname)`

如果常量存在，`defined` 函数返回 true (1)，否则返回 false (0)。

## 示例

```php
<?
define("THERMOSTAT", "72 degrees");
if(defined("THERMOSTAT"))
{
    print("THERMOSTAT is " . THERMOSTAT);
}
?>
```

## 相关函数

`define`

# `double doubleval(expression)`

`doubleval` 函数将其参数作为双精度浮点数返回。第 2 章包含了关于类型之间转换的讨论。

# 数据类型、常量和变量

## 示例

```php
<?php
$myNumber = "13cm";
print(doubleval($myNumber));
?>
```

## 相关函数

`intval`, `strval`

# `boolean empty(variable)`

`empty` 函数如果变量名从未被赋予过值，则返回 true；如果变量位于赋值运算符的左侧，则返回 false。

## 示例

```php
<?php
if(empty($Name)) {
    print("I don't know your name");
} else {
    print("Your Name is $Name");
}
?>
```

## 相关函数

`isset`

# `get_meta_tags(string file)`

`get_meta_tags` 函数扫描 HTML 文档中的元标签（meta tags）并以关联数组的形式返回它们。它在找到结束 head 标签后停止查找。每个同时包含 name 和 content 属性的 meta 标签将成为返回数组中的一个元素。索引将是 meta 标签的名称，值将是 content 属性中的文本。

# 第9 章数据函数

许多文件函数一样，`get_meta_tags` 允许指定 URL 而不是本地文件系统上的路径。

## 示例

```html
<HTML>
<HEAD>
<TITLE>get_meta_tags</TITLE>
<META name="description" content="get_meta_tags example">
</HEAD>
<BODY>
<?php
$MetaTags = get_meta_tags("get_meta_tags.php");
print($MetaTags["description"]);
?>
</BODY>
</HTML>
```

## 相关函数

无

# `string gettype(expression)`

`gettype` 函数返回一个描述变量类型的字符串。

它将是以下值之一：integer, double, string, array, object, class, unknown type。

# 示例

```php
<?
printf("%s\n", gettype(11));
printf("%s\n", gettype(7.3));
printf("%s\n", gettype("hello"));
?>
```

## 相关函数

`isset`, `settype`

# `integer intval(expression)`

`intval` 函数将其参数作为整数返回。第 2 章包含了关于类型之间转换的讨论。

## 示例

```php
<?php
$myNumber = "13.5cm";
print(intval($myNumber));
?>
```

## 相关函数

`doubleval`, `strval`

# `boolean is_array(expression)`

如果表达式是数组，`is_array` 函数返回 true，否则返回 false。

# 示例

```php
<?php
$colors = array("red", "blue", "green");
if(is_array($colors)) {
    print("colors is an array");
}
?>
```

## 相关函数

`is_double`, `is_float`, `is_int`, `is_integer`, `is_long`, `is_object`, `is_real`, `is_string`, `is_type`

# `boolean is_double(expression)`

如果表达式是双精度浮点数，`is_double` 函数返回 true，否则返回 false。

# 第9 章数据函数

# 示例

```php
<?
$Temperature = 15.23;
if (is_double($Temperature))
{
    print("Temperature is a double");
}
?>
```

## 相关函数

`is_array`, `is_float`, `is_int`, `is_integer`, `is_long`, `is_object`, `is_real`, `is_string`, `is_type`

# `is_float`

`is_float` 函数是 `is_double` 的别名。

# `is_int`

`is_int` 函数是 `is_integer` 的别名。

# `boolean is_integer(expression)`

如果表达式是整数，`is_integer` 函数返回 true，否则返回 false。

# 示例

```php
<?
$PageCount = 123;
if (is_integer($PageCount))
{
    print("PageCount is an integer");
}
?>
```

# 数据类型、常量和变量

## 相关函数

`is_array`, `is_double`, `is_float`, `is_int`, `is_long`, `is_real`, `is_string`, `is_type`, `is is_`

`is_long` 函数是 `is_integer` 的别名。

# `boolean is_object(expression)`
