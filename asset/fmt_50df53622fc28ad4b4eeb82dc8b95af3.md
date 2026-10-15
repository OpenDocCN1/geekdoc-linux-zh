
CGI 脚本有一个糟糕的习惯，会在错误日志中留下既没有时间戳也没有被完全标识的警告消息。追踪导致错误的脚本是一件痛苦的事。`CGI::Carp` 解决了这个问题。将通常的

```
use Carp;
```

替换为

```
use CGI::Carp
```

标准的 `warn()`, `die()`, `croak()`, `confess()`, `carp()` 调用将自动替换为带有良好时间戳的消息并写入 HTTP 服务器日志的函数。例如：

- `[Fri Nov 17 21:40:43 1995] test.pl: I'm confused at test.pl line 3.`

- `[Fri Nov 17 21:40:43 1995] test.pl: Got an error: Permission denied.`

- `[Fri Nov 17 21:40:43 1995] test.pl: I'm dying.`

# 标准 Perl 模块 675

使用 `carpout()` 对性能不利；然而，建议在中等应用程序中使用它。也许此模块的未来版本将在调用 `CGI::Carp` 方法时才延迟重定向。

# 在浏览器窗口显示 Perl 错误

如果你想将致命 `die`, `confess` 错误发送到浏览器，请导入 `FatalToBrowser` 子例：

```
use CGI::Carp qw(FatalToBrowser);
die "Bad error here";
```

致命错误现在也会回送到浏览器和日志。`CGI::Carp` 将一个一个 HTTP 头部以便以便编译阶段错误的错误可见。非致命错误仅重指向日志文件（除非使用 `carpout`）。

# 更改默认消息

默认情况下，软件错误消息后面会跟着通过电子邮件联系管理员的提示。如果你不喜欢此消息，可以使用 `set_message()` 例程更改它。该例程默认不导入。你应该在 `use()` 行导入它：

```
use CGI::Carp qw(FatalToBrowser set_message);
set_message("It's not a bug, it's a feature!");
```

你也可以传递代码引用来创建自定义错误消息。在运行时，你的代码将带有导致脚本 `die` 的错误消息文本调用。例如：

```
use CGI::Carp qw(FatalToBrowser set_message);
BEGIN {
    sub handle_errors {
        my $msg = shift;
        print "<h1>Oh gosh </h1>";
        print "Got an error: $msg";
    }
    set_message(\&handle_errors);
}
```

为了正确拦截编译时错误，你应该在 `BEGIN{}` 块内部调用 `set_message()`。

## `CGI::Cookie`

该模块是一个标准接口，提供了对 Netscape 风格浏览器 cookie 的读取、解析和写入。

### 概要

```
use CGI qw/:standard;
```

```
use CGI::Cookie;
```

```
# 创建新的 cookie 并发送它们
$cookie1 = new CGI::Cookie(-name=>'ID',-value=>123456);
$cookie2 = new CGI::Cookie(-name=>'preferences',
-value=>{ font => Helvetica,
 size => 12 });

print header(-cookie=>[$cookie1,$cookie2]);
```

```
# 获取现有的 cookie
%cookies = fetch CGI::Cookie;
$id = $cookies('ID')->value;
```

```
# 从外部源创建 cookie
%cookies = parse CGI::Cookie($ENV{COOKIE});
```

### 描述

`CGI::Cookie` 是 Netscape `HTTP/1.1` cookie 的接口。这允许 Web 服务器在连接的浏览器端存储信息，以便这些信息能够跨多个客户端请求持久化。尽管 `CGI::Cookie` 旨在用于与 `CGI.pm` 配合使用（并在内部被调用），但你可以独立使用该模块。

关于 cookie 的信息，请参阅：http://www.uci.edu/pub/ietf/http/rfc2109.txt。

**使用 `CGI::Cookie`** `CGI::Cookie` 是面向对象的。每个 cookie 对象都有一个名称和一个值。名称可以是任何标量值。值可以是标量或数组值（也允许关联数组）。cookie 还有几个可选属性，包括：

- **过期日期 `Expiration Date`** 过期日期告诉浏览器保留 cookie 的时间。如果 cookie 指定了未来的过期日期，浏览器会将 cookie 信息存储在磁盘文件中，并在用户每次重新连接时将其返回给服务器，直到到达过期日期。如果 cookie 指定了过去的过期日期，浏览器将从磁盘文件中删除该 cookie。如果没有指定过期日期，cookie 将仅持续到用户退出浏览器为止。

- **域名 `Domain`** 这是 cookie 有效的部分域名或完整域名名。浏览器会将 cookie 返回给任何匹配该部分域名的宿机。例如，如果你指定了域名 `.capicorn.com`，Netscape 会将 cookie 返回给运行在 `www.capicorn.com`、`ftp.capicorn.com`、`heckless.capicorn.com` 等任何机器上的 Web 服务器。域名必须包含至少两个点才能匹配像 `.edu` 这样的顶级域名。如果没有指定域名，浏览器将仅将 cookie 返回给产生该 cookie 的宿主机服务器。

- **路径 `Path`** 如果你提供了 cookie-path 属性，浏览器会在返回 cookie 之前将其与脚本的 URL 进行检查。例如，如果你指定了路径 `/cgi-bin`，cookie 将返回给 `/cgi-bin/tally.pl`、`/cgi-bin/order.pl` 和 `/cgi-bin/customer_service/complain.pl` 每个脚本，但不会返回给脚本 `/cgi-bin/private/site_admin.pl`。默认情况下，path 设置为反斜杠 `/()`，会导致 cookie 发送到你站点上的任何 CGI 脚本。

- **安全标记 `Secure Flag`** 如果设置了 secure 属性，只有当 CGI 请求发生在安全通道（如 SSL）上时，cookie 才会发送给你的脚本。

### 创建新 Cookie

```
$c = new CGI::Cookie(-name => 'foo',
-value => 'bar',
-expires => '+3M',
-domain => '.capicorn.com',
-path => '/cgi-bin/database'
-secure => 1
);
```

使用 `new` 方法从零创建 cookie。`-name` 和 `-value` 参数是强制的。名称必须是一个标量值。值可以是标量、数组引用或哈希引用。（在未来的某个时刻，cookie 将支持一种 Perl 对象序列化协议以实现完全通用性）。

除了所需的 `-name` 和 `-value` 参数外，还可以指定以下可选参数：

- `-expires` 接受 `CGI .pm` 识别的任何相对或绝对日期格式（例如 `'+3M'` 表示三个月后）。详情请参见 `CGI .pm` 的文档。

- `-domain` 指向域名或完全限定的主机名。如果没有指定，cookie 只返回给创建它的 Web 服务器。

- `-path` 指向当前服务器上的部分 URL。cookie 将返回给所有以指定路径开头的 URL。如果没有指定，默认为 `/`，这会将 cookie 返回给你站点上的所有页面。

- `-` 如果设置为真值，`secure` 指示浏览器仅在在使用加密协议时返回 cookie。

### 将 Cookie 发送到浏览器

在 CGI 脚本内部，你可以通过在 HTTP 头部中创建一个或多个 `Set-Cookie` 字段将 cookie 发送到浏览器。以下是一个典型的序列：

```
my $sc = new CGI::Cookie(-name => 'foo',
               -value => ['bar', 'baz'],
               -expires => '+3M');
```

```
print "Set-Cookie: $sc\n";
print "Content-Type: text/html\n\n";
```

要发送多个 cookie，请创建多个 `Set-Cookie` 字段。或者，你可以用分号和空格（...）连接 cookie 并在一个字段中发送它们。

内部，Cookie 重载了 `""` 运算符，以便在合并 HTTP 头部时调用其 `as_string()` 方法。`as_string()` 命令将 cookie 的内部表示转换为符合 RFC 标准的文本。你可以调用 `as_string()` 命令。
