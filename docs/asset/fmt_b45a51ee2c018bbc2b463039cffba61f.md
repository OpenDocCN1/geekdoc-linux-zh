
### 高级配置指令
Fedora/RHEL：disabled

### 子标题：DirectoryIndex

*指定用户请求目录时 Apache 提供的文件。*

```apache
DirectoryIndex filename [filename ...]
```

其中 `filename` 是 Apache 提供的文件的名称。

此指令指定了一个文件名列表。当客户端请求一个目录时，Apache 会尝试在指定目录中查找名称与列表中文件匹配的文件。当 Apache 找到匹配项时，它会返回该文件。当此指令缺失，或者此指令指定的文件中没有一个存在于指定目录中时，Apache 会显示由 `IndexOptions` 指令（第 954 页）指定的目录列表。

Fedora/RHEL 在 `httpd.conf` 文件中提供了以下 `DirectoryIndex` 指令：

```apache
DirectoryIndex index.html
```

此指令使 Apache 搜索指定目录并返回名为 `index.html` 的文件，这是标准默认 HTML 文档的名称。如果你提供 CGI 文档，可能希望在此指令中添加 `index.cgi` 值。`index` 这个名称是标准的，但也是任意的。

`.var` 文件扩展名表示内容协商文档，允许 Apache 根据客户端的指定提供多种语言之一的文档。如果你提供不同语言的内容，可以将此文件扩展名添加到 `DirectoryIndex` 指令中。有关更多信息，请参见第 963 页的“Type Maps”。

- 上下文：服务器配置、虚拟主机
- 默认值：`index.html`
- Fedora/RHEL：`index.html`

## 上下文与容器

为了提供灵活性和易于定制性，Apache 使用了配置指令、上下文和容器。上一节介绍了一些配置指令。本节讨论上下文和容器，它们在管理 Apache 服务器中至关重要。

### 上下文

有四个位置，称为 *上下文*，定义了配置指令可以出现的位置。本章对每个配置指令进行了标记，以指示它可以出现在哪个上下文中。表 26-1 描述了这些上下文中的每一个。

**表 26-1 上下文**

| 上下文 | 指令可出现的位置 |
| :--- | :--- |
| **server config** | 仅在 `httpd.conf` 文件或包含的文件中，但不包括在 `<VirtualHost>` 或 `<Directory>` 容器中（下一节），除非另有标记 |
| **virtual host** | 仅在 `httpd.conf` 文件或包含的文件中的 `<VirtualHost>` 容器内 |
| **directory** | 仅在 `httpd.conf` 文件或包含的文件中的 `<Directory>`、`<Location>` 和 `<Files>` 容器内 |
| **.htaccess** | 仅在 `.htaccess` 文件（第 939 页）中 |

通过 `Include` 指令（第 957 页）引入的文件中的指令是其所包含上下文的一部分，并且必须在该上下文中被允许。

将指令放置在错误的上下文中会导致配置错误，可能导致 Apache 无法正确提供内容或无法启动。

### 容器

*容器*，或称 *特殊指令*，是用于将其他指令分组的指令。容器由 XML 风格的标签界定。这里展示了三个示例：

```xml
<Directory> ... </Directory>
<Location> ... </Location>
<VirtualHost> ... </VirtualHost>
```

在 `httpd.conf` 中查找容器的示例。与其他指令一样，容器仅限于在指定的上下文中使用。本节描述了一些更常用的容器。

- **`<Directory>`**

  - **将指令应用于指定目录层次结构中的所有目录。**

  - 语法：`<Directory directory> ... </Directory>`

  - 其中 `directory` 是绝对路径名，指定容器内指令所应用的目录层次结构根目录所在的目录。`directory` 可以包含通配符；`*` 不匹配 `/`。

`<Directory>` 容器提供与 `.htaccess` 文件（第 939 页）相同的功能。虽然管理员可以在 Apache 配置文件中 `<Directory>` 容器，但普通用户不能使用。普通用户必须使用 `.htaccess` 文件来控制对其自身目录的访问。

以下示例中 `<Directory>` 容器内的指令适用于 `/var/www/html/corp` 目录层次结构。`Deny` 指令拒绝所有客户端的访问，`Allow` 指令授予 `192.168.10.` 子网中的客户端访问权限，而 `AllowOverride` 指令（第 960 页）使 Apache 能够处理层次结构内 `.htaccess` 文件中的指令：

```apache
<Directory /var/www/html/corp>
    Deny From all
    Allow from 192.168.10.
    AllowOverride All
</Directory>
```

以下 `<Directory>` 容器出现在 `httpd.conf` 文件中，并为整个服务器文件系统（由 `/` 指定）设置了一个限制性环境：

```apache
<Directory />
    AllowOverride None
    Require all denied
</Directory>
```

`AllowOverride` 指令导致 Apache 不处理 `.htaccess` 文件中的指令。`Require` 指令（第 961 页）拒绝所有用户访问整个服务器文件系统目录。如果你希望启用较少的限制选项，必须明确启用它们，但这可能会暴露服务器文件系统并危及系统安全。这个限制性 `<Directory>` 容器在 `httpd.conf` 中紧随其后的是一个为 `/var/www` 设置较少限制选项的容器。

```apache
<Directory "/var/www">
    AllowOverride None
    Require all granted
</Directory>
```

前一个 `<Directory>` 容器之后是一个为 `DocumentRoot`（`/var/www/html`）设置选项的容器；这个容器影响所有内容。`httpd.conf` 中的代码夹杂着许多注释。去掉注释后，它看起来像这样：

```apache
<Directory "/var/www/html">
    Options Indexes FollowSymlinks
    AllowOverride None
    Require all granted
</Directory>
```

`Options` 指令中的 `Indexes` 选项允许 Apache 显示目录列表，而 `FollowSymlinks` 选项使 Apache 跟随符号链接。这个容器比前一个限制性较小，尽管它仍然不允许 Apache 处理 `.htaccess` 文件中的指令。

上下文：`server config`, `virtual host`

- **`<Files>`**

  - **将指令应用于指定的普通文件。**

  - 语法：`<Files directory> ... </Files>`

  - 其中 `directory` 是绝对路径名，指定容器内指令所应用的普通文件所在的目录层次结构根目录。`directory` 可以包含通配符；`*` 不匹配 `/`。此容器类似于 `<Directory>`，但适用于普通文件而非目录。

以下指令来自 Fedora/RHEL `httpd.conf` 文件，拒绝访问所有文件名以 `.ht` 开头的文件，这意味着 Apache 将不提供 `.htaccess` 和 `.htpasswd` 文件。

```apache
<Files ".ht*">
    Require all denied
</Files>
```

上下文：`server config`, `virtual host`, `directory`, `.htaccess`

- **`<IfModule>`**

  - **如果加载了指定模块，则应用指令。**

  - 语法：`<IfModule [!module-name] ... </IfModule>`

  - 其中 `module-name` 是 Apache 测试的模块名称（第 968 页）。如果 `module-name` 已加载，或者如果 `module-name` 未加载且前面有 `!`，则 Apache 执行此容器中的指令。

如果你指定了一个属于未加载模块的配置指令，Apache 将无法启动。

以下 `<IfModule>` 容器位于 Fedora/RHEL `httpd.conf` 文件中，依赖于加载 `mime_magic_module` 模块。如果加载了此模块，Apache 将运行 `MIMEMagicFile` 指令，该指令告诉 `mime_magic_module` 其提示文件的位置。

```apache
<IfModule mime_magic_module>
    MIMEMagicFile conf/magic
</IfModule>
```

上下文：`server config`, `virtual host`, `directory`, `.htaccess`

- **`<Limit>`**

  - **将访问控制指令限制为指定的 HTTP 方法。**

  - 语法：`<Limit method [method] ... > ... </Limit>`

  - 其中 `method` 是 HTTP 方法。HTTP 方法指定要在 URL 上执行的操作。最常用的方法是 `GET`、`PUT`、`POST` 和 `OPTIONS`；方法名称区分大小写。`GET`（默认方法）发送 URL 指示的任何数据。`PUT` 将通信正文部分的数据存储在指定的 URL。`POST` 在指定的 URL 创建包含请求正文的新文档。`OPTIONS` 请求有关服务器功能的信息。

`<Limit>` 容器将一组访问控制指令绑定到指定的 HTTP 方法：只有此容器命名的方法才受这组指令的影响。

以下示例禁用了非 `example.com` 子域中系统的 HTTP 上传（`PUT`）：

```apache
<Limit PUT>
    Order deny,allow
    Deny from all
    Allow from .example.com
</Limit>
```

上下文：*server config, virtual host, directory, .htaccess*

> **注意：** 使用 `<LimitExcept>` 容器比使用 `<Limit>` 容器更安全，因为前者可以防止任意方法。当你使用 `<Limit>` 时，你必须小心地明确列出这组指令可能影响的所有可能方法。

- **`<LimitExcept>`**

  - **将访问控制指令限制为除指定 HTTP 方法以外的所有方法。**

  - 语法：`<LimitExcept method [method] ... ... </LimitExcept>`

  - 其中 `method` 是 HTTP 方法。有关方法的讨论请参见 `<Limit>`。

此容器导致一组访问控制指令*不*绑定到指定的 HTTP 方法。因此，*未*在 `<LimitExcept>` 中命名的方法会受到这组指令的影响。

以下 `<LimitExcept>` 容器内的访问控制指令除 `GET`、`POST` 和 `OPTIONS` 以外的 HTTP 方法。你可以将此容器放在 `<Directory>` 容器中，以限制其作用范围：

```apache
<LimitExcept GET POST OPTIONS>
    Order deny,allow
    Deny from all
</LimitExcept>
```

上下文：*server config, virtual host, directory, .htaccess*

- **`<Location>`**

  - **将指令应用于指定的 URI。**

  - 语法：`<Location URI> ... </Location>`

  - 其中 `URI` 指向内容；它指定了文件或容器内指令所应用的目录层次结构的根目录。虽然 `<Directory>` 容器指向本地文件系统内部，但 `<Location>` 指向本地文件系统外部。`URI` 可以包含通配符；`*` 不匹配 `/`。

以下 `<Location>` 容器限制来自 `example.net` 域的客户端访问 `http://server/pop`，其中 `server` 是服务器的 FQDN：

```apache
<Location /pop>
    Order deny,allow
    Deny from all
    Allow from .example.net
</Location>
```

上下文：*server config, virtual host*

## 谨慎使用 <Location>

谨慎使用这个功能强大的容器。不要用它来替代 `<Directory>` 容器：当多个 URL 指向文件系统中的同一位置时，客户端可能能够通过使用此容器未指定的 URL 来绕过预期的访问控制。

## `<LocationMatch>`

将指令应用于由正则表达式指定的 URL。

```apache
<LocationMatch regexp> ... </LocationMatch>
```

其中 `regexp` 是一个匹配一个或多个 URL 的正则表达式。此容器的作用方式与 `<Location>` 相同，但它适用于 `regexp` 匹配的任何 URL。

上下文：服务器配置，虚拟主机

## `<VirtualHost>`

将指令应用于指定的虚拟主机。

```apache
<VirtualHost addr[:port] | [addr:]port] ... > ... </VirtualHost>
```

其中 `addr` 是虚拟主机的 IP 地址（或 FQDN，尽管不推荐），或者使用 `*` 表示所有地址；`port` 是 Apache 监听该虚拟主机的端口。此指令不控制 Apache 监听的地址和端口；请使用 `Listen` 指令（第 940 页）来实现此功能。此容器包含 Apache 应用于虚拟主机的命令。更多信息请参见第 965 页的“虚拟主机”。

上下文：服务器配置

## 高级配置指令

本节讨论在熟悉 Apache 使用后可能会添加到 `httpd.conf` 中的配置指令。Fedora/RHEL 配置文件包含本节中指定的指令，并为这些指令指定了 Fedora/RHEL 的数值以及默认值。

## 控制进程的指令

### `MaxRequestWorkers`（原 `MaxClients`）

指定子进程的最大数量。

```apache
MaxRequestWorkers num
```

其中 `num` 是 Apache 同时运行的子进程（服务器）的最大数量，包括空闲进程和正在处理请求的进程。当 Apache 正在运行 `num` 个进程且没有空闲进程时，Apache 会向新连接发出 **Server too busy**（服务器太忙）错误；它不会启动新的子进程。

上下文：服务器配置

默认值：256

### `MaxConnectionsPerChild`（原 `MaxRequestsPerChild`）

指定子进程可以处理的最大请求数。

```apache
MaxConnectionsPerChild num
```

其中 `num` 是子进程（服务器）在其生命周期内可以处理的最大请求数。当子进程处理了 `num` 个请求后，它将不再处理更多请求，而是在完成当前请求的处理后终止。Apache 可以启动另一个子进程来替代终止的进程。额外的请求由服务器池中的其他进程处理。

将 `num` 设置为 0 表示不对子进程可以处理的请求数量设置限制，`MinSpareServers` 的影响除外。通过限制进程的寿命，此指令可以防止内存泄漏消耗过多的系统内存。然而，将 `MaxConnectionsPerChild` 设置为过小的值可能会因为导致 Apache 不断创建新的子服务器而损害性能。

上下文：服务器配置

默认值：0

### `MaxSpareServers`

指定空闲进程的最大数量。

```apache
MaxSpareServers num
```

其中 `num` 是 Apache 保持运行的空闲进程（服务器）的最大数量，以便随时响应传入的请求。不要将此数字设置得过高，因为每个进程都会消耗系统资源。

上下文：服务器配置

默认值：10

### `MinSpareServers`

指定空闲进程的最小数量。

```apache
MinSpareServers num
```

其中 `num` 是 Apache 保持运行的空闲进程（服务器）的最小数量，以便随时响应传入的请求。更多的空闲进程会占用更多的计算机资源；仅对繁忙站点增加此值。

上下文：服务器配置

默认值：5

### `StartServers`

指定 Apache 启动时启动的子进程数量。

```apache
StartServers num
```

其中 `num` 是 Apache 启动时启动的子进程（服务器）数量。此值仅在 Apache 启动时有效；一旦 Apache 启动并运行，空闲进程的数量由 `MinSpareServers` 和 `MaxSpareServers` 控制。使用多个服务器启动 Apache 可确保有一个服务器池随时准备立即处理请求。

上下文：服务器配置

默认值：根据负载动态控制

## 网络指令

### `HostnameLookups`

指定 Apache 在日志中记录客户端的主机名还是其 IP 地址。

```apache
HostnameLookups On | Off | Double
```

- `On`：执行 DNS 反向名称解析（第 862 页）以确定每个客户端的主机名，用于日志记录目的。
- `Off`：记录每个客户端的 IP 地址。
- `Double`：为了提供更强的安全性，执行 DNS 反向名称解析（第 862 页）以确定每个客户端的主机名，执行正向 DNS 查找以验证原始 IP 地址，并记录该主机名。如果无法验证原始 IP 地址，则拒绝访问。

上下文：服务器配置，虚拟主机，目录

默认值：Off
