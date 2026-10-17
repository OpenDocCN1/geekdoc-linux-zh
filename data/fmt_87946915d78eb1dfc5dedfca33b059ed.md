
## log_errors

`log_errors` 指令启用或禁用 PHP 错误日志记录。您必须使用 `error_log` 指令指定日志路径或 `syslog` 文件。

**语法：** `log_errors` `On` | `Off`

## magic_quotes_gpc

`magic_quotes_gpc` 指令启用或禁用 GET、POST 和 cookie 数据中引号（单引号、双引号、null 和反斜杠字符）的转义。

**语法：** `magic_quotes_gpc` `On` | `Off`

**默认设置：** `magic_quotes_gpc` `On`

## magic_quotes_runtime

`magic_quotes_runtime` 指令启用或禁用内部生成文本的自动引用。换句话说，如果您从数据库中检索一条记录，其中嵌入了 `<?php` ... `?>` 类型的标签，标签内的内容（属于数据的一部分）将被转义（即不会处理），而不会被当作 PHP 代码执行。

**语法：** `magic_quotes_runtime` `On` | `Off`

**默认设置：** `magic_quotes_runtime` = `Off`

## max_execution_time

`max_execution_time` 指令设置脚本产生输出所能运行的最大时间。当脚本运行时间超过指定的秒数后，PHP 将使该脚本超时。除非您计划运行耗时很长的 PHP 脚本，否则默认值在大多数情况下都是可接受的。

**语法：** `max_execution_time` `seconds`

**默认设置：** `max_execution_time` `30`

## memory_limit

`memory_limit` 指令设置 PHP 脚本可消耗的最大 RAM 内存量。默认值 8MB 对于中小型 PHP 脚本来说已经足够。您也可以以字节为单位指定内存大小。

**语法：** `memory_limit` `bytes` `[nM]`

**默认设置：** `memory_limit` `8M`

例如，以下两者是等效的：

```
memory_limit 8M
memory_limit 8388608
```

## output_buffering

`output_buffering` 指令允许您启用或禁用输出缓冲。当设置为 `On` 时，您可以在 PHP 脚本的任何位置打印 HTTP 头。即使在打印其他内容后，仍能在脚本中间输出头部信息，这意味着即使脚本之前部分成功，也可以显示错误页面。

**语法：** `output_buffering` `On` | `Off`

**默认设置：** `output_buffering` `On`

您也可以使用**内置**的 `ob_start()` 和 `ob_end_flush()` 指令直接开始和结束内容刷新。**例如**：

```php
<?php
ob_start();  // Buffer all output
echo "Buffered contents \n";
ob_end_flush(); // Page rendered. flush the output buffer.
?>
```

在此处，输出被缓冲。

## safe_mode

`safe_mode` 指令在将 PHP 用作 CGI 解决方案时设置 PHP 的安全模式。当设置为 `On` 时，此指令确保由 PHP 解释器在 CGI 模式下运行的 PHP 脚本不允许访问超出 Web 站点文档根目录的范围。

- **语法：** `safe_mode On | Off`
- **默认设置：** `safe_mode Off`

## safe_mode_allowed_env_vars

`safe_mode_allowed_env_vars` 指令允许您为所有用户通过使用 `putenv()` 函数可以更改的环境变量设置前缀。默认值允许用户更改任何以 `PHP_` 前缀开头的环境变量。

- **语法：** `safe_mode_allowed_env_vars prefix`
- **默认设置：** `safe_mode_allowed_env_vars PHP_`

## safe_mode_protected_env_vars

`safe_mode_protected_env_vars` 指令允许您设置一个逗号分隔的环境变量列表，任何使用 `putenv()` 函数的 PHP 脚本都不能更改这些变量。

- **语法：** `safe_mode_protected_env_vars environment_variable [environment_variable ...]`
- **默认设置：** `safe_mode_protected_env_vars = LD_LIBRARY_PATH`

如果您希望保护所有以 `HTTP_` 前缀开头的环境变量，可以使用：

```
safe_mode_protected_env_vars = HTTP_
```

## track_errors

`track_errors` 指令启用或禁用将错误消息存储在名为 `$php_errormsg` 的 PHP 变量中。

**语法：** `track_errors On | Off`

## upload_max_filesize

`upload_max_filesize` 指令设置通过 PHP 可上传的文件的最大大小。默认限制为 2MB (2M)。或者，您可以仅指定千字节数。

**语法：** `upload_max_filesize kilobytes`

**默认设置：** `upload_max_filesize 2M`

例如，以下两者是等效的：

```
upload_max_filesize = 2M
upload_max_filesize = 2097152
```

## upload_tmp_dir

`upload_tmp_dir` 指令定义通过 PHP 上传文件的临时目录位置。在 Unix 系统上，习惯上将其设置为 `/tmp`；在 Windows 系统上，通常设置为 `/temp` 或保持默认，在这种情况下，PHP 使用系统默认值。

**语法：** `upload_tmp_dir directory`

# 处理 PHP

本节介绍了一些示例，展示如何使用 PHP 脚本生成动态 Web 内容。

## 创建简单的命令行 PHP 脚本

配置好 PHP 后，您可以像运行 Perl 脚本一样从命令行运行 PHP 脚本。默认情况下，PHP 解释器在 Unix 系统中安装在 `/usr/local/bin` 目录；在 Windows 系统中，它安装在该发行版解压缩的目录中。您可以创建一个名为 `test.php` 的简单 PHP 脚本，如清单 15-1 所示。

### 清单 15-1: test.php

```php
#!/usr/local/bin/php -q

# For Windows change the above line to:

#D:/path/to/php -q

#

<?php
echo "Welcome to the PHP World\n";
?>
```

您可以使用 `/usr/local/bin/php test.php` 从命令行运行此脚本，或者通过 `chmod +x test.php` 更改脚本的文件权限，然后在脚本目录中使用 `./test.php` 执行它。这里使用的 `-q` 选项告诉 PHP 抑制 HTTP 内容类型头，否则它会打印输出以使符合 Web 标准。

## 创建简单的 PHP Web 页面

为您的网站创建 PHP 脚本就像上一节中的示例一样简单。清单 15-2 展示了一个名为 `hello.php` 的简单脚本。

### 清单 15-2: hello.php

```html
<html>
    <head><title>Hello World Script</title>
<body>
    <?php echo "Hello World from PHP"; ?>
</body>
</html>
```

当您将此脚本保存在 Web 服务器文档树中的某个目录内时，您可以通过 `http://your_web_server/path/to/hello.php` 访问它。如果如您在此前本章节“为 PHP 配置 Apache”部分中指示的那样使用了诸如 `AddType application/x-httpd-php .php` 之类的指令，那么 PHP 模块将解析并执行这个单行 PHP 脚本，打印出“Hello World from PHP”这句话。请注意，PHP 会自动打印适当的 `Content-Type` 头 (`text/html`)。

让我们编写一个更有用的脚本，如列表 15-3 所示，该脚本显示安装在 Web 服务器上的 PHP 信息。

## 列表 15-3：info.php

```html
<html>
  <head><title>Hello World Script</title>
  <body>
    <?php
```
