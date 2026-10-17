
与 Alias 指令一样，确保此行开头没有 `#` 字符。此默认设置允许执行示例 CGI 脚本（一个返回幸运运格言的 CGI 脚本）。第一个参数是虚拟路径或相对 URL，用户可以使用它来执行 CGI 脚本。第二个参数是 URL 访问的服务器上的实际路径。

例如，`/cgi-bin/` 是相对 URL 的名称，而 `/usr/local/etc/httpd/cgi-bin` 是脚本实际所在的目录，因此以下 URL 将指向 CGI 脚本 `/usr/local/etc/httpd/cgi-bin/fortune`：

```
http://www.shopt.com/cgi-bin/fortune
```

你可以根据需要添加尽可能多个 `ScriptAlias` 指令。为每个想要编写和运行自己的 CGI 脚本的（受信任）用户创建一个。例如，如果用户 `jem` 想要在 `/home/users/jem/html/cgi` 下创建一个名为 `/jembin` 的 CGI 目录，可以使用以下行来创建它：

```
ScriptAlias /jembin /home/users/jem/html/cgi
```

如果你信任服务器上的所有用户可以创建并运行 CGI 脚本而无需你的检查或干预，你可以启用 CGI MIME 类型。请参见本节较早 `AddType` 指令的描述。

## AddType（添加类型）

该指令用于使用 MIME 映射添加要提供的新类型文档（参见第 2 章“基础组件”中关于文件格式和 MIME 类型的章节）。你可能可能想要添加的新类型文档的一个很好的例子是 Adobe Acrobat 格式，它使用 `.pdf` 文件扩展名。你可能需要一种方法告诉服务器文档类型（通过扩展名），并将其发送到 Web 客户端以便使其启动 Acrobat 查看器。`AddType` 指令提供了实现此的方法。例如，你可以使用以下命令告诉服务器向 Web 客户端发送 `.pdf` 扩展名：

```
AddType application/pdf pdf
```

Apache 服务器还理解两种特殊的 MIME 类型，你可以通过 `AddType` 启用它们，这将有助于服务器的维护。这两个类型在分发版的 `srm.conf` 中被注释掉了：

```
#AddType text/x-server-parsed-html .shtml
#AddType application/x-httpd-cgi .cgi
```

第一个 `AddType` 提供高效的服务器端包含；如果你取消此语句的注释，你可以使用 `.shtml` 扩展名来指示服务器文档包含包含内容。

服务器端包含允许你指示服务器将另一个文档或命令的输出嵌入你的 Web 页面。虽然你可以为整个 Web 区域启用它们，但这将强制服务器在发送到客户端之前扫描每个 HTML 文档以检查包含状态，从而浪费大量的系统资源。有关使用服务器端包含的信息，请阅读 http://hoohoo.ncsa.uiuc.edu/docs/tutorials/includes.html。

第二个被注释的类型 `application/x-httpd-cgi` 提供了另一个扩展名 `.cgi`。当此语句启用时，该扩展名告诉服务器该文件是一个可执行的 CGI 脚本。这允许你在服务器上的任何地方调用脚本，而不仅仅是 `ScriptAlias` 指令指定的目录。

你可以通过删除开头的井号启用这两种类型。

## AddHandler & Action

除了使用 `AddType` 指令更改或添加 MIME 类型外，Apache 现在还能在将文件发送到客户端之前修改或解析特定类型的文件。`AddHandler` 指令将文件扩展名映射到某种类型的操作。其中某些操作是服务器内置的，例如，“AddHandler server-parsed” 这一行将所有扩展名为 `.shtml` 的文件映射到服务器的一项名为“server-parsed”的功能上，该功能会解析文件以寻找服务器端包含（参见第 11 章“CGI：面向程序员的高级表单”）。

（注意，在 `srm.conf` 的示例中，`AddHandler` 指令有时会在扩展名名前加一个“`.`”，而有时则省略它。根据文档，扩展名名前不需要加“`.`”。）

在 `AddHandler` 指令中命名的函数不需要内置在服务器中。`Action` 指令可以将来自 `AddHandler` 的函数映射到 CGI 脚本。例如，`srm.conf` 中的以下几行告诉服务器执行映射到 `/cgi-bin/footer` 的函数-操作，这样每次调用函数-操作时，该脚本就会运行。

```
AddHandler foot
Action foot /cgi-bin/footer
```

`Action` 指令还可以将 MIME 类型直接映射到操作。假设你有一个脚本可以检查用户是否来自竞争公司（通过读取环境变量 `$REMOTE_HOST`，这将在第 11 章中介绍）。以下行在每次请求 HTML 文档时都会运行：

## MetaDir & MetaSuffix

`MetaDir` 和 `MetaSuffix` 指令提供了与 `<META>` 标签（第 5 章“HTML”讨论）的功能，但元数据是分开存储的。`MetaDir` 指令告诉服务器元数据存储在哪个子目录下。`MetaSuffix` 指令告诉服务器元数据文件的后缀。通常，元数据文件的后缀为 `.meta`，因此 `index.html` 的元数据将存储在 `MetaDir` 指令指定的目录下的 `index.html.meta` 中。

存储在元数据中的信息类似于 HTTP 头部（参见第 2 章“基础组件”）。例如，为了向客户端发送 1998 年 7 月 5 日午夜的过期日期，你可以在元数据文件中放入行：

```
Expires: Sunday, 5-Jul-98 12:00:00 GMT
```

## ErrorDocument（错误文档）

此指令允许将 HTTP 错误代码映射到此服务器上的 URL。你可以利用此功能替换和自定义服务器的错误消息。我们将在下文的“高级配置”中详细介绍，因此现在你可以保持其被注释状态。

这就是服务器资源映射（Server Resource Map）的最后一个指令。在定义了启动所需的数值后，退出并保存 `srm.conf`。

## Server Access File（服务器访问文件）

Apache 服务器提供了广泛的功能，可以使你的网站维护变得更加方便；其中某些功能对你网站的安全有影响。服务器访问文件（位于 `/usr/local/etc/httpd/conf/access.conf`）允许你按目录启用或禁用这些功能。

此外，该文件还用于限制特定主机和用户访问你的页面；这些功能将在“访问与身份验证”部分进行详细讨论。现在，我们只需进行基础配置以使你的服务器运行。

在你的编辑器中打开 `access.conf`。随服务器分发的 `access.conf` 文件提供了三个访问描述：一个针对 `cgi-bin` 目录，第二个针对文档目录，第三个演示了你可以用于控制不同目录的几个选项。

第一个描述控制 CGI 脚本目录。注意，该文件使用了类 HTML 语法，用 `<Directory /usr/local/etc/httpd/cgi-bin>` 标签声明服务器默认 `cgi-bin` 目录部分的开始。该部分以 `</Directory>` 标签结束。

第二个指令应该如下：`<Directory /usr/local/etc/httpd/docs>`。如果你在 `httpd.conf` 中更改了文档根，也应该在 `access.conf` 中更改它。

第三个指令使用了 Apache 的新功能 `<Location>`。它与 `<Directory>` 指令的不同之处在于它指定的是 URL。URL 可以是一个目录、单个文件或通配符（`*.html`）。`httpd.conf` 中的 `<Location>` 指令设置了一个供管理员检查服务器状态的 `/status` 区域。该区域被限制只有来自 `example.com` 域的用户才能访问。如果你将 `example.com` 更改为你的域名，就可以使用此信息（假设你在在本章开始时编译了 `mod_status`）。

保存 `access.conf` 文件并退出。你现在准备好映射你的 Web 空间了。

# 设置你的 Web 空间

你可以通过多种方式选择在你的 Web 空间提供文件。如前所述 `httpd.conf` 中的 `DocumentRoot` 控制提供服务的的基础目录。服务器将 URL 映射到机器文件系统的方式如下所示：

```
http://www.example.com/home.html
```

服务器使用 `DocumentRoot` 指定的路径并附加 `home.html`。如果 `DocumentRoot` 设置为 `/usr/local/etc/httpd/docs`，服务器将从该路径提供 `home.html`。你不需要将想要提供的文件和目录放在 `ServerRoot` 目录下。你对组织网站有其他选项。

## UNIX Web 服务器

## 用户控制目录
