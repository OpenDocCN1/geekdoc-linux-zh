
当 Nessus 运行脚本以提取插件摘要信息时，`description` 变量的值设置为 1。因此，当 `description` 的值为真且非零时，我们定义了各种插件描述变量值。
`script_id` 函数为插件设置一个唯一 ID。每个插件的值必须是唯一的。在我们的情况下，可以将其设置为 9999 等高数字以确保值的独立性。`script_version` 函数显示插件的版本信息。更新此内容以反映插件的最新版本是一个好主意。`script_description` 函数设置插件描述，当用户查询插件时 Nessus 客户端会显示。同样，`script_summary` 函数用于设置插件的摘要。
`script_category` 函数根据 Nessus 的要求设置插件的类别。在我们的情况下，我们设置为 `ACT_GATHER_INFO`，因为该插件收集远程服务的信息；它检查 Web 服务器上是否存在 `/src/passwd.inc` 文件。`script_copyright` 函数用于设置作者版权信息。
Nessus 将插件分为不同的“家族”（families），以帮助对执行的漏洞进行分类。我们将其设置为“CGI abuses”，以表示对基于 CGI 的 Web 应用程序的利用。访问 http://cgi.nessus.org/plugins/dump.php?viewby=family 查看按家族分类的可用插件列表。
可以通过在 GUI 客户端的“扫描选项（Scan Option）”中选择适当的私有检查（private check）来优化测试。当启用此选项时，Nessus 会扫描与目标机器开放端口上运行的应用程序相关的漏洞。`script_require_ports` 函数可用于设置与远程机器漏洞相关的端口，在我们的案例中它被设置为 www (HTTP)。

上述函数为插件设置了各种值。可以在 Nessus GUI 客户端“插件（Plugins）”选项卡中双击相应的插件来查看插件描述。此截图如图 10-1 所示。
`http_func.inc` 文件包含了方便我们使用的有用 HTTP 函数列表。我们使用 `include` 函数在文件中引入了这些函数。
`get_port_state` 函数用于检查目标主机上特定端口的状态。在我们的情况下，我们检查 80 端口。如果该端口关闭，则没有必要继续，因此我们调用 `exit(0)`。
为了检查 Web 服务器上是否存在 `/src/passwd.inc` 文件，连接 Web 服务器的 HTTP 请求格式必须如下：

```
GET /src/passwd.inc HTTP/1.0
```

![](img/17cb132e6294dc7f5eeadf90c7f51219_0.png)

图 10-1. Nessus GUI 显示的插件描述

可以使用 `http_get` 函数创建上述 GET 请求。该请求可以作为参数传递给 `send` 函数，将请求发送到由 `http_open_socket` 打开的目标主机套接字。使用 `http_recv` 函数读取 Web 服务器的数据并将其存储在 `myrec` 变量中。完成后，使用 `http_close_socket` 关闭套接字。然后检查 `myrec` 的内容是否包含子字符串 404，如果在从 Web 服务器返回的数据未找到 404，则该文件存在，通过调用 `security_hole` 函数向 Nessus 指明这一事实。
请参阅 http://www.nessus.org/doc/nasl_reference.pdf 获取 NASL 参考。

### 运行插件

确保上述脚本放在 Nessus 的 plugins 目录中。文件名必须以 `.nasl` 结尾。运行 Nessus GUI 并选择“插件（Plugins）”选项卡。确保勾选了 CGI abuses。高亮 CGI abuses 并启用名为“Checks for /src/password.inc”的插件。如果你在查找插件时遇到困难，点击 Filter（过滤器）按钮搜索 ID 为 9999 的插件。
为了从我们的插件获得正面结果，你必须配置本地 Web 服务器提供 `/src/passwd.inc` 文件。如果你运行着 Apache Web 服务器，只需执行：

```
mkdir /www/html
touch /src/passwd
```
