

# 456 第四部分 在 SUSE Linux 中实现网络服务

```
AuthGroupFile /etc/http-groups
Require group GroupName
</Directory>
```

任何经过适当身份验证并列在 `GroupName` 组中的用户都将被允许进入“仅限邀请”区域。

基础认证（Basic authentication）的一个问题是，每当请求服务器的资源（无论是 HTML 页面、图像还是受保护目录中的任何资源）时，必须验证用户名和密码。这可能会略微降低 Web 服务器的响应速度。事实上，Web 服务器变慢与密码文件的大小成正比。请记住，Apache 服务器在每次加载页面时都必须打开该文件并按用户顺序向下查找，直到找到该用户。

这样做的结果是，一个页面能列的用户数量存在实际限制。虽然该限制取决于特定服务器的配置，但在条目增加几百后，Web 服务器的性能就会受到影响，可能需要不同的身份验证方法。

可以使用 `mod_auth_dbm` 模块找到此类方法。`mod_auth_dbm` 提供了配合 `dbmange` 程序使用的文件支持。另一个可能的选项是 `mod_auth_mysql`。`mod_auth_mysql` 允许 Apache 服务器连接到后端 MySQL 数据库，可以在其中高效地存储和访问用户名和密码。

关于您的 Apache 服务器身份验证的进一步讨论已超出本书的范围。然而，如果你对深入研究安全和 Apache 主题感兴趣，可以查看《Maximum Apache Security》（Sams, 2002）等书籍获取更多信息。

# 通用网关接口 (CGI)

通用网关接口（CGI）定义了 Web 服务器与外部程序交互的方式，这些程序被称为 CGI 程序或 CGI 脚本，用于根据客户端请求生成动态内容。要配置 Apache 服务器与 CGI 程序交互，首要任务是让 Web 服务器知道 CGI 程序所在地。

一种方法是使用 `ScriptAlias` 指令，它告诉 Apache 特定目录已为 CGI 程序预留。Apache 将尝试将给定目录中的每个文件作为 CGI 程序执行。因此，当客户端请求特定资源时，Web 服务器将执行该程序。`ScriptAlias` 指令与 `Alias` 指令非常，后者定义了一个映射到文件系统中特定目录的 URL 空间。请考虑以下示例：

# 第 16 章使用 Apache 服务器建立网站 457

ScriptAlias /cgi-bin/ /srv/www/cgi-bin/

对于给定的示例，该指令标记了目标目录 `/srv/www/cgi-bin`，该目录包含将由 Apache mod_cgi 模块的“cgi-script handler”处理的 CGI 脚本。此外，通过此指令的映射，对 `http://ourservicever/cgi-bin/` 的任何资源请求都会导致服务器运行 `/srv/www/cgi-bin/` 中的脚本。

然而，CGI 程序可以任意目录调用。要让 CGI 程序位于站点目录的任何地方，需要完成两个配置步骤。首先，必须使用 `AddHandler` 指令激活 cgi-script handler。其次，对于任何可能包含 CGI 程序的目录或子目录，必须在 `Options` 指令中指定 `ExecCGI`。

...

```
<Directory /srv/www/htdocs/dir
Options +ExecCGI
</Directory>
```

`AddHandler` 指令的作用是将所有带有 .cgi 扩展名的文件视为 CGI 程序。此外，带有 `Options +ExecCGI` 指令的 `<Directory>` 容器告诉 Apache 允许执行位于 `/srv/www/htdocs/dir` 或其子目录中的 CGI 程序。

列表 16-2 是一个 Perl 脚本和一个 CGI 程序示例，它向客户端打印带有日期的欢迎消息。

# 列表 16-2：一个 Perl CGI 脚本

```
#!/usr/bin/perl
# example.cgi
# 这是一个用于打印欢迎消息和当前
# 日期的示例脚本
$month = ('jan','feb','mar','apr','may','jun','jul','aug','sep','oct','nov','dec')[localtime[4]];
$year = (localtime)[5];
$day = (localtime)[3];

print "Content-type: text/html\n\n"
print "<html><title>This is a test, is is only a test</title><body>\n"
print "Hello, World.<br><br>"
print "Today is, $day;"
if ($day < 10) {
print "$month, 0$day";
```

续上

# 列表 16-2（续）

```
else {
    print $month, ",$day";
}
$thisyear=$year-100;
if ($thisyear < 0) {
    print " 0$thisyear;
} else {
    print $thisyear;
}
print "</body></html>";
```

CGI 程序输出的第一行是 MIME 类型标头。这是一个 HTTP 标头，告诉客户端正在接收什么类型的内容：在本脚本的情况下，客户端将接收到 `text/html` 类型的内容。其次，其余输出是 HTML，这是 Web 浏览器理解并进行显示的格式。

然而，此脚本尚未完全准备好投入使用。当 Apache 服务器启动时，它是以独立于创建脚本的用户运行的。因此，必须更改文件系统权限。

```
chmod +x example.cgi
```

> 要使用 PHP 语言，您需要安装 RPM。执行此操作，请使用 YaST 的“安装和删除软件”。您可以搜索 php，这将返回可以在您的系统中安装的 PHP 软件包。选择 `php4` 软件包。有关安装新软件的更多信息，请参阅第 1 章。

# 503
# 使用 PHP 创建动态内容

Apache 服务器是一个模块化服务器。用于它的最流行的模块是 `mod_php`。PHP 是官方称为 Hypertext Preprocessor 的缩写，由 Rasmus Lerdorf 创建，他在 1994 年正在寻找一种工具来跟踪谁在看他的简历。PHP 是一种强大的开源开发语言，提供了完成任何任务的工具和灵活性。

服务器端技术意味着意味着查看页面的客户端没有特殊的应用程序，因为安装了 PHP 的 Web 服务器在将请求文档发送给用户之前，会执行处理请求文档内任何代码的额外步骤。通过这一额外步骤，PHP 可以执行任何操作，例如访问数据库。这使得 Web 开发人员能够根据从第三源收集的数据动态构建 Web 页面，并通过互联网提供的任何方式进行通信。

这与用 Perl 编写的 CGI 脚本有何不同？首先，与 CGI 脚本不同——后者将作为一个独立进程运行，调用解释器运行脚本并将输出管道到 stdout 以供 Web 服务器使用——而 PHP 在 Apache 服务器进程内部运行解释器，以便随时运行。然而，真正的优势体现在用户在对 CGI 内部工作原理（例如，脚本可能与之通信的后端）了解甚少的情况下可以做什么。

> Perl 脚本语言也可以通过 `mod_perl` 嵌入到 Apache Web 服务器中。通过 `mod_perl` 并对现有的 Perl CGI 脚本进行修改，你可以获得与 PHP 编写的脚本相同的运行时优势。

要在核心服务器中包含 PHP 的基本功能，需要扩展 `LoadModule` 指令。Apache 还需要知道使用 PHP 模块解析哪些文件。这是通过 `AddType` 指令完成的。重启 Apache 守护进程后，一切就绪。

```
LoadModule php4_module libexec/libphp4.so
AdType application/x-httpd-php .php own
```

