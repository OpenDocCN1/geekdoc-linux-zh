
你可以通过 `httpd.conf` 文件中的 `UserDir` 指令启用用户控制的 HTML 目录。此选项允许每个用户的家目录被提供。其默认目录是 `public_html`。目录通过以波浪线 `~` 开头后跟用户名的 URL 访问。当服务器接收到此类 URL 时，它从 `/etc/passwd` 文件检索用户的家目录。通过下面的示例，可以看到服务器如何映射此位置：

```
http://www.example.com/~chris/index.html
```

如果用户 `chris` 的家目录是 `/home/users/chris` 且 `UserDir` 目录是 `public_html`，服务器将发送 `/home/users/chris/public_html/index.html`。

## 设置 Alias

你可以通过 `httpd.conf` 文件中的 `Alias` 指令将特定 URL 映射到系统上的目录。这允许你提供不在文档根指令指定的目录下的文件。例如，如果你想提供 `/public/ftp/multimedia` 目录下的文档，可以使用以下行通过 URL `http://www.example.com/multimedia` 访问 `/public/ftp/multimedia` 目录：

```
Alias /multimedia /public/ftp/multimedia
```

目前，Apache 服务器允许你通过这种方式定义最多50个别名。如果你想定义更多别名，请重新定义 `/usr/local/etc/httpd/src/httpd.h` 中的 `MAX_ALIASES` 宏并重新编译服务器（参见“编译 Apache 服务器”章节）。

## 符号链接

符号链接是 UNIX 文件系统最有价值的功能之一。它们允许你在文件系统中创建一个指向其他文件或目录的指针，使符号链接成为管理 Web 空间的不可或少的工具。

例如，你可能决定将文档根指令的默认设置为 `/usr/local/etc/httpd/docs`。然后你可以通过输入以下命令让你的文档根实际位于 `/public/html` 目录：

```
# ln -s /public/html /usr/local/etc/httpd/docs
```

为了方便管理，一种常用的约定是将顶级目录链接到文档根。如果你使用默认的 `/usr/local/etc/httpd/docs` 作为文档根，可以使用以下命令创建顶级目录链接：

```
# ln -s /usr/local/etc/httpd/docs /html
```

此命令允许你轻松地访问 `ServerRoot` 下的目录并节省了大量的输入工作。对于新接触 UNIX 环境的人来说，这也是一种记忆手段。用户会很容易记住将 Web 页面放在 `/html/` 中。然而，如果你链接得太深，你花费在寻找文件真实位置的时间将超过你节省的输入时间。务必跟踪你的链接，并仅在需要时使用它们。书的其余部分假设你拥有这样一个链接。

## 其他考虑

你选择设置 Web 空间的方式与你组织的性质以及服务器的目的和用户很大关系。例如，许多大学为学生提供主页。这些账户从定义上说是瞬时的，因此 `UserDir` 方法（即提供的文档位于用户家目录下的 `public_html` 中）效果良好。当学生毕业且账户过期时，会自动删除该账户的家目录。你为学生目录建立的任何配额也适用于你的 Web 文档，因此没有必要为 Web 文档单独设置配额。

# 84 UNIX Web 服务器

如果你的网站是一个专业机构或公司，你通常有一组稳定的文档需要提供。在这种情况下，最好将大多数文档放在根目录下的。你仍然可以通过将家目录链接到根目录下的目录来让个人对网站贡献。如果某个人离开了公司，可以轻松地删除其账户，而不必担心删除关键的 Web 文档目录。此外，可以为该部分或目录的新维护者定义一个新的符号链接，无需移动任何文档。这种设置便于管理，因为大多数 Web 文档集中在一个位置，通常更容易维护和备份。

在本节中使用的示例是通用示例，并不意味着只有一种方法适用于你，且使用一种方法并不排除使用另一种。

## 启动服务器

现在你已经配置好了服务器，是时候启动并测试它了。启动服务器有技术取决于你选择独立运行还是通过 inetd 运行。

### 独立运行

要运行独立服务器，你只需要将一行添加到启动时执行的脚本中。在 Linux 下，此脚本文件是 `/etc/rc.d/rc.local`；在其他操作系统下，文件可能名为 `/etc/rc.local`，或者你可能需要在 `/etc/rc2.d` 目录下创建一个单独的脚本。如果不确定，请咨询系统管理员手册。

找到正确的文件后，成为超级用户并使用你喜欢的文本编辑器打开脚本。在脚本末尾添加以下几行：

```
if [ -x /usr/local/etc/httpd ]
then
echo "Starting HTTP server"
cd /usr/local/etc/httpd http > /dev/console 2>&1
else
echo "Can't start HTTP server!"""
```

完成后后，保存文件并退出编辑器。这些行会检查 HTTPd 服务器是否存在；如果存在，你添加的这些行将启动它。尽管你已将这些行添加到系统的启动脚本中，但在下次重启电脑时它们不会被运行。若要现在启动服务器，你应该以超级用户身份输入以下内容：

```
# cd /usr/local/etc/httpd
# /httpd
```

假设你在屏幕或 `/usr/local/etc/httpd/logs/error_log` 中没有看到任何错误信息，你的服务器应该已成功运行。

### 来自 inetd

要从 inetd 运行服务器，必须修改两个文件。第一个文件 `/etc/services` 用于定义已知端口和使用这些端口的协议。如果你使用 NIS（也称为 YP）在本地网络上共享系统数据库，你需要使用 `ypush` 命令更新它们，以便对该文件的更改生效。切换到超级用户并使用编辑器打开 `/etc/services`，在文件末尾添加以下行：

```
http 80/tcp
```

你需要修改的第二个文件是 `/etc/inetd.conf`。这是 inetd 的配置文件；它告诉 inetd 监听哪些端口以及在检测到连接时采取什么操作。仍然以超级用户身份，打开 `/etc/inetd.conf` 文件并在末尾添加以下内容（全部写一行）：

```
http stream tcp nowwait nobody /usr/local/etc/httpd/httpd/
httpd
```

此项目在大多数 UNIX 系统上都有效。一个显著例外是 Ultrix，它使用以下格式：

```
http stream tcp nowait /usr/local/etc/httpd/httpd/httpd
```

第四个字段（在 Ultrix 下被省略）告诉 inetd 以哪个用户运行服务器。Ultrix 不允许你指定用户；从 inetd 启动的服务器始终以 root 身份运行。由于这是一个潜在的安全问题，你应该使用 `conf/httpd.conf` 中的 `User` 指令将用户设为 `nobody` 或其他适当的用户。

在 `/etc/services` 和 `/etc/inetd.conf` 中添加了相应的行后，你需要通知 inetd 它的配置文件已更改。要做到这一点，找到 inetd 的进程 ID (PID) 并向其发送 HUP（挂断）信号，如下所示（在 Solaris 和 Irix 等 System V 系统上，使用 `ps -aef` 选项）：

```
# ps -aux | inetd
root 11253 0.0 3.4 156 256 p S 23:00 0 grep inetd
root 430.0 1.0 72 80 con S Feb 1 0:00 /usr/sbin/inetd
# kill -HUP 433
```

当 inetd 接收到 HUP 信号时，它会重新读取 `/etc/inetd.conf` 并开始监听 HTTP 连接。

## 测试服务器

当服务器运行时，你应该对其进行快速测试。如果你已经准备了一些页面，可以尝试在你喜欢的浏览器中获取其中一个。如果你还没有准备任何内容或没有浏览器处理程序，可以直接输入以下内容来测试服务器：

```
$ telnet localhost 80
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'
```

这打开了到服务器 HTTP 端口的连接。当你成功连接时，可以通过输入以下内容并按两次回车来检查一切运行正常：

```
HEAD /HTTP/1.0 200 OK
Date: Friday, 12-Dec-94 05:44:30 GMT
Server: Apache/1.1
MIME-version: 1.0
Content-type: text/html
Last-modified: Sunday, 12-Dec-94 01:21:23 GMT
Content-length: 2342
```

你应该会看到类似下面的响应：
