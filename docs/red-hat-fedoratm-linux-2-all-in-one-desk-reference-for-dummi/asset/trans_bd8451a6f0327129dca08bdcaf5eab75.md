

- PidFile 文件名：设置 HTTPD 存储其进程 ID 的文件。默认的 PidFile 是 /var/run/httpd.pid。你可以使用此信息来终止或重启 HTTP 守护进程。以下示例展示了如何重启 httpd：
  - `kill -HUP $(cat /var/run/httpd.pid)`

- MaxClients num：设置可以同时连接到服务器的客户端数量限制。默认值为 150。MaxClients 的值不能超过 256。

- LoadModule module modules/modfile.so：加载作为动态共享对象 (DSO) 构建的模块。必须指定模块名称和模块的对象文件。由于模块加载顺序很重要，请将这些指令保持为默认配置文件中的样子。**注意：** mod_ssl 模块提供对使用安全套接字层 (SSL) 协议进行加密的支持。

## 资源配置指令

资源配置指令指定了 Web 页面的位置，以及如何指定各种文件的数据类型。开始时，你可以保持这些指令的默认设置。以下是 Apache Web 服务器的一些资源配置指令：

- DocumentRoot 路径名：指定 HTTP 服务器查找 Web 页面的目录。在 Fedora Core 中，默认的 DocumentRoot 是 /var/www/html。如果你将 HTML 文档放在另一个目录中，请将 DocumentRoot 设置为该目录。

- UserDir 目录名：指定用户主目录下 HTTP 服务器查找 Web 页面的子目录，当 URL 中出现用户名时（例如，在包含带有波浪号前缀的用户名的 URL http://www.psn.net/~naba 中）。默认情况下，通过将 dirname 设置为 disable 来关闭 UserDir 功能。如果你想启用它，可以将其设置为 public_html，这意味着用户的 Web 页面位于该用户主目录的 public_html 子目录中。

- DirectoryIndex 文件名 文件名2...：指示当客户端未指定文档时，服务器返回的默认文件或文件。默认的 DirectoryIndex 是 index.html。如果 HTTPD 找不到此文件，且允许对该目录进行索引，它将返回该目录的索引（基本上是一个美观的文件列表）。

- AccessFileName 文件名：指定可能出现在包含文档的每个目录中、并指示谁有权访问该目录内容的文件的名称。默认的 AccessFileName 是 .htaccess。该文件的语法与 Apache 访问控制指令相同，我将在下一节中讨论。

![img](img/9f89727199836b0f871f1745838aa8b2_653_0.png)

- AddType 类型/子类型 扩展名：将文件扩展名与 MIME 数据类型（格式为 类型/子类型，如 text/plain 或 image/gif）关联。因此，要使服务器将具有 .1st 扩展名的文件视为纯文本文件，请指定以下内容：

  ```
  AddType text/plain .1st
  ```

  默认的 MIME 类型和扩展名列于 /etc/mime.types 文件中。

- AddEncoding 类型 扩展名：将编码类型与文件扩展名关联。要使服务器标记以 .gz 或 .tgz 结尾的文件为使用 x-gzip 编码方法（GZIP 编码的标准名称）编码，请指定以下内容：

  ```
  AddEncoding x-gzip gz tgz
  ```

- DefaultType 类型/子类型：指定服务器在无法从文件扩展名确定类型时使用的 MIME 类型。如果你不指定 DefaultType，HTTPD 假定 MIME 类型为 text/html。在默认的 httpd.conf 文件中，DefaultType 指定为 text/plain。

- Redirect requested-file actual-URL：指定将对 requested-file 的任何请求重定向到 actual-URL。

- Alias requested-dir actual-dir：指定服务器使用 actual-dir 来定位 requested-dir 目录中的文件（换句话说，requested-dir 是 actual-dir 的别名）。要使对 /icons 目录的请求转向 /var/www/icons，请指定以下内容：

  ```
  Alias /icons/ /var/www/icons/
  ```

- ScriptAlias requested-dir actual-dir：指定包含通用网关接口 (CGI) 脚本的目录的实际名称。默认配置文件包含此指令：

  ```
  ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
  ```

  此指令意味着当 Web 浏览器请求脚本（例如 /cgi-bin/test-cgi）时，HTTP 服务器运行 /var/www/cgi-bin/test-cgi 脚本。

- DefaultIcon iconfile：指定服务器用于没有图标信息的文件的默认图标的位置。默认情况下，DefaultIcon 是 /icons/unknown.gif。

- ReadmeName filename：指定 README 文件的名称，其内容将附加到自动生成的目录列表末尾。默认的 ReadmeName 是 README。

- HeaderName filename：指定头部文件的名称，其内容将前置到自动生成的目录列表之前。默认的 HeaderName 是 HEADER。

- AddDescription "文件描述" 文件名：指定在目录列表中显示在指定文件名旁边的文件描述字符串。你可以使用通配符（如 *.html）作为文件名。例如，以下指令描述以 .tgz 结尾的文件为 GZIP 压缩的 tar 存档：

  `AddDescription "GZIP compressed tar archive" .tgz`

- AddIcon iconfile extension1 extension2 …：将一个图标与一个或多个文件扩展名关联。以下指令将图标文件 /icons/text.gif 与文件扩展名 .txt 关联：

  `AddIcon /icons/text.gif .txt`

- AddIconByType iconfile MIME-types：将一个图标与一组以 MIME 类型的通配符形式指定的文件类型（如 text/* 或 image/*）关联。要将 /icons/text.gif 的图标文件与所有文本类型关联，请指定以下内容：

  `AddIconByType (TXT.,/icons/text.gif) text/*`

  此指令还告诉服务器使用 TXT 代替图标，针对那些不能接受图像的客户端。（浏览器告诉服务器它们可以接受的数据类型。）

- AddIconByEncoding iconfile encoding1 encoding2 …：指定用于显示一个或多个编码类型（如 x-compress 或 x-gzip）的图标。

- IndexIgnore filename1 filename2 …：指示服务器在准备目录列表时忽略指定的文件名（它们通常包含通配符）。要排除 README、HEADER 以及所有文件名以点 (.)、尾随波浪号 (~) 或尾随井号 (#) 开头的文件，请指定以下内容：

  `IndexIgnore .?..* - #\ HEADER* README* RCS CVS *.v *.t`

- IndexOptions option1 option2 …：指示你希望服务器准备的目录列表中的选项。选项可以包括以下一个或多个：
  - FancyIndexing 开启包含文件名和代表文件类型、大小和最后修改日期的图标的精美目录列表。
  - IconHeight=N 指定图标高度为 N 像素。
  - IconWidth=N 指定图标宽度为 N 像素。
  - NameWidth=N 使文件名列宽度为 N 个字符。
  - IconsAreLinks 使图标表现得像链接一样。
  - ScanHTMLTitles 显示 HTML 文件的描述。
  - `SuppressHTMLEPreamble` 不向头部文件（由 `HeaderName` 指令指定）添加标准 HTML 前言。
  - `SuppressLastModified` 停止显示最后修改日期。
  - `SuppressSize` 停止显示文件大小。
  - `SuppressDescription` 停止显示任何文件描述。
  - `SuppressColumnSorting` 阻止列标题成为允许对列进行排序的链接。

- `ErrorDocument` *errortype filename*：指定当发生特定类型的错误时服务器发送的文件。你也可以为错误提供文本消息。以下是一些示例：

  ```
  ErrorDocument 403 "Sorry, no access to this directory"
  ErrorDocument 403 /error/noindex.html
  ErrorDocument 404 /cgi-bin/bad_link.pl
  ErrorDocument 401 /new_subscriber.html
  ```

  如果你没有 `ErrorDocument` 指令，服务器将发送内置的错误消息。*errortype* 可以是以下 `HTTP/1.1` 错误条件之一（更多详情请参见 `www.ietf.org/rfc/rfc2616.txt` 或 `www.faqs.org/rfcs/rfc2616.html` 中的 `RFC 2616`）：
  - 400: Bad Request
  - 401: Unauthorized
  - 402: Payment Required
  - 403: Forbidden
  - 404: Not Found
  - 405: Method Not Allowed
  - 406: Not Acceptable
  - 407: Proxy Authentication Required
  - 408: Request Timeout
  - 409: Conflict
  - 410: Gone
  - 411: Length Required
  - 412: Precondition Failed
  - 413: Request Entity Too Large
  - 414: Request-URI Too Long

