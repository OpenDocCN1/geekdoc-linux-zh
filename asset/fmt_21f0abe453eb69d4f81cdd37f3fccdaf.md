
要查看 MultiViews 是如何工作的，请删除你在上一节中创建的 `/var/www/index.html.var` 类型映射文件。现在访问 `http://localhost`。了正确的语言页面，但为什么呢？

当浏览器向 Apache 发送目录请求时，Apache 会在目录目录下查找名为 `index.html` 的文件。在示例中，Apache 没有找到该文件。如果启用了 MultiViews（默认即开启），Apache 会查找名为 `index.html.*` 的文件。

## 高级配置

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_987_0.png)

## /doc 索引

| 名称 | 最后修改时间 | 大小 | 描述 |
| --- | --- | --- | --- |
| 目录 | 18-Dec-2005 06:37 | | |
| index | 02-Sep-2007 15:23 | | |
| arc-support/ | 03-Sep-2007 06:18 | | |
| app/ | 02-Sep-2007 06:18 | | |
| aspid/ | 03-Sep-2007 09:14 | | |
| abstract | 02-Sep-2007 09:28 | | |
| Docs | | | |

**图 26-1** 服务器生成的目录列表

在示例中，它找到了 `index.html.en` 和 `index.html.fr`。Apache 实际上是动态创建了一个类型映射，将 `index.html.*` 文件映射到各种语言，并向你请求页面发送其最佳猜测。

MultiViews 提供了一种简单的方法来保存同一文件的多个版本，而无需创建类型映射。然而，如果你对发送的资源版本进行更精细的控制，类型映射是更好的解决方案。

## 服务器生成的目录列表（索引）

当客户端请求目录时，Apache 决定返回给客户端的内容。Apache 可以根据 `DirectoryIndex`（第 914 页）返回一个文件；如果没有文件匹配 `Directory` 且设置了 `Options Indexes`（第 928 页），则返回目录列表；如果没有文件匹配 `DirectoryIndex` 且未设置 `Options Indexes`，则返回错误信息。26-1 显示了将本地浏览器指向服务器系统上的 `http://localhost/doc/`（你必须包含尾斜杠）（假设使用默认配置）时产生的服务器生成目录列表。

## 虚拟主机

Apache 支持虚拟主机（virtual hosts），这意味着一个 Apache 实例可以响应指向多个 IP 地址或主机名的请求，就像它们是多个服务器一样。每个 IP 地址或主机名随后都可以提供不同的内容，并进行不同的配置。

## 设置虚拟主机

为了提高移植性并使软件升级更容易，Ubuntu 提供了两个包含支持虚拟主机代码目录。`apache2.conf` 文件包含一个 `Include` 指令（第 906 页），它包含了 `/etc/apache2/sites-enabled` 目录中的文件。

要创建一个新的虚拟主机，你可以在 `/etc/apache2/sites-available` 中创建一个定义虚拟主机的文件。然后运行 `a2ite`（第 906 页）并将创建的文件名作为参数。通过运行 `a2ensite` 可以通过在 `/etc/apache2/sites-enabled` 中创建链接来启用虚拟主机。

## 虚拟主机类型

虚拟主机有两种类型：主机名（host-name）和基于 IP（host-by-IP）。主机名依赖于请求中的 `Host` 头部，而基于 IP 的则检查 IP 地址。如果只有一个 IP 地址，主机名非常方便；如果你有多个 IP 地址，基于 IP 的则很有用。

## 默认虚拟主机

默认虚拟主机是 Apache 在请求不匹配任何其他虚拟主机时使用的。这通常是 `/etc/apache2/sites-enabled` 目录中定义的第一个虚拟主机。你可以通过创建一个新的虚拟主机并使其成为第一个来更改虚拟主机。

## 示例

以下示例展示了如何配置虚拟主机。

### 基于主机名的虚拟主机

下一个示例设置了两个虚拟主机。`VirtualHost` 容器通过 `ServerName` 接收指向服务器的所有流量。

```apache
<VirtualHost *>
  ServerName sam.example.com
  ServerAlias www.example.com
  ServerAdmin webmaster@example.com
  DocumentRoot /var/www
</VirtualHost>
```

```apache
<VirtualHost *>
  ServerName mail.example.com
  ServerAdmin webmaster@example.com
  DocumentRoot /var/www/webmail
</VirtualHost>
```

### 基于 IP 的虚拟主机

下一个示例展示了如何根据 IP 地址配置虚拟主机。

```apache
<VirtualHost 192.168.1.100:80>
  ServerName sam.example.com
  ServerAlias www.example.com
  ServerAdmin webmaster@example.com
  DocumentRoot /var/www
</VirtualHost>
```

```apache
<VirtualHost 192.168.1.101:80>
  ServerName mail.example.com
  ServerAdmin webmaster@example.com
  DocumentRoot /var/www/webmail
</VirtualHost>
```

```apache
<VirtualHost 111.111.0:80>
  DocumentRoot /var/www/www0
</VirtualHost>
```

```apache
<VirtualHost 111.111.0:1:80>
  DocumentRoot /var/www/www1
</VirtualHost>
```

```apache
<VirtualHost 111.111.0:8080>
  DocumentRoot /var/www/www2
  Listen 8080
  # this directive should go in ports.conf
</VirtualHost>
```

最后一个示例设置了一个只能通过 SSL 访问的 Webmail 虚拟服务器。将此示例代码放在名为 `/etc/apache2/sites-available/mail.example.com` 的文件中是合适的。要使用此示例，你必须创建一个 SSL 证书（第 943 页），使用 `a2enmod`（第 905 页）启用 ssl 模块（在默认 Apache 安装中包含），并使用 `a2ensite`（第 906 页）启用虚拟域名。

```apache
<VirtualHost mail.example.com:80>
  Redirect permanent https://mail.example.com/
</VirtualHost>

<VirtualHost mail.example.com:443>
  ServerName mail.example.com
  ServerAdmin postmaster@example.com
  DocumentRoot /var/www/mail.example.com
  ErrorLog /var/log/apache2/mail.example.com.err
  CustomLog /var/log/apache2/mail.example.com.log combined
  SSLEngine On
  SSLCertificateFile /etc/apache2/ssl/apache.pem
</VirtualHost>
```

## 故障排除

`apache2` 初始化脚本会检查 Apache 配置文件的语法，如果出现问题则会记录错误。你也可以直接调用 `apache2ctl` 来检查语法：

- `$ apache2ctl configtest`
  Syntax OK

一旦启动了 `apache2` 守护进程，你可以通过在本地系统上浏览器访问 `http://localhost/` 来确认 Apache 运行正常。从远程系统访问，使用 `http://server/`，并将 `server` 替换为服务器的主机。作为响应，除非添加了索引文件或更改了默认虚拟主机，否则 Apache 将显示 `/var/www` 的目录列表。

如果浏览器没有显示目录列表，将显示两种错误之一：连接被拒绝（Connection refused）或错误页面。如果你收到 Connection refused 错误，请确保 80 端口未被防火墙拦截（第 901 页），并检查服务器正在运行：

```
$ ps -ef | grep apache2
max 34789 0 16:55 pts/1 00:00:00 grep apache2
root 5031 1 0 Mar 26 00:00:00 /usr/sbin/apache2 -k start
www-data 5032 5031 0 Mar 26 ? 00:00:00 /usr/sbin/apache2 -k start
www-data 5088 5031 0 Mar 26 ? 00:00:00 /usr/sbin/apache2 -k start
www-data 5092 5031 0 Mar 26 ? 00:00:00 /usr/sbin/apache2 -k start
```

如果服务器正在运行，请确认你没有在 `Listen` 指令中指定 80 以外的端口。如果你指定了，在浏览器中指定的 URI 必须反映该端口（`http://localhost:port`）。否则，请检查错误日志（`/var/log/httpd/error_log`）获取关于无法工作的信息。

要验证浏览器不是故障所在，请使用 telnet 连接到服务器的 80 端口：

```
$ telnet www.example.com 80
Trying 192.0.2.146...
Connected to www.example.com.
Escape character is '^'.
CONTROL-
telnet> quit
Connection closed.
```

如果 telnet 显示 Connection refused，意味着本地系统无法连接到服务器。

## 模块

Apache 是一个骨架程序，依赖于外部模块（称为动态共享对象，DSOs）来提供大部分功能。除了 Ubuntu Linux 自带的模块外，还有许多其他模块可用。更多信息请参见 `httpd.apache.org/modules`。启用模块请参见第 905 页的 `a2mod`。

## 配置模块

tip 你可以通过编辑 `mods-available` 目录中对应的 `.conf` 文件来配置某些模块。

模块文件名以 `libapache2-mod-` 前缀开头。以下命令显示模块的完整列表。你可以通过 `grep` 过滤列表以查找所需的模块。`apt-cache` 的信息请参见第 530 页。

```
$ apt-cache search apache2-mod
libapache2-mod-auth-krb - 用于 Kerberos 认证的 apache 模块
libapache2-mod-auth-mysql - 用于 MySQL 认证的 Apache 2 模块
libapache2-mod-auth-pam - 使用 PAM 认证的 Apache2 模块
libapache2-mod-pgsql - 提供 pgsql 认证的 Apache2 模块
libapache2-mod-auth-plain - 提供明文认证的 Apache2 模块
libapache2-mod-group - 检查系统组用户的 Apache2 模块
```

## 944 第 26 章 APACHE：设置 Web 服务器

```
$ sudo apache2-ssl-certificate
正在创建自签名证书 (CA)
请用由认证机构签名的证书替换它
```

在 Common Name（通用名称）提示符处输入你的 `ServerName`（服务器名称）

如果你想让你的证书在 x 天后过期，请使用 `-days x` 调用此程序
正在生成 1024 位 RSA 私钥 ........

```
正在将新私钥写入 '/etc/apache2/ssl/apache.pem'
```

你将会被要求提供一些信息，这些信息将会被整合到你的证书请求中。
你即将输入的内容被称为“别名”（Distinguished Name，简称 DN）。
有几个字段你可以留空。
某些字段会有默认值，
如果你输入 `.`，该字段将留空。

- 国家名称（两位字母代码）[GB]:US
- 州或省份名称（全称）[Some-State]:California
- 地区名称（例如，城市）：:San Francisco
- 组织名称（例如，公司；推荐）：:Sobell Associates Inc.
- 组织单元（例如，部门）：[]
- 服务器名称（例如，ssl.domain.tld；强制！）：:www.sobell.com
- 电子邮件地址：:mg@sobell.com

前五个问题的答案是随意的：它们可以在检查证书时帮助识别一个实体。第六个问题（服务器名称）的答案至关重要。因为证书与服务器名称绑定，所以你必须准确地输入服务器的完全限定域名（FQDN）。如果你输错了这些信息，服务器名称和证书名称将不匹配。此时浏览器在每次连接时都会生成一条警告消息。

现在，你必须在 `/etc/apache2/sites-available` 中创建一个启用 SSL 的虚拟主机。基于名称的虚拟主机（Host-by-name virtual hosting）无法配合 SSL，因为 Apache 用于区分不同基于名称虚拟主机的客户端 HTTP Host 头部是被加密的。你只能使用一个 SSL 证书，每个 IP 地址匹配一个域名。虽然你在该 IP 地址上有多个虚拟主机，但如果通过 HTTPS 访问它们，客户端将收到一个显示证书与域名不匹配的错误。在你启用新的虚拟主机并重启 Apache 后，新的证书将被使用。

以下是 `/etc/apache2/sites-available/ssl` 的一个通配符设置示例。使用 `sudo a22ensite ssl` 启用它：

```apache
<VirtualHost *:80>
  Redirect permanent / https://www.sobell.com/
</VirtualHost>
```

```apache
<VirtualHost *:443>
ServerName www.sobell.com
SSLEngine On
SSLCertificateFile /etc/apache2/ssl/apache.pem
DocumentRoot /var/www
</VirtualHost>
```

此示例将所有非 SSL 流量重定向到 SSL 站点。如果你让 Apache 监听默认的 HTTPS 端口，必须在 `/etc/apache2/ports.conf` 中添加 `Listen 443` 指令。

## 证书的注意事项

- 尽管服务器名称是证书的一部分，但 SSL 连接绑定到服务器的 IP 地址：每个 IP 地址只能有一个证书。为了让多个虚拟主机拥有独立的证书，你必须指定基于 IP 的虚拟主机而不是基于名称的虚拟主机（第 937 页）。
- 只要服务器是通过颁发证书的名称来识别的，你就可以另一台服务器或 IP 地址上使用该证书。
- 根证书是标识根证书权威机构（root CA）的证书。每个浏览器都包含一个主要签名机构的公钥数据库，包括 Verisign 和 Thawte。
- 可以生成根证书并签名你所有的证书。普通客户端可以导入根 CA 的公钥，以便它们识别由该根 CA 签名的每一个证书。这种设置对于具有多个 SSL 虚拟主机且没有商业证书的服务器非常方便。更多信息见 `www.modssl.org/docs/2.8/ssl_faq.html#ToC29`。
- 自签名证书无法让客户端验证服务器的身份。

## 认证模块与 .htaccess

为了访问 Web 页面，Apache 和第三方提供了认证模块和方法来验证用户的凭据（如用户名和密码）。某些模块支持针对各种数据库进行认证，包括 LDAP（第 1156 页）和 NIS（第 741 页）。

用户认证指令通常放置在 `.htaccess` 文件中。以下是一个使用 Apache 默认认证模块（mod_auth）的 `.htaccess` 文件。请为本地服务器替换适当的值。

```
$ sudo cat .htaccess
AuthUserFile /var/www/.htpasswd
AuthGroupFile /dev/null
AuthName "Browser dialog box query"
AuthType Basic
require valid-user
```

`/var/www/.htpasswd` 是 `.htpasswd` 文件的典型绝对路径，而 `Browser dialog query` 是用户在请求用户名和密码的对话框中看到的字符串。

前述 `.htaccess` 文件的第二行关闭了组功能。第四行指定了用户认证类型为 `Basic`，它由默认的 `mod_auth` 模块实现。最后一行告诉 Apache 用户可以访问受保护的目录。`valid-user` 条目允许任何出现在 Apache 密码文件中且输入正确密码的用户访问该目录。

你可以将 Apache 密码文件放在系统的任何位置，因为将其放在与 `.htaccess` 文件相同的目录中是安全的，因为通过...
