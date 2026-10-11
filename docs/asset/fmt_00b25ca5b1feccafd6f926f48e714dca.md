
# Apache Web 服务器

## 指令行为

指令的注释部分已被删除以减少空间消耗。让我们讨论每条指令的行为。

在 `Server` 指令中，会附加日志文件或附加配置文件的名称。默认 `Server` 指令值为 `/etc/httpd`。在 `Pidfile` 指令中，定义服务器进程的 PID。默认其值设置为 `/httpd.pid`。`Timeout` 指令定义 Apache 等待发送和接收操作的最大时间。其单位为秒，值设置为 `120`。`KeepAlive` 指令（值=`On`）设置与客户端之间通过 `KeepAliveTimeout` 指定的直接连接。此处被设置为 `Off`。`MaxAliveRequests` 指令设置每个连接允许的请求数。默认支持 `100` 个。`KeepAliveTimeout` 指令设置了服务器上来自同一客户端的请求之间允许通过连接之前的间隔秒数。如果 `KeepAlive` 设置为 `On`，其值设置为 `15`。

`StartServers` 指令定义了 Apache 启动时创建的子服务器数量。默认 Apache 启动时创建 `8` 个子服务器。`MinSpareServers` 定义了允许的最小子服务器数量。默认值为 `5`，`MaxSpareServers` 定义了主服务器可以生成的子服务器的最大值。`ServerLimit` 指定了同时运行的服务器进程或线程数量的上限。默认上限为 `256`。`MaxClients` 指令设置支持的最大连接数。默认设置为 `256`。`MaxRequestsPerChild` 定义了每个子服务器终止之前执行的最大请求数。默认是 `4000`。

`LoadModule` 指令将文件名加载到服务器中并使用名称将其添加到活动模块列表中。`Listen` 指令定义了 Apache 监听连接的 IP 地址和端口组合。默认情况下它监听 `80` 端口，你可以使用多个指令。`Include` 指令包含以 `.conf` 结尾的文件内容。

对于大多数情况，配置文件中的默认值已经足够。通常不需要更改，除非将 `MaxSpareServers` 和 `StartServers` 的值分别减少到 `10` 和 `5`。将 `KeepAlive` 设置为 `On` 会获得更好的性能。

## 配置默认服务器

让我们学习配置默认服务器。

第二部分由定义“主”或“默认”服务器参数的指令组成，该服务器响应未被虚拟机处理的请求。这些指令还为所有虚拟主机的设置提供了默认值。虚拟主机是通过 `/etc/httpd/conf/httpd.conf` 中指定的 IP 地址或端口与主服务器区分的虚拟主机。

### Section 2: 'Main' server

```
ServerAdmin apache

Group apache

DocumentRoot "/var/www/html"

<Directory />

Options FollowSymLinks

AllowOverride None

</Directory>

<Directory "/var/www/html">

Options FollowSymLinks

AllowOverride None

</Directory>

<IfModule mod_dir.c>

DirectoryIndex index.html

</IfModule>

<IfModule mod_mime_type.c>

AddType text/plain *

</IfModule>

<IfModule mod_access_file.c>

Order Allow,Deny

</IfModule>

<IfModule mod_log_config.c>

ErrorLog logs/error.log

LogLevel warn

LogFormat "%h %l %u %t \"%r\" %>s %b" common

CustomLog logs/access_log combined

ServerSignature off

Alias /icons/ "/var/www/icons/"

<Directory "/var/www/icons/">

Options FollowSymLinks

AllowOverride None

</Directory>
```

```
BrowserMatch "^WebDAVFS/1.[0123]" redirect-carefully

BrowserMatch "^Agnome-vfs/1.0" redirect-carefully

BrowserMatch "^XML spy" redirect-carefully

BrowserMatch "^Dreamweaver-webdav-SKI" redirect-carefully
```
