
### TransferLog 配置

- `TransferLog filename`：设置 `httpd` 记录所有客户端访问（包括失败的访问）的文件。默认的 `TransferLog` 是 `/var/log/httpd/access_log`。以下示例展示了典型访问在此日志文件中如何记录：

```
192.168.0.3 - - [13/Mar/2004:18:10:23 -0500] "GET / HTTP/1.1" 200 3888 "-" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)"
192.168.0.3 - - [13/Mar/2004:18:10:23 -0500] "GET /icons/apache_pb2.gif HTTP/1.1" 200 244 "/192.168.0.6" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT5.1; (R1 1.3); .NET CLR 1.1.4322)"
192.168.0.3 - - [13/Mar/2004:18:10:23 -0500] "GET /icons/powered_by_fedora.png HTTP/1.1" 200 2243 "http://192.168.0.6/" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; (R1 1.3); .NET CLR 1.1.4322)"
```

- `LogFormat formatstring formatname`：指定 `TransferLog` 日志文件条目的格式。`CustomLog` 指令也使用此格式以特定格式生成日志。

- `CustomLog filename formatname`：设置自定义日志文件的名称，`httpd` 在该文件中记录所有客户端访问（包括失败的访问），格式由 `formatname` 指定（你使用 `LogFormat` 指令定义该名称）。

### 进程与连接配置

- `PidFile 文件名`：设置 HTTPD 存储其进程 ID 的文件。默认的 `PidFile` 是 `/var/run/httpd.pid`。你可以使用此信息来终止或重启 HTTP 守护进程。以下示例展示了如何重启 `httpd`：

  - `kill -HUP $(cat /var/run/httpd.pid)`

- `MaxClients num`：设置可以同时连接到服务器的客户端数量限制。默认值为 `150`。`MaxClients` 的值不能超过 `256`。

- `LoadModule module modules/modfile.so`：加载作为动态共享对象 `DSO` 构建的模块。必须指定模块名称和模块的对象文件。由于模块加载顺序很重要，请将这些指令保持为默认配置文件中的样子。注意：`mod_ssl` 模块提供对使用安全套接字层 `SSL` 协议进行加密的支持。

### 资源配置指令

资源配置指令指定了 Web 页面的位置，以及如何指定各种文件的数据类型。开始时，你可以保持这些指令的默认设置。以下是 Apache Web 服务器的一些资源配置指令：

- `DocumentRoot 路径名`：指定 HTTP 服务器查找 Web 页面的目录。在 Fedora Core 中，默认的 `DocumentRoot` 是 `/var/www/html`。如果你将 HTML 文档放在另一个目录中，请将 `DocumentRoot` 设置为该目录。

- `UserDir 目录名`：指定用户主目录下 HTTP 服务器查找 Web 页面的子目录，当 URL 中出现用户名时（例如，在包含带有波浪号前缀的用户名的 URL `http://www.psn.net/~naba` 中）。默认情况下，通过将 `dirname` 设置为 `disable` 来关闭 `UserDir` 功能。如果你想启用它，可以将其设置为 `public_html`，这意味着用户的 Web 页面位于该用户主目录的 `public_html` 子目录中。

- `DirectoryIndex 文件名 文件名2...`：指示当客户端未指定文档时，服务器返回的默认文件或文件。默认的 `DirectoryIndex` 是 `index.html`。如果 `HTTPD` 找不到此文件，且允许对该目录进行索引，它将返回该目录的索引（基本上是一个美观的文件列表）。

- `AccessFileName 文件名`：指定可能出现在包含文档的每个目录中、并指示谁有权访问该目录内容的文件的名称。默认的 `AccessFileName` 是 `.htaccess`。该文件的语法与 Apache 访问控制指令相同，我将在下一节中讨论。

![img](img/9f89727199836b0f871f1745838aa8b2_653_0.png)

- `AddType 类型/子类型 扩展名`：将文件扩展名与 MIME 数据类型（格式为 `类型/子类型`，如 `text/plain` 或 `image/gif`）关联。因此，要使服务器将具有 `.1st` 扩展名的文件视为纯文本文件，请指定以下内容：

```
AddType text/plain .1st
```

默认的 MIME 类型和扩展名列于 `/etc/mime.types` 文件中。

- `AddEncoding 类型 扩展名`：将编码类型与文件扩展名关联。要使服务器标记以 `.gz` 或 `.tgz` 结尾的文件为使用 `x-gzip` 编码方法（GZIP 编码的标准名称）编码，请指定以下内容：

```
AddEncoding x-gzip gz tgz
```

- `DefaultType 类型/子类型`：指定服务器在无法从文件扩展名确定类型时使用的 MIME 类型。如果你不指定 `DefaultType`，`HTTPD` 假定 MIME 类型为 `text/html`。在默认的 `httpd.conf` 文件中，`DefaultType` 指定为 `text/plain`。

- `Redirect requested-file actual-URL`：指定将对 `requested-file` 的任何请求重定向到 `actual-URL`。

- `Alias requested-dir actual-dir`：指定服务器使用 `actual-dir` 来定位 `requested-dir` 目录中的文件（换句话说，`requested-dir` 是 `actual-dir` 的别名）。要使对 `/icons` 目录的请求转向 `/var/www/icons`，请指定以下内容：

```
Alias /icons/ /var/www/icons/
```

- `ScriptAlias requested-dir actual-dir`：指定包含通用网关接口 `CGI` 脚本的目录的实际名称。默认配置文件包含此指令：

```
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
```

此指令意味着当 Web 浏览器请求脚本（例如 `/cgi-bin/test-cgi`）时，HTTP 服务器运行 `/var/www/cgi-bin/test-cgi` 脚本。

- `DefaultIcon iconfile`：指定服务器用于没有图标信息的文件的默认图标的位置。默认情况下，`DefaultIcon` 是 `/icons/unknown.gif`。

- `ReadmeName filename`：指定 README 文件的名称，其内容将附加到自动生成的目录列表末尾。默认的 `ReadmeName` 是 `README`。

- `HeaderName filename`：指定头部文件的名称，其内容将前置到自动生成的目录列表之前。默认的 `HeaderName` 是 `HEADER`。

- `AddDescription "文件描述" 文件名`：指定在目录列表中显示在指定文件名旁边的文件描述字符串。你可以使用通配符（如 `*.html`）作为文件名。例如，以下指令描述以 `.tgz` 结尾的文件为 GZIP 压缩的 tar 存档：

`AddDescription "GZIP compressed tar archive" .tgz`

- `AddIcon iconfile extension1 extension2 …`：将一个图标与一个或多个文件扩展名关联。以下指令将图标文件 `/icons/text.gif` 与文件扩展名 `.txt` 关联：

`AddIcon /icons/text.gif .txt`

- `AddIconByType iconfile MIME-types`：将一个图标与一组以 MIME 类型的通配符形式指定的文件类型（如 `text/*` 或 `image/*`）关联。要将 `/icons/text.gif` 的图标文件与所有文本类型关联，请指定以下内容：

`AddIconByType (TXT.,/icons/text.gif) text/*`

此指令还告诉服务器使用 `TXT` 代替图标，针对那些不能接受图像的客户端。（浏览器告诉服务器它们可以接受的数据类型。）

- `AddIconByEncoding iconfile encoding1 encoding2 …`：指定用于显示一个或多个编码类型（如 `x-compress` 或 `x-gzip`）的图标。
