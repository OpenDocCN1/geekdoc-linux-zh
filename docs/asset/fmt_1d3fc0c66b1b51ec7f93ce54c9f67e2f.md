
## 多选框
```perl
print $query->b("<br>Music Tastes<br>");
print $query->param('type');
```

## 文本框
```perl
print $query->b("<br>Other<br>");
print $query->param('othermusic');
```

## 复选框
```perl
print $query->b("<br>Sports Interest<br>");
print $query->param('sports');
print $query->param('foot');
print $query->param('soccer');
```

## 单选按钮
```perl
print $query->b("<br>Gender<br>");
print $query->param('gender');
```

## 多行文本区域
```perl
print $query->b("<br>Comments<br>");
print $query->param('comments');
```

## 密码框
```perl
print $query->b("<br>Password<br>");
print $query->param('passwd');
```

## 隐藏域
```perl
print $query->b("<br>Hidden (Version)<br>");
print $query->param('version');
```

现在，我们只需要将此程序复制到我们的 CGI 目录并提交表单。图 10-8 显示了表单完成后的样子，图 10-9 显示了我们的结果页面。

### 快速格式化

到为止，我们一直在反复使用 `print()` 函数。实际上，你可以通过将所有行封装在一个标记（token）中来节省输入它的时间。例如，你可以使用 `print"_HTML_";`。

# 模块 10：编写 CGI 程序 357

![](img/2070407c4a70134aab89572f10d21e60_380_0.png)

## 图 10-8 我们完成的表单

![](img/2070407c4a70134aab89572f10d21e60_380_1.png)

## 图 10-9 我们的结果页面

使用 `_HTML_` 开始序列，用 `_HTML_` 结束。与其试图解释这一点，这里有一个快速示例。

```perl
#!/usr/bin/perl -w
use CGI;

## 定义 CGI 实例并写出头部
$query = new CGI;
print $query->header;

## 打印以下所有内容
print<<"HTML_";
<html>
<head>
<title>Using Tokens</title>
</head>
<body>
<p>现在所有这些内容都将被打印，而无需为每一行专门使用 print() 函数。</p>
</body>
</html>
_HTML_
```

### 你可以手动执行的额外操作

啊啊，完整的 Perl 库真是美极。CGI.pm 让它变得简单了，不是吗？那么，如果你想自己更改某些默认值而不是让它自动设置会呢？比如标头指令（header directives）。那时怎么办？嗯，你可以这样做，所以不要担心。这里快速查看你可能想自己执行的几项。

### 指定内容类型 (Content Type)

Web 服务器可以向浏览器返回许多数据类型。例如，Web 服务器可以返回 HTML 文档、图像、纯文本、音频、视频等。然而，返回给浏览器的响应部分必须包含所返回信息的的 `Content-type` 标头。

`Content-type` 标头让你指定 MIME 数据类型，然后浏览器可以对其进行适当处理。`Content-type` 标头的第一部分是顶级 MIME 类型，后面跟着正斜杠，然后是 MIME 子类型。例如，为 HTML 文档返回的通用内容-type 为：

Content-type: text/html

# 模块 10：编写 CGI 程序 | 359

当使用 CGI.pm 模块时，此标头指令使用以下格式设置：

```perl
#!/usr/bin/perl -w
use CGI;

$query = new CGI;
print $query->header(-type=>'text/html');
```

### 重定向

你可能想使用的第二个流行的标头是 `Location` 标头，它允许将浏览器重定向到另一个位置。当页面移动时，你会看到这个。这是最容易实现的内容之一，可以在没有 CGI.pm 模块帮助的情况下完成。

如果你想在没有 CGI.pm 模块帮助的情况下完成它，请使用以下语法。例如，这将用户发送到 `/error.html` 页面。注意语句末尾的 `\n\n`。这对于告诉用户响应的头部部分已结束是必要的。这仅应用于最后一个标头指令，否则它下方的任何标头指令将被解释为正文并在浏览器中显示。

如果你决定使用 CGI.pm 模块，那么只需要包含以下内容即可实现重定向：

```perl
#!/usr/bin/perl -w
use CGI;

$query = new CGI;
print $query->redirect('/error.html');
```

### 提示

使用 CGI.pm 的优势在于它还会插入其余所需的 HTTP 标头指令。浏览器通常在没有这些 HTTP 标头的情况下也能工作，但有了它们会更完整。

## Perl：初学者指南

### HTTP 状态码

当服务器响应 HTTP 请求时，如之前讨论的，它会带有头部（header）和正文（body）进行响应。然而，头部的一部分包含响应的状态码。此状态告诉浏览器返回的是哪种响应。例如，如果发生错误或浏览器被重定向到另一个位置，是这个代码告诉浏览器的。

通常由 Web 服务器指定这些代码，尽管在你的脚本中可能需要这样做。当使用 CGI.pm 模块时，你只需要设置 `header` 属性的 `-status` 属性。例如，假设你想向浏览器发送一个虚构的状态码 699。你可以使用 `/usr/bin/perl -w` 配合以下代码。

```perl
#!/usr/bin/perl -w
use CGI;

$query = new CGI;
print $query->header(-status=>699, 'My Crazy Status');
```

这向浏览器返回以下内容：

```
HTTP/1.0 699 My Crazy Status
Content-type: text/html
```

要发送状态码，你需要知道响应的类型。它们被分为以下几类：

- 1xx 信息提示 (Informational)
- 2xx 成功 (Success)
- 3xx 重定向 (Redirection)
- 4xx 客户端错误 (Client Error)
- 5xx 服务错误 (Server Error)

# 模块 10：编写 CGI 程序 384

表 10-2 描述了可能的状态码。

| 代码 | 响应 | 描述 |
|---|---|---|
| 100 | Continue | 应该继续。 |
| 101 | Switching Protocols | 应该切换协议。 |
| 200 | OK | 请求成功了。 |
| 201 | Created | 请求已创建。 |
| 202 | Accepted | 请求已接收，但尚未完成处理。 |
| 204 | No Content | 没有要返回的内容。 |
| 206 | Partial Content | 请求已部分完成。 |
| 300 | Multiple Choices | 资源有多个位置。 |
| 301 | Moved Permanently | 资源永久移动。 |
| 303 | See Other | 应该从指定的地址获取。 |
| 304 | Not Modified | 文档未更改。 |
| 305 | Use Proxy | 在之前的 HTTP 版本中使用的代码。 |
| 307 | Temporary Redirect | 请求已临时移动。 |
| 400 | Bad Request | 请求错误，例如语法错误。 |
| 401 | Unauthorized | 身份验证请求失败。 |
| 402 | Payment Required | 预留用于响应。 |
| 403 | Forbidden | 禁止访问。 |
| 404 | Not Found | 文档、查询或 URL 未找到。 |
| 405 | Method Not Allowed | 用户发送的请求方法不被允许。 |
| 406 | Not Acceptable | 根据用户发送的 Accept 头部，资源不可接受。 |
| 407 | Proxy Authentication Required | 与 401类似，用户必须在代理中进行验证。 |
| 408 | Request Time-out | 用户未在规定时间内完成请求。 |
