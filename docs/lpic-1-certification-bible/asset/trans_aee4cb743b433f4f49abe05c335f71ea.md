

## 默认页面

大多数用户不会输入完整的 URL，例如 `http://www.debian.org/index.html`，而是只输入 `http://www.debian.org`。那么，站点如何知道应该提供哪个页面？这是通过 `DirectoryIndex` 指令设置的。

```
DirectoryIndex index.html index.htm index.shtml index.cgi
```

默认情况下，服务器会按照列出的顺序查找页面，并显示找到的第一个页面。

## 用户 Web 目录

许多站点允许用户创建 Web 站点。这是通过 `UserDir` 指令配置的。

```
UserDir public_html
```

这告诉服务器在 `~/public_html` 目录中查找。如果有人尝试打开 `http://www.homepages.com/~jnash`，服务器实际上会访问 `http://www.homepages.com/~jnash/public_html`。这是一种让用户设置自己页面的好方法，无需担心存储这些页面的中心位置。

## MIME 类型

`TypesConfig` 指令告诉服务器 `mime.types` 配置文件存储在哪里。该文件告诉服务器哪些 MIME 类型对应哪些文件扩展名。

```
TypesConfig /etc/mime.types
```

`DefaultType` 指令告诉服务器如何处理未知 MIME 类型的文件。

```
DefaultType text/plain
```

## CGI 文件

CGI（通用网关接口）文件是用于提供站点动态内容的程序或脚本。`ScriptAlias` 指令定义了这些文件所在的目录。

```
ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
```

必须特别注意 CGI 文件，因为错误的权限或不良代码可能导致严重的安全漏洞。

```
IndexOptions FancyIndexing
```

还有其他一些有用的 `IndexOptions` 可用，例如 `ScanHTMLTitles`、`IconsAreLinks` 和 `FoldersFirst`。`ScanHTMLTitles` 读取 HTML 文件并使用标题而不是文件名。`IconsAreLinks` 允许用户点击图标，而不仅仅是点击文件名。`FoldersFirst` 将文件夹列在顶部，文件列在下方。

```
IndexOptions ScanHTMLTitles IconsAreLinks FoldersFirst
```

以下指令允许你微调用于列表的图标。

```
DefaultIcon /icons/unknown.gif
AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip
AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
```

`AddDescription` 指令允许你为匹配某个模式的文件或一组文件添加描述。

```
AddDescription "GZIP compressed tar archive" .tgz
```

`HeaderName` 和 `ReadmeName` 指令指定某些文本文件的显示方式。由 `HeaderName` 定义的文件附加在目录列表的顶部，而 `ReadmeName` 附加在底部。

```
ReadmeName README
HeaderName HEADER
```

## 认证

Apache 提供了认证机制，允许你保护目录或整个站点。最基本的形式使用包含用户账户和加密密码的文件。下面是一个示例块，显示了所需的指令。

```
<Directory /home/httpd/html/private>
AuthType Basic
AuthName Private
AuthUserFile /etc/web.users
AuthGroupFile /etc/web.groups
Require valid-user
</Directory>
```

这个块使 `/home/httpd/html/private` 受到保护，只有 `web.users` 文件中包含的有效用户才能访问。当用户尝试访问此目录时，系统会提示输入用户名和密码。`htpasswd` 命令用于创建此文件。其选项如表 16-14 所示。

**表 16-14**

**htpasswd 选项**

| 参数 | 功能 |
| :--- | :--- |
| -c | 创建一个新的密码文件。 |
| -n | 将结果显示到控制台，而不是密码文件。 |
| -m | 强制使用 MD5 加密。 |
| -d | 强制使用 Crypt 加密（默认）。 |
| -p | 不加密密码。 |
| -s | 强制使用 SHA 加密。 |
| -b | 将密码放在命令行中；不提示输入。 |

例如，要添加用户并创建一个新的密码文件，你会使用以下命令：

```
europa:~# htpasswd -c /etc/web.users jason
New password:
Re-type new password:
Adding password for user jason
```

要向现有文件添加新用户，你会使用以下命令：

```
europa:~# htpasswd /etc/web.users angie
New password:
Re-type new password:
Adding password for user angie
```

## 虚拟主机

Apache 支持从一台服务器上托管许多不同的 Web 站点。有两种不同的设置方法。第一种方法为每个虚拟主机使用单独的 IP 地址，而第二种方法只需要一个地址。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_665_0.png)

现在 IP 地址严重短缺，不再分配用于基于 IP 的虚拟主机。

### 基于 IP 的虚拟主机

基于 IP 的虚拟主机可以配置为所有主机使用一个守护进程，或使用单独的域名。要使用单独的域名，你需要为每个主机创建一个新的配置文件，并使用 `Bind` 和 `Listen` 指令。

```
BindAddress 192.168.10.10
Listen 192.168.10.10:80
```

这些指令指示服务器仅监听特定的 IP 地址和端口号。要为多个主机使用一个守护进程，你会使用 `VirtualHost` 指令。

```
<VirtualHost 192.168.10.10>
    ServerAdmin jason@the-nashes.net
    DocumentRoot /home/httpd/html/nash
    ServerName www.the-nashes.net
    ...
</VirtualHost>
```

你也可以在指令中使用域名。

```
<VirtualHost www.the-nashes.net>
```

除了配置 Apache 基本功能的指令外，大多数指令都可以在 `VirtualHost` 指令内部使用。

### 基于名称的虚拟主机

基于名称的虚拟主机不需要为每个主机使用单独的 IP 地址。客户端 Web 浏览器必须支持 HTTP v1.1 才能使其工作，因为它将请求的站点名称放在请求头中。如果客户端浏览器不支持此功能，用户将获得服务器上设置的默认站点，通常是第一个配置的站点。

基于名称的虚拟主机的指令与基于 IP 的类似，只是增加了 `NameVirtualHost` 指令。

```
NameVirtualHost 192.168.10.11
<VirtualHost 192.168.10.11>
    ServerName www.domain.com
    DocumentRoot /www/domain
</VirtualHost>

<VirtualHost 192.168.10.11>
    ServerName www.otherdomain.com
    DocumentRoot /www/otherdomain
    ServerAlias www.site.otherdomain.com
</VirtualHost>
```

`NameVirtualHost` 指令设置了应使用的 IP 地址，用于基于名称的虚拟主机。`ServerAlias` 指令为虚拟服务器提供其他别名。现在用户可以使用名称 `www` 或 `site.otherdomain.com` 访问该站点。

## 日志记录指令

Apache 提供了非常自定义的日志控制。默认情况下，Apache 使用通用日志格式（CLF）。CLF 格式由以下条目组成，每个请求占据一行：

```
host ident authuser date request status bytes
```

表 16-15 显示了每个条目的含义。日志示例如下：

```
24.163.40.182 - - [04/Jan/2001:11:11:19 -0500] "GET /angle/angle2.htm HTTP/1.1" 404 297
24.163.40.182 - - [04/Jan/2001:11:11:25 -0500] "GET /angle/angle2.htm HTTP/1.1" 200 4089
24.163.40.182 - - [04/Jan/2001:11:11:25 -0500] "GET /cgi-bin/img_counter.pl?test.txt HTTP/1.1" 200 171
24.163.40.182 - - [04/Jan/2001:11:12:14 -0500] "GET /angle/angle2.htm HTTP/1.1" 200 4090
24.163.40.182 - - [04/Jan/2001:11:12:14 -0500] "GET /angle/blue511.jpg HTTP/1.1" 304
```

**表 16-15 CLF 条目**

| 条目 | 含义 |
| :--- | :--- |
| `host` | 请求主机完全限定域名。如果无法解析，则显示 IP 地址。 |
| `ident` | 如果启用了 `IdentifyCheck` 指令且客户端机器运行 `identd`，则这是客户端报告的识别信息。 |
| `authuser` | 已认证用户的用户 ID，如果启用。 |
| `date` | 请求的日期。 |
| `request` | 客户端的请求行。 |
| `status` | 客户端返回的三位数字状态码。 |
| `bytes` | 传输的字节数，不包括头部。 |

默认日志可能无法捕获你需要的所有数据，或者可能过于冗长。此外，默认情况下所有信息都记录到一个文件中。以下示例显示了启用自定义日志的多个日志指令。

