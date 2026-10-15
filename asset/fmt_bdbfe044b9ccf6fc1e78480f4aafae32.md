
这两个指令为仅存储 referrer 和 user-agent 信息的日志格式创建了昵称。默认情况下，`common`格式与`CustomLog`指令一起使用。然而，由于大多数日志分析程序接受`combined`格式，你可能希望将其设为默认值。毕竟，更多的日志信息总是有助于确定谁在访问你的网站以及如何访问。

## LogLevel [emerg | alert | crit | errors | warn | debug ]

此指令指定`ErrorLog`指令的日志级别。默认值`warn`通常足够。它告诉 Apache 记录所有紧急（`emerg`）错误条件、警报（`alert`）条件、严重（`crit`）错误以及所有警告（`warn`）。如果你计划进行大量调试，请将其设置为`debug`，这将捕获几乎所有类型的错误、警告和服务器信息消息。还请记住，服务器执行的磁盘 I/O 越多，速度越慢，因此将`LogLevel`保持在`debug`对于生产服务器来说并不理想。

## ServerAdmin 电子邮件地址

此指令设置服务器管理员的电子邮件地址。当服务器生成错误消息页面时，电子邮件地址会显示。通常设置为如下：

```
ServerAdmin webmaster@domain.tld
```

## ServerName hostname

此指令设置服务器的 Internet 主机名。通常，您希望输入类似`www.yourcompany.com`的主机名。然而，请务必确保您在此处输入的主机名具有指向服务器机器的正确 DNS 记录。

## ServerRoot 路径

此指令指定服务器的配置文件、错误文件和日志文件所存放的顶级目录。这是所有服务器相关文件的父目录。如果您使用 APACI 接口编译并安装了 Apache，则默认的`ServerRoot`设置为作为`configure`脚本参数提供的`PREFIX`值。例如，如果您从 Apache 分发目录按如下方式运行`configure`脚本：

```
./configure --PREFIX=/usr/local/apache
```

默认情况下，`ServerRoot`将被设置为`/usr/local/apache`。然而，如果您手动编译了 Apache，您可能需要更改默认值以指向适当的目录。

## Timeout 数字

使用此指令，您可以设置 Apache 等待客户端的秒数。默认值应该就足够了。

## UseCanonicalName 开 | 关

设置为`on`时，此指令告诉 Apache 在创建自引用 URL 时使用`ServerName`和`Port`指定的值。相反，当设置为`off`时，服务器使用客户端提供的主机名和端口信息构建自引用 URL。如果客户端未提供此类信息，服务器随后使用`ServerName`和`Port`指定的值。大多数站点不使用自引用 URL 地址，因此这对大多数管理员来说不是一个重要的指令。

您需要配置的下一组指令用于告诉服务器您希望从网站提供哪些资源，以及如何提供它们。

## AccessFileName 文件名 文件名 文件名 . . .

此指令设置目录访问控制文件名。一些 Web 管理员会更改默认的`(.htaccess)`以增强安全性，因为`.htaccess`名称广为人知。如果您计划更改名称，请选择以句点开头的名字，这样它就不会出现在目录列表中。另请注意，默认的`access.conf`文件禁止 Apache 查看任何目录级别的访问控制文件。如果您计划使用此类访问控制文件，请确保相应地修改`httpd.conf`文件。例如，默认的`httpd.conf`文件具有以下配置段：

```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

此配置使用`AllowOverride`指令禁止 Apache 查看`AccessFileName`指定的文件。如果您有兴趣允许 Apache 在网站的某个子部分中查找访问控制文件，请使用以下配置：

```
<Directory "/path/to/your/dir">
Options FollowSymLinks
AllowOverride All
</Directory>
```

此配置允许您在`/path/to/your/dir`目录或其下的任何子目录中拥有`.htaccess`等访问控制文件。它还允许您覆盖所有允许的指令。如果您有兴趣采用更受限制的设置，请将`AllowOverride`设置为以下设置之一：

- `AuthConfig:` 允许授权指令，例如`AuthDBMGroupFile`、`AuthDBMUserFile`、`AuthGroupFile`、`AuthName`、`AuthType`、`AuthUserFile`和`require`。
- `FileInfo:` 允许文档类型指令，例如`AddEncoding`、`AddLanguage`、`AddType`、`DefaultType`、`ErrorDocument`和`LanguagePriority`。
- `Indexes:` 允许目录索引指令，例如`AddDescription`、`AddIcon`、`AddIconByEncoding`、`AddIconByType`、`DefaultIcon`、`DirectoryIndex`、`FancyIndexing`、`HeaderName`、`IndexIgnore`、`IndexOptions`和`ReadmeName`。
- `Limit:` 允许主机访问指令，例如`allow`、`deny`和`order`。
- `Options:` 允许目录选项指令，例如`Options`和`XbitHack`。

```
AddEncoding MIME-encoding file-extension file-extension . . .
```

此指令为文件名扩展名分配 MIME 编码信息。保持默认值不变。

```
AddIcon icon name name . . .
```

此指令为特定文件扩展名设置图标文件名。当`FancyIndexing`打开时，Apache 会在此指令指定的扩展名匹配的每个文件旁边显示此图标。保持默认值不变。

```
AddIconByEncoding icon MIME-encoding mime-encoding . . .
```

此指令为`FancyIndexing`设置要在具有 MIME 编码的文件旁边显示的图标。保持默认值不变。

```
AddIconByType icon MIME-type MIME-type . . .
```

此指令还为`FancyIndexing`设置要在具有 MIME 编码的文件旁边显示的图标。保持默认值不变。

```
AddLanguage MIME-language file-extension file-extension . . .
```

此指令为文件名扩展名分配特定语言的 MIME 编码信息。保持默认值不变。

```
Alias URL-path path
```

您可以使用此指令为物理目录创建别名。默认别名`/icons/`指向存储服务器图标图像的目录。如果路径不正确，请相应地修改它。图标图像用于创建花哨的目录列表。

```
BrowserMatch variable[=value] [ . . ]
```

此指令基于`User-Agent`HTTP 请求头字段定义环境变量。保持默认值不变。

```
DefaultIcon url
```

此指令设置在没有特定图标已知时为文件显示的图标。保持默认值不变。

```
DefaultType MIME-type
```

使用此指令设置默认内容类型。当服务器无法使用存储在`mime.types`中的映射信息或其他方式（例如`AddType`指令）确定文档的 MIME 类型时，它使用此指令设置的值。保持默认值不变。

```
DirectoryIndex filename filename filename . . .
```

此指令指定 Apache 服务器应将哪个文件视为所请求目录的索引。例如，当请求类似`www.yourcompany.com`的 URL 时，Apache 服务器确定这是访问网站`/`（文档根）目录的请求。如果`DocumentRoot`指令设置如下：

```
DocumentRoot "/www/www.yourcompany.com/public/htdocs"
```

Apache 服务器会查找名为`/www/www.yourcompany.com/public/htdocs/index.html`的文件；如果服务器找到该文件，Apache 通过将文件内容返回给请求的 Web 浏览器来提供服务。然而，如果`DirectoryIndex`被分配为`welcome.html`而不是默认的`index.html`，Web 服务器则会查找`/www/www.yourcompany.com/public/htdocs/welcome.html`。如果文件不存在，Apache 通过创建 DHTML 页面返回目录列表。您还可以在`DirectoryIndex`指令中指定多个索引文件名。例如，
