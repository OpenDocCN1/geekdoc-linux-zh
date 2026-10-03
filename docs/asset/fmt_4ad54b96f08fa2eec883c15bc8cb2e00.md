
# Apache 软件包提供的 `apxs` 应用

Apache 软件包提供的 `apxs` 应用用于构建 Apache 模块。通过 `apxs` 应用，你可以用 C 语言编译 Apache 源代码，并动态创建共享对象，这些共享对象可以通过 `LoadModule` 指令加载。`apxs` 应用要求 `mod_so` 是你的 Apache 应用程序的一部分。它包含了丰富的选项，例如用于修改模块名称的 `-n`，以及用于在你的 Web 服务器上安装该模块的 `-i`。

你可以在 Apache 网站（httpd.apache.org）以及位于你网站 Web 根目录下的 Apache 手册中找到 Apache 配置指令的完整列表。在许多系统中，它位于 `manual` 子目录中，该子目录由分发版设置了 Web 默认目录（在 Mandrake 和 Red Hat 上，这是 `/var/www/manual`）。许多常用的指令列在表 21-4 中。

# 服务器配置

某些指令用于配置你服务器的整体操作。指令放置在 `httpd.conf` 配置文件中。某些指令需要路径名，而另一些只需通过 `on` 和 `off` 关键字开启或关闭。Apache 提供了一个默认的 `httpd.conf` 配置文件。`httpd.conf` 文件已经包含了这些指令。某些指令前面带有 `#` 符号被注释掉了。你可以通过删除 `#` 号来激活指令。许多条目前面都有解释其用途的注释。以下是 `ServerAdmin` 指令的示例，用于设置用户遇到管理问题时发送邮件的地址。你将 `you@your.address` 条目替换为你想要用于接收系统管理邮件的地址。默认情况下，它被设置为 `root@localhost`。

```
# ServerAdmin: 你的地址，问题应发送至此处。

ServerAdmin you@your.address
```

某些指令需要关于你的特定信息。例如，`ServerName` 持有你 Web 服务器的主机名。指定主机名对于避免不必要的 DNS 查找失败非常重要，因为失败可能会挂起你的服务器。注意该条目前面有 `#` 注释。只需删除 `#` 并在 `new.host.name` 处输入你的 Web 服务器主机名即可。

```
# ServerName 允许你设置一个主机名，如果它与程序
# 获取的主机不同，则将该主机名发送回给客户端
#（例如，使用 "www" 而不是主机的真实名称）。
#ServerName new.host.name
```

在 Mandrake、SuSE 和 Red Hat 系统上，已经使用 `/var/www` 作为你的 Web 站点目录完成了标准的 Web 服务器安装。你可以通过更改适当的指令来根据你自己的需求定制你的 Web 站点。`DocumentRoot` 指令决定了你 Web 页面的根目录。`ServerRoot` 指令指定了你的 Web 服务器配置、错误和日志文件的存放位置。

```
DocumentRoot /var/www/html
ServerRoot /etc/httpd
```

`MaxClients` 指令设置同时连接到你服务器的最大客户端数量。

```
MaxClients 150
```

# 目录级配置：.htaccess 和 `<Directory>`

Apache 最灵活的方面之一是它配置单个目录的能力。通过 `Directory` 指令，你可以定义一个仅适用于特定目录的指令块。此类指令可以放置在 `httpd.conf` 或 `access.conf` 文件中。你也可以在特定目录中使用 `.htaccess` 文件来存放配置指令。这些指令将仅应用于该目录。`.htaccess` 的名称实际上是由 `AccessFileName` 指令设置的。如果你愿意，可以更改它。

```
AccessFileName .htaccess
```

`Directory` 块以 `<Directory pathname>` 指令开始，其中 `pathname` 是要配置的目录。结束指令使用相同的 `<>` 符号，并在“Directory”单词前加斜杠：`</Directory>`。在此块内的指令仅适用于指定的目录。以下示例拒绝来自 `www.myvids.com` 的请求对 `mypics` 目录的访问。

```
<Directory /var/www/html/mypics>
Order Deny,Allow
Deny from www.myvids.com
</Directory>
```

通过 `Options` 指令，你可以在目录中启用某些功能，例如使用符号链接、自动索引、执行脚本。默认是 `All`，启用除内容协商之外的所有功能。

```
Options Indexes FollowLinks
```

`AllowOverride` 指令控制 `.htaccess` 文件中的指令是否覆盖主配置文件中的指令。如果你的网站允许用户控制或客户端控制的目录，你可能需要仔细监控或禁用这些目录中对 `.htaccess` 文件的使用。（除非使用 `AllowOverride` 指令禁用，否则 `.htaccess` 文件中的指令可能会覆盖标准配置文件中的指令。）`all` 参数允许覆盖。`none` 参数禁用覆盖，有效地禁用 `.htaccess` 文件。

```
AllowOverride all
```

# 访问控制

通过 `allow` 和 `deny` 等访问控制指令，你可以根据远程用户和主机控制对网站的访问。`allow` 指令后跟主机列表限制对这些主机的访问。`deny` 指令带有主机列表拒绝对这些系统的访问。`all` 参数适用于所有主机。`order` 指令指定访问控制指令的顺序。其他访问控制指令，如 `require`，可以建立身份验证，要求用户登录。访问控制指令可以全局用于控制整个站点，也可以放置在 `Directory` 中以访问单个目录。在以下示例中，所有用户都被允许访问：

```
order allow,deny
allow from all
```

# Linux：完全参考

## URL 路径

某些指令可以修改或完成用于访问你网站的 URL 路径段。URL 的路径段指定了你网站上的特定目录或 Web 页面。指令允许你对路径名设置别名或重定向，还可以选择默认页面。通过 `Alias` 指令，你可以让用户访问位于系统其他部分、其他文件系统或其他网站上的资源。别名可以使用互联网网站的 URL，而不是你系统上目录的路径名。通过 `Redirect` 指令，你可以将用户重定向到另一个网站。

```
Alias /mtrain /home/dylan/trainproj
Redirect /mycars http://www.myautos.com/mycars
```

如果 Apache 只被赋予访问一个目录，而不是特定的网页，它会查找该目录下的索引网页并显示它。默认网页的可能名称由 `DirectoryIndex` 指令列出。通常使用的名称是 `index.html`，但你可以添加其他名称。标准名称在此显示。当 Apache 只被赋予一个 Web 目录进行访问时，它会查找并显示位于其中的 `index.html` 网页。

```
DirectoryIndex index.html index.shtml index.cgi
```

Apache 还允许用户在用户主目录的特殊子目录下维护 Web 页面，而不是在主网站目录下。使用 `~` 加上用户名即可访问此目录。该目录的名称通过 `UserDir` 指令指定。默认名称为 `public_html`，如下所示。网站 `turtle.mytrek.com/~dylan` 访问主机 `turtle.mytrek.com`上的 `turtle.mytrek.com/home/dylan/public_html` 目录。

```
UserDir public_html
```

## MIME 类型

当浏览器访问网站上的 Web 页面时，它通常正在访问许多不同对象，包括 HTML 文件、图片或声音文件以及脚本文件。为了正确显示这些对象，浏览器必须知道它们是种类的对象。JPEG 文件的处理方式与简单的文本文件不同。服务器以 MIME 类型的形式（见第 13 章）提供这种类型信息。MIME 类型与通过 Pine 等互联网邮件程序发送附件时使用的类型相同。每种对象都关联一个特定的 MIME 类型。提供了 MIME 类型后，浏览器就能正确处理并显示该对象。

协议将特定类型与特定扩展名的文件关联。例如，带有 `.jpg` 扩展的文件具有 MIME 类型 `image/jpeg`。`TypesConfig` 指令持有 `mime.types` 文件的位置，该文件列出了所有的 MIME 类型及其关联的文件扩展名。`DefaultType` 是任何无法确定类型的文件的默认 MIME 类型。`AddType` 允许你在不编辑 MIME 文件的情况下修改 `mime.types` 列表。

```
TypesConfig /etc/mime.types
DefaultType text/plain
```

其他指令用于指定对某些文档执行的操作。`AddEncoding` 将压缩文件扩展名映射到操作，而 `AddLanguage` 允许你指定文档的语言。以下示例将带有 `.gz` 扩展的文件名映射为 gzip 编码文件，将带有 `.fr` 扩展的文件映射为法语文件：

```
AddEncoding x-gzip gz
AddLanguage fr .fr
```

Web 服务器可以显示并执行许多不同类型的文件和程序。然而，并不是所有的 Web 浏览器都能显示所有这些文件。旧浏览器限制性最大。某些浏览器（如 Lynx）的设计甚至无法显示简单的图形。为了允许 Web 浏览器显示页面，服务器会与其进行协商，以确定它可以处理的文件类型。要启用此类协商，你需要启用 `multiviews` 选项。

- Option multiviews

## CGI 文件

通用网关接口 (CGI) 文件是由 Web 浏览器访问你的网站时可以执行的程序。CGI 文件通常由 Web 页面启动，作为其显示内容的一部分。传统上，CGI 程序被放在名为 `cgi-bin` 的目录中，并且只有当它们位于特殊目录时才能被执行。通常，每个网站只存在一个 `cgi-bin` 目录。发行版通常在默认 Web 服务器目录下设置一个 `cgi-bin` 目录（`/var/www/cgi-bin/ ...`）。在这里，你可以放置任何可以在网站上执行的 CGI 程序。`ScriptAlias` 指令为你的 `cgi-bin` 目录指定别名。任何 Web 页面或浏览器都可以使用该别名引用此目录。

- ScriptAlias /cgi-bin/ /var/www/cgi-bin/

如果你想执行位于网站上任何位置的 CGI 程序，可以指定带有 `.cgi` 扩展的文件被视为可执行的 CGI 程序。你可以通过 `AddHandler` 指令实现此操作。它对给定类型的文件应用某些处理器。用于此操作的 handler 指令包含在 Apache 源码文件提供的默认 `httpd.conf` 文件中，尽管它被注释掉了。你可以删除注释符号 (`#`) 来启用它。

```
AddHandler cgi-script cgi
```

## 自动目录索引

当给的是目录的 URL 而不是 HTML 文件，且目录中没有默认网页时，Apache 会动态创建一个页面并显示它。这通常只是目录中不同文件的列表。实际上，Apache 为你索引了这些项目。你可以为生成和显示此类索引设置若干候选项。如果开启了 `FancyIndexing`，Web 页面项将带有图标和列头显示，这些头可以用于对列表进行排序。

```
FancyIndexing on
```

图标设备告诉 Apache 为特定类型的文件显示什么图标。`AddIconByType` 和 `AddIconByEncoding` 指令使用 MIME 类型信息来确定文件类型，然后将指定的图像与其关联。`AddIcon` 使用文件的扩展名来确定其类型。在示例中，扩展名为 `.txt` 的文本文件将显示 `text.gif` 。你也可以使用 `AddIcon` 将图像与特定文件关联。`DefaultIcon` 指令指定用于未确定类型的图像。

```
AddIcon /icons/text.gif .txt
DefaultIcon /icons/unknown.gif
AddIconByType (VID,/icons/movie.gif) video/*
```

通过 `AddDescription` 指令，你可以为文件名条目添加简短的描述短语。该描述可以应用于单个文件或特定模式的文件名。

```
AddDescription "Reunion pictures" /var/www/html/reunion.html
```

在目录内，你可以放置特殊文件，用于在生成的列表之前之后显示某些文本。`HeaderName` 指令用于设置在列表之前插入文本的文件名。`ReadmeName` 指令设置在列表末尾放置文本的文件名。你可以在 `.htaccess` 文件或 `<Directory>` 块中使用这些指令来选择目录内的特定文件。`Readme` 指令通常被设置为 `readme`，而 `HeaderName` 设置为 `HEADER`。在那种情况下，Apache 会在目录中搜索名为 `README` 的文件。

```
HeaderName HEADER
ReadmeName README
```

通过 `IndexOptions` 指令，你可以为显示索引设置不同的选项。索引选项用于设置图标的高度和宽度。`IconsAreLinks` 选项使文件名锚点成为链接。`ScanHTMLTitles` 选项读取 HTML 文档中的标题并使用它们显示索引中的项。对于不同的索引功能（如排序、描述以及头部/readme 插入），存在多种选项。你可以使用 Directory 块或 .htaccess 文件为单个目录设置选项。通常，在高级目录中设置的选项会被低级目录继承。如果你使用 `IndexOption` 指令设置新选项，所有继承的选项将被清除。如果你想保留继承的选项，可以使用加 (+) 或减 (-) 符号设置选项。添加或删除选项。然而，如果你在没有加减符号的情况下设置选项，所有继承的选项将被清除。

```
IndexOptionsLinks FancyIndexing
IndexOptions +ScanHTMLTitles
```

## 身份验证

你的 Web 服务器还可以按用户或组控制网站上特定目录的访问。你需要不同级别的身份验证。访问可以限制为特定用户并要求密码，也可以扩展为组员访问。你可以完全放弃密码，或者设置匿名访问类型，如 FTP。

要将身份验证指令应用于特定目录，你需要将它们放置在 Directory 块或目录的 `.htaccess` 文件中。你使用 `require` 指令来确定哪些用户可以访问目录。你可以列出特定的用户或组。`AuthName` 指令向用户提供验证域，用于识别通过此验证过程访问的特定资源的名称。`AuthType` 指令指定身份验证类型，例如 basic 或 digest。`require` 指令还需要 `AuthType`、`AuthName` 以及指定组和用户验证文件位置的指令。在以下示例中，用户 george、 robert 和 mark 被允许访问 newpics 目录：

```
<Directory /var/www/html/newpics
AuthType Basic
AuthName web
AuthFile /web/users
AuthGroupFile /web/groups
<Limit GET POST>
require users george robert mark
</Limit>
</Directory>
```

下一个示例允许管理员通过组访问 CGI 目录：

```
<Directory /var/www/html/cgi-bin
AuthType Basic
AuthName CGI
AuthGroupFile /web/groups
<Limit GET POST>
require groups admin
</Limit>
</Directory>
```
