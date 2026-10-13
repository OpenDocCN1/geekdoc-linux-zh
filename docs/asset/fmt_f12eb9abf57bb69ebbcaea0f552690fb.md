
要理解这些额外配置文件是如何组织的，你需要理解 Apache 是模块化的。安装额外的模块可以扩展 `httpd` 进程的功能。一个例子就是你将在在本章晚些时候使用的 `mod_ssl` 模块，用于通过 TLS 加密掌握 Apache 服务器。

有许多模块可以提供不同的功能。每个模块通常都有自己的配置文件，存储在 `/etc/httpd/conf.d` 目录。这些模块的名字以 `.conf` 结尾，以确保它们被你的 Web 服务器包含。

![](img/17f0db741e978e043c6f38c58e661452_416_0.png)

> 创建不以 `.conf` 结尾的配置文件是管理员常犯的错误。请确保文件名始终以 `.conf` 结尾。否则，它们不会被你的 Apache 服务器包含。

如前所述，主配置文件是 `/etc/httpd/conf/httpd.conf`。该文件包含了位于 `/etc/httpd/conf.d` 的各种配置文件。

# 第 16 章 • 在 Red Hat Enterprise Linux 上配置 Apache

```apache
<Directory>
Options Indexes MultiViewsFollowSymLinks
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

```
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"

<Directory "/var/www/cgi-bin">
AllowOverride None
Options None
Order allow,deny
Allow from all
</Directory>
```

## 通用参数

列表 16.1 中的示例配置文件从通用配置设置开始。一个重要的指令是 `ServerRoot`。它定义了配置目录的服务器根目录。在 Red Hat Enterprise 上，默认服务器根目录设置为 `/etc/httpd`。这一点这一点，因为配置文件的稍后部分引用了其他文件名。例如 `PidFile`（一个包含 `httpd` 进程 PID 的文件），被设置为 `/run/httpd.pid`。此文件名必须与服务器根目录相关；因此，完整名称为 `/etc/httpd/run/httpd.pid`。

配置文件开头的另一个重要参数是 `Listen` 参数。在本示例中，它引导 `httpd` 监听 80 端口。由于没有特定的 IP 地址可用，它将绑定到所有地址的 80 端口。如果你希望 `httpd` 绑定到特定的 IP 而不是其他 IP，可以包含一个特定的 IP 地址。

下一组通用参数位于 `httpd.conf` 文件的稍下位置。这些参数是 `user` 和 `Group`，它们指定了 Apache 服务器应该使用的用户和组。Apache 通常以 `root` 身份启动，一旦启动，将以该用户运行并具有较低的权限。默认情况下，两者都设置为 `apache`。最重要的是记住，Apache 绝不能以 `root` 身份提供服务；

另一个重要的指令是 `DocumentRoot`。它指定了 Apache 应该在何处查找内容。存储在 `DocumentRoot` 中的文档会被默认提供。Red Hat Enterprise Linux 的标准行为是显示 `DocumentRoot` 中创建的 `index.html` 文件的内容。然而，该背后还有一些参数，将在本章稍后部分解释。

## Apache 模式

Apache 可以两种不同的模式启动：`prefork` 模式（预叉模式）和 `worker` 模式（工作模式）。`prefork` 模式是默认模式。在这种模式下，会启动一个主 `httpd` 进程，主进程将启动不同的 `httpd` 服务器。作为替代，可以使用 `worker` 模式。在这种模式下，一个 `httpd` 进程处于激活状态，并使用线程来处理客户端请求。即使 `worker` 模式在资源利用方面效率更高，但某些模块无法处理，因此 `prefork` 模式被用默认。

然而，如果你需要 `httpd` 能提供的最佳性能，并且想使用与 `worker` 模式兼容的模块，那么使用 `worker` 模式是一个好主意。`worker` 模式可以配置为提供更多的并发进程。

要更改 Apache 的默认设置，你可以修改 `/etc/sysconfig/httpd` 中的 `HTTPD` 参数。要使用 `worker` 模式，你必须启动 `/usr/sbin/httpd.worker` 二进制文件在内部。要实现这一点，只需删除 `/etc/sysconfig/httpd` 中示例行中的井号，并使用 `service restart` 重启 `httpd` 进程。

对于两种模式，你都可以执行一些参数：

- `StartServers`：这是 `httpd` 应该始终保持的服务器进程数量。
- `MinSpareServers`：这是保留的空闲进程最小数量。保持某个最小数量是有好处的，因为它允许 `httpd` 极快地处理客户端请求。然而，最小值不应太高，因为每个服务器都会使用系统资源。
- `MinSpareThreads`：在 `worker` 模式下，这是 `httpd` 应该保持的空闲线程最小数量。你可以看到它比 `prefork` 模式下的 `MinSpareServers` 参数设置得多。
- `MaxSpareServers` and `MaxSpareThreads`：这是 `httpd` 应该保持的空闲服务器或线程的最大数量。
- `ServerLimit`：这是最多可以启动的服务器进程总数。注意，256 的值相当高，对于大多数服务器来说是足够的。
- `MaxClients`：这是可以连接的最大客户端数量。注意在 `worker` 模式下，一个客户端可以有多个同时打开的并发请求。
- `MaxRequestPerChild`：这是服务器进程可以打开的请求数。在 `prefork` 模式下，最大值限制为 4,000；在 `worker` 模式下，没有最大设置。

## 模块

让 Apache Web 服务器具有吸引力的特性之一是模块化的。通过包含模块，可以为 Apache 添加功能。要包含 Apache 模块，首先需要安装它们。默认情况下，一些常用的模块被安装在 `/etc/httpd/modules` 目录中。要告诉 Apache 应该加载特定模块，你需要使用 `LoadModule` 指令。默认情况下，此指令用于包含许多模块。

如果加载了模块，它也可以有特定的配置。有三种方法为模块加载额外的配置：

- 在 `httpd.conf` 中使用 `IfModule` 指令。
- 放入包含文件（`include file`）。
- 如果某个模块是通用的，其参数可以直接输入 `httpd.conf` 而无需进一步指明。

默认情况下，某些模块将其配置放在单独的配置文件中并存储在 `/etc/httpd/conf.d/` 中。`include` 指令确保 Apache 启动时，所有以 `.conf` 结尾的文件都被默认包含。在本章中，你将读到 `mod_ssl_module`，它在 `/etc/httpd/conf.d/` 中创建了自己的文件。

另一种引入特定模块相关参数的方法是在 `httpd.conf` 中使用 `IfModule` 指令。这种方法对于指令有限的模块实用。

如果某个模块非常常见且几乎总是使用，其参数可以直接输入 `httpd.conf`。接下来将讨论 `DirectoryIndex` 选项。

## 设置目录选项

管理员还可以在 Apache 上设置目录选项。这些选项用于定义如何向访问该目录的用户展示内容。默认行为是 `http` 请求在文档根目录中查找是否存在以 `index` 开头的文件。`DirectoryIndex` 指令可以指定考虑其他文件。如果是这样，它将显示此文件的内容，而不是目录列表。

要修改此行为，可以使用 `DirectoryIndex` 和 `Options` 指令。目录定义中的 `Options` 指令（如 `/var/www/icons` 目录所示）可以进一步微调显示目录内容的选项。你也可以使用 `Options` 来确定特定目录下可用的功能。

`Options` 指令的一个有用参数是 `Indexes`。如果你使用此选项，在没有 `index.html` 的情况下将看到目录列表。与此选项相关的是 `FollowSymLinks`。此选项将确保如果在目录中存在符号链接，则跟踪它们。不要使用这个，因为被认为是一个安全威胁。

## 处理基础目录限制

在 Apache 提供的目录中，可以使用一些基础限制。首先是 `AllowOverride` 指令。该指令与管理员可用于限制访问给定目录的 `.htaccess` 文件相关。如果 `AllowOverride` 设置为 `none`，则当前目录任何子文件夹中找到的 `.htaccess` 文件的内容将被

### 配置 Apache Web 服务器

忽略。如果你不知道子目录的所有者以限制对其目录的访问，则你应该将 `AllowOverride` 设置为 `none`。如果你想允许用户限制对子目录的访问，请将其设置为 `All`。在高性能环境中，请不要使用它，因为这将强制 Apache 在每次请求时都递归遍历整个目录树。
