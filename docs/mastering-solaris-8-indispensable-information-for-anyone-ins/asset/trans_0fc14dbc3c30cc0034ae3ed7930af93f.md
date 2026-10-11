

### 目录指令

目录指令用于控制对存储 HTML 文件的各个目录的访问。Web 服务器的文档根目录（Document Root）是主目录。所有的 HTML 文档都存储在 DocumentRoot 中。在收到文档请求后，Apache 会相对于此目录搜索该文件。文档根目录通过以下指令定义：

```apache
DocumentRoot '/home/httpd/htdocs'
```

一旦定义了 Web 服务器的根目录，你应该使用 `Directory` 指令来定义该目录的访问权限：

```apache
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>

<Directory "/home/httpd/htdocs">
    Options Indexes FollowSymLinks MultiViews
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
```

第一个针对根目录 / 的 `Directory` 设置是让 Apache 知道整个系统仅允许 `FollowSymLinks`，但不允许索引或其他信息。第二个针对 "/home/httpd/htdocs" 的 `Directory` 设置更改了这些权限，允许客户端查看信息。`Options` 指令控制当 Apache 处于 `DocumentRoot` 目录时采取何种类型的操作。可用的选项包括 `Indexes`、`Includes`、`FollowSymLinks`、`ExecCGI` 和 `MultiViews`。当使用 `Indexes` 选项时，如果客户端请求的是目录而不是文档，且该目录没有默认 HTML 文件，Apache 将生成目录列表。`Includes` 选项在将文档内容发送给客户端之前对其进行过滤。`FollowSymLinks` 选项将符号链接解析为文件和目录，但必须谨慎使用，因为它可能会允许用户链接到你不希望被显示的系统其他部分。`ExecCGI` 选项告知 Apache，某个目录中的文档应被视为程序并执行。

`AllowOverride` 指令控制特殊的 .htaccess 文件是否可以覆盖 Options 设置。由于可以从该文件中启用额外的选项，你可能希望阻止在你的 HTML 文档根目录中启用它们。你还可以使用 `Order` 指令来控制对 Web 服务器的访问，该指令允许你定义希望允许访问的主机以及希望拒绝访问的主机。

一旦定义了根目录，你可以定义 Apache 使用的特殊文件的名称：目录索引文件、访问控制文件和 MIME 类型文件。Apache 使用目录索引文件来处理客户端对目录的请求。当客户端请求一个目录时，Apache 将列出其内容。如果这不是客户端想要的，你可以使用 DirectoryIndex 指令来指定要使用的 HTML 文件的名称。使用以下语法，如果文件存在，它将被返回给客户端：

```apache
DirectoryIndex index.html
```

访问控制文件用于允许访问使用 AccessFileName 指令定义名称的特定目录。

```apache
AccessFileName .htaccess
<Files .htaccess>
    Order allow, deny
    Deny from all
</Files>
```

> **提示：** 访问文件可能包含特权或敏感信息。出于安全考虑，你可能希望定义一个 Files 指令来防止客户端访问这些文件。默认情况下，Apache 包含保护这些文件不被 Web 客户端查看或下载的代码。

MIME 类型文件用于确定特定文件的正确 MIME 类型。你可以使用 TypesConfig 指令来控制此文件的位置，如下例所示：

```apache
TypesConfig /home/httpd/conf/mime.types
```

无需更改此位置，因为它是标准配置文件的一部分，并随 httpd.conf 文件一起安装。

DefaultType 指令定义了 Web 服务器上文档的默认 MIME 类型。它与 MIME 类型文件相关：

```apache
DefaultType text/plain
```

如果你的服务器主要包含文本或 HTML 文档，那么 text/plain 是最佳值。然而，如果大部分内容是二进制文件，你可以使用值 application/octet-stream。这样浏览器将不会尝试将二进制文件作为文本显示。

### CGI 脚本

CGI 脚本使您能够在服务器上执行命令并将输出返回给客户端。由于 CGI 脚本包含关于您服务器的信息，因此对它们的访问权限应比根目录更严格。

如果你希望使用安全的 CGI 脚本，应将 `ScriptAlias` 指令与 `Directory` 指令结合使用。`ScriptAlias` 指令让 Apache 知道存储在目录中的文件是脚本并且应该执行。该指令作为 `ExecCGI` 的替代方案，允许你将一个目录及其所有子目录标记为仅包含 CGI 程序。要启用 CGI 程序，请使用以下代码：

```apache
ScriptAlias /cgi-bin/ '/home/httpd/cgi-bin'
<Directory "/home/httpd/cgi-bin">
    AllowOverride None
    Options None
    Order allow, deny
    Allow from all
</Directory>
```

> **提示：** 定义 `ScriptAlias` 后，为 CGI 目录定义一个 `Directory` 指令，禁止所有选项并防止覆盖。这可以防止带有恶意意图的网站访客发现你拥有哪些 CGI 程序。

### 目录列表

如果 Apache 收到对目录而不是文件的请求，它会尝试查找该目录的索引文件。如果文件不存在，Apache 将响应该目录内容的列表。`IndexOptions` 指令控制列表的样式。如果你想要一个简单的目录列表，只需将此选项设置为 `Standard`：

```apache
IndexOptions Standard
```

如果你更喜欢返回目录中每个文件的描述，请使用：

```apache
IndexOptions FancyIndexing
```

使用 `FancyIndexing` 时，你还可以为文件添加描述。该指令的语法如下：

```apache
AddDescription 'description' .file-extension
```

### 日志记录指令

Apache 使用日志记录指令来控制关于请求的日志信息：

```apache
HostnameLookups Off
ErrorLog /var/log/httpd/error-log
LogLevel warn
LogFormat '%h %l %u %t "%r" %>s %b "%{Referer}i"\n"%{User-Agent}i"\n' 
LogFormat '%h %l %u %t "%r" %>s %b' common
LogFormat '%{Referer}i -> %>s' referer
LogFormat '%{User-agent}i' agent
#CustomLog /var/log/httpd/access-log common
#CustomLog /var/log/httpd/referer-log referer
#CustomLog /var/log/httpd/agent-log agent
#CustomLog /var/log/httpd/access-log combined
```

HostnameLookups 指令控制是否记录主机名而不是客户端的 IP 地址。由于解析客户端的主机名至少需要一次 DNS 查询，你应该关闭此选项以减少每个请求产生的网络流量。Apache 附带一个脚本，用于在以后查找主机名。

*ErrorLog* 指令定义了错误日志的位置，该日志存储有关请求错误和响应错误的信息。它在调试 CGI 程序时很有用。虽然你可以将其存储在任何位置，但大多数站点最常使用默认值。

*LogLevel* 和 *LogFormat* 指令定义了用于记录信息的 Syslog 级别和格式。如果默认格式提供的信息不足以满足你的需求，你可以定义自己的格式。*CustomLog* 指令使用请求、客户端类型和来源页面。

### BrowserMatch 指令

*BrowserMatch* 指令用于修改正常的 HTTP 响应行为。以下是标准设置：

```apache
BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "RealPlayer 4\.0" force-response=1.0
BrowserMatch "Java/1\.0" force-response=1.0
BrowserMatch "JDL/1\.0:" force-response=1.0
```

第一个指令禁用了 I2.x 的 keepalive。该版本在处理持久连接时存在问题。其余指令强制 RealPlayer 和 Java 使用 HTTP 版本 1，因为它们不支持 HTTP 版本 1.1。

### 虚拟主机配置

有时你可能需要托管不同组织的 Web 网站，特别是如果你拥有包含不同[内容截断]

