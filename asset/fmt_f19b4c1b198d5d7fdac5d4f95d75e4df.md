
## 安装 MySQL

MySQL 数据库系统分为三个主要包：服务器、客户端和客户端库。服务器包含在 `mysql-server` 包中，需要另外两个才能工作。APT 感知这一点，这意味着当安装 `mysql-server` 时，这些包将自动安装：

> 确保在第 9 章中配置了主机名。

```
apt-get install mysql
```

## 编辑你的 Apache 配置

`ApacheD` 的配置文件极其灵活，这意味着你可以配置服务器以几乎任何方式运行。这种灵活性是以增加大量配置选项（*指令*）形式的复杂性为代价的，但在实践中，你只需要了解其中几个。

> 访问 `http://apache.org/docs/` 获取 Apache 支持的指令完整列表。

Apache 配置存储在文本文件中，由 Apache 服务器读取，从 `/apache/http.conf` 开始。配置从头到尾读取，大多数指令按照读取的顺序进行处理。

其他文件可能也基于 `AccessConfig`、`ResourceConfig` 和 `Include` 指令。在现代安装中，`AccessConfig` 和 `ResourceConfig` 选项指向空文件，其内容已移动到主 `httpd.conf` 文件。

`Include` 指令与 `AccessConfig` 和 `ResourceConfig` 的区别在于，它可以出现多次，并且一次可以包含多个文件。由 `Include` 指令引用的文件处理就像其内容出现在相关 `Include` 语句的位置一样。`Include` 可以指向单个文件、一个读取所有文件的目录，或者指向目录内特定文件集的通配符。

> 当 `Include` 指向目录时，子目录也会被处理。

## 运行你的服务器

当你的服务器组件已安装并运行后，你已经准备好使用名为虚拟主机的功能来配置你的域名了，之后你将看到如何

### 第 23 章 ◆ 运行 Linux、Apache、MySQL 和 PHP (LAMP) 服务器

存在不同类型的位置标签，并根据指定的资源位置类型进行选择。起始标签中包含的指定符将根据位置标签的类型进行处理。你通常会使用和遇到的标签有 `Directory`（目录）、`Files`（文件）和 `Location`（位置）。

> 注意：在本章中，`Location` 指的是第三种标签，而 `location` 通常指这三种标签中的任何一种。

- `Directory` 标签用于根据文件系统上的位置指定路径。例如，`<Directory />` 指向计算机的根目录。目录继承其上级目录的设置，最具体的 `Directory` 块将覆盖特定的块，而不论它们在配置文件中出现的顺序顺序如何。
- `Files` 标签用于通过名称指定文件。`Files` 标签可以包含在 `Directory` 块中，以将其限制在它们使用的文件中。`Files` 块中的设置将覆盖 `Directory` 块中的设置。
- `Location` 标签用于指定访问文件或目录的 URI。这与 `Directory` 的不同之处在于它与请求中包含的地址，而不是文件在驱动器上的实际位置。`Location` 标签最后被处理，并将覆盖 `Directory` 和 `Files` 块中的设置。

这些标签的匹配版本——`DirectoryMatch`、`FilesMatch` 和 `LocationMatch`——功能相同，但在指定符中可以包含正则表达式。`FilesMatch` 和 `Location` 块分别与 `Files` 和 `Location` 块同时处理。`Directory` 块在 `Directory` 块之后处理。

Apache 可以配置为处理位于 `AccessFileName` 指令中指定名称（通常设置为 `.htaccess`）的文件中的配置选项。访问配置文件中的指令将应用于其所包含的目录下的所有对象，包括子目录及其内容。访问配置文件与 `Directory` 块同时处理，并使用“最具体匹配”顺序。

> 注意：访问控制用于允许用户在没有服务器配置文件访问权限的情况下更改特定设置。在访问配置文件内允许的配置指令取决于它们所包含目录的 `AllowOverride` 设置。某些指令在那个层级上没有意义，在尝试访问 URI 时，通常会导致“服务器内部错误（server internal error）”消息。`AllowOverride` 选项在 `http://httpd.apache.org/docs/mod/core.html#allowoverride` 中有详细介绍。

### 第五部分 运行服务器

在 `location` 块和访问控制文件中常见的三个指令是 `DirectoryIndex`、`Options` 和 `ErrorDocument`：

- `DirectoryIndex` 告诉 Apache 当 URI 包含目录名但不包含文件时应加载哪个文件。此指令在 `Files` 块中不起作用。
- `Options` 用于调整 Apache 处理目录内文件的方式。`ExecCGI` 选项告诉 Apache 目录中的文件可以作为 CGI 脚本运行，`Includes` 选项告诉 Apache 允许服务器端包含 (SSI)。同样常用的是 `Indexes` 选项，它告诉 Apache 生成 `DirectoryIndex` 设置中找到的所有文件的列表。可以指定绝对选项列表，也可以通过在选项名称前加上 `+` 或 `-` 来修改选项列表。更多信息请参阅 `http://httpd.apache.org/docs/options/`。
- `ErrorDocument` 指令用于指定在错误结果中发送哪个文件。该指令必须指定错误代码。可能的错误代码包括 `403`（拒绝访问）、`404`（未找到文件）和 `500`（服务器内部错误）。关于 `ErrorDocument` 指令的更多信息可以在 `http://httpd.apache.org/docs/mod_core.html#errordocument` 处找到。

`location` 块和访问控制文件的另一个常见用途是限制对资源的访问。`Allow` 指令用于允许对匹配主机的访问，`Deny` 指令用于禁止访问。这两个选项都可以在块中出现多次，并根据 `Order` 设置进行排序。设置为 `Allow` 将允许任何未在 `Deny` 指令中列出的主机。设置为 `Deny.Allow` 将拒绝任何在 `Allow` 指令中未允许的主机的访问。与其他选项一样，将使用针对主机最具体的 `Allow` 或 `Deny` 选项，这意味着你可以访问一个范围并允许访问该范围。通过使用 `Satisfy` 选项和一些额外参数，你可以添加密码验证。关于访问控制的更多信息，请参阅 `http://httpd.apache.org/docs/mod_access.html`。

`Location` 块（广义上）可以包含在 `VirtualHost` 块中。虚拟主机将在下一节中详细描述，它们对于托管多个网站非常有用。

## 添加虚拟主机

你可能希望将各个虚拟主机放在单独的文件中以便于操作。然而，你应该小心将你的主虚拟主机保留在会在其他文件之前读取的文件中。在商业 Web 托管环境中，通常创建一个特殊的默认虚拟主机，其中包含指示未配置网站的错误消息。以下是一个模板：

创建一个名为 `/etc/apache/conf.d/vhosts.conf` 的文件：
