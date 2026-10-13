
`order allow,deny`

`allow all`

</Limit>

</Directory>

控制规则从上级目录继承到下级目录。如果你想对你的 Web 站严格地按目录控制访问，可以使用以下条目拒绝所有用户的访问。然后，在各个目录中，你可以允许某些用户、组或主机的访问。

```
<Directory /var/www/html>

Order Deny,Allow

Deny from All

</Directory>
```

# URL 路径名

某些指令可以修改或完成访问你站点的 URL 路径段。URL 的路径段指定了你站点上的特定目录或 Web 页面。指令允许你对路径名进行别名或重定向，还可以选择默认页面。通过 `Alias` 指令，你可以让用户访问位于系统其他部分、其他文件系统或其他 Web 站上的资源。`Alias` 可以用于互联网上站点的 URL，重定向你系统的路径名。通过 `Redirect` 指令，你可以重定向到另一个站点。

```
Alias /mytrain /home/dylan/trainproj

Redirect /mycars http://www.myautos.com/mycars
```

如果只给 Apache 提供一个目录进行访问，而不是特定的 Web 页面，它会在该目录下查找一个索引 Web 页面并显示它。默认 Web 页面的可能名称由 `DirectoryIndex` 列出。通常使用的名称是 `index.html`，但你也可以使用其他的。标准名称在此显示。当只给 Apache 提供一个 Web 目录访问时，它会查找并显示其中的 `index.html` Web 页面。

```
DirectoryIndex index.html index.shtml index.cgi
```

Apache 允许你维护位于用户主目录下特殊子目录中的 Web 页面，而不是主 Web 站目录。使用 `~` 后跟用户名可以访问此目录。该目录的名称通过 `UserDir` 指令指定。默认名称是 `public_html`，如下所示。`dylan` 访问 `/home/dylan/public_html`。

`UserDir public_html`

# MIME 类型

当浏览器访问 Web 站点上的页面时，它经常访问许多类型的对象，包括 HTML 文件、图片或声音文件以及脚本。为了正确显示这些对象，浏览器必须拥有它们是什么种类型的指示。JPEG 图片文件的处理方式与简单的文本文件不同。服务器以 MIME 类型的形式提供这种信息。第 14 章。每种对象都与给定的 MIME 类型关联。提供了 MIME 类型，浏览器就能正确处理并显示该对象。

MIME 协议访问特定扩展名的类型。例如，具有 `.jpg` 扩展的文件具有 `image/jpeg` MIME 类型。`TypesConfig` 指令持有 `mime.types` 文件的位置，该文件列出了所有的 MIME 类型及其关联的文件。`DefaultType` 是任何无法确定文件的 MIME 类型。`AddType` 允许你在不编辑 MIME 文件的情况下修改类型列表。

```
TypesConfig /etc/mime.types

DefaultType text/plain
```

其他指令用于对特定文档指定操作。`AddEncoding` 允许动态压缩文件。`AddHandler` 将文件扩展映射到操作，`AddLanguage` 为文档指定语言。此示例显示 `.gz` 扩展用于 gzip 编码文件，`.fr` 扩展用于法语语言文件：

```
AddEncoding x-gzip gz

AddLanguage fr .fr
```

# CGI 文件

CGI 文件是浏览器访问你的站点时可以执行的程序。CGI 文件作为显示内容的一部分执行程序。传统上，CGI 程序被放置在名为 `cgi-bin` 的目录中，并且当它们位于特殊目录时才能被执行。通常，每个 Web 站点存在一个 `cgi-bin` 目录。Red Hat 在 `/var/www` 目录中设置了一个 `cgi-bin` 目录，即 `/var/www/cgi-bin`。在这里，你放置任何可以的 CGI 程序

在您的网站上执行。`ScriptAlias` 指令为您的 `cgi-bin` 目录指定一个别名。任何 Web 页面或浏览器可以使用该别名来引用此目录。

```
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
```

如果您想执行位于 Web 网站任何位置的 CGI 程序，可以指定具有 `.cgi` 扩展名的文件被处理为可执行的 CGI 程序。您可以使用 `AddHandler` 指令来实现此。该指令对给定类型的文件应用处理程序。用于此目的 `AddHandler` 指令包含在 Apache 源代码文件提供的默认 `httpd.conf` 文件中，尽管它们被注释掉了。您可以移除注释符号（`#`）来启用它。

```
AddHandler cgi-script cgi
```

# 自动目录索引

当给定目录的 URL 而不是 HTML 文件，且目录中没有默认 Web 页面时，Apache 会动态创建一个页面并显示它。这通常只是目录中不同文件的列表。实际上，Apache 为您索引了目录中的项目。您可以选择几个选项来生成和显示此类索引。当开启 `FancyIndexing` 时，Web 页面将带有图标和列标题显示，这些内容可用于列表。

`FancyIndexing on`

`AddIcon` 告诉 Apache 为特定类型的文件显示什么图标。`AddIconByType` 和 `AddIconByEncoding` 指令使用 MIME 类型信息来确定文件类型，然后将指定的图像与其关联。`AddIcon` 使用文件的扩展名来确定其类型。在下一个示例中，`text.gif` 将被显示于具有 `.txt` 扩展名的文本文件。您还可以使用 `AddIcon` 将图像与特定文件关联。`DefaultIcon` 指定用于未知类型文件的图像。

```
AddIcon /icons/text.gif .txt

DefaultIcon /icons/unknown.gif

AddIconByType TYPE(VIDEO,/icons/movie.gif) video/*
```

通过 `Description` 指令，您可以为文件名条目添加一个短短语。该描述可以应用于单个文件，也可以应用于特定模式的文件。

```
AddDescription "Reunion pictures" /var/www/html/reunion.html
```

在目录内，您可以放置特殊文件以便在列表的前后都显示文本。`HeaderName` 指令用于设置在列表之前插入文本的文件名。`ReadName` 指令设置在列表末尾放置文本的文件名。您可以在 `.htaccess` 或 `<Directory>` 块中使用这些指令来选择目录内的特定文件。`ReadName` 指令通常设置为 `README`，`HeaderName` 设置为 `HEADER`。在这种情况下，Apache 在目录中搜索名为 `HEADER` 和 `README` 的文件。

```
HeaderName HEADER

ReadName README
```

通过 `IndexOptions` 指令，您可以为生成的索引设置不同的选项。存在用于设置图标和文件名高宽的选项。`IconsAreLinks` 选项使文件名成为锚点的一部分。`ScanHTMLTitles` 选项读取 HTML 文档中的标题，并使用它们在索引列表中显示条目，而不是文件名。存在多种选项来抑制索引功能，如排序、描述以及页眉/页脚插入。可以使用 `Directory` 块或 `.htaccess` 文件为单个目录设置选项。通常情况下，在较级目录中设置的选项会被较低级目录继承。如果您使用 `Index` 指令设置任何新选项，之前继承的选项将被清除。如果您想保留继承的选项，可以使用 `(+)` 或 `(-)` 符号设置选项。添加或移除选项。尽管如此，如果您也使用 `+` 或 `-` 符号设置了选项，所有继承的选项将被清除。

```
IndexOptions IconsAreLinks FancyIndexing

IndexOptions+ScanHTMLTitles
```
