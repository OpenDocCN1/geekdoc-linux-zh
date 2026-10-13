
`SetHandler server-status`

</Location>

`SetHandler`指令为前面提到的URL设置处理程序（`server-status`）。此配置段通常应放在`access.conf`文件中，但实际上可以放在任何三个配置文件中。

在其中一个文件中添加配置后，您可以重新启动服务器并从浏览器访问前面的URL。请注意，此示例中的`<Location ...>`容器允许任何人使用此URL查看服务器状态，这在安全方面可能并不理想。为了确保只有您域上的机器可以访问状态页面，请将前面的配置替换为以下内容：

```
<Location /apache-status>
SetHandler server-status
order deny, allow
deny from all
allow from .yourdomain.com
</Location>
```

其中`yourdomain.com`应替换为您自己的域名。如果您只希望一个或多个选定主机可以访问此页面，只需在`allow`指令行中列出主机名即可。

### 提示
如果您的浏览器支持`refresh`命令，您可以让状态页面自动更新。访问页面`http://www.yourdomain.com/server-status?refresh=N`以每`N`秒刷新一次页面。

要简化状态显示，请在URL末尾添加`?auto`。此查询字符串告诉Apache显示简化的输出。

## 记录命中和错误

默认情况下，标准Apache发行版包含一个名为`mod_log_config`的模块，负责基本日志记录，并默认写入`Common Log Format`（`CLF`）日志文件。您可以使用`LogFormat`指令更改此行为。然而，`CLF`在大多数环境中涵盖了日志记录需求。

`CLF`文件包含每个请求的单独一行。一行由多个空格分隔的标记组成：

`host ident authuser date request status bytes`

如果标记没有值，则用连字符（`-`）表示。标记的含义如下：

- **Host.** 客户端的完全限定域名或其IP 地址。
- **Ident.** 如果`IdentityCheck`指令已启用并且客户端机器运行`identd`，则这是客户端报告的身份信息。
- **Authuser.** 如果请求的URL需要成功的`Basic HTTP`身份验证，则这是用户名。
- **Date.** 请求的日期和时间。
- **Request.** 来自客户端的请求行，用双引号括起来。
- **Status.** 返回给客户端的三位HTTP状态码。
- **Bytes.** 返回给客户端的对象中的字节数，不包括所有HTTP头。

日期字段可以具有以下格式：

```
date = [day/month:year:hour:minute:second zone]
```

例如，

```
[02/Jan/1998:00:22:01 -0800]
```

`mod_log_config`模块中有四个指令可用，其中第一个如下：

```
TransferLog filename | " | " /path/to/external/program
```

此指令设置日志信息将被发送到的日志文件或程序的名称。默认情况下，日志信息采用`CLF`格式，可使用`LogFormat`指令进行自定义。

当在虚拟主机容器内找到`TransferLog`指令时，日志信息会使用上下文中`found`的`LogFormat`指令进行格式化。但是，如果在同一上下文中找不到`LogFormat`指令，则使用服务器的日志格式。

`TransferLog`指令将日志文件路径或指向外部程序的管道作为参数。如果未找到前导`/`字符，则假定日志文件名相对于`ServerRoot`设置。例如，如果`ServerRoot`设置为`/etc/httpd`，则以下内容告诉Apache将日志信息发送到`/etc/httpd/logs/access.log`文件：

```
TransferLog logs/access.log
```
