
```
<IfModule mod_ssl>
Listen 443
</IfModule>

<IfModule mod_alias.c>
ScriptAlias /cgi-bin/ "/home/httpd/cgi-bin/"
</IfModule>

<IfModule mod_mime>
AddType application/x-tar .tgz
</IfModule>

ErrorDocument 500 "The server made a boo."
ErrorDocument 404 http://192.168.1.1/error.htm
ErrorDocument 403 "Access Forbidden -- Go away."

<IfModule mod_setenv>
BrowserMatch "Mozilla/2* keepalive"
BrowserMatch "MSIE 4.0*, keepalive downgrade-1.0"
BrowserMatch "RealPlayer/4.0* keepalive"
BrowserMatch "Java/1.0* keepalive"
BrowserMatch "JDK/1.0* keepalive"
</IfModule>

<IfDefine SSL>
AddType application/x-x09-ca-cert .crt
AddType application/x-pkcs7 .crt
</IfDefine>

<IfModule mod_ssl>
SSLPhrDialog
SSLSessionCache dbm:/var/run/ssl_scache
SSLSessionTimeout 300
</IfModule>

SSLMutex file:/var/run/ssl_mutex

SSLRandomSeed start builtin
SSLRandomSeed connect builtin

SSLEog /var/log/httpd/ssl_engine_log
SSLLLogLevel warn
</IfModule>

<IfDefine SSL>
<VirtualHost _default_:443>
DocumentRoot "/home/httpd/www"
ServerName www.openapi.com
ServerAdmin admin@openapi.com
ErrorLog /var/log/httpd/error_log

SSLEngine on
SSLCipherSuite All:ADH:RC4+RSA:HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL

SSLCertificateFile /etc/ssl/certs/server.crt
SSLCertificateKeyPath /etc/ssl/private/server.key
SSLCertificatePath /etc/ssl/certs
SSLCertificateFile /etc/ssl/certs/ca.crt
SSLRevocationPath /etc/ssl/crt
SSLVerifyClient none
SSLVerifyDepth 10

SSLOptions +ExportData +StrictRequire
</VirtualHost>
</IfDefine>
```

## 服务器软件（Web 网络服务） | 第9章

```
SetEnvIf User-Agent: "MSIE ..." nokeepalive ssl-unclean-shutdown
SetEnvIf Request_URI \.gif$ -image
CustomLog /var/log/http/ssl_request_log \
  "%t %h %(SSL_PROTOCOL)x %(SSL_CIPHER)x \"%s %b" env=gif-image
<VirtualHost>
</Define>
```

这告诉 `httpd.conf` 文件为此特定的配置设置进行初始化：

`ServerType` `standalone`

"`ServerType`" 选项指定了 Apache 在系统上的运行方式。你可以从超级服务器 `iptd` 运行它，也可以作为独立守护进程（daemon）运行。强烈建议以独立类型运行 Apache，以获得更好的性能和速度。

`ServerRoot` "`etc/httpd`"

"`ServerRoot`" 选项指定了 Apache 服务器配置文件所在的目录。它允许 Apache 在启动时知道可以在哪里找到配置文件。

`PidFile` `/var/run/httpd.pid`

"`PidFile`" 选项指定了服务器启动时记录守护进程进程 ID（PID）的位置。只有当你以独立模式配置 Apache 时才需要此项。

`ResourceConfig` `/dev/null`

"`ResourceConfig`" 选项指定了旧 "`srm.conf`" 文件的位置，Apache 在读取完 "`httpd.conf`" 后会读取它。当你将其设置为 "`/dev/null`" 时，Apache 允许将该文件的内容包含在 "`httpd.conf`" 中，这样你只需要一个文件处理所有的配置参数，更加简单。

`AccessConfig` `/dev/null`

"`AccessConfig`" 选项指定了旧 "`access.conf`" 文件的位置，Apache 在读取完 "`srm.conf`" 后会读取它。当你将其设置为 "`/dev/null`" 时，Apache 允许将该文件的内容包含在 "`httpd.conf`" 中，这样你只需要一个文件处理所有的配置参数。

`Timeout` `300`

"`Timeout`" 选项指定 Apache 等待 GET、PUT 请求以及传输 ACK 的。你可以安全地保持默认值。

`KeepAlive` `On`

"`KeepAlive`" 选项如果设置为 "`On`"，将启用此 Web 服务器的持久连接。为了更好的性能，建议将此选项设置为 "`On`" 并允许每个连接处理多个请求。

`MaxKeepAliveRequests` `0`

"`MaxKeepAliveRequests`" 选项指定了当上述 "`KeepAlive`" 设置 "`On`" 时，每个连接允许的请求数。当此选项的值设置为 "`0`" 时，服务器允许无限请求。为了服务器性能，建议允许无限请求。

`KeepAliveTimeout` `15`

"`KeepAliveTimeout`" 选项指定了 Apache 在关闭连接之前等待后续请求的秒（秒）。"`15`" 秒是服务器性能的良好平均值。

Copyright 1999 - 2000 Gerhard Maurani, Open Network Architecture © and OpenDocs Publishing 383

## 服务器软件（Web 网络服务）

# 第9章

`MinSpareServers` `16`

"`MinSpareServers`" 选项指定了 Apache 不处理请求的空闲子进程最小数量。这是一个关于 Apache 服务器性能的重要调优参数。对于高负载运行，互联网上的各种基准测试建议值为 "`16`"。

`MaxSpareServers` `64`

"`MaxSpareServers`" 选项指定了 Apache 不处理请求的空闲子进程最大数量。这也是一个关于 Apache 服务器性能的重要调优参数。对于高负载运行，互联网上的各种基准测试建议值为 "`64`"。

`StartServers` `16`

"`StartServers`" 选项指定了 Apache 在启动时创建的子进程数量。这同样是一个关于 Apache 服务器性能的重要调优参数。对于高负载运行，互联网上的各种基准测试建议值为 "`16`"。

`MaxClients` `512`

"`MaxClients`" 选项指定了 Apache 支持的并发数。这是一个关于 Apache 服务器性能的重要调优参数。对于高负载运行，互联网上的各种基准测试建议值为 "`512`"。

`MaxRequestsPerChild` `100000`

"`MaxRequestsPerChild`" 选项指定了单个子进程处理的请求数。这同样是 Apache 服务器性能的重要调优参数。

`User` `www`

"`User`" 选项指定了 Apache 服务器运行的 UID。创建一个对系统访问权限最小、且仅用于运行 Web 服务器守护进程之功能的新用户是关重要的。

`Group` `www`

"`Group`" 选项指定了 Apache 服务器运行的 GID。创建一个对系统访问权限最小、且仅用于运行 Web 服务器守护进程之功能的新组是关重要的。

`DirectoryIndex` `index.html index.html index.php default.html index.cgi`

"`DirectoryIndex`" 选项指定了 Apache 用作预写 HTML 目录索引的文件。换句话说，如果 Apache 找不到显示的目录索引页，它将尝试此参数中的下一个条目（如果可用）。为了提高 Web 服务器的性能，建议列出网站最常用的默认索引页。

`Include/mmap.conf`
