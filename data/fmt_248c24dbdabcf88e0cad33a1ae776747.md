
此文件的第一行是 `package HelloWorld`。这创建了一个名为 `HelloWorld` 的包（在某些语言中也称为命名空间）。此行确保了我们定义的任何变量和子程序都不会与其他 `mod_perl` 程序中的发生冲突。所有的 `mod_perl` 程序都是作为模块创建的。这个包从第一行开始，延伸到文件末尾。该文件将被命名为 `HelloWorld.pm`。

在模块中使用 `strict` 始终是一个好主意。它通过强制将所有变量声明为 `my` 变量（因此没有全局变量）来强制良好的编程风格，从而消除了由全局变量引起的讨厌问题。全局变量有其用途，但在在使用之前应该仔细考虑。

`Apache::Constants` 模块包含一些非常有用的常量（如 `OK`）。当 Apache 接收到与 `mod_perl` 程序关联的请求时，它会调用 `handler()` 方法，并传递它一个存储在 `$r` 中的 Apache 请求对象。该对象可以供 `mod_perl` API 中定义的许多方法使用。

第一个执行的请求对象是 `content_type()`，它告诉 Apache 内容类型为 `text/html`。HTTP 标头通过 `send_header()` 发送。HTML 内容使用 `print()` 方法生成，该方法打印了一个 here-document。最后，`handler()` 子程序返回值 `OK`，这告诉 Apache 一切正常并可以像往常一样继续运行。

再次，就像我们编写的所有模块一样，`HelloWorld.pm` 模块必须以 `1;` 结束。

确保此文件是可读的（你必须对本章描述的所有 `.pm` 文件都这样做）：

```bash
$ chmod a+r HelloWorld.pm
```

我们需要告诉 Apache 如何使用此文件。在 `/etc/httpd/conf/httpd.conf` 的底部添加以下内容：

```apache
<Location /helloworld>
SetHandler perl-script
PerHandler HelloWorld
</Location>
```

此 Apache 指令表示，当请求 `/helloworld` URI 时，Apache 应该执行 Perl 模块 `HelloWorld`（存储在 `/var/www/mod_perl` 目录下的 `HelloWorld.pm` 文件中）。重启：

```bash
# /etc/init.dd graceful
```

并通过 `http://localhost/helloworld` 或 `www.opensourcewebbook.com/helloworld` 在浏览器中加载它。你应该看到图 8.4。

![](img/9b05e38e58495be06a08eeb2b6906346_280_0.png)

图 8.4 使用纯 `mod_perl` 的 hello, world!

## 8.4.1 关于 mod_perl 的重要说明

由于 `mod_perl` 模块在第一次执行时会在 Apache 中编译，因此每当模块更改时，必须重启服务器。即使磁盘上的程序文件发生了变化，`mod_perl` 也不会为我们重新编译。这可能是一个缺点，因为每次更改代码都要重启服务器是一件麻烦。所以，这就是你为了获得编译后的持久化代码的速度而做的权衡——当你更改内容时，必须重启服务器，而不是每次调用时都编译 Perl 代码。一旦程序开发并正常运行，由于此原因导致的重启就不是一个问题了。

## 8.4.2 使用 mod_perl 处理 POST 表单数据

正如你所看到的，CGI 程序的主要任务之一是处理 POST 表单数据。`mod_perl` 程序也需要执行相同的任务。使用 `mod_perl` 与 `CGI.pm` 有不同，因为我们使用的是 `mod_perl` API。

让我们来看一个示例。将以下内容放在 `/var/www/mod_perl/HandleCGIData.pm`：

```perl
package HandleCGIData;

# file: HandleCGIData.pm

use strict;

use Apache::Constants ':common';

sub handler {
    # 将参数位给 $r
    my $r = shift;
    # 初始化 %params，然后根据
    # 使用的方法
    # 为其分配表单数据
    my %params = ();
    if ($r->method() eq 'POST') {
        %params = $r->content();
    } else {
        $params = $r->args();
    }
    # 设置内容类型并发送
    # 标头
    $r->content_type(`text/html`);
    $r->send_http_header();
    # 打印初始 HTML
    $r->print(<<HTML);
<html>
<head>
<title>Processing CGI Data</title>
</head>
<body bgcolor="#ffffff">
<h1>Processing CGI Data!</h1>
</body>
</html>
HTML
    return OK;
}
1;
```

# 250

# 第三部分 动态

为了展示使用此模块的示例，我们回到 `mod.perl` 模块目录：

```bash
$ cd /var/www/mod.perl
```

创建 `HandleCGIData2.pm` 文件并将以下代码放入其中：

```perl
package HandleCGIData2;

# file: HandleCGIData2.pm

# 使用 语句，包括
# 我们新的 Apache::Request 模块
use strict;
use Apache::Constants `:common`;
use Apache::Request;

sub handler {
    # 移出参数并传递给
    # Apache::Request 类中的 new( ) 方法
    my $r = Apache::Request->new(shift);
    # 现在我们可以以类似于使用 CGI.pm 的方式
    # 使用 Apache::Request 对象调用 param() 
    my $name = $r->param('name') || 'John Doe';
    my $age = $r->param('age') || 50;
    # 设置内容类型并发送头信息
    $r->content_type('text/html');
    $r->send_http_header();
    # 打印 HTML，包括我们的变量
    # $name 和 $age
    $r->print(<<EOHTML);
<html>
<head>
<title>Using Apache::Request</title>
</head>
<body bgcolor="#ffffff">
<h1>Using Apache::Request</h1>
name = $name<br>
age = $age
</body>
</html>
EOHTML
    return OK;
}
```

[第 286 页]

# 第 8 章 mod.perl

# 251

![](img/9b05e38e58495be06a08eeb2b6906346_286_0.png)

图 8.6 使用 `Apache::Request` 通过 `mod.perl` 处理 CGI 数据

此版本的 `handler()` 在配合 `Apache::Request` 时，与之前的不同之处在于获取传递给程序的数据的方式。我们不再需要调用 `content()` 或 `args()`；`$r->param()` 的调用方式与使用 `CGI.pm` 调用 `param` 的方式相似。程序打印 HTML，返回 `0 OK`，并以 `1` 结束；

下一步要做的是通过 `/etc/httpd/conf/httpd.conf` 中添加以下内容来告知 Apache 此模块：

```apache
<Location /cgidata2>
SetHandler perl-script
PerlHandler HandleCGIData2
</Location>
```

重启 Apache：

```bash
# /etc/init.d/httpd graceful
```

然后访问这些 URL 之一：`http://localhost/cgidata2?name=John-Doe&age=39` 或 `www.opensourcewebbook.com/cgidata2?name=John-Doe&age=39`。你应该能图 8.6。

### 8.4.4 获取路径信息

可以通过简单的调用 `path_info()` 方法来获取路径信息，如下 `PathInfo` 中的示例所示：

[第 287 页]

```perl
package PathInfo;

# file: PathInfo.pm;
```
