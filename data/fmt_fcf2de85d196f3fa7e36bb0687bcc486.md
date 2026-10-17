
`AddType text/html .shtml` 行将 `.shtml` 路径添加到 `text/html` MIME 类型中。`AddOutputfilter INCLUDES .shtml` 指令告诉 Apache 以 `.shtml` 扩展的文件应使用 `mod_include` 进行处理，该模块提供了 Apache 的 SSI 支持。配置文件的参数用于告诉 Apache 哪些目录的内容需要针对 SSI 指令进行解析。

例如，你创建了一个目录 `/var/www/html/tests`，并想要为该目录启用 SSI。在路径 `/etc/httpd/conf.d` 目录下添加一个名为 `tests.conf` 的文件，其中包含上述 `<Directory>` 块。将 `<Directory>` 块中的路径替换为 `'/var/www/html/tests'`。`Includes` 指令指示 Apache 解析其为该目录提供的文件中的 SSI 指令。现在创建一个 Web 页面 `itself.shtml` 并将其放在 `/var/www/html/tests` 中，如下：

```html
<html>
<head>
<title>SSI Test Page</title>
</head>
<body>
<h1>SSI Test Page</h1>
<div id="div1">
<!-- exec cmd="ls -lh /var/www" -->
</div>
<div id="div2">
<!-- content -->
<!--#include virtual="footer.html" -->
</div>
</body>
</html>
```

SSI 指令采用以下格式：

```html
<!--#element attribute=value -->
```

SSI 指令看起来像 HTML 注释。如果在服务器上配置不当，浏览器将忽略其内容。在上面的 `itself.shtml` 中，第一条 `<!-- exec cmd="ls -lh /var/www" -- >` 语句使用内置的 `exec` 命令来执行 `'ls -lh /var/www'` 命令。
以下内容的输出所示：

```
# ls -lh /var/www
total 24k
drwxr-xr-x. 2 root 4.0K 2010-04-06 18:31 cgi-bin
drwxr-xr-x. 2 root 4.0K 2012-06-05 05:56 error
drwxr-xr-x. 2 root 4.0K 2010-04-06 18:31 html
drwxr-xr-x. 3 root 4.0K 2012-06-05 05:56 icons
drwxr-xr-x. 14 root 4.0K 2012-06-05 05:59 manual
```

# 第 5 章

第二个 `<#include virtual="footer.html">` -> SSI 指令包含了一个标准的页脚文件。为了确认 SSI 已正确配置并正常工作，请在 浏览器中运行测试页面（`ssitest.html`）。你可以看到所需的测试页面运行正常并展示了你的 SSI 配置，如图 1 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_137_0.png)

让我们学习启用 CGI。

### 启用 CGI

通用网关接口（CGI）是一种提供标准方法的协议，允许 Web 服务器与外部程序进行通信。这些通常被称为 CGIs、CGI 脚本或 CGI 程序。有许多编程和脚本语言可以提供 CGI 实现。在 Linux 中，使用 Perl、Python、Ruby 和 Bash 来创建 CGIs。CGI 脚本用于动态创建或更新 页面。CGI 比 SSI 灵活得多，因为它提供了额外的功能。

在学习 Apache 配置和启用 CGI 的步骤之前，请执行以下任务以确保 Apache 的配置允许 CGI 脚本执行。在 `httpd.conf` 中找到 `ScriptAlias` 指令。该指令将目录名称与文件系统路径相关联，意味着 Apache 会将该目录中的每个文件都视为脚本。如果没有，请添加以下指令：

```apache
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
```

此指令告诉 Apache 任何调用 `/cgi-bin/` 的 URL 都应该从 `/var/www/cgi-bin` 提供。例如，在 `/var/www/cgi-bin` 目录下创建一个 CGI 测试脚本 `cgiscript.pl`。你可以使用以下内容来测试 CGI 的配置。

```perl
#!/usr/bin/perl
print 'Content-type: text/html\n\n';
print '<<html>';
print '<head>';
print '<title>CGI Test Page</title>';
print '</head>';
print '<body>';
print '<h1>CGI Test Page</h1>';
print '<div id="div1">';
print `ls -lh /var/www`;
print '</div>><!--content-->';
print '<div id="footer">';
print `cat /var/www`;
print '</div>';
print '</body>';
print '</html>';
```

## 第 5 章

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_141_0.png)

**图 4：** 显示证书列表的证书管理器

数字证书有两种类型：一种由 CA 签名，另一种是自签名的。现在，你已经在上一节内容中学习了由 CA 签名的证书。现在，让我们来学习自签名证书。

自签名证书是使用证书本身进行签名。它用于创建不信任正式 CA 提供的大型根树的安全服务器。按照规定，你不要在公共访问的网站上使用自签名证书，因为 Web 浏览器不会自动接受它们，而且它们没有提供足够的信任级别。

让我们学习如何在 Fedora Core 上创建自签名数字证书。

使用以下命令创建自签名证书（使用 root 用户的登录据）：

- 通过以下命令切换目录到 `/etc/pki/tls/certs`：

```bash
# cd /etc/pki/tls/certs
```

- 创建密钥对：

```bash
# makekeypair
umask 077 ;
usr/bin/openssl req -new -des3 1024 > /etc/pki/tls/private/localhost.key
Generating RSA private key, 1024 bit long modulus
+++++
+++++
e is 65537 (0x100001)
Enter pass phrase:
Verifying: Enter pass phrase:
```

此步骤用于创建用于加密和解密数据的公钥和私钥。请使用容易记忆但他人难以猜到的短语。生成的密钥文件为 `/etc/pki/tls/private/localhost.key`。

- 如果你想从 CA 获取数字证书，则你需要创建一个证书签名请求（在自签名证书中不需要此步）：

### Apache Web 服务器 133

```bash
# makecertreq
umask 077 :
/usr/bin/openssl -utf8 -new -key /etc/pki/tls/private/localhost.key -out
/etc/pki/tls/certs/localhost.csr
Enter pass phrase for /etc/pki/tls/private/localhost.key:
You are to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value.
If you enter '.', the field will be left blank.
----
```
