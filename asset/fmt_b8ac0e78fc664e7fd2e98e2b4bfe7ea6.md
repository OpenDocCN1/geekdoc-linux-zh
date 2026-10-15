
虚拟主机从`httpd.conf`的第 1 节（第 871 页）和第 2 节（第 872 页）继承其配置。在第 3 节中，`<VirtualHost>`容器创建虚拟主机，并指定覆盖继承值和默认值的指令。你可以为单个 Apache 实例指定许多虚拟主机。

下面的`<VirtualHost>`容器为名为 intranet.example.com 的网站设置了一个基于名称的主机。此虚拟主机处理指向 intranet.example.com 的请求。

```
<VirtualHost intranet.example.com>
  ServerName intranet.example.com
  DocumentRoot /usr/local/www
  ErrorLog /var/log/httpd/intra.error_log
  CustomLog /var/log/httpd/intra.server_log
  <Directory /usr/local/www>
    Order deny,allow
    Deny from all
    Allow from 192.168.   # allow from private subnet only
  </Directory>
</VirtualHost>
```

# 故障排除

你可以使用`service`和`httpd`初始化脚本来检查 Apache 配置文件的语法：

```
# service httpd configtest
Syntax OK
```

一旦你启动了`httpd`守护进程，你就可以通过让本地系统上的浏览器指向`http://localhost/`来确认 Apache 是否正常工作。从远程系统，使用`http://server/`，将服务器的主机名替换为`server`。作为响应，Apache 显示 Fedora/RHEL 测试页面。

如果浏览器没有显示测试页面，它将显示两个错误之一：**连接被拒绝**或错误页面。如果你得到**连接被拒绝**错误，请确保端口 80 没有被防火墙阻止（第 844 页），并检查服务器是否在运行：

```
# /sbin/service httpd status
httpd (pid 21406 21405 21404 21403 21402 21401 13622) is running...
```

如果服务器在运行，请检查你是否在`Listen`指令中指定了 80 以外的端口。如果是这样，你在浏览器中指定的 URI 必须反映此端口号（`http://localhost:port`指定端口`port`）。否则，检查错误日志（`/var/log/httpd/error_log`）以获取有关什么没有正常工作的信息。

为了验证浏览器是否没有问题，使用`telnet`尝试连接到服务器的端口 80：

```
$ telnet www.example.com 80
Trying 192.0.34.166...
Connected to www.example.com.
Escape character is '^'.
^J
telnet> quit
Connection closed.
```

如果显示**连接被拒绝**，你已经验证了无法连接到服务器。

# 模块

Apache 是一个框架程序，依靠称为动态共享对象（DSO）的外部模块来提供其大部分功能。本节列出了这些模块并讨论了一些更重要的模块。除了随 Fedora/RHEL 包含的模块外，还有许多其他模块可用。有关更多信息，请参阅 httpd.apache.org/modules。

# 模块列表

以下是 Apache 下可用的一些模块列表：

- `access`（`mod_access.so`）根据客户端特征控制访问。
- `actions`（`mod_actions.so`）允许根据请求方法执行 CGI 脚本。
- `alias`（`mod_alias.so`）允许将外部目录映射到 DocumentRoot。
- `asis`（`mod_asis.so`）允许发送包含自己头的文件。
- `auth`（`mod_auth.so`）通过`htaccess`提供用户身份验证。
- `auth_anon`（`mod_auth_anon.so`）提供匿名用户对受限区域的访问。
- `auth_dbm`（`mod_auth_dbm.so`）使用 DBM 文件进行身份验证。
- `auth_digest`（`mod_auth_digest.so`）使用 MD5 摘要进行身份验证。
- `autoindex`（`mod_autoindex.so`）允许生成目录索引。
- `cern_meta`（`mod_cern_meta.so`）允许使用 CERN`httpd`元文件语义。
- `cgi`（`mod_cgi.so`）允许执行 CGI 脚本。
- `dav`（`mod_dav.so`）允许分布式创作和版本管理。
- `dav_fs`（`mod_dav_fs.so`）为 mod_dav 提供文件系统。
- `dir`（`mod_dir.so`）允许目录重定向和作为索引文件的列表。
- `env`（`mod_env.so`）允许 CGI 脚本访问环境变量。
- `expires`（`mod_expires.so`）允许生成 Expires HTTP 头。
- `headers`（`mod_headers.so`）允许自定义请求和响应头。
- `imap`（`mod_imap.so`）允许在服务器端处理图像映射。
- `include`（`mod_include.so`）提供服务器端包含（SSI）。
- `info`（`mod_info.so`）允许查看服务器配置。
- `log_config`（`mod_log_config.so`）允许记录发送到服务器的请求。
- `mime`（`mod_mime.so`）允许将文件扩展名与内容关联。
- `mime_magic`（`mod_mime_magic.so`）确定文件的 MIME 类型。
- `negotiation`（`mod_negotiation.so`）允许内容协商。
- `proxy`（`mod_proxy.so`）允许 Apache 充当代理服务器。
- `proxy_connect`（`mod_proxy_connect.so`）允许处理连接请求。
- `proxy_ftp`（`mod_proxy_ftp.so`）提供 FTP 扩展代理。
- `proxy_http`（`mod_proxy_http.so`）提供 HTTP 扩展代理。
- `rewrite`（`mod_rewrite.so`）允许根据规则进行即时 URI 重写。
- `setenvif`（`mod_setenvif.so`）根据请求设置环境变量。
- `speling`（`mod_speling.so`）如果请求的 URI 大写不正确且有一个拼写错误，自动纠正拼写。
- `status`（`mod_status.so`）允许查询和查看服务器状态。
- `unique_id`（`mod_unique_id.so`）为每个请求生成唯一 ID。
- `userdir`（`mod_userdir.so`）允许用户拥有内容目录（public_html）。
- `usertrack`（`mod_usertrack.so`）允许跟踪用户在网站上的活动。
- `vhost_alias`（`mod_vhost_alias.so`）允许配置虚拟托管。

# mod_cgi 和 CGI 脚本

CGI（通用网关接口）允许外部应用程序与 Web 服务器接口。如果程序在实时运行（在请求时）并将其输出中继到请求客户端，那么任何程序都可以是 CGI 程序。各种类型的脚本，包括 shell、Perl、Python 和 PHP，是最常见的 CGI 程序，因为脚本可以调用程序并将输出重新格式化为 HTML 供客户端使用。

Apache 可以用几种不同的方式处理对 CGI 程序的请求。最常见的方法是将 CGI 程序放入`cgi-bin`目录，然后仅启用从该目录执行。如`ScriptAlias`指令（第 868 页）所指定的`cgi-bin`目录的位置是`/var/www/cgi-bin`。或者，`AddHandler`指令（第 862 页）可以识别常规内容中脚本的文件名扩展名，例如 .cgi 或 .pl（例如，`AddHandler cgi-script .cgi`）。如果使用`AddHandler`，你还必须在适当的`<Directory>`容器中的`Options`指令中指定`ExecCGI`选项。必须加载`mod_cgi`模块才能访问和执行 CGI 脚本。

以下 Perl CGI 脚本显示 Apache 环境。如果外部客户端可以访问该脚本，它会带来安全风险，因此该脚本应仅用于调试：
