
例如，要读取文件的前 1024 字节并将字符串赋值为变量 `$content` 的值，请使用此代码：

```php
$fp = fopen("/home/username/temp.txt", "r"); // 打开文件指针
$content = fread($fp, 1024); // 读取 1024 字节到变量中
```

### `fputs()`

`fputs()` 函数向已打开的文件指针写入字符串。`fputs()` 的语法为
`fputs($filepointer, content, [length]);`

文件指针必须处于打开状态才能向文件写入。`length`（长度）参数是可选的。如果未指定，则会将所有指定的内容都写入文件。
例如，要向打开的文件指针写入 "I love PHP"，请使用

`fputs($filepointer, "I love PHP");`
或者，你也可以将内容放在变量中，然后只引用该变量：

```php
$content = "I love PHP"
fputs($filepointer, $content);
```

### `fclose()`

使用 `fclose()` 函数关闭已打开的文件指针。`fclose()` 的语法为
`fclose($filepointer);`

例如，如果你使用 `fopen()` 函数打开了一个名为 `$new_file` 的文件指针，将使用以下代码来关闭该文件指针：

```php
fclose($new_file);
```

### `file_exists()`

`file_exists()` 函数检查指定名称的文件是否已经存在。`file_exists($filename)` 的语法为

```php
file_exists("filename");
```

例如，以下代码检查目录中是否存在 `index.html` 文件，并根据结果打印消息：

```php
if (file_exists("/home/username/index.html")) {
    echo "The file index.html does not exist.";
} else {
    echo "Success! index.html exists.";
}
```

### `mkdir()`

与 shell 命令中的 `mkdir` 命令一样，`mkdir()` 函数在文件系统上创建一个新目录。`mkdir()` 的语法为

```php
mkdir("pathname", mode);
```

例如，要在你的主目录下创建一个名为 `public_html` 的目录，请使用
`mkdir("/home/username/public_html", 0755);`

PHP 用户必须在指定的目录中具有写权限。

### `rename()`

正如其名所示，`rename()` 函数尝试给现有文件赋予新名称。`rename()` 的语法为

```php
rename("oldname", "newname");
```

例如，要将你主目录下的 `index.html` 文件重命名为 `temp1.html`，请使用
`rename("/home/username/index.html", "/home/username/temp1.html");`

PHP 用户必须拥有修改文件的权限。

### `rmdir()`

与 shell 命令中的 `rmdir` 命令一样，`rmdir()` 函数从文件系统删除删除目录。`rmdir()` 的语法为

```php
rmdir("pathname");
```

例如，要删除你主目录下的 `public_html` 目录，请使用
`rmdir("/home/username/public_html");`

PHP 用户必须在指定的目录中具有写权限。

### `symlink()`

`symlink()` 函数从文件系统上的现有文件或目录到指定的链接名称创建一个符号链接。`symlink()` 的语法为

```php
symlink("targetname", "linkname");
```

例如，要为名为 `index.html` 的现有文件创建一个名为 `index.html` 的符号链接，请使用
`symlink("index.html", "index.phtml");`

### `unlink()`

`unlink()` 函数从文件系统删除一个文件。`unlink()` 的语法为 `unlink("filename");`

例如，要删除你主目录下的名为 `index.html` 的文件，`unlink("/home/username/index.html");`

PHP 用户必须拥有该文件的写权限。

### HTTP Functions

用于发送特定 HTTP 头和 cookie 数据的内置函数是 PHP 中开发大型 Web 应用程序至关重要的方面。幸运的是，这些函数的语法非常容易理解和实现。

### `header()`

`header()` 函数输出 HTTP 头字符串，例如位置重定向。此输出必须在向浏览器发送任何其他数据（包括 HTML 标签）之前发生。

> 这个信息需要反复强调：切勿在发送 `header()` 之前尝试向浏览器发送任何类型的信息。你可以在 `header()` 之前执行任何数据库操作或其他计算，但不能向屏幕打印任何内容，即使是一个换行符也不行。

![](img/f8bb5053a1d20d75df488da4d4dbfceb_350_0.png)

例如，使用 `header()` 函数将用户重定向到新位置，请此代码：

```php
header("Location: http://www.newlocation.com");
exit; // 在 header 语句后跟随 exit 命令。
// 这确保了代码不会继续执行。
```

### `setcookie()`

`setcookie()` 函数向用户发送 cookie。cookie 必须在向 Web 浏览器发送任何其他头部之前之前。`setcookie()` 的语法为

```php
setcookie("name", "value", "expire", "path", "domain", "secure");
```

例如，你使用以下代码发送一个名为 `username`、值为 `joe` 的 cookie，它在 `testcompany.com` 域名的所有目录内有效期为一小时：

```php
setcookie("username", "joe", time()+3600, "/", ".testcompany.com");
```

### Mail Function

```php
mail()
```

如果你的服务器可以访问 sendmail 或 SNMP 网关，`mail()` 函数将向指定的收件者发送邮件。`mail()` 的语法为

```php
mail("recipient", "subject", "message", "headers");
```

例如，要返回 0 到 576 之间的随机值，请使用

```
echo rand(0,576);
```

### `round()`

`round()` 函数将小数四舍入到下一个更高的整数或更低的整数。`round()` 函数的语法为：

```
round(number);
```

例如：

```
round(2.56); // 返回 "3"
round(1.22); // 返回 "1"
round(55.22); // 返回 "55"
```

### `sqrt()`

`sqrt()` 函数返回给定数字平方根。`sqrt()` 的语法为：

```
sqrt(number);
```

例如，要找到 5561 的平方根，请使用

```
echo sqrt(5561);
```

结果为 74.572112750009。

### `rand()`

`rand()` 函数为随机数生成器提供一组可能的值。`rand()` 的语法为：

```
rand(seed);
```

一种常见的做法是使用微秒数为随机数生成器设置种子：

```
rand((double)microtime()*1000000);
```

### 杂函数

`die()` 和 `exit` 函数为你的脚本执行提供了实用的控制，为编程错误提供了“逃生路线”。

### `die()`

`die()` 函数在返回值为 FALSE 时输出给定的消息并终止脚本。`die()` 的语法为：

```
die("message");
```

例如，你将使用以下代码在连接数据库失败时打印消息并停止脚本执行：

```
$connection = mysql_connect("servername", "username", "password") or die("Can't
connect to database.");
```

### `exit`

`exit` 函数在调用 `exit` 函数的用点处终止当前脚本的执行。

例如，在发送了位置重定向头后退出脚本，请使用

```
header("Location: http://www.newlocation.com/*");
```

```
exit;
```
