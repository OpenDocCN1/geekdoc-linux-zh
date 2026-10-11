
# Linux 管理：入门指南

## LogLevel

此选项设置发送到错误日志的信息的详细程度。允许的日志级别有 `emerg`、`alert`、`crit`、`error`、`warn`、`notice`、`info` 和 `debug`。默认日志级别为 `warn`。

```
Syntax: LogLevel level
```

## Alias

`Alias` 指令允许文档（Web 内容）存储在文件系统中任何不同于 `DocumentRoot` 指令指定的位置。它允许你为可能很长的路径名创建缩写（或别名）。

```
Syntax: Alias URL_path actual_file_or_directory_path
```

## ScriptAlias

`ScriptAlias` 选项指定包含 CGI 脚本的目标目录或文件，这些脚本将由 CGI 模块 (`mod_cgi`) 处理。

```
Syntax: ScriptAlias URL-path actual_file-path_OR_directory-path

Example: ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
```

## VirtualHost

Apache 最常用的功能之一是它支持虚拟主机的能力。这使得如果每个网站都有自己的专有硬件，单台服务器就可以托管多个网站。它的工作原理是允许 Web 服务器根据客户端请求的主机、端口号或 IP 地址提供不同的、自主的内容。这是通过 HTTP 1.1 协议实现的，它在 HTTP 请求头中指定所需的站点，而不是依赖服务器来学习从其 IP 地址中获取什么内容。

此指令实际上由两个标签组成：一个起始 `<VirtualHost>` 标签和一个结束的 `</VirtualHost>` 标签。它用于指定与特定虚拟主机相关的选项。我们之前讨论的大多数指令在这里也有效。

```
Syntax: <VirtualHost ip_address_OR_hostname[:port]

Options

</VirtualHost>
```

例如，假设我们想为名为 `www.another-example.org` 的主机设置虚拟主机配置。为了做到这一点，我们在 `httpd.conf` 文件中创建一个 `VirtualHost` 条目（或使用 `Include` 指令指定一个单独的文件），如下所示：

```
<VirtualHost www.another-example.org>

ServerAdmin webmaster@another-example.org

DocumentRoot /www/docs/another-example.org

ServerName www.another-example.org

ErrorLog logs/another-example.org-error_log

</VirtualHost>
```

在类 Debian 发行版中，你可以使用任何工具集（`a2ensite` 和 `a2dissite`）在 Apache 下快速启用或禁用虚拟主机和网站。
例如，假设我们为虚拟网站创建了上述名为 `another-example.org` 的配置文件，并将文件存储在 `/etc/apache2/sites-available/` 目录下。我们可以使用以下命令启用虚拟网站：

```bash
master@ubuntu-server:-$ sudo a2ensite www.another-example.org
```

同样，对于虚拟站点，你可以运行此命令：

```bash
master@ubuntu-server:-$ sudo a2dissite www.another-example.org
```

在运行之前的任何一个命令（`a2ensite` 或 `a2dissite`）后，你应该通过运行以下命令让 Apache 重新加载配置文件：

```bash
master@ubuntu-server:-$ sudo /etc/init.d/apache2 reload
```

最后，不要忘记，仅使用 Apache 配置虚拟主机是不够的。

# 快速教程：从用户目录提供 HTTP 内容

在启用 `UserDir` 后，假设用户 `yang` 想要通过 Web 服务器从其家目录下发布某些内容，按照以下步骤操作即可：

- 1. 以用户 `yang` 的身份登录系统时，创建 `public_html` 文件夹：

```bash
yyang@server:-$ mkdir ~/public_html
```

- 2. 为父目录设置适当权限：

```bash
yyang@server:-$ chmod a+x
```

- 3. 为 `public_html` 文件夹设置适当权限：

```bash
yyang@server:-$ chmod a+x public_html
```

- 4. 在 `public_html` 文件夹下创建一个示例页面：

```bash
yyang@server:-$ echo "Ying Yang's Home Page" >>/public_html/index.html
```

由于这些更改，放置在特定用户 `public_html` 目录并设置为世界可读的文件将通过 Web 服务器发布在 Web 上。
要通过 HTTP 访问该目录的内容，你需要将 Web 浏览器指向其 URL：

```
http://<YOUR_HOST_NAME>/<USERNAME>
```

`WHERE_HOST_NAME` 是 Web 服务器的完全限定域名或 IP 地址。如果你直接坐在 Web 服务器上，可以简单地将该变量替换为 `localhost`。
对于示例中的用户 `yang`，实际 URL 将是 `http://localhost/~yang`。
请注意，在启用了 SELinux 子系统的 Fedora 系统上，你可能需要多做一些操作才能让 `UserDir` 目录工作。这是因为存储在每个用户家目录下的文件具有默认的安全上下文。默认情况下，该上下文是 `user_home_t`。为了让此功能正常运行，你必须将 `~username/public_html/` 下所有文件的上下文更改为 `httpd_sys_content_t`。这允许 Apache 读取 `public_html` 目录下的文件。执行此操作的命令是：

```bash
[yyang@fedora-server ~]$ chcon -Rt httpd_sys_content_t public_html/
```
