
（第 944 页），如果没有任何文件匹配 `DirectoryIndex` 且设置了 `Options Indexes` 指令（第 957 页），则显示目录列表；如果没有任何文件匹配 `DirectoryIndex` 且未设置 `Options Indexes`，则显示错误消息。图 26-1 展示了一个由服务器生成的目录列表。

## 虚拟主机

Apache 支持虚拟主机，这意味着 Apache 的单个实例可以像多个服务器一样，响应发往多个 IP 地址或主机名的请求。然后，每个 IP 地址或主机名都可以提供不同的内容并具有不同的配置。

虚拟主机有两种类型：按名称主机（也称为基于主机名的虚拟主机）和按 IP 地址主机（host-by-IP）。按名称主机依赖客户端在请求 Apache 时使用的完全限定域名（FQDN）——例如，`www.example.com` 与 `www2.example.com`。按 IP 地址主机会检查主机解析出的 IP 地址，并根据该匹配结果进行响应。

如果只有一个 IP 地址但 Apache 必须支持多个 FQDN，按名称主机会很方便。虽然如果某个 Web 服务器有别名，你可以使用按 IP 地址主机，但无论使用哪个名称，Apache 都应该提供相同的内容。

`NameVirtualHost` 指令指定哪个 IP 地址支持基于主机名的虚拟托管；`ServerName`（或 `ServerAlias`）指令必须匹配客户端请求才能匹配该虚拟主机。如果没有 `NameVirtualHost` 指令，虚拟主机就是一个基于 IP 地址的虚拟主机；`ServerName` 指令指定服务器用于识别自身的主机名。

你可以为单个 Apache 实例指定许多虚拟主机。

## 示例

以下基于主机名的虚拟托管示例使用通配符 (*) 以保持尽可能大的灵活性。当 Apache 服务多个虚拟主机时，你可能希望用服务器的 IP 地址替换通配符，以获得更精确的控制。第一个 `<VirtualHost>` 容器为名为 example.com 的网站设置基于主机名的虚拟托管。此虚拟主机处理定向到 example.com 的请求。`ServerAlias` 指令允许它也处理定向到 www.example.com 的请求。

```apache
<VirtualHost *>
ServerName example.com
ServerAlias www.example.com
ServerAdmin webmaster@example.com
DocumentRoot /var/www/html/example.com
CustomLog /var/log/httpd/example.com.log combined
ErrorLog /var/log/httpd/example.com.err
</VirtualHost>
```

下一个示例与上一个类似。它添加了一个 Directory 指令，阻止远程用户（不来自 192.168. 子网的用户）访问该网站。

```apache
<VirtualHost >
   ServerName        intranet.example.com
   ServerAdmin       webmaster@example.com
   DocumentRoot      /var/www/html
   ErrorLog          /var/log/httpd/intra.error_log
   CustomLog         /var/log/httpd/example.com.log combined
   <Directory /var/www/html>
      Order deny,allow
      Deny from all
      Allow from 192.168.  # allow from private subnet only
   </Directory>
</VirtualHost>
```

下一个示例设置了两个虚拟主机。VirtualHost 容器通过指定 * 接受所有定向到该服务器的流量。ServerName 指令接受针对 sam.example.com（或别名 www.example.com/sam）和 mail.example.com 的流量。第一个虚拟主机从 Sam 的 public_html 目录提供文档；第二个是一个 Webmail 服务器，其内容位于 /var/www/html/squirmail。此示例有效，因为所有三个地址都解析到该服务器的 IP 地址。

```apache
NameVirtualHost *:80
<VirtualHost >
   ServerName        sam.example.com
   ServerAlias       www.example.com/sam
   ServerAdmin       webmaster@example.com
   DocumentRoot      /home/sam/public_html
</VirtualHost>

<VirtualHost >:
   ServerName        mail.example.com
   ServerAdmin       webmaster2@example.com
   DocumentRoot      /var/www/html/squirmail
</VirtualHost>
```

如果用户指定 IP 地址而不是 URL，该地址可能匹配多个虚拟主机，如示例所示。在这种情况下，Apache 将提供最佳匹配的虚拟主机。如果没有任何虚拟主机地址比其他虚拟主机更好地匹配该 IP 地址，Apache 将提供第一个虚拟主机。在上面的示例中，两个虚拟主机以相同的方式匹配 IP 地址；没有一个是更好的匹配，因此 Apache 提供第一个虚拟主机（sam.example.com）。如果 mail.example.com 被定义为 `<VirtualHost 192.168.1.102>` 且用户指定了该 IP 地址，Apache 将提供 mail.example.com，因为与其他虚拟主机指定的通配符相比，它是该 IP 地址更好的匹配。

下一个示例展示了基于 IP 地址服务器的 VirtualHost 容器。该示例假设 11.111.0.0 和 111.11.0.1 指向本地服务器。这里每个虚拟主机都有自己的 IP/端口组合。第三个虚拟主机通过请求进来的端口与第一个虚拟主机区分开来。

```apache
<VirtualHost 111.111.0.0:80>
   DocumentRoot /var/www/html/ww0
</VirtualHost>
```

```apache
<VirtualHost 111.111.0.1:80>
  DocumentRoot /var/www/html/www1
</VirtualHost>
<VirtualHost 111.111.0.0:8080>
  DocumentRoot /var/www/html/www2
  Listen 8080
</VirtualHost>
```

最后一个示例设置了一个仅能通过 SSL 访问的 Webmail 虚拟服务器。要使用此示例，你必须创建 SSL 证书（第 970 页）。

```apache
<VirtualHost mail.example.com:80>
  Redirect permanent / https://mail.example.com/
</VirtualHost>
<VirtualHost mail.example.com:443>
  ServerName mail.example.com
  ServerAdmin postmaster@example.com
  DocumentRoot /var/www/html/mail.example.com
  ErrorLog /var/log/httpd/mail.example.com.err
  CustomLog /var/log/httpd/mail.example.com.log combined
  SSLEngine On
  SSLCertificateFile /etc/pki/tls/certs/apache.pem
</VirtualHost>
```

## 故障排除

如果浏览器未显示你预期的信息，请确保它没有显示该页面的缓存版本。尝试清除浏览器缓存并重载页面。同时，请确保 Apache 具有读取其服务的文件和正在运行的脚本的权限。

httpd 服务检查 Apache 配置文件的语法，如果存在问题则记录错误日志。你也可以直接调用 apachectl 来检查语法：

```bash
$ apachectl configtest
Syntax OK
```

一旦启动 httpd 守护进程，你可以通过在本地系统上的浏览器中指向 http://localhost/ 来确认 Apache 是否正常工作。从远程系统，使用 http://server/，将服务器的主机名或 IP 地址替换 server。作为响应，除非你添加了索引文件或更改了默认虚拟主机，否则 Apache 将显示 Fedora/RHEL 测试页面（第 937 页）。

如果浏览器未显示测试页面，它将显示两个错误之一：连接被拒绝或错误页面。如果它显示连接被拒绝，请确保端口 80 没有被防火墙（第 934 页）阻止，检查 SELinux（第 934 页）是否设置正确，并检查服务器是否正在运行：

```bash
# systemctl status httpd.service
httpd.service - The Apache HTTP Server
  Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled)
  Active: active (running) since ...
```

如果服务器正在运行，请确认你在 Listen 指令中没有指定 80 以外的端口。如果你确实指定了其他端口，你在浏览器中指定的 URI 必须反映此端口号（http://localhost:port 指定端口 port）。否则，请检查错误日志（/var/log/httpd/error_log）以获取有关什么不起作用的信息。

要验证浏览器是否有故障，请使用 telnet 连接到服务器的 80 端口：

```bash
$ telnet www.example.com 80
Trying 192.0.34.166...
Connected to www.example.com.
Escape character is `^\`.
CONTROL+
telnet> quit
Connection closed.
```

如果 telnet 显示连接被拒绝，这意味着本地系统无法连接到服务器。

## 模块

Apache 是一个骨架程序，它依靠外部模块，称为 DSO（动态共享对象），来提供其主要功能。除了 Fedora/RHEL 包含的模块外，还有许多其他可用模块。更多信息请参见 httpd.apache.org/modules 和 httpd.apache.org/docs/2.4/mod。

以下是 Apache 下可用的一些模块列表。

- **actions** (mod_actions.so) 允许根据请求方法执行 CGI 脚本。
- **alias** (mod_alias.so) 允许将外部目录映射到 DocumentRoot。
- **asis** (mod_asis.so) 允许发送包含自身头信息的文件。
- **auth_basic** (mod_auth_basic.so) 通过 .htaccess 提供用户身份验证。
- **auth_digest** (mod_auth_digest.so) 使用 MD5 摘要进行身份验证。
- **auth_anon** (mod_auth_anon.so) 提供对受限区域的匿名用户访问。
- **auth_dbd** (mod_authn_dbd.so) 使用 SQL 文件进行身份验证。
- **autoindex** (mod_autoindex.so) 允许生成目录索引。
- **cgi** (mod_cgi.so) 允许执行 CGI 脚本。
- **dav** (mod_dav.so) 允许分布式创作和版本管理。
- **dav_fs** (mod_dav_fs.so) 为 mod_dav 提供文件系统。
- **dir** (mod_dir.so) 允许将目录索引和列表作为索引文件。
- **env** (mod_env.so) 允许 CGI 脚本访问环境变量。
- **expires** (mod_expires.so) 允许生成 Expires HTTP 头。
- **headers** (mod_headers.so) 允许自定义请求和响应头。
- **include** (mod_include.so) 提供服务器端包含 (SSI)。
- **info** (mod_info.so) 允许查看服务器配置。
- **log_config** (mod_log_config.so) 允许记录发送到服务器的请求。
- **mime** (mod_mime.so) 允许将文件扩展名与内容类型关联。
- **mime_magic** (mod_mime_magic.so) 确定文件的 MIME 类型。
