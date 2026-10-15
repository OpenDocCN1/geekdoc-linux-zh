
点击浏览器上的“重新加载”按钮将再次请求相同的 URL，浏览器将从服务器接收到相同的身份挑战。这次输入“reader”作为用户名，“bought-it”作为密码，并点击 OK 按钮。Apache 现在将允许你访问该目录。

如果你想，可以使用 `ErrorDocument` 指令更改“需要验证”消息：

```
ErrorDocument 401 /nice_401message.html
```

将此行插入到你的 `srm.conf` 文件中并在 `nice_401message.html` 文件中创建一个友好的消息，让你的用户感到愉快。

与其像上一个示例那样使用名为“reader”的单一用户访问受限区域，在这里你将允许任何属于“ash_readers”组的成员访问同一个目录。假设该组有两个用户：`pikejb` 和 `bcaridad`。按照以下步骤让 `ash_readers` 组的用户获得目录访问权限。

### 第 1 步：使用 htpasswd 创建用户文件
使用 `htpasswd` 工具创建用户 `pikejb` 和 `bcaridad`。

## 第四部分：设置内网/互联网服务

### 第 2 步：创建组文件
使用如 `vi` 等文本编辑器创建一个名为 `/data/web/apache/secrets/.htgroup` 的文件。该文件只有一行，如下：

```
asb_readers: pikejb bcaridad
```

### 第 3 步：在 `/data/web/apache/public/htdocs/chapter_10` 中创建 `.htaccess` 文件
使用文本编辑器，在 `/www/IDGbooks/readers/.htaccess` 文件中添加以下行：

```
AuthName "IDG Readers Only"
AuthType Basic
AuthUserFile /data/web/apache/secrets/.htpasswd
AuthGroupFile /data/web/apache/secrets/.htgroup
require group asb_readers
```

这与我在上一个示例中讨论的配置几乎相同，但有两个更改。第一个更改是增加了一个新指令 `AuthGroupFile`，它指向之前创建的 `.htgroup` 组文件。下一个更改位于 `require` 指令行，它现在要求一个名为“asb_readers”的组。换句话说，Apache 将允许任何属于该组的人访问。你也可以同样轻松使用以下行：

```
require user pikejb bcaridad
```

而不是：

```
require group asb_readers
```

然而，在 `require` 行中列出所有用户可能会变得繁琐并引起不必要的头疼。使用 `group`，你可以轻松地添加或删除多个用户。在上一个示例中，确保 `.htaccess`、`.passwd` 和 `.htgroup` 文件仅供 Apache 读取，并且除所有者外无人可以访问这些文件很重要。

你还可以将 Apache 的基于主机的访问控制与基础 HTTP 认证方案结合。例如：

```
AuthName "IDG Readers Only"
AuthType Basic
AuthUserFile /data/web/apache/secrets/.htpasswd
AuthGroupFile /data/web/apache/secrets/.htgroup
require group asb_readers
order deny, allow
deny from all
allow from nitec.com
```

## 第 12 章：Web 服务

这与上一个示例相同，但增加了前面章节讨论过的三个基于主机的访问控制指令。第一个是 `order` 指令，它告诉 Apache 在执行 `allow` 指令之前评估 `deny` 指令。`deny` 指令告诉 Apache 拒绝所有主机的访问。`allow` 指令告诉 Apache 允许来自 `apache-training.niteec.com` 域的访问。这实际上告诉 Apache `.niteec.com` 域中的主机欢迎访问此目录。请注意，这里 Apache 将假设基于主机的和基础 HTTP 认证对于此目录是可读的。如果你想在用户输入有效的用户名/密码对或从 `nitec.com` 域发送请求时允许访问，你需要满足前面配置末尾的任何条件。

## 监控服务器状态

`mod_status_module` 允许 Apache 管理员通过 Web 监控服务器。创建一个 HTML 页面。两个页面上显示的信息包括：服务器版本、编译日期、服务器运行时间、到目前的总请求数、到目前传输的字节数、空闲服务器数量、CPU 使用率、服务器负载以及正在处理的请求数。

该模块默认没有编译进 Apache，因此你需要将其编译。假设你的域名是 `mydomain.com`，你想使用以下 URL：`www.mydomain.com/server-status`。使用 `<Location>` 容器，你可以告诉服务器使用哪个 URL。以下行将完成工作：

```
<Location /apache-status>
SetHandler server-status
</Location>
```

在这里，`SetHandler` 指令为上述的 URL 设置处理器（`server-status`）。此配置段通常应该放在 `access.conf` 中，也可以放在三个文件中的一个。如果你在其中文件中添加了配置，可以从浏览器访问之前的 URL。注意，此示例中的 `<Location>` 容器允许任何人使用此 URL 查看服务器状态；这在安全性方面可能不是好事。为了确保只有你域名的机器可以访问状态页，可以将之前的配置替换为：

```
<Location /apache-status>
SetHandler server-status
order deny, allow
deny from all
allow .yourdomain.com
</Location>
```

`yourdomain.com` 应替换为你自己的域名。如果你只想让一个或多个特定的主机访问此页面，可以在 `allow` 指令中直接列出主机名。

> TIP 如果你的浏览器支持刷新命令，可以让页面自动更新。访问 `http://www.yourdomain.com/server-status?refresh=N` 每刷新 N 秒。在 URL 末尾添加 `?auto` 可以简化状态显示。

## 记录访问和错误

了解服务器的运行状态对于管理服务器很有帮助，了解谁或什么正在访问你的网站也非常重要，而且令人兴奋。许多 Web 服务器日志分析程序也随之出现。随之而来的是日志文件不兼容，这导致日志分析变得困难繁琐；没有一个分析程序可以处理所有日志文件。然后出现了通用日志格式（CLF）规范。这使得所有 Web 服务器都能以类似的方式写入日志，使服务器之间的日志分析变得更容易。

默认情况下，标准 Apache 包含一个名为 `mod_log_config` 的模块，它负责基础日志记录并默认写入 CLF 日志文件。你可以使用 `LogFormat` 指令来更改这种行为。

CLF 文件每个请求包含单独的一行。每行由多个用空格分隔的标记（tokens）组成：

`host ident autuser date request status bytes`

如果某个标记没有值，则用连字符 (`-`) 表示。标记具有以下含义：

- Host：这是客户端的完全限定域名名，或其 IP 地址。
- Ident：如果启用了 `IdentityCheck` 指令且客户端机器运行了 `ident`，则这是由客户端报告的身份信息。
- Autuser：如果请求的 URL 需要成功的 HTTP 身份验证，则用户名是该标记的值。
- Date：这是请求的日期和时间。
- Request：这是来自客户端的请求行，包含在双引号 (`"`) 中。
- Status：这是返回给客户端的三位 HTTP 状态码。
- Bytes：这是返回给客户端的对象的字节数，不包括所有 HTTP 头部。

日期字段可以具有以下格式：

```
date = [day/month/year:hour:minute:second zone]
```

例如：

```
[02/Jan/1998:00:22:01 -0800]
```

`mod_log_config` 模块提供了四个指令：

`TransferLog filename | "/path/to/external/program"`

此指令设置用于发送日志信息的日志文件名称或程序路径。默认情况下，日志信息采用常用日志文件 (CLF) 格式。该格式可以使用 `LogFormat` 指令进行自定义。

当在虚拟主机容器内找到 `TransferLog` 指令时，日志信息将使用该上下文中的 `LogFormat` 指令进行格式化。然而，如果在同一上下文中没有找到 `LogFormat` 指令，则将使用服务器的日志格式。

`TransferLog` 指令接受日志文件路径或指向外部程序的管道（pipe）作为参数。如果未发现开头的 `/` 字符，则假设日志文件名相对于 `ServerRoot` 设置。例如，如果 `ServerRoot` 设置为 `/etc/httpd`，则以下命令告诉 Apache 将日志信息发送到 `/etc/httpd/logs/access.log`：
