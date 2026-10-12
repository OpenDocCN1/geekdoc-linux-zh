
## 第 6 章

若要启用重写日志，使其与其他默认的 Apache 日志文件并列，请使用以下指令：

```apache
RewriteLog "logs/rewrite_log"
```

在指定重写日志的路径时，可以使用绝对路径或相对路径。如果使用相对路径，它将相对于 httpd.conf 中的 **ServerRoot** 设置。

请注意，**RewriteLog** 指令是按服务器粒度应用的，因此必须放置在 httpd.conf 中的服务器配置或虚拟主机容器内——它不允许出现在 `<Directory>` 部分或 .htaccess 文件中。

### RewriteLogLevel

为了控制重写日志记录的详细程度，您可以使用 **RewriteLogLevel** 指令。给定 0 到 9 之间的数字，9 代表最详细，您可以控制记录多少内部处理过程。设置为 0 会完全禁用日志记录，而大于 2 的值仅应用于调试——在较高设置下可能会降低 Apache 的性能。

如果您希望深入了解 mod_rewrite 的工作原理，请查看 Apache 在线手册中的 mod_rewrite 章节：

```
http://httpd.apache.org/docs/2.0/mod/mod_rewrite.html
```

### URL 拼写检查

凭借 mod_rewrite 的强大功能，对于格式错误或变更的 URL，几乎没有什么您无法处理的，但拼写错误呢？当然，您可以为网站中的每个文件列出一个巨大的可能拼写错误列表，并编写大约一千条 RewriteRules，但这并没有必要。为了减轻您进行“简单”拼写检查的负担，Apache 自带 **mod_spelling** 模块（是的，它确实只用了一个“t”）。借助 mod_spelling，您可以将处理 URL 拼写错误的任务交给 Apache，它将自动尽力确定用户想要加载的文件。

要使用 mod_spelling，首先检查它是否已作为静态编译模块对 Apache 可用：

```bash
/path/to/httpd -l
```

如果在列表中看不到 mod_spelling.c，请检查 Apache 模块目录中是否有 mod_spelling.so：

```bash
ls /path/to/apache/modules
```

如果您没有找到静态库或动态模块，您需要自己构建它们。与之前一样，您可以选择将该模块静态编译到 Apache 本身，或者将其构建为动态模块。

要构建静态版本，请更改您的 configure 命令以包含 `mod_spelling`，如下所示：

```bash
./configure \
--enable-spelling \
# ...以及您使用的任何其他 configure 设置
```

如果您更倾向于使用动态模块，只需在 `mod_spelling` 行添加 `shared`：

```bash
./configure \
--enable-spelling=shared \
# ...以及您使用的任何其他 configure 设置
```

在 configure 脚本之后，使用 `make` 和 `make install` 构建并安装新的二进制文件和模块是一件简单的事情。如果您选择对 `mod_spelling` 使用动态模块，还需要额外执行一步。要在 `httpd.conf` 文件中启用 `mod_spelling` 作为动态模块，请取消注释或添加以下行：

```apache
LoadModule speling_module modules/mod_spelling.so
```

完成更改后，重启 Apache。如果 Apache 错误日志中没有显示错误，则您已成功为服务器添加了 `mod_spelling` 功能。

要实际使用拼写检查，请在全局服务器配置部分、虚拟主机部分、`<Directory>` 部分或简单的 .htaccess 文件中添加以下指令：

```apache
CheckSpelling on
```

配置 `mod_spelling` 仅涉及 `CheckSpelling` 指令——值“on”启用拼写检查，“off”禁用所有检查，这是默认行为。

要查看 `mod_spelling` 的实际运行情况，请在您选择的目录中启用 `CheckSpelling`，然后在该目录中创建名为 `info.php` 的脚本：

```php
<?php phpinfo(); ?>
```

此时，您应该能认出这是标准的 PHP 信息输出，但不要使用正确的 `info.php` URL 加载文件，而是尝试使用稍微拼写错误的名称 `lidngp.php` 加载。在启用 `mod_spelling` 的情况下，Apache 会执行快速的 HTTP 301 重定向到它认为您意图的最佳猜测，而不是返回冰冷的 404 Not Found 页面。

## 内容压缩

如果我们告诉您，只需几分钟的 Apache 配置，就可以大幅削减您的每月带宽使用量呢？您可能认为这是谎言，但事实并非如此——您只需要内容压缩和几条配置指令。

什么是内容压缩？当网页通过互联网下载时，默认情况下，构成页面标记、图像、样式表和其他内容的位和字节处于基本未压缩的状态。您编写的 HTML 会直接按您保存时的样子发送，包括所有空白字符。内容压缩允许您透明地压缩页面标记，并将其通过互联网发送到用户的浏览器，在那里它在渲染到屏幕之前会被静默解压缩。另一种理解方式是与通过电子邮件发送 zip 文件相关联。您可以轻松地将大型文档或媒体文件作为普通附件发送到电子邮件，但很多时候，您会在发送前将文件压缩为 zip 或 tar.gz 归档，以缩短下载消息和附件所需的时间。

在 Apache 中使用内容压缩非常简单。您只需要 `mod_deflate`，它随 Apache 源代码提供，在构建 Apache 时可以轻松编译为模块。

### 使用 mod_deflate

与前面讨论的模块一样，您需要做的第一件事是检查该模块是否作为 Apache 静态部分或动态模块可用：

```bash
/path/to/httpd -l
ls /path/to/apache/modules/
```

如果您在第一个命令的输出中看到 `mod_deflate.c`，或在第二个命令的输出中看到 `mod_deflate.so`，则您已拥有对 `mod_deflate` 的访问权限，可以跳过重新构建 Apache 的下一步骤。

如果您在任一命令结果中都没有看到 `mod_deflate`，您需要将其静态编译到 Apache 二进制文件中，或者作为动态模块添加。在从源代码构建 Apache 时，若要静态包含 `mod_deflate`，您只需在运行 `configure` 时添加以下内容：

```bash
./configure \
--enable-deflate
```

如果您希望使用动态可加载模块，只需在启用 `mod_deflate` 的行的末尾添加 `=shared`：

```bash
./configure \
--enable-deflate=shared \
# ...以及您可能使用的任何其他 configure 设置
```

显然，如果您计划在运行 `configure` 时包含其他指令，也需要添加它们。配置完源代码后，执行常规的 `make` 和（以 root 身份）`make install`。

如果您将 `mod_deflate` 构建为动态模块，则必须在 `httpd.conf` 中使用 `LoadModule` 启用该模块：

```apache
LoadModule deflate_module modules/mod_deflate.so
```

然后重启 Apache 以使更改生效。

构建并启用 `mod_deflate` 后，告诉 Apache 使用 `mod_deflate` 以及要压缩的文件类型只是一件简单的事情。为此，您需要编辑 `httpd.conf` 文件，或在要使用压缩的目录中创建或修改 `.htaccess` 文件——如果可用，首选前者。

要在 Apache 中全局启用压缩，请在您的 httpd.conf 中添加以下内容：

```apache
AddOutputFilterByType DEFLATE text/*
AddOutputFilterByType DEFLATE application/ms*
AddOutputFilterByType DEFLATE application/vnd*
AddOutputFilterByType DEFLATE application/postscript
```

然后您只需要重启 Apache，内容压缩即可运行。

所有这些配置指令具体是什么意思？其实很简单——在 Apache 2.x 中，`AddOutputFilterByType` 指令的确如其名所示：它告诉 Apache 将输出通过给定的过滤器（在此情况下为 `mod_deflate`）进行处理，然后再将响应发送给最终用户的浏览器。前面的示例代码告诉 Apache 对任何基于文本的文件（`text/*`）、任何 Microsoft 文档（如 Word 或 Excel 文件，即 `application/ms*` 和 `application/vnd*`）以及任何 postscript 文件（如 Adobe Illustrator 或 EPS 图形，即 `application/postscript`）使用 DEFLATE 过滤器 `mod_deflate`。通过简单组合文档的 MIME 类型和通配符（类似示例），可以将您喜欢的任何文档类型添加到 `mod_deflate` 的过滤列表中。

如果您只想压缩纯文本和 HTML 文件，请使用以下指令：

```apache
AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/html
```

如果您希望压缩 Apache 提供的所有内容怎么办？使用另一个 Apache 指令 `SetOutputFilter`，您可以告诉 Apache 将每个文件通过 `mod_deflate` 处理：

```apache
SetOutputFilter DEFLATE
```

然而，在大多数服务器设置中，这并不是一个好主意。实际上，有些文件类型从压缩中获益甚微，有些文件在压缩后对最终用户来说会损坏。在大多数情况下，没有必要压缩图像格式，因为最常用的 Web 格式已经具有某种内置压缩。此外，PDF 也是压缩的，绝对不应通过 `mod_deflate` 进行过滤，因为在 Acrobat Reader 中它们将变得无法阅读。

> 需要注意的是，Netscape Navigator 4.x 版本的可靠解压缩能力仅限于 `text/html` 以外的任何文件类型，且特定版本的 Netscape Navigator 4.x 无法解压缩任何文件类型。

为了进一步调整所选文件类型的压缩，`mod_deflate` 提供了以下章节中描述的配置指令。

#### DeflateCompressionLevel

`DeflateCompressionLevel` 设置用于缩小文件大小的压缩级别，范围从 1 到 9。压缩级别 1 产生最快的压缩速度，压缩率最低（文件较大），而压缩级别 9 使用最慢的压缩速度，但生成的文件小得多。在决定使用哪个级别时，您必须确定对您来说什么更重要——节省处理器周期还是节省下载时间。默认的压缩级别 6 通常是两者之间的良好折中。

