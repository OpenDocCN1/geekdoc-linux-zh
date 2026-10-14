
`AuthName` "`Restricted Directory`"

`UserFile` `/etc/http-passwd`

`Require` `paul`

```
</Directory>
```

在 `<Directory>` 容器中：

- `AuthType` 指令选择验证用户的方法；最常见的方法是 `Basic`，由 `mod_auth` 实现。

# 第 16 章 使用 Apache Web 服务器设置网站 455

![](img/e45c9f32e76fb35abb21a96f1a1e)

由 Apache 服务器实现的 Basic 身份验证以明文方式在网络上传递用户名和密码。Apache 服务器支持其他身份验证方法，例如 `AuthType` `Digest`，它由 Apache 模块 `mod_auth_digest` 实现。`Digest` 类型通过在网络上发送密码的 MD5 哈希值提供了一种更安全的密码系统。然而。

- `AuthName` 指令设置访问前所需的领域（Realm）。领域名称有两个功能：
- 第一，客户端应用程序将此信息作为密码框的一部分展示给用户。
- 第二，它被客户端用于确定在给授权区域应发送什么密码。
- `UserFile` 指令设置用 `htpasswd` 创建的密码文件的路径。
- `Require` 指令提供了授权路径，通过为 Web 服务器定义在有效验证后允许访问定义领域的用户。

## 设置组访问

上一个示例只允许一个用户 `paul` 进入。在大多数情况下，这并不实际，因为大多数网站需要允许更多人进入。这两种不同的方式实现。

- 取代仅允许用户 `paul` 访问目录的 `Require user` 指令，`Require valid-user` 将允许密码文件中的任何人在输入密码后访问目录。
- 另一个选项是创建一个组文件，将组名与文件中的用户列表关联。该文件的格式直观，可以使用你喜欢的编辑器完成。

`GroupName: paul roger`

目录容器需要知道密码文件和组文件的位置。由于组文件中可能列出多个组，哪些组可以获得访问也需要指定。

```
<Directory /srv/www/htdocs/private>

AuthType Basic

AuthName "By Invite Only"

UserFile /etc/http-passwd
```

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

`ScriptAlias` `/cgi-bin/` `/srv/www/cgi-bin/`

对于给定的示例，该指令标记了目标目录 `/srv/www/cgi-bin`，该目录包含将由 Apache `mod_cgi` 模块的“cgi-script handler”处理的 CGI 脚本。此外，通过此指令的映射，对 `http://ourservicever/cgi-bin/` 的任何资源请求都会导致服务器运行 `/srv/www/cgi-bin/` 中的脚本。

然而，CGI 程序可以任意目录调用。要让 CGI 程序位于站点目录的任何地方，需要完成两个配置步骤。首先，必须使用 `AddHandler` 指令激活 cgi-script handler。其次，对于任何可能包含 CGI 程序的目录或子目录，必须在 `Options` 指令中指定 `ExecCGI`。

```
<Directory /srv/www/htdocs/dir

Options +ExecCGI

</Directory>
```

`AddHandler` 指令的作用是将所有带有 `.cgi` 扩展名的文件视为 CGI 程序。此外，带有 `Options +ExecCGI` 指令的 `<Directory>` 容器告诉 Apache 允许执行位于 `/srv/www/htdocs/dir` 或其子目录中的 CGI 程序。

列表 16-2 是一个 Perl 脚本和一个 CGI 程序示例，它向客户端打印带有日期的欢迎消息。

## 列表 16-2：一个 Perl CGI 脚本

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

## 列表 16-2（续）

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
