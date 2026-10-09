
```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

`Options` 指令（第 811 页）允许 Apache 跟踪符号链接，但禁止许多选项。`AllowOverride` 指令（第 813 页）使 Apache 忽略 `.htaccess` 文件。如果你想使用限制性选项，必须显式启用它们，但请注意这样做可能会暴露根文件系统并损害系统安全。

接下来另一个 `<Directory>` 容器为 `DirectoryRoot (/var/www/html)` 设置了限制性选项。`httpd.conf` 中的代码穿插着许多命令。在没有注释的情况下，它看起来像这样：

```
<Directory "/var/www/html">
Options FollowSymLinks
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

`Options` 指令中的 `Indexes` 选项允许 Apache 显示目录列表。`Order`（第 814 页）和 `Allow`（第 812 页）指令结合使用，允许来自所有客户端的请求。此容器的限制比前一个略少，尽管它仍然不允许 Apache 跟踪 `.htaccess` 中的指令。

```
DirectoryIndex
```

如第 797 页所示，`DirectoryIndex` 指令导致 Apache 从请求的目录返回文件索引 `index.php`、`index.html`、`index.htm` 或 `index.shtml`。因为在之前的 `<Directory>` 容器中指定了 `Options Indexes`，如果这些文件中都不存在，Apache 将返回目录列表：

```
DirectoryIndex index.php index.html index.shtml
```

`httpd.conf` 的此部分还有许多指令。文件中的注释提供了这些指令的作用指南。在使用 Apache 时，这里没有你需要更改。

## 第 3 节：虚拟主机

此节的所有行都是注释或注释掉的指令。如果你想设置虚拟主机，请参见第 18 页。

### 重定向

Apache 可以通过请求请求不同的 `URI` 来响应 `URI` 请求。这种响应被称为重定向。重定向是 `HTTP` 实现的一部分：Apache 发适当的响应代码和新的 `URI`，符合标准的浏览器请求新位置。

### UseCanonicalName

`ServerName` 指令 (796) 建立服务器名称，`UseCanonicalName` 指令 (805) 在服务器具有多个名称并需要执行自动重定向时都是非常重要的。例如，假设名为 `zach.example.com` 的服务器 `ServerName` 设置为 `example.com`。当客户端指定目录的 `URI` 但缺少结尾斜杠时 (`zach.example.com/dir`)，Apache 必须执行重定向以确定请求目录的 `URI`。当 `UseCanonicalName` 设置为 `On` 时，Apache 使用 `ServerName` 的值并返回 `www.example.com/dir/`。当 `UseCanonicalName` 设置为 `Off` 时，Apache 使用请求中的名称。

## Multiview

`Multiview` 以不同方式表示页面的方法，通常不同的语言。使用请求头，浏览器可以从服务器请求特定语言。无法处理这些请求的服务器忽略它们。

# RHEL

`Multiview` 由 Apache 手册演示，它可以本地安装在 `/var/www/manual`。当你将浏览器指向 `http://server/manual/index.html` 时，浏览器以默认语言显示页面。如果你更改浏览器默认语言设置并刷新页面，浏览器将用新语言显示。浏览器可以显示不同语言的页面，因为服务器为每种语言都有页面的副本。例如，`index.html.en` 和 `index.html.de` 都存在于 `/var/www/manual` 目录。

## 服务器生成的目录列表（索引）

当客户端请求目录时，Apache 配置决定返回什么。Apache 可以返回由 `DirectoryIndex` 指令 (797) 指定的文件；如果没有匹配的文件且 `Options Indexes` 指令（第 811 页）已设置，则返回目录列表；如果没有匹配的文件且 `Options Indexes` 未设置，则返回错误消息。

## 虚拟主机

Apache 支持虚拟主机，这意味着 Apache 实例可以响应指向多个 `IP` 地址或主机名的请求，就像是多个服务器一样。每个 `IP` 地址或主机名都可以提供不同的内容并进行不同的配置。虚拟主机有两种类型：`host-name` 和 `host-IP`。`host-name` 依赖客户端在请求 Apache 时使用的 `FQDN`，例如 `www.example.com` 与 `www2.example.com`。`host-IP` 检查它解析的 `IP` 地址并对其响应。如果只有一个 `IP` 地址，`host-name` 非常方便，但 Apache 必须支持多个 `FQDN`。尽管如果指定的 Web 服务器有别名可以使用 `host-IP`，但无论使用哪个名称，Apache 都应该提供相同的内容。虚拟主机的配置继承自 `httpd.conf` 第 1 own（第 815 页）和第 2 部分（第 816 页）。如果只有一个 `IP` 地址，`host-name` 非常方便，但 Apache 必须支持多个 `FQDN`。尽管如果指定的 Web 服务器有别名可以使用 `host-IP`，但无论使用哪个名称，Apache 都应该提供相同的内容。

## 故障排除

Apache 可以通过请求请求不同的 `URI` 来响应 `URI` 请求。这种响应被称为重定向。重定向是 `HTTP` 实现的一部分：Apache 发送适当的响应代码和新的 `URI`，符合标准的浏览器请求新位置。

`Redirect` 可以建立一个显式重定向，当网站移动时将客户端发送到不同的页面。或者，当用户在浏览器中输入目录 `URI` 但缺少结尾斜杠时，Apache 可以自动将客户端重定向到带有斜杠的相同 `URI`。

### UseCanonicalName

`ServerName` 指令 (796) 建立服务器名称，`UseCanonicalName` 指令 (805) 在服务器具有多个名称并需要执行自动重定向时都是非常重要的。例如，假设名为 `zach.example.com` 的服务器 `ServerName` 设置为 `example.com`。当客户端指定目录的 `URI` 但缺少结尾斜杠时 (`zach.example.com/dir`)，Apache 必须执行重定向以确定请求目录的 `URI`。当 `UseCanonicalName` 设置为 `On` 时，Apache 使用 `ServerName` 的值并返回 `www.example.com/dir/`。当 `UseCanonicalName` 设置为 `Off` 时，Apache 使用请求中的名称。

## Multiview

`Multiview` 以不同方式表示页面的方法，通常不同的语言。使用请求头，浏览器可以从服务器请求特定语言。无法处理这些请求的服务器忽略它们。

# RHEL

`Multiview` 由 Apache 手册演示，它可以本地安装在 `/var/www/manual`。当你将浏览器指向 `http://server/manual/index.html` 时，浏览器以默认语言显示页面。如果你更改浏览器默认语言设置并刷新页面，浏览器将用新语言显示。浏览器可以显示不同语言的页面，因为服务器为每种语言都有页面的副本。例如，`index.html.en` 和 `index.html.de` 都存在于 `/var/www/manual` 目录。

## 模块

Apache 是一个骨架程序，依赖于称为动态对象 (`DSM`) 的外部模块来提供大部分功能。本节列出了这些模块，并讨论了其中最重要的模块。除了 Apache 自带的模块外，还有许多其他模块可用。参见 `apache.org/modules`。

## 模块列表

以下是 Apache 下可用的模块列表：

- `access (mod_access.so)` 基于客户端控制访问。
- `actions (mod_actions.so)` 根据请求方法执行 `CGI` 脚本。
- `alias (mod_alias.so)` 允许外部目录映射到 `DocumentRoot`。
- `asis (mod_asis.so)` 允许发送包含自身标部的文件。
- `auth (mod_auth.so)` 通过 `htpasswd` 提供用户验证。
- `auth_anon (mod_auth_anon.so)` 为匿名用户提供受限区域。
- `auth_dbm (mod_dbm.so)` 使用 `DBM` 文件进行认证。
- `auth_digest (mod_digest.so)` 使用 `MD5` 摘要进行认证。
- `autoindex (mod_autoindex.so)` 允许生成目录索引。
- `cern_meta (mod_cern_meta.so)` 允许使用 `CERN` 元语义。
- `cgi (mod_cgi.so)` 允许执行 `CGI` 脚本。
- `dav (mod_dav.so)` 允许分布式作者和版本控制。
- `dav_fs (mod_dav_fs.so)` 为 `mod_dav` 提供文件系统。
- `dir (mod_dir.so)` 允许目录重定向和作为索引文件的列表。
- `env (mod_env.so)` 允许 `CGI` 脚本访问环境变量。
- `expires (mod_expires.so)` 允许生成 `Expires` 头部。
- `headers (mod_headers.so)` 允许自定义请求和响应头部。
- `imap (mod_imap.so)` 允许在服务器端处理图像映射。
- `include (mod_include.so)` 提供服务器端包含 (`SSI`)。
- `info (mod_info.so)` 允许查看服务器配置。
- `log_config (mod_log_config.so)` 允许记录对服务器的请求。
- `mime (mod_mime.so)` 允许将文件扩展名与内容关联。
- `mime_magic (mod_mime_magic.so)` 确定文件的 `MIME` 类型。
- `proxy (mod_proxy.so)` 允许 Apache 作为代理服务器。
- `proxy_connect (mod_proxy_connect.so)` 允许处理连接请求。
- `proxy_ftp (mod_proxy_ftp.so)` 提供 `FTP` 扩展代理。
- `proxy_http (mod_proxy_http.so)` 提供 `HTTP` 扩展代理。
- `rewrite (mod_rewrite.so)` 允许根据规则进行即时重写。
- `setenvif (mod_setenvif.so)` 根据请求设置环境变量。
- `spelling (mod_spelling.so)` 如果 `URI` 的大小写不正确或有一个拼写错误，则会自动纠正拼写。
- `status (mod_status.so)` 允许查询并显示服务器。
- `unique_id (mod_unique_id.so)` 为每个请求生成唯一 `ID`。
- `userdir (mod_userdir.so)` 允许用户拥有内容目录 (`public_html`)。
- `usertrack (mod_usertrack.so)` 允许跟踪网站上的用户活动。
- `vhost_alias (mod_vhost_alias.so)` 允许配置虚拟主机。

## mod_cgi 和 CGI 脚本

`CGI`（通用网关接口）允许外部程序与 Web 服务器交互。只要程序是实时（在请求时）运行并将输出转发到请求客户端，任何程序都可以运行。各种类型的脚本，包括 `Shell`、`Perl`、`Python` 和 `PHP`，是最常见的 `CGI` 程序，因为脚本可以调用程序并为客户端将其输出重新格式化为 `HTML`。

Apache 可以通过几种不同的方式处理 `CGI` 请求。最方法是将 `CGI` 程序放在 `cgi-bin` 目录中，然后允许从该目录执行。`cgi-bin` 目录的位置（第 812 页）是 `/var/www/cgi-bin`。此外，`AddHandler` 指令（第 806 页）可以识别普通内容的脚本扩展名，例如 `.cgi` 或 `.pl`（例如 `AddHandler cgi-script .cgi`）。如果你使用 `AddHandler`，还必须在 `<Directory>` 的 `Options` 指令中指定 `Execute` 选项。必须加载 `mod_cgi` 模块才能访问和执行 `CGI` 脚本。

以下 `Perl` 脚本显示 Apache 环境。此脚本仅用于调试，因为如果用户可以访问它将存在安全风险：

```
#!/usr/bin/perl
##
print -- demo CGI program that prints its environment
##
print "Content-type: text/plain";
foreach $var (sort(keys(%ENV))) {
  $val = $ENV{$var};
  $val = s/\n//g;
  $val = s/"///g;
  print "$var=$val\n";
}
```

## mod_ssl

`SSL`（安全套接层）由 `mod_ssl` 模块实现，有两个功能：它允许客户端验证服务器身份，并确保客户端与服务器之间的安全双向通信。`SSL` 用于带有密码、信用卡或其他敏感数据的 Web 表单。

Apache 使用 `HTTPS` 协议 通 通。当 Apache 使用 `SSL` 时，它监听端口（默认为 `443`）等待连接，并在向客户端发送请求内容之前执行握手序列。

服务器验证对于金融交易至关重要。毕竟，你不想将信用卡号交给伪装成已知网站的欺诈性网站。在互联网等公共网络上，只有当证书包含来自 `VerSign` 或 `Trust` 等权威源的数字签名时，身份识别才是可靠的。`SSL` 页面以 `https://` 开头的 `URI` 表示。

数据加密防止恶意用户监听互联网连接并复制个人信息。为了加密通信，`SSL` 位于网络和应用程序之间，并加密服务器与客户端之间的通信。

## 设置 mod_ssl

`/etc/httpd/conf.d/ssl.conf` 文件配置 `mod_ssl`。该文件中的第一个指令加载 `mod_ssl` 模块，指示 Apache 监听 `443` 端口，并设置 `SSL` 操作参数。文件大约三分之一处有一个标记为 `SSL Virtual Host` 的部分，用于设置虚拟主机 (818)。

`ssl.conf` 中的 `<VirtualHost>` 容器类似于 `httpd.conf` 中的容器。作为任何 `<VirtualHost>`，它持有需要配置的 `ServerName` 和 `ServerAdmin` 等指令。此外，它还包含一些 `SSL` 相关的指令。

## 使用自签名证书进行加密

如果你只需要 `SSL` 加密而不是验证，并且客户端已经可以生成和使用自签名证书，就可以节省获取数字签名证书的时间和费用。连接到服务器时，自签名证书会产生警告。大多数浏览器会显示对话框，允许你检查并接受证书。`sendmail` 进程使用证书 (650)。

自签名证书依赖于两个文件：私钥和证书。每个文件的位置在 `/etc/httpd/conf.d/ssl.conf` 中指定。在 `Fedora` 和 `RHEL` 下，具有不同的名称并存储在不同的位置。

`FEDORA`

```
# grep *SSLCertificate* /etc/httpd/conf.d/ssl.conf
SSLCertificateFile /etc/pki/tls/certs/localhost.crt
SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
```

要生成加密依赖的私钥，进入到 `/etc/pki/tls/certs` 并输入适当命令：

```
# cd /etc/pki/tls/certs
# make localhost.key
```

```
umask 77
openssl req -new -newkey rsa:2048 -nodes -out localhost.key -x509 -days 365 -out localhost.crt
```

（注：命令的 `OCR` 识别非常混乱。我根据提供的上下文重构了可能的 `openssl` 命令。）

`.htaccess` 的第二行禁用了组功能。第四行使用了由默认 `mod_auth` 实现的基础身份验证（Basic authentication）。最后一行告诉 Apache 用户可以访问受保护的目录。`valid-user` 条目允许在 Apache 密码文件中存在且输入正确密码的用户访问该目录。你也可以指定由空格分隔的 Apache 用户。

只要 Apache 可以读取密码文件，你就可以将密码文件放置在系统的任何位置。将此文件与 `.htaccess` 文件放在同一目录下是安全的，因为 Apache 不会对任何名称以 `.` 开头的文件发起任何请求。

以下命令为 `Sam` 创建一个 `htpasswd` 文件：

```
$ htpasswd -c .htpasswd sam
New password:
Re-type new password:
Adding password for user sam
```

在现有的 `htpasswd` 文件中添加用户或更改密码时，请省略 `c` 选项。记得使用 `AllowOverride` 指令（第 813 页）允许 Apache 读取 `.htaccess` 文件。

## 脚本模块 (Scripting Modules)

Apache 可以在将内容发送给客户端之前对其进行处理。在 Apache 的早期版本中，只有 `CGI` 脚本可以处理内容。在当前版本中，脚本模块可以与嵌入在 `HTML` 文档中的脚本配合。

脚本模块在 Apache 将内容提供给客户端之前对其进行处理。由于它们内置在 Apache 中，因此运行速度很快。脚本模块在处理外部数据源（如关系型数据库）时特别高效。客户端可以将数据传递给脚本模块，由模块修改 Apache 提供的信息。

将脚本模块与 Apache 外部 `CGI` 脚本进行对比：`CGI` 脚本不允许客户端交互，并且由于它们必须进行外部调用，速度较慢。
