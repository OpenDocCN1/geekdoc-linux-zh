

## 10.6. 默认模块

Apache HTTP Server 分发了许多模块。默认情况下，Red Hat Linux 上的 httpd 软件包安装并启用了以下模块：

```
mod_access
mod_auth
mod_auth_anon
mod_auth_dbm
mod_auth_digest
mod_include_config
mod_env
mod_mime_magic
mod_cern_meta
mod_expires
mod_headers
mod_usertrack
mod_unique_id
mod_setenvif
mod_mime
mod_dav
mod_status
mod_autoindex
mod_asis
mod_info
mod_cgi
mod_dav_fs
mod_vhost_alias
mod_negotiation
mod_dir
mod_imap
mod_actions
mod_speling
mod_userdir
mod_alias
mod_rewrite
mod_proxy
mod_proxy_ftp
mod_proxy_http
mod_proxy_connect
```

此外，通过安装额外的软件包可以使用以下模块：

```
mod_auth_mysql
mod_auth_pgsql
mod_perl
mod_python
mod_ssi
php
squirrelmail
```

## 10.7. 添加模块

Apache HTTP Server 提供了动态共享对象 (DSO) 或模块，可以根据需要方便地运行时加载。

Apache 项目在网上提供了完整的 DSO 文档，地址为 http://http.apache.org/docs-2.0/dso.html；或者如果安装了软件包，可以在 http://localhost/mod/ 找到关于 DSO 的文档。

要让 Apache HTTP Server 使用 DSO，必须在 /etc/http/conf/http.conf 中的 `LoadModule` 指令中指定它；如果该模块是由单独软件包提供的，则该行必须出现在 /etc/http/conf.d/ 目录下的模块文件中。有关 `LoadModule` 指令的更多信息，请参阅第 10.5.15 节 LoadModule。

如果从 http.conf 中添加或删除模块，必须重新加载或重启 Apache HTTP Server，具体见第 10.4 节 启动和停止 httpd。

如果创建一个新模块，请先安装 `httpd-devel` 软件包，因为它包含了包含文件、头文件以及 Apache 扩展 (/usr/bin/apxs) 程序，该程序使用包含文件和头文件来编译 DSO。

编写模块后，使用 /usr/bin/apxs 在 Apache 源码树之外编译模块源码。有关使用 /usr/bin/apxs 命令的更多信息，请参阅 Apache 在线文档 http://apache.org/docs-2.0/dso.html 和 `apxs` 手册页。

编译完成后，将模块放在 /usr/lib/httpd/ 目录中。然后向 http.conf 中添加一条 `LoadModule` 行，使用以下结构：

```
LoadModule <module-name> <path/to/module.so>
```

在上面的示例中，将 `<module-name>` 更改为模块名称，将 `<path/to/module.so>` 更改为 DSO 的路径。

## 10.8. 虚拟主机

Apache HTTP Server 内置的虚拟主机允许服务器根据请求的 IP 地址、主机名或端口提供不同的信息。使用虚拟机的完整指南可以在 http://apache.org/docs-2.0/vhosts/ 查看。

### 10.8.1. 设置虚拟主机

要创建一个基于虚拟机的主机，最好以 httpd.conf 中提供的虚拟主机容器作为示例。

虚拟主机的读取示例如下：

```
#NameVirtualHost *
#
#<VirtualHost *>
# ServerName webmaster@dummy-host.example.com
# DocumentRoot /www/docs/dummy-host.example.com
# ServerName dummy-host.example.com
# ErrorLog logs/dummy-host.example.com-error_log
# CustomLog logs/dummy-host.example.com-access_log common
#</VirtualHost>
```

要激活原生虚拟主机，请通过删除井号 (#) 取消 `NameVirtualHost` 行的注释，并将星号 (*) 替换为分配给机器的 IP 地址。

接下来，通过取消注释并自定义 `<VirtualHost>` 容器来配置虚拟主机。

在 `<VirtualHost>` 行上，将星号 (*) 更改为服务器的 IP 地址。将 `ServerName` 更改为分配给机器的有效 DNS 名称，并根据需要配置其他指令。

`<VirtualHost>` 容器具有高度可定制性，并接受主服务器配置中提供的几乎每一个指令。

> 提示
> 如果配置虚拟主机监听非默认端口，则必须在 /etc/httpd/conf/http.conf 文件的全局设置部分在 `Listen` 指令中添加该端口。

要激活新创建的虚拟主机，必须重新加载或重启 Apache HTTP Server。有关此的说明请参考第 10.4 节 启动和停止 httpd。

关于配置和创建基于名称和基于 IP 地址的虚拟机的全面信息，可以在 http://httpd.apache.com/docs-2.0/vhosts/ 查看。

### 10.8.2. Web 服务器虚拟主机

默认情况下，Apache HTTP Server 被配置为非安全和安全服务器。非安全服务器和安全服务器使用相同的 IP 地址和主机名，但监听不同的端口上：分别为 80 和 443。这允许同时进行非安全和安全通信。

SSL 增强型 HTTP 传输的一个方面是它们比标准 HTTP 协议更消耗资源，因此安全服务器提供的页面数量永远不会比普通服务器多。因此，减少安全服务器的可用信息通常是一个好主意，特别是在高流量网站上。

> 注意
> 不要与安全 Web 服务器结合使用基于名称的虚拟主机，因为 SSL 握手发生在 HTTP 识别相应的名称的虚拟主机之前。基于名称的虚拟主机仅适用于非安全 Web 服务器。

安全服务器的配置指令包含 /etc/httpd/conf.d/ssl.conf 文件中的 `<VirtualHost>` 标签内。

默认情况下，安全和非安全 Web 服务器共享相同的 `DocumentRoot`。建议安全 Web 服务器使用不同的 `DocumentRoot`。

要停止非安全服务器接受连接，请通过放置井号 (#) 将 httpd.conf 中读取 `Listen 80` 的行注释掉。

