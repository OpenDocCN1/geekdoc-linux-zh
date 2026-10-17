
通常，当你配置 Apache 时，你不会修改 `apache2.conf`；相反，修改 `Include` 指令指定的文件。这种设置允许更新 Apache 而不影响服务器。当 Apache 读取其配置文件时，如果发现同一个指令的多次出现（即使在包含文件中），它将使用最后一次遇到的该指令所赋值的值。

在 `apache2.conf` 文件中，`httpd.conf` 文件的 `Include` 指令位于设置全局环境的指令之后，这些表 26-1 所示的各种超时和限制。要更改其中任何内容，请将其复制到 `httpd.conf` 并进行更改。你必须修改在其他包含文件中 `Include` 指令之后的指令，如本节所述。

### 表 26-1 可以在 httpd.conf 中覆盖的指令

| AccessFileName | MaxRequestsPerChild |
| :--- | :--- |
| DefaultType | MaxSpareThreads |
| ErrorLog | MinSpareThreads |
| Group | PidFile |
| HostNameLookups | ServerRoot |
| KeepAlive | StartServers |
| KeepAliveTimeout | ThreadsPerChild |
| LockFile | Timeout |
| LogLevel | TypesConfig |
| MaxClients | User |
| MaxKeepAliveRequests | |

控制日志格式、索引选项、MIME 处理和浏览器处理的指令出现在 `httpd.conf` 的 `Include` 指令之后，但在 `/etc/apache2/sites-enabled` 的 `Include` 指令之前（后者是 `apache2.conf` 的最后一行）。你可以通过将这些指令复制到 `sites-enabled` 目录下的文件中并进行修改，从而按站点单独覆盖这些指令。

如果你管理多个多个 Ubuntu Web 服务器，将所有自定义配置代码与主配置分开是很有的。这样你就可以使用 `sc` 将文件复制到每个新服务器。或者，你可以将自定义代码维护在版本控制系统中，通过检出（checkout）来配置新系统。这种技术比使用 `diff` 来查找系统之间的更改要简单得多。

# 文件系统布局

本节列出了配置 Apache 和提供 Web 服务时将用的文件位置和用途。

## 二进制文件

# 第 26 章 APACHE：设置 Web 服务器

默认启用。两个最常用的模块二进制文件是 `mod_perl`（`libapache2-mod-perl` 包的一部分）和 `mod_python`（`libapache2-mod-python` 元包的一部分）。此目录下的 `*.load` 文件从 `/usr/lib/apache2/modules` 目录加载（见第 941 页）。`*.conf` 文件用于配置模块的使用。参阅第 905 页有关使用 `a2enmod` 启用模块的信息。

- `/etc/apache2-enabled`——存放指向 `mods-available` 的链接。使用 `a2enmod` 创建链接，使用 `a2dismod` 链接（见第 905 页）。

Apache 配置文件保留在 `/etc/apache2` 层级结构中：
- `/etc/apache2/apache2.conf`——存放配置指令。该文件是主配置文件。你通常不会修改此文件，而是将任何配置指令放在 `httpd.conf` 等文件中。
- `/etc/apache2/vars`——存放修改 Apache 运行环境的变量。
- `/etc/apache2/ports.conf`——存放 `Listen` 指令（见第 910 页），用于控制 Apache 监听的 IP 地址和端口。
- `/etc/apache2/sites-available`——存放包含虚拟主机代码的文件。参阅第 906 页有关使用 `a2ensite` 启用站点的信息。
- `/etc/apache2/sites-enabled`——存放指向 `sites-available` 的链接。使用 `a2ensite` 链接（见第 906 页）。
- `/etc/apache2/httpd.conf`——存放本地配置指令。该文件是同目录 la `apache2.conf` 文件的片段。配置讨论从第 909 页开始。
- `/etc/apache2/conf.d`——存放配置文件。

日志保留在 `/var/log/apache2/`：

- `/var/log/apache2/access_log`——记录发送到服务器的请求。
- `/var/log/apache2/error_log`——记录请求和服务器运行时错误。

Web 文档（包括客户端浏览器显示的 Web 页面）、自定义错误消息和 CGI 脚本默认保留在 `/var/www` 中：

- `/usr/lib/cgi-bin`——存放 CGI 脚本（见第 942 页）。该目录别名为 `/cgi-bin/`。
- `/usr/share/apache2/error`——存放默认错误文档。你可以修改这些文档以确认你 Web 站的样式。该目录别名为 `/error/`。参阅 `ErrorDocument`（见第 924 页）。
- `/usr/share/apache2/icons`——存放用于显示目录条目的图标。该目录别名为 `/icons/`。
- `/usr/share/doc/apache2-doc/manual/index.html`——Apache 服务器版本 2.2 文档。当 Apache 运行且安装了 `apache2-doc` 时，将浏览器指向 `server/manual`，其中 `server` 是 `localhost` 或你的 IP 或 Apache 服务器地址。

文档根 默认情况下，文档根（见第 902 页）是 `/var/www`。你可以通过 `DocumentRoot` 指令（见第 913 页）更改此位置。除了 Apache 提供的 Web 页面内容外，此目录还可以存放 `webizer` 目录，其中存放 `webalizer`（见第 948 页）的输出。

`.htaccess` `.htaccess` 文件包含配置指令，可以出现在文档根层级中的任何目录。`.htaccess` 文件的位置至关重要：存放 `.htaccess` 文件的目录指令适用于该层级中的所有文件。`AllowOverride` 指令（见第 930 页）控制 Apache 是否检查 `.htaccess` 文件。由于默认站点允许 `AllowOverride None` 指令，你必须使用 `AllowOverride` 指令让 Apache 检查 `.htaccess` 文件并处理其中的指令。这种保护在 Ubuntu 分发的 `configapache2.conf` 文件中得到了复制和增强，其中一个指令允许 Apache 不提供文件名以 `.ht` 开头的文件（它会提供 `.htaccess` 文件）。

# 配置指令

配置指令（或简称指令）是配置文件中的行，用于控制 Apache 运行的某些方面。配置指令由一个关键字后跟由空格分隔的一个或多个参数（值）组成。

## 指令 I：入门时可能想要修改的指令

当 Apache 启动时，会读取 `apache2.conf`（默认）来获取 Apache 运行各个方面的指令。本节详细介绍了你可能想要添加到 `httpd.conf` 或在其他一个文件中更改的指令。

- `ServerRoot`：指定 Apache 安装的根目录。
- `StartServers`：启动时启动的子进程数。
- `ThreadsPerChild`：每个子进程处理的线程数。
- `MaxSpareThreads`：Apache 保留的最大空闲线程数。
- `MinSpareThreads`：Apache 保留的最少空闲线程数。
- `MaxClients`：Apache 最大并发请求数。
- `MaxKeepAliveRequests`：每个持久连接允许的请求数。
- `KeepAliveTimeout`：Apache 等待另一个请求的时间。
- `LockFile`：Apache 的锁文件路径。
- `Timeout`：Apache 等待请求完成的秒数。
- `LogLevel`：日志记录级别。
- `TypesConfig`：包含 MIME 类型定义的文件。
- `User`：运行 Apache 的用户。
- `MaxRequestsPerChild`：子进程在被杀死之前提供的请求数。
- `AccessFileName`：访问日志文件的前缀。
- `DefaultType`：未指定文件的默认 MIME 类型。
- `ErrorLog`：错误日志文件路径。
- `Group`：运行 Apache 的组。
- `HostNameLookups`：Apache 是否应客户端查找主机名。

默认：无（如果没有此指令，Apache 将不会启动）
Ubuntu：`Listen 80`

`Redirect` 通知客户端从另一个指定的位置获取请求的资源。

```
Redirect [status] requested-path [new-URI]
```

其中 `status` 是 Apache 随重定向一起返回的状态码。如果省略了 `status`，Apache 将假设为 temp（临时）。该状态可以是 300–399 范围内的错误代码，或者是以下状态之一：

- `permanent` 返回状态 301（资源已永久移动）
- `temp` 返回状态 302（资源临时移动）
- `seeother` 返回状态 303（资源已被替换）
- `gone` 返回状态 410（资源已删除——不接受 new-URI 参数）

`requested-path` 是 Apache 应当对其请求进行重定向的文件或目录的绝对路径名。Apache 会重定向所有以 `requested-path` 指定的路径名开头的请求。（见下文示例）。如果你想在此参数中使用正则表达式，请使用 `RedirectMatch`（后文将进行讨论）。

`new-URI` 是 Apache 请求的 URI。如果 `new-URI` 以斜杠（`/`）开头而不是 `http://` 或类似的前缀，Apache 将使用相同的前缀来修复其调用的路径。大多数 `Redirect` 指令都需要 `new-URI` 参数。

请求必须匹配 `requested-path` 参数的所有分段。假设有以下指令：

```
Redirect /www.example.com/pictures http://pictures.example.com/
```

Apache 将把对 `http://www.example.com/pictures/mom.jpg` 的请求重定向到 `http://pictures.example.com/mom.jpg`，但如果最后一个段不匹配，它将不会重定向对 `http://www.example.com/pictures/mom.jpg` 的请求。

上下文：服务器配置 (`server config`), 虚拟主机 (`virtual host`),  (`directory`), `.htaccess`
在 `sites-available/*` 中指定
默认：无
Ubuntu：无

`RedirectMatch` 通知客户端从由正则表达式指定的另一个位置获取请求资源。

```
RedirectMatch [status] requested-path [new-URI]
```

此指令与 `Redirect`（上文描述）相同，不同之处是你可以在 `requested-path` 中使用正则表达式（附录 A）。

上下文：服务器配置 (`server config`), 虚拟主机 (`virtual host`),  (`directory`), `.htaccess`
在 `sites-available/*` 中指定
默认：无
Ubuntu：无

## 第 26 章 APACHE：设置 Web 服务器

## ServerAdmin 设置错误页面上 mailto: 链接使用的电子邮件地址。

### ServerAdmin email-address

`email-address` 是负责管理 Web 内容的人员的电子邮件地址。Apache 在生成的错误页面上会将此地址作为链接包含。然而，Ubuntu Linux 将 `ServerSignature`（第 927 页）设置为 `On`，这会导致 Apache 在错误页面上显示有关服务器的信息，而不是指向电子邮件地址的链接。如果你想在错误页面上显示该链接，请将 `ServerSignature` 设置为 `EMail`。确保 `email-address` 指向一个有人经常检查的邮箱账户。用户可以使用此地址帮助网站，或向管理员告知处理过程。`ServerAdmin` 没有默认值；如果你不使用此指令且 `ServerSignature` 设置为 `EMail`，则错误页面上的 `mailto:` 链接将指向 [未给出地址]。

### ServerAdmin 吸引垃圾邮件

`security` 安全 你在 `ServerAdmin` 中填写的电子邮件地址往往会吸引垃圾邮件。可以使用一个受垃圾邮件保护的地址，例如 "`mgs at sobel com`"（你必须使用引号），或者使用自定义错误页面指向一个带有表单的网页，以便向正确的人发送邮件。

你可以使用如域名下的 `webmaster` 这样的角色，并通过一个设置为 `webmaster` 的邮件别名将其转发给负责维护网站的人员。见第 722 页关于邮件别名的讨论。

上下文：服务器配置 (`server config`), 虚拟主机 (`virtual host`)
在 `sites-available/*` 中指定
默认：无
Ubuntu：`webmaster@localhost`

## ServerName 指定服务器的名称以及其监听的端口。

### ServerName FDN [:port]

其中 `FDN` 是服务器的全限定域名名（FQDN）或 IP 地址，`port` 是 Apache 监听的可选端口号。服务器的域名可能（通过 DNS 或 `/etc/hosts`）解析，并可能与运行服务器的系统主机名不同。如果你不指定 `ServerName`，Apache 将对系统的 IP 地址执行 DNS 反向域名解析（第 831 页），并将该值分配给 `ServerName`。如果反向查找失败，Apache 将将系统 IP 分配给 `ServerName`。

在以下示例中，将 `www.example.com` 替换为服务器的 FDN 或 IP 地址。将 `80` 更改为 Apache 监听的端口（如果不是 80 的话）。

```
# ServerName www.example.com:80
```

如果你希望 `ServerName` 指定的 FDN 与 `Listen` 指令指定的 IP 地址绑定，则 `ServerName` 和 `Listen`（第 910 页）指定的端口是相同的。

Apache 在重定向客户端时使用 `ServerName` 来构建 URI（第 935 页）。
另请 `UseCanonicalName`（第 922 页）。

上下文：服务器配置 (`server config`), 虚拟主机 (`virtual host`)
在 `sites-available/*` 中指定
默认：无
Ubuntu：无

## DocumentRoot（文档根）指向包含服务器内容的目录层次结构的根目录。

```
DocumentRoot dirname
```

其中 `dirname` 是包含 Apache 所服务的内容的目录层次结构根目录的绝对路径名。不要在末尾使用斜杠。你可以将文档根放在任何地方，只要 `www-data` 对普通文件具有访问权限，并对目录中的文件具有执行权限。

DocumentRoot Points to the root of the directory hierarchy that holds the server's content.

```
DocumentRoot dirname
```

where `dirname` is the absolute pathname of the directory at the root of the directory hierarchy that holds the content Apache serves. Do not use a trailing slash. You can put the document root wherever you like, as long as the `www-data` has access to the ordinary files and execute access to the directory files in the directory.

# 上下文与容器

为了实现灵活且易于定制，Apache 使用配置指令、上下文和容器。配置指令在上一节中已经介绍过。本节将讨论上下文和容器，它们对于管理 Apache 服务器至关重要。

# 上下文

四个被称为“上下文（contexts）”的位置定义了配置指令可以出现的位置。本章标记了每个配置指令，以指示它们可以在哪些上下文中出现。表 26-2 描述了这些上下文。

表 26-2 上下文

| 上下文 | 指令出现的位置 |
|---|---|
| 服务器配置 (`server config`) | 在 `apache2.conf` 或包含的文件，但不在 `<VirtualHost>` 或 `<Directory>` 容器内（下一节），除非已标记 |
| 虚拟主机 (`virtual host`) | 在 `apache2.conf` 或包含文件的 `<VirtualHost>` 容器内 |
| 目录 (`directory`) | 在 `apache2.conf` 或包含文件的 `<Directory>`、Location> 和 `<Files>` 容器内 |
| `.htaccess` | 仅在 `.htaccess` 文件（第 909 页）中 |

通过 `Include` 指令（第 927 页）引入的文件中的指令属于其被包含的上下文，并且必须在该上下文中被允许。

将指令放在错误的上下文中会导致配置错误，并可能导致 Apache 无法正确提供内容或启动。

# 容器

容器（Containers）或特殊指令是分组其他指令的指令。容器由 XML 风格的标签分隔。这里显示了三个示例：

```
<Directory> ... </Directory>

<Location> ... </Location>
```
