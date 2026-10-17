
## 每目录上下文

指令存储在目录内的文件（通常是 `.htaccess`）中。

## 服务器配置上下文

指令可以出现在主服务器配置文件中的任何位置，且不在任何容器内部。您可以将此上下文视为全局上下文或范围；也就是说，将未包含在容器中的指令视为*全局指令*。在此上下文中适用的指令默认会影响所有其他上下文。这些指令可用于服务器配置文件中的任何位置（例如 `httpd.conf`、`srm.conf` 和 `access.conf`），但不能用于任何容器或每目录配置文件（`.htaccess`）中。

## 容器上下文

要限制指令的范围，您可以使用容器，其外观类似于 HTML 标签对。容器标签对包围一组指令，限制容器内部指令的范围。Apache 提供这些标准容器：

- `\<VirtualHost ...> ... </VirtualHost>` 用于将一个或多个指令应用于容器开始标签中指定的虚拟主机。
- `\<Directory ...> ... </Directory>` 用于将一个或多个指令应用于特定目录。请注意，如果您使用此容器标签为目录指定一个或多个指令，这些指令将自动应用于所有子目录。然而，如果这不是您想要的副作用，您可以为每个子目录创建单独的目录容器，并不同地控制服务器在目录每个子级别上的行为。
- `\<DirectoryMatch regex> ... </DirectoryMatch>` 与 `\<Directory>` 容器完全相同；然而，它接受正则表达式（*regex*）作为参数，而不是普通目录名称。例如，`<DirectoryMatch "/^\www/mydir[1-3]/"> ... </DirectoryMatch>` 匹配所有命名为 `/www/mydir1`、`/www/mydir2` 和 `/www/mydir3` 的目录。

> **交叉引用**
>
> 正则表达式（*regex*）通常由普通字符和特殊字符组成，以创建模式。该模式用于匹配一个或多个子字符串或整个字符串。有关正则表达式的更多信息，请参阅附录 B。

- `\<Files ...> ... </Files>` 用于将一个或多个指令应用于特定文件或文件组。
- `\<FilesMatch regex> ... </FilesMatch>` 与 `<Files>` 容器完全相同；然而它接受正则表达式（*regex*）作为参数，而不是一个或多个文件名。例如，`<FilesMatch "\.(doc|txt)$"> ... </FilesMatch>` 将把一个或多个指令应用于所有以 `.doc` 或 `.txt` 扩展名结尾的文件。
- `\<Location ...> ... </Location>` 用于将一个或多个指令应用于特定 URL。

> **注意**
>
> *URI*（*统一资源标识符*）是统一资源标识符家族的通用术语，其中 URL 只是其中一员。其他成员包括统一资源名称（URN）、统一资源特征（URC）和位置无关文件名（LIFN）。然而，只有 URL 被广泛使用。

- `\<LocationMatch regex> ... </LocationMatch>` 与 `\<Location>` 容器完全相同；然而，它接受正则表达式（*regex*）作为参数，而不是 URL。
- `\<Limit ...> ... </Limit>` 用于将一个或多个指令应用于控制对 Web 站点特定区域或特定 HTTP 请求方法的访问。此容器拥有所有容器中最窄的范围。以下是容器范围的一个示例：`httpd.conf` 文件的一个片段：

```html
<VirtualHost 206.171.50.50>

    ServerName www.nitec.com

    DocumentRoot "/www/nitec/public/htdocs"

    DirectoryIndex welcome.html

    <Location /secured/>

       DirectoryIndex login.html

    </Location>

</VirtualHost>
```

在这个例子中，使用 `<VirtualHost>` 容器定义了一个名为 `www.nitec.com` 的虚拟主机。三个指令——`ServerName`、`DocumentRoot` 和 `DirectoryIndex`——位于虚拟主机上下文中，因此适用于整个虚拟主机。`DirectoryIndex` 指令指定，如果发出请求以访问此虚拟服务器中的目录，如果可用，应返回名为 `welcome.html` 的文件。然而，`<Location>` 容器指定，当有人尝试访问 `www.nitec.com/secured/` URL 时，应返回另一个文件 `login.html`。因为 `<Location>` 容器定义了更窄的范围（在 `/secured` 子目录中），它覆盖了 `<VirtualHost>` 容器中 `DirectoryIndex` 指令的更高范围。

> **注意** 定义更窄范围的容器总是覆盖具有更高范围的容器。

在使用任何容器定义 Web 空间部分的行为时，您应该牢记一些规则：

- `<VirtualHost>` 容器不能嵌套在任何类型的其他容器内。
- 最窄上下文容器 `<Limit>` 内部不能包含任何容器。
- `<Files>` 容器内部只能包含最窄的容器 `<Limit>`。
- `<Location>` 和 `<Directory>` 容器不混合使用，因此不要在一个内部使用另一个。

## 每目录上下文

您还可以在每目录配置文件中包含指令。每目录配置文件（每目录配置的默认文件名为 `.htaccess`）是一个文本文件，包含一个或多个仅适用于当前的目录。这些指令也可以封装在诸如 `<Files ...>` 或 `<Limit ...>` 等容器中。通过使用每目录配置文件，你可以控制当客户端对目录中的文件发起请求时 Apache 的行为。

**注意** `AllowOverride` 指令允许你禁用每目录配置文件中在服务器配置或虚拟主机上下文中可被覆盖的所有或部分设置。因此，根据当前生效的覆盖设置，此上下文中的所有指令可能不会被处理。

## 通用配置指令

本节讨论的指令属于基础性质，通常同时适用于主服务器（*服务器配置上下文*）和虚拟服务器（*虚拟主机上下文*）。

### AccessFileName

`AccessFileName` 指令指定每目录访问控制文件的名称。默认设置（*.htaccess*）使 Apache 在每次客户端系统发起访问请求时都会查找 `.htaccess` 文件。

**语法：** `AccessFileName filename [filename ...]`

**默认设置：** `AccessFileName .htaccess`

**上下文：** 服务器配置，虚拟主机

例如，假设名为 `www.mycompany.com` 的 Apache 网站其 `DocumentRoot` 指令设置为 `DocumentRoot "/www/mycompany/public/htdocs"`，而 Web 浏览器请求了 `http://www.mycompany.com/feedback.html`。这将导致 Apache 搜索以下访问控制文件：

- `/.htaccess`
- `/www/.htaccess`
- `/www/mycompany/.htaccess`
- `/www/mycompany/public/.htaccess`
- `/www/mycompany/public/htdocs/.htaccess`

只有在检查完所有这些文件后，Apache 才会查找 *feedback.html* 文件。如果你觉得这涉及大量的磁盘 I/O，那确实如此。你可以通过使用此指令指定访问文件名来避免所有这些不必要的操作。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_90_0.png)

如果你不使用*每目录访问控制*文件，并希望 Apache 停止检查它，只需使用 `<Directory>` 指令禁用覆盖权限如下所示：

```
<Directory />

    AllowOverride None

</Directory>
```

有关更多详细信息，请参阅本章中关于 `<Directory>` 容器和 `AllowOverride` 指令的章节。

### AddDefaultCharset

`AddDefaultCharset` 指令设置 Apache 发送给浏览器的 `Content-Type` 头中的默认字符集。

**语法：** `AddDefaultCharset On | Off | charset`

**默认设置：** `AddDefaultCharset Off`

**上下文：** 全部

当启用此指令（使用 `On` 选项）时，除非你指定字符集作为该指令的第二个参数，否则 Apache 会发送 `iso-8859-1`（西欧）作为默认字符集。例如，`AddDefaultCharset On utf-8` 将发送 UTF-8 作为默认字符集。常用的字符集包括：

- `ISO-8859-1`—西欧
- `ISO-8859-15`—支持欧元货币符号的西欧
- `Windows-1252`—西欧
- `CP850`—西欧
- `UTF-8`—8 位 Unicode
- `UTF-7`—7 位 Unicode

![](img/e11fcbd2818a3495ac70085e5d8d1c26_90_1.png)

如果你的 HTML 文档通过使用 `<META http-equiv="Content-Type" content="content_type; charset=character_set_name">` 标签设置了字符集，`AddDefaultCharset` 指令允许你覆盖它。

### ContentDigest

当设置了 `ContentDigest` 指令时，它会为整个正文内容生成一个消息摘要（MD5）头，这使得 Web 客户端能够验证页面的完整性。对于 Web 服务器来说，这是一个主要的性能负担，因为 MD5 摘要需要在 Web 服务器提供的每个静态页面上进行计算。

请注意，此摘要不为除核心模块以外的任何模块生成的任何输出生成。这意味着通用网关接口（CGI）输出无法使用此功能。由于对服务器性能的影响，除非你知道服务器有足够的余力，否则不建议使用此功能。

**语法：** `ContentDigest On | Off`

**默认设置：** `ContentDigest Off`

**上下文：** 全部

### DefaultType

`DefaultType` 指令用于建立默认的 MIME 类型，这样当 Apache 收到请求一个文件类型未知的文档（换句话说，无法从服务器可用的 MIME 类型映射中确定）时，它将使用预定的默认类型。

**语法：** `DefaultType mime-type`

**默认设置：** `DefaultType text/html`

**上下文：** 全部

**覆盖：** `FileInfo`

例如，如果你有一个目录用于存储大量没有扩展名的文本文件，你可以在指向该目录的 `<Directory>` 容器内使用 `DefaultType` 指令。在这种情况下，将 `DefaultType` 设置为 `text/plain` 可以告知对端（Web 浏览器）这些是纯文本文件。以下是一个示例：

```
<Directory /www/mycompany/public/htdocs/plaindata>

    DefaultType text/plain

</Directory>
```

这里，`/www/mycompany/public/htdocs/plaindata/` 目录中的所有文件都被视为纯文本文件。

### DocumentRoot

此指令指定的 `DocumentRoot` 目录将成为 Apache 服务的所有文档的顶层目录。

**语法：** `DocumentRoot directory_path`

**默认设置：** `DocumentRoot /usr/local/apache/htdocs`

**上下文：** `服务器配置，虚拟主机`

例如，如果为服务器 `www.mycompany.com` 设置了 `DocumentRoot "/www/mycompany/public/htdocs"`，那么对 `www.mycompany.com/corporate.html` 的访问请求将促使服务器查找以下文件：
`/www/mycompany/public/htdocs/corporate.html`

如果找到该文件，它将返回给客户端（即 Web 浏览器）。

> 注意：`mod_dir` 模块中的一个 bug 导致当 `DocumentRoot` 末尾带有斜杠时出现问题（例如，`DocumentRoot /usr/web/`），因此你应该避免在任何指令的路径末尾输入 `/` 字符。

> 提示：服务器可以查找 `DocumentRoot` 目录之外的目录中的文件。如果你想访问 `DocumentRoot` 树之外的某些文件，可以使用 `Alias` 指令创建一个虚拟目录名称，它可以指向服务器文件系统任何位置的实际目录。

### ErrorDocument

当服务器遇到问题时，它会生成一条包含错误代码的标准错误消息。然而，这对大多数人来说并不友好，因此更希望使用定制版本的错误消息，或者可能的恢复措施。如果你需要这种定制，请使用 `ErrorDocument` 指令覆盖标准错误消息。

- **语法：** `ErrorDocument error_code [filename | error_message | URL]`
- **默认设置：** 无
- **上下文：** 全部
- **覆盖：** `FileInfo`

该指令需要两个参数。第一个参数是标准 HTTP 错误代码，你可以在附录 A 中找到；第二个参数是错误对应的操作项。根据需求，你可以定义希望服务器针对特定错误状态采取的操作。

例如，如果你希望为所有导致标准“文件未找到”消息的请求提供自定义消息，你只需找到该错误状态的服务器状态代码并使用 `ErrorDocument` 指令即可。由于缺少文件的服务器状态代码为 404，以下指令设置可让 Apache 显示自定义消息：

```
ErrorDocument 404 "Sorry, this is an invalid request because %s "
```

请注意，整个消息被引号包围，服务器会用有关错误的可用信息替换 `%s`。然而，如果你觉得这有点限制，可以使用文件作为错误消息响应。例如：

```
ErrorDocument 404 /errors/404.html
```

每当发生文件缺失错误时，位于 `DocumentRoot` 目录下 `errors` 目录中的 `404.html` 文件将返回给客户端（Web 浏览器）。

如果你希望做的不仅仅是返回一个静态页面，你可以使用 CGI 脚本来执行某些特定操作。在这种情况下，你用调用 CGI 脚本替换文件名：

```
ErrorDocument 404 /cgi-bin/missingurl.cgi
```

每当发生 404 错误时，这会调用名为 `missingurl.cgi` 的 CGI 脚本。你也可以使用 URL 而不是文件名将客户端重定向到另一个网站：

```
ErrorDocument 404 http://www.newsite.com/we.moved.html
```

这可以用于页面或整个网站已迁移到另一位置的情况。

如果发生错误 401（未授权），你不能将客户端指向远程服务器。此指令的值必须是本地文件或消息。

### \<IfDefine>

`IfDefine` 容器指令允许你创建条件配置。特殊命令行参数选项通过在与 `httpd` 程序一起使用 `-D` 选项来指定。

**语法：** `<IfDefine [!]special_command_line_param> ... </IfDefine>`

**默认设置：** 无

**上下文：** 全部

例如，如果你从 `bin` 目录运行 Apache 服务器，命令为 `./httpd -D something`，则可以使用：

```
<IfDefine something>

# #directives that should be executed only when

# -D something is specified

</IfDefine>
```

在特殊命令行参数前放置 `!` 字符告诉 Apache 仅在命令行中未找到 `-D something` 时处理 `IfDefine` 容器内的指令。例如：

```
<IfDefine !something>

# directives that should be executed only when

# -D something is NOT specified

</IfDefine>
```

## \<IfModule>

如果某些指令来自可能并不存在于你的 Apache 安装环境中的自定义模块，请使用 `IfModule` 容器指令。

- **语法：** `<IfModule [!]module_name> ... </IfModule>`
- **默认设置：** 无
- **上下文：** 全部

例如，如果你只想在某个模块可用时才使用某些指令，可以使用以下条件结构：

```
<IfModule module_name>

   # 如果该模块是 Apache 的一部分，则为以下指令分配相应的值

   # 在此处放置你的指令。

</IfModule>
```

其中，`module_name` 参数是该模块在编译时的文件名（例如，`mod_rewrite.c`）。

如果你需要一个与上述逻辑完全相反的条件语句，只需在模块名前插入一个 `!`（感叹号或 bang）即可。`<IfModule>` 区域可以嵌套；这是一种可用于实现简单多模块条件测试的方法。例如：

```
<IfModule module_A>

   # 如果模块 A 是

   # Apache 的一部分，则在此处理指令

   <IfModule module_B>

      # 仅当模块 A 和 B 都是

      # Apache 的一部分时才进入此处

      <IfModule ! module_C>
```
