
从当前目录及其所有子目录中提供文件服务。此外，如果一个文件位于特殊的 CGI 目录（由 `cgi_directories` 变量定义，该变量被设置为 `['/cgi-bin', '/htbin']`），则处理器将把该文件作为 CGI 脚本运行。这些处理器支持 GET、HEAD 和 POST 方法。它不支持 HTTP 重定向（HTTP 状态码 302），这限制了它仅用于简单的应用程序。出于安全考虑，CGI 脚本以 `nobody` 的用户 ID 执行。在 Python 2 中，此类类定义在 HTTPServer 模块中。

`SimpleRequestHandler(request, client_address, server)`

从当前目录及其所有子目录提供文件服务。该类分别提供对 HEAD 和 GET 请求的支持。IOError 异常将导致 "404 Directory not found" 错误。在 Python 2 中，此类定义在 SimpleHTTP 模块中。

这两个处理器都定义了以下类，如果需要可以通过继承进行更改：

```python
handler.server_version
返回给客户端的服务器字符串。默认情况下，它被设置为类似于 'SimpleHTTP/0.6' 的字符串。
```

`handler.extensions_map`

一个将后缀映射到 MIME 类型的字典。未识别的文件类型被认为是 'application/octet-stream'。

这里是一个使用这些处理器类运行能够执行 CGI 脚本的独立 Web 服务器的示例：

```python
try:
    from http.server import HTTPServer, CGIHTTPRequestHandler # Python 3
except ImportError:
    from BaseHTTPServer import HTTPServer      # Python 2
    from CGIBHTTPServer import CGIHTTPRequestHandler
import os
```

```python
# 修改文档根目录
os.chdir("/home/httpd/html")
# 在端口 8080 上启动 CGI 服务器
serv = HTTPServer(('', 8080), CGIHTTPRequestHandler)
serv.serve_forever()
```

# BaseHTTPRequestHandler

BaseHTTPRequestHandler 是处理 HTTP 请求的基类。要让服务器实际执行任何操作，你必须提供一个处理器类。有两个内置的处理器和一个可以用于定义你自定义处理器的基类。它们在接下来将被描述：

### SimpleRequestHandler 和 CGIRequestHandler

（注：此处根据原文逻辑，翻译可能存在重复，下文为 BaseHTTPRequestHandler 的详细描述）

BaseHTTPRequestHandler 是处理 HTTP 请求的基类。在 Python 2 中，它位于 HTTPServer 模块中。它位于特殊的 CGI 目录（由 `cgi_directories` 变量定义，该变量被设置为 `['/cgi-bin', '/htbin']`）。这些处理器支持 GET、HEAD 和 POST 方法。它不支持 HTTP 重定向（HTTP 状态码 302），这限制了它仅用于简单的应用程序。出于安全考虑，CGI 脚本以 `nobody` 的用户 ID 执行。在 Python 2 中，此类定义在 HTTPServer 模块中。

### BaseHTTPRequestHandler.server_version

指定服务器报告的服务器版本字符串。可以在子类中重写。

### BaseHTTPRequestHandler.sys_version

Python 系统版本，例如 'Python/2.6'。

### BaseHTTPRequestHandler.error_message_format

用于构建错误信息的格式字符串。例如：

```
<head>
<title>Error response</title>
</head>
<body>
<h1>Error code: %(code)s</h1>
<p>Message: %(message)s</p>
<p>Explanation: %(explanation)s.</p>
</body>
```

`HTTPRequest.protocol_version`

在响应中使用的 HTTP 版本。默认是 'HTTP/1.0'。

`HTTPRequest.responses`

整数错误代码映射到二元组 (message, explain)，用于描述问题。例如，错误代码 404 被映射为 ("Not Found", "Nothing matches the given URI")。

处理连接时，HTTPRequest 的实例 b 具有以下属性：

| 属性 | 描述 |
|---|---|
| b.client_address | 客户端地址，元组形式。 |
| b.command | 请求类型，例如 'GET'。 |
| b.path | 请求路径，如 '/index.html'。 |
| b.request_version | 请求版本，使用 'HTTP/1.0'。 |
| b.headers | 存储在映射对象中的 HTTP Header。要测试或提取标头内容，使用字典操作如 `headername in b.headers` 或 `headerval = b.headers[headername]` |
| b. | 用于读取可选数据的输入流。当客户端上传数据时使用（例如 POST 请求期间）。 |
| b.file | 向客户端写入响应的输出流。 |

以下方法在子类中常用或被重写：

- b.send_error(code [, message] ): 为失败的请求发送响应。code 是数值 HTTP 响应码。message 是可选错误。调用 log_error() 记录错误。该方法使用 error_message_format 创建一个完整的响应，将其发送给客户端并关闭连接。调用后不应进行任何后续操作。
- b.send_response(code [, message] ): 为成功的请求发送响应。发送 HTTP 响应行，随后是 Server 和 Date Header。code 是 HTTP 响应码，message 是可选消息。调用 log_request() 记录请求。
- b.send_header(keyword, value): 向输出流写入 MIME Header 条目。keyword 是标头关键字，value 是其值。这应该在 send_response() 之后调用。
- b.end_headers(): 发送空行以指示 MIME Header 的结束。

## 510 第 22 章 网络应用程序编程

```python
b.log_request([code, size])
```

记录一个成功的请求。`code` 是 HTTP 状态码，`size` 是响应的字节大小（如果可用）。默认情况下，调用 `log_message()` 进行记录。

```python
b.log_error(format, ...)
```

记录一条错误消息。默认情况下，调用 `log_message()` 进行记录。

```python
b.log_message(format, ...)
```

将任意消息记录到 `sys.stderr`。`format` 是应用于传递的额外参数的格式化字符串。每条消息都会带有客户端地址和当前时间的前。

这里有一个自定义 HTTP 服务器的示例，该服务器运行并用于管理字典的内容，并将请求路径解释为键。
