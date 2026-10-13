
对于基本服务器配置，你需要修改以下几行：

```
ServerAdmin: you@your.address
```

ServerAdmin 中列出的地址会出现在 Apache 自动生成的错误信息中，并发送到访客浏览器当出现问题时。这为访客提供了联系你关于他们在网站上遇到的问题的方式。此地址应替换为你希望用于接收服务器问题邮件的地址。

```
ServerName: new.host.name
```

通常你应在此处设置主机名，并将第一部分别名为 www。例如，如果你的完整主机名是 simba.mycompany.com，则应在此配置文件中填写的名称为 www.mycompany.com。这有时在服务器需要查找其自己的主机名时使用。

```
DocumentRoot: /usr/local/apache/htdocs
```

该目录是存储网页的根目录。换句话说，如果有人输入 www.mycompany.com，发送给他们的文件就是 /usr/local/apache/htdocs/index.html。如果你不想将网页存储在此目录中，应将此路径更改为你希望保存网页的任何目录。

![](img/ba0161b65b37e94cffc801ecbacaba5e_373_0.png)

> DocumentRoot 指令指示的目录中位于其中的任何文件或目录都将可供 Web 服务器读取并通过互联网发送出去。因此，只有打算在网站上显示的文档才应存储在 /usr/local/apache/htdocs 或其任何子目录中。

要让一个基本的 Web 服务器运行起来，这些通常是最初你需要关心的唯一选项。有关文件中其余部分的更多信息，可在 Apache 网站 www.apache.org 上找到。

## 启动和停止 Apache 服务器

如前所述，Apache 服务器会在每次启动系统时自动启动，因为安装过程在 /usr/local/etc/rc.d 中安装了启动脚本。然而，如果你想随时手动启动服务器，可以使用 apachectl 程序。例如，

```
#apachectl start
/usr/local/sbin/apachectl start: httpd started
```

apachectl 程序也可以用来停止服务器，而且这是最简单也是最好的方法。例如，

```
#apachectl stop
/usr/local/sbin/apachectl stop: httpd stopped
```

如果你想重启服务器，apachectl 也有一个命令可以做到这一点，而不必发出两个命令：

```
#apachectl restart
/usr/local/sbin/apachectl restart: httpd restarted
```

请注意，Apache 只在首次启动时读取一次配置文件。因此，在 Apache 运行期间对它们所做的任何更改都不会生效，直到通过发出前述命令重启它为止。

如果在 Apache 运行期间查看进程列表，你会看到多个 httpd 进程，因为主 Apache 进程会生成多个子进程来处理传入的 httpd 请求。Apache 总是保持多个进程运行以处理请求——即使当前没有网站流量。如果出于某种原因，你想通过直接向进程发出 kill 命令来终止 Apache 服务器，必须确保你向父进程发出命令。如果你杀掉其中一个子进程，父进程只会生成一个新的进程来替换它。

![](img/ba0161b65b37e94cffc801ecbacaba5e_374_0.png)

> apachectl restart 命令会立即杀死父进程以及所有子进程，即使子进程当前正在处理请求。这意味着当前正在接收或向你的 Web 服务器发送数据的网站访客基本上会“被突然中断”。因此，apachectl 程序还提供了 graceful 选项，可在 restart 选项代替使用（例如 apachectl graceful）。该命令会重启服务器，但不会中断正在进行的任何事务。当前正在处理事务的进程不会在当前事务完成之前被重启。

默认情况下，Apache 运行在网络端口 80 上，对于公共 Web 服务器，你可能不想更改它。Web 浏览器除非在 URL 中另有指定，否则假定端口为 80。

作为操作系统的一般安全措施，低于 1024 的端口号只能由 root 用户打开。因此，父 Apache 进程需要以 root 身份运行。然而，子进程通常以 nobody 运行，这是一个没有特殊权限且无法登录系统的账户。

请注意，Apache 受 UNIX 文件权限的约束。因此，为了使文件和目录可供网站访客访问，它们需要能被用户 nobody 读取。通常这不会成为问题，因为文件可以设置为全局可读。

在 Apache 服务器安装并启动后，你应该能够通过在 Web 浏览器中加载以下地址来访问它（如果你尝试从 Web 服务器运行的同一台机器访问。）

```
http://127.0.0.1
```

如果服务器正在运行，你应该会看到默认的 Apache 欢迎页面。当然，你会想用网站的主页替换此页面。

请注意，如果服务器当前在网络上，你也应该能够通过在 Web 浏览器中输入 Web 服务器机器的 IP 地址，从另一台计算机访问 Web 服务器。

## CGI

CGI 代表通用网关接口。它是一种 Web 服务器可以通过它运行外部程序，甚至将网页表单中输入的数据传递给外部程序的方法。外部程序也可以将输出发送回 Web 服务器，然后可以在网页上显示，例如。

尽管这些外部程序通常被称为 CGI 脚本，但它们不一定必须是脚本。CGI 程序可以用任何语言编写。在 UNIX 中编写 CGI 脚本最常见的语言是 Perl。然而，CGI 也可以用 Python、TCL、shell 脚本、AWK、SED、Java 或甚至完全编译的语言如 C 编写。关于如何在网页中使用 CGI 脚本的讨论超出了本书的范围。然而，我们将介绍如何在 Apache 服务器中启用 CGI，以及如何确保它们不会最终损害系统的安全性。

## 为 CGI 配置 Apache

CGI 脚本通常具有如下所示的地址：

```
http://www.mycompany.com/cgi-bin/myscript.pl
```

通常，Apache 只允许位于 cgi-bin 目录中的脚本执行。cgi-bin 目录不应位于提供普通网页的同一目录中，因为你不希望访客能够像普通网页一样加载 CGI 脚本。

在 httpd.conf 文件中，以 ScriptAlias 开头的行决定 CGI 脚本存储的位置。例如，

```
ScriptAlias /cgi-bin/ "/usr/local/www/cgi-bin/"
```

这行意味着 CGI 程序实际存储在 /usr/local/www/cgi-bin 中。对该目录的别名是 Web 服务器根目录后跟 cgi-bin 目录（例如 www.mycompany.com/cgi-bin）。所有 CGI 脚本都需要存储在 /usr/local/www/cgi-bin 中。存储在普通网页目录中的 CGI 脚本将被视为普通 HTML 文件并仅显示而不是执行。

请注意，CGI 脚本是实际在 Web 服务器上执行的程序。通常，它们将以 Web 服务器进程运行的用户身份运行，这意味着 CGI 脚本通常将以用户 nobody 运行。

如前所述，我们在这里不会深入讨论如何使用 CGI；然而，以下是一个非常简单的 CGI 程序，你可以用它来测试是否已正确配置 Apache 的 CGI 支持：

```
#!/bin/sh
echo "Hello. The current date and time is: "
date
```

将此文件保存到 /usr/local/www/cgi-bin 目录中，扩展名为 .sh。例如，mycgi.sh。确保文件设置为可执行（回顾第 5 小时的课程，“用户和组”）。

为了证明这是一个可以从 FreeBSD 命令提示符直接执行的普通文件，只需像平常一样运行它。请注意，因为该目录不在你的路径中，你需要明确告诉 FreeBSD 文件位于当前目录。这可以通过在命令前加上 ./ 来完成——例如 ./mycgi.sh。以下是程序显示的示例：

```
$ ./mycgi.sh
Hello, the current date and time is:
Tue Jul 23 23:14:12 CDT 2002
```
