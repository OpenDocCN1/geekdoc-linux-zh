
```
Error 400 Server could not understand this request.
Error 401 Server could not verify your authorization.
Error 403 Access Forbidden - Go away.
Error 404 "/error.html"
Error 405 Method not allowed for the requested method.
Error 408 Server closed the network connection.
Error 410 Requested URL is no longer available.
Error 411 Requested method requires a valid header.
Error 412 Precondition required failed positive evaluation.
Error 413 Method not allowed for the data transmitted.
Error 414 Method used exceeds the capacity limit.
Error 415 Server temporarily unavailable.
Error 500 Server encountered an internal error.
Error 501 Server does not support the action requested.
Error 502 Proxy server received an invalid response.
Error 503 Server temporarily unavailable.
Error 506 Access not possible.
```

```
<IfModule mod_setenvif.c>
BrowserMatch "Mozilla/2" keepalive
BrowserMatch "MSIE 4\.0b" keepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4\.0" keepalive force-response-1.0
BrowserMatch "Java/1.0" force-response-1.0
BrowserMatch "Mozilla/1.0" force-response-1.0
BrowserMatch "Mozilla/2.0" force-response-1.0
BrowserMatch "Mozilla/3.0" force-response-1.0
BrowserMatch "Mozilla/4.0" force-response-1.0
BrowserMatch "Mozilla/5.0" force-response-1.0
BrowserMatch "Mozilla/6.0" force-response-1.0
BrowserMatch "Mozilla/7.0" force-response-1.0
BrowserMatch "Mozilla/8.0" force-response-1.0
BrowserMatch "Mozilla/9.0" force-response-1.0
BrowserMatch "Mozilla/10.0" force-response-1.0
BrowserMatch "Mozilla/11.0" force-response-1.0
BrowserMatch "Mozilla/12.0" force-response-1.0
BrowserMatch "Mozilla/13.0" force-response-1.0
BrowserMatch "Mozilla/14.0" force-response-1.0
BrowserMatch "Mozilla/15.0" force-response-1.0
BrowserMatch "Mozilla/16.0" force-response-1.0
BrowserMatch "Mozilla/17.0" force-response-1.0
BrowserMatch "Mozilla/18.0" force-response-1.0
BrowserMatch "Mozilla/19.0" force-response-1.0
BrowserMatch "Mozilla/20.0" force-response-1.0
BrowserMatch "Mozilla/21.0" force-response-1.0
BrowserMatch "Mozilla/22.0" force-response-1.0
BrowserMatch "Mozilla/23.0" force-response-1.0
BrowserMatch "Mozilla/24.0" force-response-1.0
BrowserMatch "Mozilla/25.0" force-response-1.0
BrowserMatch "Mozilla/26.0" force-response-1.0
BrowserMatch "Mozilla/27.0" force-response-1.0
BrowserMatch "Mozilla/28.0" force-response-1.0
BrowserMatch "Mozilla/29.0" force-response-1.0
BrowserMatch "Mozilla/30.0" force-response-1.0
BrowserMatch "Mozilla/31.0" force-response-1.0
BrowserMatch "Mozilla/32.0" force-response-1.0
BrowserMatch "Mozilla/33.0" force-response-1.0
BrowserMatch "Mozilla/34.0" force-response-1.0
BrowserMatch "Mozilla/35.0" force-response-1.0
</IfModule>
```

# Apache 4

## 第 3 章

### MaxRequestsPerChild 0

"`MaxRequestsPerChild`" 选项用于定义单个子服务器进程处理的请求数。在我们的配置中，我们将此指令的值设置为 "`0`"，以获得服务器的最优性能和可扩展性。这是关于 Apache Web 服务器性能的另一个重要调优参数。

```
Listen 1.2.3.4:80
Listen 1.2.3.4:443
```

"`Listen`" 指令用于通知 Web 服务器在指定的端口或地址-端口组合上接收传入的请求。在我们的示例中，我们定义了跨系统的 Web 服务器的 IP 地址和端口号。端口号 "`80`" 是 HTTP 请求的标准端口，而 "`443`" 是 HTTPS 请求的标准端口。通过这种方式，我们在配置文件中同时配置了端口和 IP 地址。

```
User www
```

"`User`" 指令用于定义 Apache 守护进程运行时的 UID。创建一个对系统访问权限最小、且专门用于运行 Web 服务器守护进程目的的新用户是非常重要的。使用系统中已存在的不同 UID（例如 `nobody`）可能会允许服务访问彼此的资源。在我们的示例中，我们使用了之前创建的名为 "`www`" 的 Apache 组。

```
Group www
```

"`Group`" 指令用于定义 Apache 守护进程运行时的 GID。创建一个对系统访问权限最小且用于运行 Web 服务器守护进程目的的新组是非常重要的。在我们的示例中，我们使用了之前创建的名为 "`www`" 的 Apache 组。

```
ServerAdmin root@localhost
```

"`ServerAdmin`" 指令用于定义服务器在返回给客户端的任何错误信息中包含的电子邮件地址。请将上述值更改为您的真实邮箱地址。

```
ServerName localhost
```

"`ServerName`" 指令用于定义服务器识别自身身份的主机名。如果您的服务器可以通过 `www.domain.com` 访问，此指令的值将是 `www.domain.com`。请将上述值更改为您真实的 FQDN（完全限定域名）。

```
DocumentRoot "/home/httpd/html"
<Directory />
  Options None
  AllowOverride None
  Order deny,allow
  Deny from all
</Directory>
```

此块指令通过阻止用户覆盖宽泛设置，允许极其严谨的运行。这是因为 Apache 对 `<Directory />` 的默认访问是 Allow from All，这意味着它将提供任何从 URL 映射的文件。因此，强烈建议您修改此块（如我们所配置的那样），然后对您想要允许访问的目录进行覆盖设置。这是一项安全功能。

```
<IfModule mod_dir.c>
DirectoryIndex index.htm index.html index.php index.php3
</IfModule>
```

"`DirectoryIndex`" 指令用于定义将 Apache 作为预写 HTML 目录索引的文件。换句话说，如果 Apache 找不到索引页目录，它将尝试特定的下一个条目。为了提高 Web 服务器的性能，建议使用您网站最常用的默认索引，不要包含过多的内容。这是一项性能功能。

### HostnameLookups Off

"`HostnameLookups`" 指令如果设置为 "`Off`"，则指定禁用 DNS 查询。建议将此选项设置为 "`Off`"，以避免每次请求的延迟、节省网络流量并提高您的 Apache Web 服务器的性能。这是一项性能功能。

### ServerTokens Prod

"`ServerTokens`" 指令用于控制发送给客户端的服务器响应头字段是否包含服务器通用操作系统类型的描述以及有关编译模块的信息。出于安全考虑，我建议限制 Web 服务器向外部发送的信息。通过将此指令的值设置为 "`Prod`"，可以实现这一点，这将仅显示服务器名称（Apache）。这有助于版本检测。这是一项安全功能。

> 注意：如果您的 `http.conf` 文件包含许多内容相同的 `<VirtualHost>` 部分，我建议您阅读 Apache 的“动态配置大量虚拟主机”，它描述了如何有效地提供任意数量的虚拟主机。这是一篇在线文档，可以在 Apache 网站获取：`http://apache.org/docs-2.0/vhosts/`

## /etc/logrotate.d/httpd Apache 日志轮文件

`/etc/logrotate.d/httpd` 文件允许 Web 服务器每周轮转所有 Apache 日志。

### 第一步

在这里配置 `/etc/logrotate.d/httpd` 每周轮转其日志。

- 创建 `httpd` 文件（`touch /etc/logrotate.d/httpd`）并添加以下行：

```apache
/var/log/httpd/access_log {
    missingok
    postrotate
    /usr/bin/killall -HUP httpd
endscript
}
/var/log/httpd/error_log {
    missingok
    postrotate
    /usr/bin/killall -HUP httpd
endscript
}
```

```
/var/log/httpd/access_log {
    missingok
    postrotate
    /usr/bin/killall -HUP httpd
endscript
}
```

> 注意：如果您的 `http.conf` 文件包含许多内容相同的 `<VirtualHost>` 部分，我建议您阅读 Apache 的“动态配置大量虚拟主机”，它描述了如何有效地提供任意数量的虚拟主机。这是一篇在线文档，可以在 Apache 网站获取：`http://apache.org/docs-2.0/vhosts/`

### 第二步

现在，我们需要为错误日志配置轮转。

- 创建 `httpd` 文件（`touch /etc/logrotate.d/httpd`）并添加以下行：

# Apache 4

## 第3 章

```
kill -USR1 `cat /var/run/httpd.pid'
RETVAL=$?
;
condrestart() {
nif [ -f /var/lock/subsys/httpd ]; then
  kill -USR1 `cat /var/run/httpd.pid'
  RETVAL=$?
fi
};
;
echo "Usage: $0 (start|stop|status|restart|condrestart)"
esac
exit 1

esac
exit $RETVAL
```

### 第 2

一旦创建了 `http` 脚本文件，将其设置为可执行、更改其默认权限、创建必要的链接并启动它就非常重要。将此文件设为可执行将允许系统运行它；更改其默认权限是为了安全考虑，只允许 root 用户进行更改；而创建符号链接将处理 Linux 的进程控制初始化，该初始化负责启动系统在开机时需要运行的所有网络授权进程，以便在每次重启时自动启动该程序。

- 要将其设置为可执行并更改其默认权限，请使用命令：

```
[root@]# chmod 700 /etc/init.d/httpd
```

```
[root@]# chown 0.0 /etc/init.d/httpd
```

- 要为 Apache 创建符号 `.rc` 链接，请使用以下命令：

```
[root@]# chkconfig --add httpd
```

```
[root@]# chconfig --level 345 httpd on
```

- 要手动启动 Apache 软件，请使用以下命令：

```
[root@]# /etc/init.d/httpd start
Starting Apache:
[OK]
```

# 带有 TLS/SSL 支持运行 Apache

本节仅适用于你想通过 SSL 连接运行 Apache 的情况。在 Apache 的新版本中，我们不需要使用任何如 `mod_ssl` 的外部程序即可使其支持 SSL 功能。

新版本的 Apache 软件自带了 SSL 模块，该模块随软件一起编译并安装。我们只需要像我们在配置 Web 服务器时所做的那样，启用 SSL 模块，并创建所需的证书使其正常工作。下面我将展示如何设置用于供 Apache 使用的证书。

## 第 1 步

首先，您需要知道要请求证书的 Apache Web 服务器的完全限定域名 (FQDN)。当您想通过 `www.domain.com` 访问 Web 服务器时，您的 Apache 服务器的 FQDN 就是 `www.domain.com`。

### 第 2 步

其次，从您的硬盘中选择五个大且相对随机的文件（压缩后的日志文件是一个很好的开始），并将它们放在 `/usr/share/ssl/` 目录下。这些文件将作为您的随机种子增强器。在下文中，我们将它们称为 `random1:random2....random:random5`。

- 要选择五个随机文件并将它们放在 `/usr/share/ssl` 下，请使用命令：

```
[root@deep]$ # cp /var/log/boot.log /usr/share/ssl/random1
```

```
[root@deep]$ # cp /var/log/cron /usr/share/ssl/random2
```

```
[root@deep]$ # cp /var/log/dmesg /usr/share/ssl/random3
```

```
[root@deep]$ # cp /var/log/messages /usr/share/ssl/random4
```

```
[root@deep]$ # cp /var/log/secure /usr/share/ssl/random5
```

### 第 3 步

第三，为 Apache 服务器创建一个受密码（pass-phrase）保护的 RSA 密钥。该命令将生成 1024 位的 RSA 私钥并将其存储在文件 `www.key` 中

- 要生成密钥，使用以下命令：

```
[root@deep]$ # cd /usr/share/ssl/
```

```
[root@deep]$ # openssl genrsa -rand random1:random2:random3:random4:random5 -out www.key 1024
```

```
123600 bytes loaded
Generating RSA private key, 1024 bit long modulus
+++++
e is 65537 (0x10001)
```

> WARNING：请备份您的 `www.key` 文件。良好的选择是将此信息备份到磁盘或其他可移动介质。

### 第 4 步

最后，使用服务器 RSA 私钥生成证书签名请求 (CSR)。该命令将提示您输入证书的 X.509 属性。请记住在提示输入“Common Name”（通用名称）时，给出名称 `www.domain.com`。不要输入您的个人姓名。我们正在为 Web 服务器请求证书，因此通用名称必须与您网站的 FDN 匹配。

- 要创建 CSR，使用以下命令：

```
[root@deep]$ # openssl req -new -key www.key -out www.csr
```

```
Using configuration from /usr/share/ssl/openssl.cnf
Enter PEM pass phrase:
```

您被要求输入将包含在证书请求中的信息。您要输入的内容被称为差异名称（Distinguished Name 或 DN）。有几个字段可以留空。某些字段将有一个默认值：

Country Name（两个字母代码） `[CA]`:

State or Province Name（州或省） `[Quebec]`:

Locality Name（例如，城市） `[Montreal]`:

Organization Name（例如，公司） `[OpenNA, Inc.]`:
