

## 选择特定的 CGI 文件扩展名

我并不喜欢 `ScriptAlias` 指定目录中的任意文件都作为 CGI 程序运行的想法。我更倾向于一种能够限制 CGI 程序名称的解决方案，使得只有具有特定扩展名的文件才被当作 CGI 程序处理。下面讨论如何通过使用 `mod_cgi` 模块中找到的 Apache 处理程序来实现这一目标，并包含一个示例配置，其中我通过 `AddHandler` 处理程序启用一组选定的文件扩展名，使其被当作 CGI 程序。

在这个示例中，假设 Apache 服务器名称为 `www.domain.com`，且其 `DocumentRoot` 目录设置为 `/www/website/public/htdocs`；CGI 程序目录为 `/www/nitec/public/cgi-bin`。请注意，CGI 程序目录是故意保留在 `DocumentRoot` 指定目录之外的。这确保了没有人可以浏览该目录，因为 Apache 只能通过别名看到它。

请按照以下步骤设置 Apache，以从目录中运行给定扩展名的 CGI 脚本：

- 1. 通过完全从 `httpd.conf` 中移除现有的 `ScriptAlias` 指令，或者在该行开头插入井号（#）将其变成注释行，来禁用现有的 `ScriptAlias` 指令。
- 2. 为 CGI 程序目录创建一个别名。由于 CGI 程序目录位于文档树之外，如果没有别名（或符号链接），就无法访问它。可以使用 `Alias` 指令定义别名，其语法如下：
    ```
    Alias /alias/ "/path/to/cgi/dir/outside/doc/root/"
    ```
    按照此语法，所需的 `Alias` 指令看起来如下：
    ```
    Alias /cgi-bin/ "/www/website/public/cgi-bin/"
    ```
- 3. 通过为该特殊目录定义 `<Directory>` 容器，指示 Apache 从此目录执行 CGI 程序。使这一切发生（即将该目录转变为 CGI 程序目录）所需的目录容器定义如下：
    ```
    <Directory "/path/to/cgi/dir/outside/doc/root/">
        Options ExecCGI -Indexes
        AddHandler cgi-script extension-list
    </Directory>
    ```

`Options` 指令为 `/path/to/cgi/dir/outside/doc/root` 目录设置了两个选项。首先，设置了 `ExecCGI` 选项，它告诉 Apache 允许从此目录内部执行 CGI 程序。其次，`-Indexes` 选项告诉 Apache 不允许目录列表，因为允许访客查看 CGI 脚本目录的内容不是一个好主意。接下来，`AddHandler` 指令为该目录中发现的一组文件扩展名设置 cgi-script 处理程序。列表中具有指定扩展名的任何文件都将被视为 CGI 程序。当 Web 客户端请求此类文件时，程序将运行并将输出返回给 Web 客户端。我们当前示例中的实际指令如下所示：

```
<Directory "/www/mysite/public/cgi-bin">
    Options ExecCGI -Indexes
    AddHandler cgi-script .cgi .pl
</Directory>
```

在此处，你已启用 `.cgi` 和 `.pl` 作为 CGI 程序扩展名，因此，当发起诸如以下请求时：

```
http://www.domain.com/cgi-bin/anything.cgi
http://www.domain.com/cgi-bin/anything.pl
```

Apache 将尝试将这些文件作为 CGI 程序执行。当然，如果这些文件实际上不是可执行文件或不存在，Apache 将显示并记录错误消息。

前面提到的 CGI 程序目录权限设置仍然适用于此配置。相同的配置也适用于虚拟主机站点。例如，在以下示例中，www.client01.com 的 `/cgi-bin/` 别名被设置为在 /www/client01/public/cgi-bin 目录中执行 CGI 程序：

```
<VirtualHost 192.168.2.100>
    ServerName www.client01.com
    DocumentRoot "/www/client01/public/htdocs"
    CustomLog logs/www.client01.com.access.log
    ErrorLog logs/www.client01.com.errors.log
    Alias /cgi-bin/ "/www/client01/public/cgi-bin/"
    <Directory "/www/client01/public/cgi-bin">
        Options ExecCGI -Indexes
        AddHandler cgi-script .cgi .pl
    </Directory>
</VirtualHost>
```

在这里，www.client01.com 的 `/cgi-bin/` 别名被设置为在 /www/client01/public/cgi-bin 目录中执行 CGI 程序。

## 为用户启用 cgi-bin 访问

许多互联网服务提供商（ISP）提供带有用户账户的网站空间。这些网站通常拥有这样的 URL：

```
http://www.isp.net/~username
```

这些站点通常会收到用户通过其客户端（浏览器）发出的 cgi-bin 访问请求。术语 cgi-bin 访问是一个通用术语，用于指示 Web 服务器上的 CGI 功能。传统上，CGI 程序目录已被别名为 /cgi-bin/，因此产生了这个术语。另一个变得非常流行的常见术语是主页（home page），它指的是用户 Web 目录的顶级索引页。

以下部分讨论在 Apache Web 服务器中为用户提供 cgi-bin 访问的两种方式。你只需要实施这些方法中的任何一种。

### Directory 或 DirectoryMatch 容器

当 `UserDir` 指令设置为目录名称时，Apache 将其视为用户网站的顶级目录，例如：

```
ServerName www.domain.com
UserDir public_html
```

现在，当对 `http://www.domain.com/~username` 的请求到来时，Apache 会定位指定用户的家庭目录（通常通过检查 Unix 系统上的 /etc/passwd 文件），然后附加 `UserDir` 指定的目录以创建顶级用户 Web 目录的路径名。例如，URL

```
http://www.domain.com/~joe
```

使 Apache 寻找 /home/joe/public_html（假设 /home/joe 是 Joe 的家庭目录）。如果该目录存在，则该目录的索引页将发送给请求客户端。

为每个用户添加 CGI 支持的一种方法是在 `httpd.conf` 文件中添加以下配置：

```
<Directory ~ "/home/[a-z]+/public_html/cgi-bin">
Options ExecCGI
AddHandler cgi-script .cgi .pl
</Directory>
```

或者你可以使用此配置：

```
<DirectoryMatch "/home/[a-z]+/public_html/cgi-bin">
Options ExecCGI
AddHandler cgi-script .cgi .pl
</DirectoryMatch>
```

在这两种方法中，Apache 将 `http://www.yourcompany.com/~username/cgi-bin/` 请求转换为 `/home/username/public_html/cgi-bin/`，并允许具有正确扩展名（.cgi 或 .pl）的任何 CGI 程序执行。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_370_0.png)

> 为了使这正常工作，所有用户名必须由全小写字母组成。如果你有字母数字用户名，你必须使用不同的正则表达式。例如，如果你有 *stev01* 或 *stev02* 这样的用户名，你需要使用 `[a-z0-9]`+ 修改 `[a-z]`+ 字符集以包含数字，或者如果你还允许大写的用户名，则使用 `[a-zA-Z0-9]`+ 作为正则表达式。

### ScriptAliasMatch

通过使用 *ScriptAliasMatch* 指令，你可以为每个用户支持 CGI 程序目录。例如：

```
ScriptAliasMatch ^~([a-z]+)/cgi-bin/(.*) /home/$1/public_html/cgi-bin/$2
```

将 *username* 匹配到反向引用变量 $1，其中 $1 等于 --*username*，且 *username* 是一个小写字符串，例如 *joe* 或 *stev01*，然后 Apache 将 `/cgi-bin/` 之后的所有内容匹配到反向引用变量 $2。接着，Apache 使用 $1 和 $2 变量创建实际的 CGI 程序路径。例如：

```
http://www.domain.com/~joe/cgi-bin/search.cgi?author=kabir
```

在此处，`([a-z]+)` 将波浪号标记 `(~)` 之后的一个或多个小写字母映射到 $1。换句话说，这个正则表达式使我们能够捕获波浪号 `(~)` 和用户名后的尾部斜杠 `(/)` 之间的所有内容。因此，在上面的示例中，$1 被设置为 *joe*。请注意，`^` 确保该指令仅应用于以 `~` 开头的 URL，如上例所示。

指令中的下一个正则表达式是 `(.*)`，它将 `/cgi-bin/` 之后的所有内容映射到 $2。因此，$2 被设置为 *search.cgi?author=kabir*。

现在，Apache 可以使用以下内容创建 CGI 程序目录的物理路径：

```
/home/$1/public_html/cgi-bin/$2
```

对于前面的示例，此正则表达式得出以下路径：

```
/home/joe/public_html/cgi-bin/search.cgi?author=kabir
```

因为这是存储 CGI 程序 *search.cgi* 的位置，所以它会执行并将输出返回给 Web 客户端。

如果你不喜欢将 CGI 程序目录放在 *public_html*（即 *UserDir* 指定的目录）之下，你可以通过从表达式中移除 *public_html* 部分来将其保留在该目录之外，如下所示：

```
ScriptAliasMatch ^~([a-z]+)/cgi-bin/(.*) /home/$1/cgi-bin/$2
```

