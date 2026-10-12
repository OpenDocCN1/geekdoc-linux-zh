
# 配置常用指令

独立运行和基于 inetd 的服务器共享以下常用指令：

- `CustomLog _path_/_logfile`

此指令设置用于存储成功访问请求日志的日志文件路径。它还设置了记录访问请求时需要使用的日志格式。例如，默认设置使用通过 `LogFormat` 指令指定的通用日志格式。如果您选择使用不同的日志格式，例如 combined，请确保将默认值从 common 更改为 combined。

- `ErrorLog _path_/_to_/_logfile`

此指令指定用于记录错误消息的日志文件。如果将此指令设置为相对路径（即不以斜杠字符开头的路径），则假设该路径是相对于 `ServerRoot` 目录的。例如，如果您的 `ServerRoot` 目录设置为 /usr/local/apache，并且 `ErrorLog` 设置为 `var_/logs/error_log`，则等价于以下命令：

```
ErrorLog /usr/local/apache/logs/error_log
```

无论您将日志保存在哪个目录，请确保只有主服务器进程在该目录中拥有写入权限。这是一个重大的安全问题；允许其他用户或进程写入日志目录可能会使未经授权的人能够接管主要 Web 服务器进程的 UID，通常这是 root 账户。

- `HostnameLookups on | off`

当此指令设置为 _off_ 时，它会指示 Apache 不执行 DNS 查找来确定请求客户端的主机名。由于 DNS 查找耗时较长，因此使用默认值 _off_ 是一个非常好的主意。如果将其开启，如果 ISP 未正确设置客户端的反向 DNS 设置，可能会导致客户端超时。

- `LogFormat _format`

LogFormat 指定服务器日志文件的格式，并为该格式分配一个昵称。默认的 httpd.conf 文件包含多个 LogFormat 指令，但只使用其中一个与 CustomLog 指令配合使用。例如：

```
LogFormat "%h %l %u %t "%r" %>s %b" %"{Referer}i\"
%"{User-Agent}i\"" combined
```

这个昵称为 combined 的日志格式指定了所有通用日志格式 (CLF) 字段，并添加了 referrer 和 user-agent 字段。默认配置中的下一个格式如下：

```
LogFormat "%h %l %u %t "%r" %>s %b" common
```

此格式仅仅是 CLF，因此被昵称为 "common"。默认 httpd.conf 文件中的最后两个 LogFormat 指令如下：

```
LogFormat "%{Referer}i --> %U" referrer
LogFormat "%{User-agent}i" agent
```

这两个指令为仅存储 referrer 和 user-agent 信息的日志格式创建昵称。默认情况下，common 格式与 CustomLog 指令一起使用。但是，由于大多数日志分析程序都接受 combined 格式，您可能希望将其设置为默认值。毕竟，更多的日志信息对于确定谁正在访问您的站点以及访问方式总是有用的。

- `LogLevel [emerg | alert | crit | errors | warn | debug ]`

此指令指定 ApacheLog 指令的记录级别。默认值 warn 通常就足够了。它告诉 Apache 记录所有紧急 (emerg) 错误状况、告警 (alert) 状况、严重 (crit) 错误和警告 (warn)。如果您打算进行大量调试，请将其设置为 debug，这将捕获几乎所有类型的错误、警告和来自服务器的信息性消息。另外，请记住服务器执行的磁盘 I/O 越多，速度就越慢，因此将 LogLevel 保持在 debug 对于生产服务器来说并不是理想的选择。

- `ServerAdmin e-mail address`

此指令设置服务器管理员的电子邮件地址。当服务器生成错误消息页面时，会显示该电子邮件地址。通常设置如下：

```
ServerAdmin webmaster@domain.tld
```

- `ServerName hostname`

此指令设置服务器的 Internet 主机名。通常，您希望输入诸如 www.yourcompany.com 这样的主机名。但是，请务必确保您在此输入的主机名具有适当的 DNS 记录，并将其指向您的服务器机器。

- `ServerRoot path`

此指令指定服务器配置、错误和日志文件所在的顶层目录。这是所有服务器相关文件的父目录。如果您使用 APACI 接口编译和安装 Apache，则默认 ServerRoot 设置为您作为 configure 脚本参数提供的 PREFIX 的值。例如，如果您从 Apache 分发目录运行 configure 脚本如下：

```
./configure --PREFIX=/usr/local/apache
```

默认情况下，ServerRoot 将被设置为 /usr/local/apache。但是，如果您手动编译 Apache，可能需要更改默认值以指向适当的目录。

- `Timeout number`

使用此指令，您可以设置 Apache 等待客户端的秒数。默认值应该是合适的。

- `UseCanonicalName on | off`

当设置为 on 时，此指令告诉 Apache 在创建自引用 URL 时使用 ServerName- 和 Port- 指定的值。相反，当设置为 off 时，服务器使用客户端提供的服务器名称和端口信息构建自引用 URL。如果客户端未提供任何此类信息，服务器则使用 ServerName- 和 Port- 指定的值。大多数站点不使用自引用 URL 地址，因此对于大多数管理员来说，这不是一个重要的指令。

您需要配置的下一组指令用于告诉服务器您希望从 Web 站点提供哪些资源，以及在哪里和如何提供它们。

# AccessFileName filename filename filename . . .

此指令设置目录访问控制文件名。一些 Web 管理员更改默认名称（.htaccess）以增强安全性，因为 .htaccess 名称是广为人知的。如果您打算更改名称，请选择一个以句点开头的名称，这样它就不会出现在目录列表中。此外，请注意，默认 **access.conf** 文件禁止 Apache 查看任何目录级别访问控制文件。如果您打算使用此类访问控制文件，请确保相应地修改 **httpd.conf** 文件。例如，默认 **httpd.conf** 文件具有以下配置段：

```
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>
```

此配置使用 **AllowOverride** 指令禁止 Apache 查看 **AccessFileName**-指定的文件。如果您希望允许 Apache 在网站的某个子部分中查找访问控制文件，请使用以下配置：

```
<Directory "/path/to/your/dir">
    Options FollowSymLinks
    AllowOverride All
</Directory>
```

此配置允许您在 */path/to/your/dir* 目录或其下方的任何子目录中拥有诸如 **.htaccess** 这样的访问控制文件。它还允许您覆盖所有允许的指令。如果您希望获得更严格的设置，请将 **AllowOverride** 设置为以下设置之一：

- **AuthConfig**，允许授权指令，例如 **AuthDBMGroupFile**、**AuthDBMUserFile**、**AuthGroupFile**、**AuthName**、**AuthType**、**AuthUserFile** 和 **require**。
- **FileInfo**，允许文档类型指令，例如 AddEncoding、AddLanguage、AddType、DefaultType、ErrorDocument 和 LanguagePriority。
- **Indexes**，允许目录索引指令，例如 AddDescription、AddIcon、AddIconByEncoding、AddIconByType、DefaultIcon、DirectoryIndex、FancyIndexing、HeaderName、IndexIgnore、IndexOptions 和 ReadmeName。
- **Limit**，允许主机访问指令，例如 allow、deny 和 order。
- **Options**，允许目录选项指令，例如 Options 和 XbitHack。

- `AddEncoding MIME-encoding file-extension file-extension . . .`

此指令将 MIME 编码信息与文件扩展名关联。请保持默认值不变。

- `AddIcon icon name name . . .`

此指令为特定的文件扩展名设置图标文件名。当开启 FancyIndexing 时，Apache 会在每个匹配此指令中指定扩展名的文件旁边显示此图标。请保持默认值不变。

- `AddIconByEncoding icon MIME-encoding mime-encoding . . .`

此指令为带有 MIME-encoding 的文件设置用于 FancyIndexing 的显示图标。请保持默认值不变。

- `AddIconByType icon MIME-type MIME-type . . .`

此指令也为带有 MIME-encoding 的文件设置用于 FancyIndexing 的显示图标。请保持默认值不变。

- `AddLanguage MIME-language file-extension file-extension . . .`

此指令将语言特定的 MIME 编码信息与文件扩展名关联。请保持默认值不变。

- `Alias URL-path path`

您可以使用此指令为物理目录创建别名。默认别名 /icons/ 指向服务器图标图像所在的目录。

