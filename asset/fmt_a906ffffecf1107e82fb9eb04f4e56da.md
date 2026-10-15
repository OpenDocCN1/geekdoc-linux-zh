
随着现在对隐私问题的讨论得轰轰烈，我们相信你知道在浏览时许多网站会掉落 Cookie。这种 Cookie 无非是一个包含标识符（如 `ID`）、一个值（如 `12345`）以及其他指示哪些服务器可以读取它以及何时过期的信息的文件。

# 第 10 模块：编写 CGI 程序 345

![](img/2070407c4a70134aab89572f10d21e60_368_0.png)

图 10-4 运行我们输出环境变量的 CGI 程序的结果

在下一节中，我们将快速查看 Cookie，因为它们在 Web 开发中很重要。

## 为什么用 Cookie？

HTTP 是一个无状态协议，这意味着服务器不会记录请求之间的客户端。为了解决这个问题，我们使用 Cookie 来存储会话信息。

# 346 | Perl：初学者指南

HTTP 是一个无状态协议，这意味着服务器不会在请求之间记住客户端。为了解决这个问题，我们使用 Cookie 来存储会话信息。

## 基础

Cookie 是服务器发送给浏览器的小段数据。浏览器随后存储这些数据并在每次请求时将其传回服务器。这使得服务器能够识别客户端。

Cookie 有三种创建方式：

- 在 HTTP 响应中发送 `Set-Cookie` 头部。
- 如果浏览器支持 JavaScript，可以使用 `document.cookie()` 方法设置 Cookie。
- 最后，可以在 HTML 文档中使用 `<meta>` 标签设置 Cookie。

## 字段

Cookie 使用 `Set-Cookie` 头部发送给浏览器。这是 Web 服务器或 CGI 脚本生成的 HTTP 响应的一部分。该头部指令格式如下：

```
Set-Cookie: key=value; expires=date; path=dir; domain=domain;secure
```

并不是所有的字段都是必须或显而易见的，让我们来看每一个：

- `key=value`: 键值对包含 Cookie 的名称及其分配的值。这是你应该在 CGI 脚本中查找的内容——它包含了你想留在浏览器上的信息。
- `expires=date`: 指定 Cookie 的持续时间。一旦超过此日期，浏览器将删除 Cookie。日期设置使用以下格式：

```
Weekday, DD-Mon-YYYY HH:MM:SS GMT
```

这些部分的具体含义如下：

- `Weekday`: 代表星期几，例如 Monday。
- `DD`: 代表日期，例如 23。
- `Mon`: 代表月份的三位字母缩写，如 Oct。
- `YYYY`: 代表年份，例如 2001。
- `HH`: 代表小时，如 08。
- `MM`: 代表分钟，如 58。
- `SS`: 代表秒，如 43。
- `GMT`: 代表格林治标准时间。

## Perl：初学者指南

### 注意

在设置 cookie 时，并非所有浏览器都要求指定所有这些字段。事实上，如果不包含日期，该 cookie 将成为会话级 cookie（session cookie），并将一直持续到读者退出浏览器为止。

- `path=dirpath` 指定 cookie 适用的服务器路径。这通常被设置为 `"/"`，通常称为根目录，但也可以指定另一个目录。这意味着一旦设置了 cookie，只有此目录中的文件和程序有能力读取该 cookie。

### 注意

如果未指定此设置，路径（path）将默认为设置 cookie 的文档的路径。

- `domain=domain` 指定要返回 cookie 的域名。此项目可以包含一个完整的机器主机名，例如 `shop.osborne.com`，或者仅包含域名，例如 `.osborne.com`。当你使用第二种方法时，该域名下的所有机器都有读取、删除或修改 cookie 的权限。

- `secure` 表明只有在您运行安全服务器时，才传输 cookie。此设置可以防止 cookie 在非安全端口上进行传输。

### 注意

如果你没有运行安全服务器而使用了 `secure` 设置，cookie 将不会发送。

## 设置

使用 `CGI.pm` 模块设置 cookie 非常简单。它提供了指定 `Set-Cookie` 指令值的所有必要方法。要查看如何实现，请看下文。在例例中，我们设置了一个名为 `ID` 的 cookie，值为 `12345`。它从今天起一年后过期，可以被从根目录开始的所有目录读取，可以传回位于 `192.168.1.101` 的服务器，并且是不安全的。最后一行是在发送到浏览器之前在 HTTP 头部中实际打印 cookie 的代码。

```
#!/usr/bin/perl -w
use CGI;

$query = new CGI;
$cookie = $query->cookie(-name=>'ID',
-value=>'12345',
-expires=>'+1y',
-path=>'/',
-domain=>'192.168.1.101',
-secure=>0);
print $query->header(-cookie=>$cookie);
```

发送的完整头部如下所示。而且，如果你配置了浏览器提示处理 cookie，那么你就会看到类似图 10-5 的内容，它显示了一个 Internet Explorer 5 浏览器提示你接受这个 cookie。

```
HTTP/1.1 200 OK
Server: Microsoft-IIS/5.0
Date: Fri, 01 Sep 2000 17:40:05 GMT
Set-Cookie: ID=12345; domain=127.0.0.1; path=;
expires=Sat, 01-Sep-2001 17:40:05 GMT
Date: Fri, 01 Sep 2000 17:40:05 GMT
Content-Type: text/html
```

![](img/2070407c4a70134aab89572f10d21e60_372_0.png)

图 10-5 Internet Explorer 5 提示你接受 cookie

既然你已经知道了如何设置 cookie 并理解了修改它需要做什么，这里是读取 cookie 的方法。

## 读取

读取 cookie 并不复杂。你只需要访问 `HTTP_COOKIE` 环境变量即可所有数据。所以，例如，你可能会得到下面的内容。请看下图查看我们在上一个示例中设置 cookie 后的输出。

```
#!/usr/bin/perl -w
use CGI;
$query = new CGI;
print $query->header;
print "<html><head>";
print $query->title('Cookies');
print "</head><body>";
print $query->h3('Cookies Sent To The Server');
print $ENV{'HTTP_COOKIE'};
print "</body></html>";
```

![](img/2070407c4a70134aab89572f10d21e60_373_0.png)

显然，这只打印了整个 cookie 字符串，因此如果服务器有多个 cookie 可以读取，你只需要看到它们以逗号分隔的格式列出来即可。由于你可能为了单独读取的目的而分离这些 cookie，我们向你展示如何创建一个 cookie 数组，然后将它们写回浏览器。因为我们需要多个 cookie，所以使用之前的方法设置了另一个名为 `ID2` 的 cookie。然后我们运行以下脚本。输出可以在图 10-6 中看到。

```
#!/usr/bin/perl -w
use CGI;
$query = new CGI;
$i = 0;

if (defined $ENV{HTTP_COOKIE}) {
  @array = split(//, $ENV{HTTP_COOKIE});
}

print $query->header;
print "<html><head>";
print $query->title('Cookies');
print "</head><body>";
print $query->h3('Cookies Sent To The Server');
print "Total Cookie String: $ENV{HTTP_COOKIE}<br>";
foreach $cookie (@array) {
    print "<br>Cookie[$i]: $cookie";
    $i++;
}
print "</body></html>";
```

![](img/2070407c4a70134aab89572f10d21e60_374_0.png)

图 10-6 返回 cookie 数组

## 模块 10：编写程序
