
## 探索 httpd.conf 文件

当你在计算机上运行 Apache 后，下一步是确保它配置正确，并反映出你自己的系统配置和设置。有一些简单的改动值得去做，以提高服务器的安全性和能力，我们会在后续内容中重点介绍这些改动。

### 任务 23.2：httpd.conf 文件的内部结构

Apache 的早期版本（直到 1.2 版）将配置分成三个单独的文件：srm.conf、access.conf 和 httpd.conf。这很有用，但也令人困惑，因为从来没有明确的规则规定哪种配置语句应该放在哪个文件中。因此，从 Apache 1.3 版本开始，所有配置都存储在一个文件中：httpd.conf。

这个文件的位置因不同的 Unix 变体而异（你可以使用 locate，或查看 apache 或 httpd 的手册页）。常见位置有 /etc/apache（Solaris）、/private/etc/httpd（Mac OS X），以及 /etc/httpd/conf 或 /usr/local/apache/conf（Linux）。

- **1.** 在通常相当长的 httpd.conf 文件（预计你的文件至少有 1000 行）中，也许唯一最重要的变量是 DocumentRoot。它告诉你服务器在文件系统中的哪个位置查找要提供的网页。

```
# grep DocumentRoot httpd.conf
# DocumentRoot: The directory out of which you will serve your
DocumentRoot "/var/apache/htdocs"
# This should be changed to whatever you set DocumentRoot to.
# DocumentRoot /www/docs.host.some_domain.com
```

在 Solaris 上，网页从 /var/apache/htdocs 提供。Red Hat Linux 的默认目录是 /var/www/html 或 /usr/local/apache/htdocs，而 Mac OS X 的默认目录是 /Library/WebServer/Documents。

- **2.** 当 Web 浏览器连接到我们的 Web 服务器并请求“主页”或“根”文档时，将返回 DocumentRoot 目录中的默认文件（可能是 index.html）。（通常这可以通过不指定任何文档来实现，例如当你连接到 http://www.smoothjazz.com/ 时。）

```
# pushd /var/www/html
/var/www/html /etc/httpd/conf
# ls -l
total 8
-rw-r--r-- 1 root root 2890 Sep 5 2001 index.html
-rw-r--r-- 1 root root 1154 Sep 5 2001 poweredby.png
# popd
/etc/httpd/conf
```

默认情况下，Apache 服务器有一个页面，显示它正在运行、它是 Apache，并且是时候放入个人页面了。poweredby.png 是默认 index.html 页面中引用的图形文件。

> 如果你想临时跳到另一个目录，然后再快速回到原来的位置，pushd 和 popd 工具是一个很大的福音。pushd 类似于 cd，但 popd 知道你在当前目录之前的位置。非常有用！

- **3.** 给定目录的可能默认文件名的完整列表可以通过在配置文件中搜索 index.html 来找到。同样，我们将使用 -2 来获取匹配项周围的几行上下文：

```
# grep -2 index.html httpd.conf
#
<IfModule mod_dir.c>
DirectoryIndex index.html index.htm index.shtml index.php index.php4 index.php3 index.phtml index.cgi
</IfModule>
```

这个看起来相当令人困惑的语句表示，如果 mod_dir 模块被加载（默认情况下确实如此），Apache 应该尝试按顺序提供以下文件之一：index.html、index.htm、index.shtml、index.php、index.php4、index.php3、index.phtml 或 index.cgi。

最后一个文件值得进一步探索：带有 .cgi 文件名后缀的文件是可执行程序，编写它们是为了与 Apache 通用网关接口（Common Gateway Interface）兼容。它们可以非常简单，甚至可以是 shell 脚本：

```
#!/bin/sh
echo "Content-type: text/html"
echo ""
echo "Hello world!"
```

但它们也可以相当复杂，连接数据库和其他复杂的程序。

- **4.** 表 23.1 列出了 Web 服务器的一些关键设置，所有这些都可以在 httpd.conf 文件中找到。同时还显示了 Apache 1.3.23 的 Red Hat Linux 7.2 发行版的默认值。如果你偏离标准设置，请务必谨慎：在使用这些较不常见的设置之前，请确保你了解其中一些设置的安全影响！

### 表 23.1 关键 Apache 配置字段

| 名称 | 示例值 | 含义 |
|---|---|---|
| Port | 80 | Web 服务器监听的端口。默认情况下，始终是端口 80，但实际上你可以让 Web 服务器运行在你喜欢的任何端口上。例如，SSL 连接使用端口 443。 |
| User | apache | Web 服务器运行所用的账户名。不要为此使用 root！ |
| ServerAdmin | root@localhost | 对外公告为服务器管理员的电子邮件地址。 |
| UserDir | public_html | 由 `<IfModule mod_userdir.c>` 和 `</IfModule>` 两行包裹，此行定义用户主目录中特殊目录的名称，使服务器能够提供 ~account URLs。 |
| ErrorLog | logs/error_log | Apache 错误日志的位置，以 ServerRoot 为根。这是需要确定的关键信息片段，因为关注错误文件将帮助你防患于未然。 |
| LogLevel | warn | 应该记录哪些级别的事务。如果你的服务器繁忙，请保留此设置；但如果你想了解运行情况，或者如果您的 Web 服务器遇到错误，请将其提升到 info 或 debug。如果你想减少记录，请尝试 error 或 alert。 |

httpd.conf 文件中还有很多很多设置，但仅这些就足够让你忙上至少第一个星期。

- **5.** 需要注意的一点是 CGI 设置。默认情况下，Apache 只允许 CGI 脚本存在于特殊的 cgi-bin 目录中。当然，它的位置在配置文件中定义。查找变量 ScriptAlias。以下是该片段在我们的配置文件中的样子：

```
# ScriptAlias: This controls which directories contain server scripts.
# ScriptAliases are essentially the same as Aliases, except that
# documents in the realname directory are treated as applications and
# run by the server when requested rather than as documents sent to the
# client.
# The same rules about trailing "/" apply to ScriptAlias directives as to
# Alias.
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"

#
# "/var/www/cgi-bin" should be changed to whatever your ScriptAliased
# CGI directory is, if you have that configured.
```

如果你想给用户更多的自由，让他们可以通过简单地确保脚本命名为 .cgi 而在系统上的任何地方拥有 CGI 脚本，请查找并取消注释以下序列的最后一行：

```
# AddHandler allows you to map certain file extensions to "handlers",
# actions unrelated to filetype. These can be either built into the server
# or added with the Action command (see below)
#
# If you want to use server side includes, or CGI outside
# ScriptAliased directories, uncomment the following lines.
#
# To use CGI scripts:
#
#AddHandler cgi-script .cgi
```

你能用什么语言编写 CGI 脚本？几乎任何能够在被调用时执行，并在其余内容返回之前输出正确 CGI 返回序列作为标头的语言都可以。

实际上，启用 CGI 稍微扩展了协议。除了“我想要/这是”之外，我们现在还有“请运行/这是输出”。如果你要编写自己的 CGI 脚本，这是一个基本的概念补充——确保它们输出 HTML！

- **6.** 每个提供 Web 页面的目录，无论是 DocumentRoot 还是子目录，都可以设置特定的权限或能力。默认情况下，目录继承其父目录的权限，因此设置 DocumentRoot 的权限也会为所有其他未明确指定的内容设置能力。

此能力设置在 Directory 块内进行，通常分为两部分。第一部分指定 / 的权限，以涵盖整个文件系统中的所有目录，甚至包括 DocumentRoot 区域之外的目录：

```
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>

