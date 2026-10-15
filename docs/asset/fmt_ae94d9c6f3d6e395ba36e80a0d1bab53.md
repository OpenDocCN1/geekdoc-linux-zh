
# 第 33 章 配置 Apache

## 高功能

这意味着任何以 `.asis` 结尾的文件都可以包含其自己的 MIME 头部。然而，它在内容的正文之前必须包含两个回车符。实际上，它应该包含两个回车/换行符组合，Apache 是宽容的，它会为你插入换行符。如果你想发送一个没有向服务器注册的特殊 MIME 类型的文档，你可以发送：

```
Content-type: text/foobar
```

这是一个非常特殊的 "foobar" MIME 类型文本。

我运行过的此功能最重要的应用是作为一种极其高效的机制，用于在服务器推送（内联图形）对象时无需 CGI 脚本。需要 CGI 脚本来创建服务器推送的原因通常是内容类型通常包含 multipart 分隔符（因为服务器推送实际上是一个 MIME multipart 消息）。在下面的示例中，XXXXXXX 表示 multipart 消息各部分之间的边界：

```
Content-type: multipart/x-mixed-replace;boundary=XXXXXXX

XXXXXXX

Content-type: image/gif
```

```
...(GIF data)...

XXXXXXX

Content-type: image/gif
```

```
...(GIF data)...

XXXXXXX
```

通过在 `AddType` 指令中使用 `.asis` 参数将数据流简单地作为文件，而不是使用 CGI 脚本，你可能为自己节省了大量的开销。你唯一失去的几乎仅仅是执行定时推送的能力。对于许多人来说，缓慢的 Internet 连接充当了足够的时间缓冲。

如果你开启了 `Multiview`，你可以在文件名末尾添加 `.asis`，而你的任何链接都不需要重命名。例如，`foobar.html` 可以很容易变成 `foobar.html.asis`，但你仍然可以调用 `foobar.html`。

![](img/bffdba228b656a1846f7f38a3801d7f2_694_0.png)

"asis" 的最后一个引人注目的应用是在无需访问服务器配置文件的情况下进行 HTTP 重定向。例如，以下 `.asis` 文件将把人们重定向到另一个位置：

```
Status 302 Moved

Location: http://some.other.place.com/path/

Content-type: text/html
```

```html
<HTML>
<HEAD><TITLE>We've Moved!</TITLE></HEAD>
<body
<H1>We used to be</H1>
</body>
</HTML>
```

## 基于主机的访问控制

## 用户身份验证

`AuthType` 指令设置该区域的认证类型。在 HTTP/1.0 中，只有一种认证类型——Basic（基本）。HTTP/1.1 将会有更多几种，例如 MD5。

`AuthFile` 指令指定包含用户名和密码列表的文件，每行一个。密码通过简单的 UNIX `crypt()` 句例进行加密。例如：

```
joe:D2W2ylfjaJao
mark:21slfOUYksie
```

`AuthGroup` 指令指定包含组列表及其成员列表的文件，成员之间用空格分隔。例如：

```
managers: joe mark
production: mark shelley paul
```

最后，`require` 指令指定了授予访问权限需要满足的条件。它可以仅列出允许连接的特定用户，指定一个允许连接的用户组或用户组列表，或者表示数据库中的任何有效用户都将自动获得访问权限。例如：

```
require user mark paul

（只有 mark 和 paul 可以访问。）
```

```
require group managers

（只有 managers 组中的人员可以访问。）
```

```
require valid-user

（AuthUser 数据库中的任何人都可以访问。）
```

配置文件的最终外观看起来如下所示：

```
<Directory /www/htdocs/protected/
AuthName Protected
AuthType basic
AuthUserFile /usr/local/etc/httpd/conf/users
<Limit GET POST>
require valid-user
</Limit>
</Directory>
```

如果您想为特定组保护某个目录，配置文件看起来如下所示：

```
<Directory /www/htdocs/protected/
AuthName Protected
AuthType basic
AuthUserFile /usr/local/etc/httpd/conf/users
AuthGroupFile /usr/local/etc/httpd/conf/group
<Limit GET POST>
require group managers
</Limit>
</Directory>
```

`http://www.quecorp.com`

## 数据库管理文件认证

您还可以配置 Apache 使用 DBM 文件来更快速地查找密码和组成员身份。要使用 DBM 文件，您必须在服务器中编译了 `mod_auth_dbm` 模块。

DBM 文件是 UNIX 文件类型，实现了快速哈希表查找，使其成为处理大型用户/密码数据库的理想选择。平文件系统需要为每次访问解析密码，直到找到匹配项，在返回“找不到该用户”错误之前，可能会遍历整个文件。相比之下，哈希表可以瞬间判断数据库中是否存在某个“键”以及其值是什么。

某些系统使用 ndbm 文件；另一些系统使用 berkeley db 库。然而，通过 Apache 提供的接口是完全相同的。

要使用数据库而不是普通文件，您需要使用不同的指令 `AuthDBMUserFile` 来代替 `UserFile`。同样，对于组文件，使用 `AuthDBMGroupFile` 代替 `AuthFilePath`。

## 虚拟主机

> 提示 Apache 1.2 通过 HTTP 1.1 协议规范支持非基于 IP 的虚拟主机。有了此新功能，您不再需要为每个虚拟主机提供 IP 地址。

虚拟主机通过使用 `httpd.conf` 中的容器进行配置。它们看起来像这样：

```
<VirtualHost www.host1.com>
DocumentRoot /www/htdocs/host1/
TransferLog logs/access.host1
ErrorLog logs/error.host1
</VirtualHost>
```

`VirtualHost` 标签中的属性是主机名，服务器通过查找它来获取 IP 地址。

> 注意 如果 `host1.com` 有任何可能返回多个数字的情况，或者 Web 服务器在任何时候可能无法将主机名解析为 IP 数字，您可能希望直接使用 IP 数字。

`VirtualHost` 容器内的任何指令都仅适用于指向该主机名的请求。`DocumentRoot` 指向一个认为专门包含 `www.host1.com` 内容的目录。

每个虚拟主机都可以有自己的访问日志、自己的错误日志，以及其他日志的变体；每个主机都可以有自己的 `Redirect` 和 `Alias` 指令、自己的 `ServerName` 和 `ServerAdmin` 指令，以及更多。事实上，虚拟主机服务器在核心指令集中唯一无法支持的项是：

| `ServerType` | `MaxRequestsPerChild` |
| :--- | :--- |
| `UserId` | `BindAddress` |
| `GroupId` | `PidFile` |
| `StartServers` | `TypeConfig` |
| `MaxParseServers` | `ServerRoot` |
| `MinSpareServers` | |

如果您计划运行带有大量虚拟主机的 Apache，您需要小心观察进程限制。例如，某些 UNIX 平台一次允许打开 64 个文件描述符。因为 Apache 子进程为每个虚拟主机的每个日志文件消耗一个描述符，32 个虚拟主机——每个都有自己的传输日志和错误日志——将迅速突破该限制。如果您的错误日志开始报告此类无法 `fork()` 的错误，或者所有访问日志都没有被写入，您就会注意到自己遇到了这类问题。Apache 确实尝试调用 `setrlimit()`（一种限制进程的系统函数调用）来自行处理此问题，但系统有时会阻止其成功执行系统调用。

## 自定义错误消息

Apache 可以在发生错误时提供自定义的响应。这是通过使用 `ErrorDocument` 指令控制的。语法为：

```
ErrorDocument HTTP_response_code action
```
