
## 第 6 章

每个指令分别检查输入字符串是否小于、大于或等于 `CondPattern`。例如，如果你想让网站在给定年份后禁止访问某个区域，可以使用以下代码：

```
RewriteCond %{TIME_YEAR} >2005
RewriteRule .* - [F]
```

除了这些简单的比较运算符外，你还可以使用另外六种条件检查来评估文件和目录的状态：

| 比较运算符 | 含义 |
|---|---|
| -d (is directory) | 测试是否存在匹配测试字符串的目录 |
| -f (is regular file) | 测试是否存在匹配测试字符串的常规文件 |
| -s (is regular file with size) | 测试是否存在匹配测试字符串且大小大于 0 字节的常规文件 |
| -l (is symbolic link) | 测试是否存在匹配测试字符串的符号链接 |
| -f (is existing file via subrequest) | 在考虑服务器所有访问控制后，测试常规文件是否可访问；使用内部子请求来执行检查（会影响性能） |
| -U (is existing URL via subrequest) | 在考虑服务器所有访问控制后，测试 URL 是否可访问；使用内部子请求来执行检查（会影响性能） |

例如，要检查图像是否存在且实际包含一些数据，可以使用以下代码：

```
RewriteCond %{REQUEST_FILENAME} \.jpg$
RewriteCond %{REQUEST_FILENAME} !-s
RewriteRule .* - [G]
```

第一个条件检查是否调用了 .jpg 文件，第二个条件实际检查文件是否不存在或大小为 0 字节。注意条件模式 `!-s` 前使用感叹号。`RewriteCond` 中的任何条件模式都可以在前面加感叹号，从而否定该条件——这与 PHP 条件中感叹号的作用相同。

### RewriteCond 标志

为了更好地控制 `RewriteCond`，提供了一些与 `RewriteRule` 标志类似的标志。

#### nocase|NC

与在 `RewriteRule` 中使用的同名标志一样，`nocase` 指定要评估的正则表达式是不区分大小写的。

#### or next| OR

多个 RewriteCond 指令的默认链式方法是使用逻辑与（AND）。如果使用 or next 标志，则两个连接的 RewriteCond 使用逻辑或（OR）进行比较。

虽然 RewriteRule 和 RewriteCond 指令提供了 mod_rewrite 的大部分功能，但还有一些其他关键指令可以帮助你控制重写并解决问题。

## Apache 技巧

### RewriteBase

在大多数情况下，你的网站 URL 不会与你的物理文件系统布局匹配。你的网站根目录几乎从不位于本地文件系统的根目录（/）处。在 Apache 服务器的正常运行中，这通常不是问题；但在使用 RewriteRule 时，这可能变得非常棘手。RewriteBase 允许你为一系列 URL 重写指定基础或前缀路径。

为了完全理解 RewriteBase 的理由，请查看以下用于重写一组简单文件的示例规则集：

```
RewriteEngine On

RewriteRule ^foo\.html$ bar.html [R]
```

假设你的 Web 根目录由本地文件系统的 /www 文件夹提供（即你的 DocumentRoot 设置为 /www）。如果你尝试在目录访问文件 (.htaccess) 中使用前面的规则，实际上会导致请求被错误地重写——而不是返回你期望的 http://www.domain.com/bar.html 文件，你会得到 http://www.domain.com/www/ bar.html。为什么会这样？以下是 Apache 内部发生情况的简化版本：

请求：/www/foo.html（本地物理路径）

重写过程：
/www/foo.html -> foo.html（移除目录前缀）
foo.html -> bar.html（应用 RewriteRule）
bar.html -> /www/bar.html（重新应用目录前缀）
/www/bar.html -> http://www.domain.com/www/bar.html
（将域名前缀应用于 URL，发送到浏览器）

为了解决这个问题，你只需在规则集中添加一个 RewriteBase 语句：

```
RewriteEngine On
RewriteBase /

RewriteRule ^foo\.html$ bar.html [R]
```

### RewriteLog

为了亲眼目睹 mod_rewrite 实际发生的内部情况，请尝试 RewriteLog 指令。你可以使用 RewriteLog 来指定一个日志文件，内部重写处理的运行记录将被发送到该文件中。

要在其他默认 Apache 日志文件旁边启用重写日志，使用以下代码：

```
RewriteLog "logs/rewrite_log"
```

在指定重写日志的路径时，你可以使用绝对路径和相对路径。如果使用相对路径，它将以 httpd.conf 中 _ServerRoot_ 设置为基准。

请注意，_RewriteLog_ 指令是按服务器应用的，因此必须放在 httpd.conf 中的服务器配置或虚拟主机容器内——不允许在 <Directory> 部分或 .htaccess 文件中使用。

### RewriteLogLevel

要控制重写日志记录的详细程度，可以使用 _RewriteLogLevel_ 指令。给定 0 到 9 之间的数字，其中 9 表示最详细，你可以控制记录多少内部处理。设置为 0 将完全禁用日志记录，而大于 2 的设置仅用于调试——在较高设置下可能会降低 Apache 的速度。

如果你希望更深入地了解 mod_rewrite 的工作原理，请查看 Apache 在线手册中的 mod_rewrite 部分：

```
http://httpd.apache.org/docs-2.0/mod/mod_rewrite.html
```

### URL 拼写检查

有了 mod_rewrite 的力量，对于格式错误或更改的 URL，你几乎可以处理任何情况，那拼写错误呢？当然，你可以为网站中的每个文件列出一个巨大的可能拼写错误列表，并编写大约一千条 RewriteRule，但这并不是必须的。为了解除你“简单”拼写检查的负担，Apache 附带了 mod_spelling 模块（是的，它真的只拼写了一个 't'）。使用 mod_spelling，你可以将处理 URL 拼写错误的任务移交给 Apache，它将自动尽力确定用户打算加载哪个文件。

要使用 mod_spelling，首先检查它是否已作为静态构建模块可用：

```
/path/to/httpd -l
```

如果你在列表中看不到 mod_spelling . c，请检查 Apache 模块目录中的 mod_spelling . so：

```
ls /path/to/apache/modules
```

如果你没有找到静态库或动态模块，你需要自己构建它们。与之前一样，你可以选择将该模块静态构建到 Apache 本身，或将其构建为动态模块。

要构建静态版本，请更改你的 configure 命令以包含 mod_spelling，如下所示：

```
./configure \
--enable-spelling \
# ...以及你使用的其他 configure 设置
```

如果你更喜欢使用动态模块，只需在 mod_spelling 行中添加 --enable-spelling=shared：

```
./configure \
--enable-spelling=shared \
# ...以及你使用的其他 configure 设置
```

configure 脚本运行后，使用 make 和 make install 构建和安装新的二进制文件和模块是一件简单的事。如果你选择为 mod_spelling 使用动态模块，你需要执行一个额外的步骤。要在 httpd.conf 文件中启用 mod_spelling 作为动态模块，请取消注释或添加以下行：

```
LoadModule speling_module modules/mod_spelling.so
```

完成更改后，重启 Apache。如果 Apache 错误日志中没有显示错误，则说明你已成功为服务器添加了 mod_spelling 功能。

要实际使用拼写检查，请在全局服务器配置部分、虚拟主机部分、<Directory> 部分或简单的 .htaccess 文件中添加以下指令：

```
CheckSpelling on
```

配置 mod_spelling 仅涉及 CheckSpelling 指令——值为“on”启用拼写检查，“off”禁用任何检查，这是默认行为。

要查看 mod_spelling 的实际效果，请在你选择的目录中启用 CheckSpelling，然后在该目录中创建名为 info.php 的以下脚本：

```
<?php phpinfo(); ?>
```

到现在为止，你应该能认出这是标准的 PHP 信息转储输出，但与其使用正确的 info.php URL 加载文件，不如尝试使用稍微拼错的名字，如 ingo.php。启用 mod_spelling 后，Apache 会执行快速的 HTTP 301 重定向到它对你意图的最佳猜测，而不是提供 404 Not Found 冷盘。

## 内容压缩

如果我们告诉你，只需花几分钟进行 Apache 配置，就可以大幅削减你的每月带宽使用量？你可能认为这是谎言，但事实恰恰相反——你只需要内容压缩和几个配置指令。

什么是内容压缩？当网页通过互联网下载时，默认情况下，组成页面标记、图像、样式表和其他内容的位和字节大部分是未压缩的

