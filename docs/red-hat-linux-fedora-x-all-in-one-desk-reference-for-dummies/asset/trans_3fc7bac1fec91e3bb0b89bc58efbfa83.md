

# 配置 Apache Web 服务器 623

- 性能调整：在此选项卡上，你可以设置某些参数来控制整体性能。你可以设置最大连接数、连接超时时间以及每个连接的最大请求数。

![](img/d9230b719dc0efd80851f363d8c6f571_649_0.png)

| 虚拟主机属性 | 目录页面搜索列表 | | |
|---|---|---|---|
| 站点配置 | index.html | 添加... | |
| 环境变量 | index.shtml | 编辑... | |
| 目录 | | 删除 |
| | 请求目录时搜索的文件列表。例如：index.html, index.shtml 等。 | | |
| 错误页面 | 行为位置 | 编辑... |
| 错误代码 | default | | |
| 需要授权 | default | | |
| 禁止访问 | default | | |
| 未找到 | default | | |
| 方法不允许 | | | |
| 错误代码 400 - Bad Request | | | |
| 默认错误页页脚 | 显示带有电子邮件地址的页脚： | | |

配置窗口最初显示来自配置文件 `/etc/http/httpd.conf` 的默认值。在进行任何更改后，点击 OK 按钮。配置工具会提示你是否想要保存更改并退出。如果是，点击 Yes 即可完成。

![](img/d9230b719dc0efd80851f363d8c6f571_649_1.png)

当此通过此配置工具配置 Apache HTTP 服务器时，你正在更改存储在 `/etc/httpd/httpd.conf` 文件中的选项和属性。你可以通过编辑该配置文件（这是一个纯文本文件）来轻松地进行更改。在接下来的章节中，我将向你介绍 Apache 配置文件中的一些配置指令。

# Apache 配置文件

Apache 服务器的运行由位于 `/etc/httpd/conf` 目录下的 `httpd.conf` 配置文件控制。该文件控制服务器如何运行、提供哪些文档，以及谁可以访问这些文档。

在接下来的几部分中，我将总结了关于 `httpd.conf` 配置文件的关键信息。通常情况下，你不需要更改配置文件中的任何内容即可运行 Apache Web 服务器。然而，了解配置文件的格式以及其中使用的各种关键词的含义是非常有用的。

第八卷
第 2 章

运行 Apache 服务器

# 624 配置 Apache Web 服务器

当你在学习 `/etc/httpd/conf` 目录下的配置文件时，请记住这些语法规则：

- 每个配置文件都是一个文本文件，你可以使用喜爱的文本编辑器进行编辑，并使用 `more` 命令进行查看。
- 所有注释行都以 `#` 开头。
- 每行只能有一个指令。
- 多余的空格和空行会被忽略。
- 除了路径名和 URL 外，所有条目均不区分大小写。

# httpd.conf 配置文件

`/etc/httpd/conf/httpd.conf` 文件是主 HTTP 配置文件——它包含了控制 Apache Web 服务器运行方式的指令。例如，`httpd.conf` 文件指定了服务器使用的端口号、网站名称，以及当服务器出现任何问题时发送邮件的电子邮件地址。此外，`httpd.conf` 还包含了关于 Web 页面所在位置以及谁可以访问哪些目录的信息。

在接后的章节中，我将 Apache 指令分为三个独立的类别：通用 HTTP 指令、资源配置指令和访问控制指令。最后，我将解释如何在 Apache Web 服务器中设置虚拟主机，以便单台 Web 服务器可以处理发送到多个 IP 地址或主机名的 Web 请求。

![](img/d9230b719dc0efd80851f363d8c6f571_650_0.png)

如需在线查阅 Apache HTTP 文档，请访问 http.apache.org/docs-2.0/。具体来说，你可以在 http.apache.org/docs-2.0/mod/directives.html 查找有关配置指令的信息。

# 通用 HTTP 指令

`httpd.conf` 文件中的一些有趣项目

- ServerName 指定了你的网站的名称（格式为 `your.domain`）以及 Web 接受连接的端口号。`ServerName` 仅在将网页重定向到另一个网页时使用。该名称是其他用户可以通过名称服务器定位的注册域名。这里是一个示例：

```
ServerName www.myhost.com:80
```

如果你没有注册域名，请使用 Fedora Core 系统的 IP 地址。

# 625 配置 Apache Web 服务器

- ServerAdmin 是 Web 服务器在发生任何错误时提供给客户端的电子邮件地址。`ServerAdmin` 的默认值为 `@localhost`。将此地址设置为有效的电子邮件地址，互联网上的任何人都可以使用它来报告你的网站包含的错误。
- Include 从指定文件加载报告指令。例如，默认的 `/etc/httpd/conf/httpd.conf` 使用以下 `Include` 指令加载 `/etc/httpd/conf.d` 目录下的所有配置文件：

Include conf/*.conf

此命令意味着你可以仅通过向 `/etc/httpd/conf.d` 目录中添加文件来加载另一组配置。事实上，你发现各种 Apache HTTPD 模块（如 Perl、PHP 和 SSL）的配置文件的目录就在那里。研究 `/etc/httpd/conf.d` 目录下的配置文件，以了解影响 Apache 服务器的所有指令集。

许多指令控制 Apache 服务器的运行。在接下来的部分中，我总结了这些 `httpd.conf`。了解这些指令的工作方式是重要的。

- Listen 地址：强制 Web 服务器监听特定的 IP 地址。
- ServerName：指定了你的网站的名称（格式为 `your.domain`）以及 Web 接受连接的端口号。`ServerName` 仅在将网页重定向到另一个网页时使用。该名称是其他用户可以通过名称服务器定位的注册域名。
- ServerAdmin：是 Web 服务器在发生任何错误时提供给客户端的电子邮件地址。`ServerAdmin` 的默认值为 `@localhost`。将此地址设置为有效的电子邮件地址，互联网上的任何人都可以使用它来报告你的网站包含的错误。
- Include：从指定文件加载报告指令。例如，默认的 `/etc/httpd/conf/httpd.conf` 使用以下 `Include` 指令加载 `/etc/httpd/conf.d` 目录下的所有配置文件：

Include conf/*.conf

此命令意味着你可以仅通过向 `/etc/httpd/conf.d` 目录中添加文件来加载另一组配置。事实上，你发现各种 Apache HTTPD 模块（如 Perl、PHP 和 SSL）的配置文件的目录就在那里。研究 `/etc/httpd/conf.d` 目录下的配置文件，以了解影响 Apache 服务器的所有指令集。
- Error Code 400 - Bad Request：
- Default Error Page Poster：显示带有电子邮件地址的页脚：
- Error Pages：行为位置：
- Error Code：错误代码
- Authorization Required：需要授权
- Forbidden：禁止访问
- Not Found：未找到
- Method Not Allowed：方法不允许
- Virtual Host Properties：

如果你没有注册域名，请使用 Fedora Core 系统的 IP 地址。

# 626 配置 Apache Web 服务器

- StartServers：设置启动 Apache 服务器的进程数。
- MaxSpareClients：设置允许的最大空闲客户端数。
- MinSpareProcesses：设置允许的最小空闲进程数。
- Timeout：设置服务器等待客户端响应的秒数。
- ErrorLog：设置记录错误的文件路径。如果不以斜杠 `/` 开头，则相对于 `ServerRoot`。
- TransferLog：设置记录所有客户端访问（包括失败访问）的日志文件。在下面的部分中，我总结了这些指令。

- LogFormat formatname：指定 `TransferLog` 日志文件条目的格式。`CustomLog` 指令也使用此格式产生特定格式的日志。
- CustomLog filename：设置自定义日志文件的名称，其中 httpd 记录所有客户端访问（包括失败访问），格式由 `formatname` 指定（你通过 `LogFormat` 定义）。

