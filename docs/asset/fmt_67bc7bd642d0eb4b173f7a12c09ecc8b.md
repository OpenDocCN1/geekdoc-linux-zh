
你的 Apache Web 服务器的 SSL 版本在 `httpd.conf` 中被设置为虚拟主机。SSL 指令通过使用 `HAVE_SSL` 标志的 `IfDefine` 块启用。几个默认指令被实现 SSL 密钥目录的位置，以及虚拟服务器 SSL 版本将监听的端口 `443`。其他的被注释掉了。你可以通过删除 `#` 符号并设置你自己的选项来启用它们。显示了几个指令：

```apache
<IfDefine HAVE_SSL>

## SSL 虚拟主机

# Apache 默认只监听 80 端口。定义的
virtual server
#（下文）不会让它自动监听虚拟服务器的端口。
Listen 443

<VirtualHost _default_:443>

# 虚拟主机的通用设置
DocumentRoot "/var/www/html"

# SSL 引擎切换:
# 为此虚拟主机启用/禁用 SSL。
SSLEngine on

#SSLCipherSuite
ALL:ADH!RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL

# 服务器证书:
SSLCificateFile /etc/httpd/conf/ssl.crt/server.crt
#SSLCificateFile /etc/httpd/conf/ssl.crt/server-dsa.crt

# 服务器私钥:
SSLCificateKeyFile /etc/httpd/conf/ssl.key/server.key

# 证书权威机构 (CA):
#SSLCertificatePath /etc/httpd/conf/ssl.crt
#SSLCertificateFile /etc/httpd/conf/ssl.crt/ca-bundle.crt
```

美国政府对超过 40 位的 SSL 加密技术实施出口限制，但支持许多使用 168 位、128 位和 40 位密钥的密码算法（128 位被认为是安全的，与此相比，可出口的 40 位版本是无用的）。这意味着如果 Apache 包含了 SSL，它将无法在美国境外进行分发。然而，在美国境外，有项目使用 OpenSSL 为 Apache 分发 SSL。这些项目在美国境的非商业用途是免费的，但受出口限制的影响。Apache-SSL 项目免费分发内置 SSL 的 Apache，即 `apache ssl`。你可以从 `http://www.apache.org` 下载它（尽管对出口加密技术有限制，但不需要进口）。`modSSL` 项目提供了一个 SSL 模块，你可以在你的 Apache Web 服务器上使用它整合 SSL（`www.modssl.org`），`mod_ssl` 在 Apache 风格许可下对商业和非商业用途均免费的。

Red Hat 在 `mod_ssl` 软件包中包含了 `mod_ssl` 模块分发。

```bash
rpm -i mod_ssl-2.8.1-5.1386.rpm
```

`mod_ssl` 的 SSL 实现为你的 Web 服务器提供了使用不同端口 `443` 和不同协议 `https` 的替代方案。实际上，你同时拥有一个 SSL 服务器和一个非安全服务器。要访问 SSL 版本，你需要在 Web 服务器的 URL 地址中使用该协议而不是 `http`。例如，要访问运行在 `mytrek.com` 上的 Web 服务器的 SSL 版本，你将在其 URL 中使用 `https` 协议，所示：

`https://www.mytrek.com`

你可以使用 Apache 配置文件 `httpd.conf` 中的多个指令来配置 `mod_ssl`。在 Red Hat 上，随 Apache 安装的默认配置文件包含一个用于 SSL 指令的章节，并带有详细的注释。请查看 `www.modssl.org` 上的 `mod_ssl` 文档以获取列出所有指令的详细参考列表。有全局、基于服务器和基于目录的指令可用。

在 Red Hat 组合中，SSL 指令的包含由 `HAVE_SSL` 标志启用的 `IfDefine` 块控制。例如，以下代码将加载：

```apache
<IfDefine HAVE_SSL>
LoadModule ssl_module modules/libssl.so
</IfDefine>
```

你的 Apache Web 服务器的 SSL 版本在 `httpd.conf` 中被设置为虚拟主机。SSL 指令通过使用 `HAVE_SSL` 标志的 `IfDefine` 块启用。几个默认指令被实现 SSL 密钥目录的位置，以及虚拟服务器 SSL 版本将监听的端口 `443`。其他的被注释掉了。你可以通过删除 `#` 符号并设置你自己的选项来启用它们。显示了几个指令：

```apache
<IfDefine HAVE_SSL>

## SSL 虚拟主机

# Apache 默认只监听 80 端口。定义的
virtual server
#（下文）不会让它自动监听虚拟服务器的端口。
Listen 443

<VirtualHost _default_:443>

# 虚拟主机的通用设置
DocumentRoot "/var/www/html"

# SSL 引擎切换:
# 为此虚拟主机启用/禁用 SSL。
SSLEngine on

#SSLCipherSuite
ALL:ADH!RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL

# 服务器证书:
SSLCificateFile /etc/httpd/conf/ssl.crt/server.crt
#SSLCificateFile /etc/httpd/conf/ssl.crt/server-dsa.crt

# 服务器私钥:
SSLCificateKeyFile /etc/httpd/conf/ssl.key/server.key

# 证书权威机构 (CA):
#SSLCertificatePath /etc/httpd/conf/ssl.crt
#SSLCertificateFile /etc/httpd/conf/ssl.crt/ca-bundle.crt
```
