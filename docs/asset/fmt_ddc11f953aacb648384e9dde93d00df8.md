
- `AUTH_TYPE`—如果页面受密码保护，则为授权类型

- `CONTENT_LENGTH`—正在写入标准输入的字节数（用于 POST 表单）

- `CONTENT_TYPE`—表单的内容类型

- `DOCUMENT_ROOT`—Web 服务器文档树的根目录

- `GATEWAY_INTERFACE`—Web 服务器使用的 CGI 标准版本

- `HTTP_ACCEPT`—浏览器可接受的数据类型（例如，`text/html`）

- `HTTP_ACCEPT_CHARSET`—Web 浏览器请求的字符集

- `HTTP_ACCEPT_ENCODING`—Web 浏览器允许的压缩方法（例如，`gzip`）

- `HTTP_ACCEPT_LANGUAGE`—Web 浏览器请求的语言（例如，英语为 `en`）

- `HTTP_USER_AGENT`—用户使用的浏览器

- `HTTP_HOST`—URL 的主机名

- `HTTP_REFERER`—执行此 CGI 程序的网页

- `PATH_INFO`—包含在 URL 中的额外信息

- `PATH_TRANSLATED`—作为文档树根下的文件/目录的 `PATH_INFO`

- `QUERY_STRING`—对于 GET 表单，即表单中的变量

- `REMOTE_ADDR`—用户计算机的 IP

- `REMOTE_HOST`—用户计算机的主机名

- `REMOTE_USER`—访问受密码保护页面时使用的用户名

- `REQUEST_METHOD`—通常是 `GET` 或 `POST`

- `SCRIPT_NAME`—正在执行的脚本的路径名

- `SCRIPT_FILENAME`—正在执行的脚本的绝对路径名

- `SERVER_ADDR`—Web 服务器的 IP 地址

- `SERVER_ADMIN`—发送给 Web 服务器负责人的电子邮件地址

- `SERVER_NAME`—Web 服务器的域名

- `SERVER_PORT`——用于连接 Web 服务器的 TCP/IP 端口

- `SERVER_PROTOCOL`——服务器使用的 HTTP 版本

- `SERVER_SOFTWARE`——Web 服务器的描述

## 表单处理

环境变量在 HTML 中的等价物是表单。每个表单都包含一组变量。例如，表单输入标签：

```html
<input type='hidden' name="user" value="bmith">
```

是以下命令的 HTML 等价形式：

```bash
declare user="bmith"
```

其他非隐藏输入标签代表那些值可以被用户通过表单上的项目修改的变量。此类项目包括按钮、菜单和文本框。在所有这些情况下，用户所做的选择会在表单发送给 CGI 脚本之前被保存为该变量的新值。

由于 CGI 脚本并未接收到 Web 页面的副本，它如何得知输入标签的值呢？有两种方法。较旧的 `GET` 方法将 HTML 变量存储在一个名为 `QUERY_STRING` 的环境变量中。请考虑以下表单。

```html
<html>
<head>
<title>Form Test</title>
</head>
<body>
<form action="http://localhost/cgi-bin/form.cgi">
<input type="hidden" name="user" value="bmith">
<input type="submit" name="submit" value="Click Me!">
</form>
</body>
</html>
```

查询字符串包含这两个变量的名称和值。

`user=bmith&submit=Click+Me%21`

表单难以处理的原因之一是信息是经过编码的。标准表单编码（`x-www-form-urlencoded`）将空格转换为加号，将非字母数字字符转换为带有前导百分号的 ASCII 十六进制数。在这种情况下，感叹号被转换为十六进制 21。

`POST` 方法将变量写入标准输入，如果变量列表变得非常长，这就消除了 Web 服务器中缓冲区溢出的风险。它还使变量不出现在 Web 页面的 URL 中。如果脚本在 while 循环中读取变量，则由于该行没有以换行符结尾，while 循环中的最后一行不会执行。

```bash
while read LINE; do
    echo "$LINE"
done
echo "$LINE"
```

这显示了与使用 GET 方法时出现在 `QUERY_STRING` 中的相同编码信息。

`user=smith&submit=Click+Me%21`

列表 16.4 中所示的 `form.cgi` 脚本解码并显示表单变量。

### 列表 16.4 form.cgi
