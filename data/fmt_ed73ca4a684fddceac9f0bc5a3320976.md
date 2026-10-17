
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
      phpinfo();
    ?>
  </body>
</html>
```

此页面调用名为 `phpinfo()` 的 PHP 函数，根据当前使用 `php.ini` 配置的参数，显示大量的 PHP 选项。

## 使用 PHP 脚本作为服务器端包含

如果您希望在服务器端包含（SSI）调用中使用 PHP 脚本，可以使用以下 SSI 标签调用您的 PHP 脚本：

```
<!--#include virtual="/path/script_name.php"-->
```

例如：

```
<!--#include virtual="/phppssi/test.php"-->
```

此处，名为 `/phppssi/test.php` 的 PHP 脚本将从使用上述 SSI 调用的页面中加载。要使 PHP 脚本与 SSI 配合工作，您必须执行以下操作：

- 在包含需要通过 SSI 调用运行的 PHP 脚本的目录中启用 `ExecCGI` 选项。
- 确保相同目录中的 `IncludesNoExec` 选项已禁用。例如：

```apache
DocumentRoot  "/www/mysite/htdocs"

<Directory  "/www/mysite/htdocs/parsed">

    Options +Includes

    AddType text/html .shtml

    <FilesMatch "\\.shtml[.$]">

        SetOutputFilter INCLUDES

    </FilesMatch>

</Directory>

<Directory "/www/mysite/htdocs/php">

    Options +ExecCGI

    <Files *.php>

        SetOutputFilter PHP

        SetInputFilter PHP

    </Files>

</Directory>
```

在上述配置片段中，`/www/mysite/htdocs/parsed` 目录中所有以 `.shtml` 扩展名结尾的文件都被视为 SSI 页面，而 `/www/mysite/htdocs/php` 目录中的所有文件都被视为可以通过 SSI 调用运行的 PHP 脚本。现在，`/www/mysite/htdocs/parsed` 目录中的 SSI 页面可以通过以下 SSI 调用调用 `/www/mysite/htdocs/php` 目录中的脚本：

```
<!--#include virtual="/php/script_name.php"-->
```

## 使用 PHP 页面作为目录索引

如果之前正如“配置 Apache 以支持 PHP”中所述，您已在 `httpd.conf` 中启用了 PHP 支持，也可以使用 PHP 脚本作为目录索引页面。例如：

```
DirectoryIndex index.html index.php
```

这里指令将 `index.html` 设置为目录的首选索引页面，但如果缺少 `index.html`，则使用 `index.php` 代替。

然而，如果您希望使用 PHP 脚本作为默认索引，请反转文件名的顺序，使 `index.php` 位于其他文件名之前。例如：

```
DirectoryIndex index.php index.html
```

这样，Apache 将首先查找 `index.php` 脚本。

## 使用包含文件

PHP 允许您在脚本中包含外部 PHP 代码库文件或普通 HTML 文件。例如：

```html
<html>
<head>
  <title> PHP Resource Site </title>
</head>
<body>
<h1>PHP Resource</h1>
<hr>
<p>Welcome to PHP Resource Site. </p>
<?php
  include('/www/mysite/htdocs/global/copyright.html');
?>
</body>
</html>
```

这里简单的 PHP 脚本是一个单一的函数调用 `include('/www/mysite/htdocs/global/copyright.html');`，它告诉 PHP 包含名为 `/www/mysite/htdocs/global/copyright.html` 的文件。这个 `copyright.html` 页面被包含在当前页面中，就像 `<!--#include virtual="/path/filename"-->` 服务器端包含（SSI）标签一样。但是，被包含的文件本身也可以是 PHP 脚本。例如：

```php
include('/www/mysite/htdocs/global/copyright.php');
```

从给定目录加载名为 `copyright.php` 的 PHP 脚本。包含文件中的脚本将被执行。包含文件中的任何代码都可以访问父脚本中的变量。例如，`copyright.php` 脚本可以访问 `$year` 变量。

```php
<?php
  $year = '2001';
  include('/www/mysite/htdocs/global/copyright.php');
?>
```

因此，`copyright.php` 脚本可以包含诸如 `echo "The current year is: $year \n";` 这样的语句。您可以包含多个文件，或者多次包含同一个文件。每次被包含的脚本都会被执行。例如：

```php
<?php
    $year = '2001';
    include('/www/mysite/htdocs/global/copyright.php');
    $year = '2002'
    include('/www/mysite/htdocs/global/copyright.php');
?>
```

如果 `copyright.php` 脚本由一个简单的 PHP 脚本组成，例如 `<?php echo "The current year is: $year\n"; ?>`，那么上述脚本将显示：

```
The current year is: 2001

The current year is: 2002
```

您还可以使用 `include_once()` 来包含 PHP 脚本或静态 HTML 文件。然而，如果您使用 `include_once()` 代替 `include()`，包含脚本中的代码只执行一次。例如：

```php
<?php
    $year = '2001';
    include_once('/www/mysite/htdocs/global/copyright.php');
    $year = '2002'
    include_once('/www/mysite/htdocs/global/copyright.php');
?>
```

这里相同的 `copyright.php` 的输出是：

```
The current year is: 2001
```

第二次 `include_once()` 不会再次执行 `copyright.php`。您可以使用 `include()` 或 `include_once()` 函数来集中管理多个 PHP 页面所需的通用代码或 HTML 文件。

您还可以类似地使用 `require()` 和 `require_once()` 函数。`require()` 函数用指定文件的内容替换自身。此替换发生在 PHP 引擎编译代码期间，而不是在调用脚本执行期间。`require_once()` 函数仅插入所需脚本的内容一次。

> **注意** `include()`、`include_once()`、`require()` 和 `require_once()` 函数可以访问文件系统中的任何文件，只要用于运行 Web 服务器的用户 ID 对该文件具有读取访问权限。

## 使用 PHP 增强错误处理

Apache 提供了一个名为 `ErrorDocument` 的指令，它允许您显示服务器错误的自定义错误页面。例如：

```
ErrorDocument 404 /missing.html
```

每当服务器遇到缺失文件或目录的请求时，它都会发送 `Status: 404 Not Found` 响应，然后显示 `/missing.html` 页面。您可以将其更改为：

```
ErrorDocument 404 /missing.php
```

这会导致每当 Apache 遇到相同错误时执行名为 `missing.php` 的 PHP 脚本。但是，Microsoft IE 会检测 40x 响应并显示其生成的自定义错误消息。为了绕过此类页面，您可以使 `missing.php` 页面返回 `Status: 200 OK` 响应，而不是其他。例如，使用此代码：

```php
<?php
   header("Status: 200 OK\n");
   header("Location: /missing.html");
?>
```

`missing.php` 脚本显示 HTTP 成功头部，然后指示 Apache 将 Web 客户端重定向到 `/missing.html`。

## 使用 PHP 处理 Web 表单

PHP 使 Web 表单处理变得简单。您可以在 PHP 脚本中将 Web 表单数据字段作为变量访问。列表 15-4 显示了一个简单的 Web 表单，其中有一个名为 `keywords` 的单个输入字段。

```html
<html>
<head><title>Simple HTML Form</title>
</head>
<body>
<form action="form.php">
<input type="text" name="keywords" size=30>
<input type=submit>
</form>
</body>
</html>
```

当用户通过 Web 浏览器提交此表单时，浏览器会发送类似 `http://server/form.php?keywords=value_entered_in_the_form` 的 GET 请求。

例如，如果您输入关键字 `makesite` 并提交上述表单到 `www.domain.com`，Web 服务器将收到对 `http://www.domain.com/form.php?keywords=makesite` 的请求。

负责处理此 Web 表单的 `form.php` 脚本如列表 15-5 所示。

```php
<?php
    echo "You have entered $keywords keyword(s).\n";
?>
```

这个简单的 PHP 脚本打印出在名为 `form.html` 的 HTML 表单的 `keywords` 字段中输入的关键字。

**对于以下请求：**

`http://www.domain.com/form.php?keywords=makesite`

**脚本打印：**

`You have entered makesite as keyword(s).`

在此处，变量 `$keywords` 被赋值为 `makesite`，因为通过 GET 方法传递给服务器的查询字符串为 `keywords=makesite`。如果将 Web 表单中的 `<form action="form.php">` 行修改为 `<form action="form.php" method="POST">`，那么将使用 HTTP POST 方法，`keywords=makesite` 数据将由 PHP 模块读取，并自动作为脚本变量 `$keywords` 的值提供给脚本。

如果 Web 表单包含多个字段，所有字段都会被转换为相应命名的脚本变量。例如，`simple_form.html` 的修改版如清单 15-6 所示。

### 清单 15-6: modified_simple_form.html

```html
<html>
    <head>
        <title>Simple HTML Form</title>
    </head>
    <body>
        <form action="modified_form.php" method="POST">
