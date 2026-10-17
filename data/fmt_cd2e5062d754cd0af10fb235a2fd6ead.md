
## 显示花哨的目录索引
这会打开目录的花哨索引，这意味着文件和目录将提供图标。这配置了 `FancyIndexing` 子指令。

## 显示 HTML 标题作为描述
如果目录中的文件包含 HTML 标题信息，则这些标题将作为其各自文件的名称显示。此选项配置 `ScanHTMLTitles` 子指令。

## 图标高度
这设置花哨目录列表中图标的高度。这对应于 `IconHeight` 子指令。

## 图标宽度
这设置花哨目录列表中图标的宽度。这对应于 `IconWidth` 子指令。

## 允许用户对列进行排序
默认情况下，Apache 将生成可通过单击列标题进行排序的列表。如果您不希望用户能够按最后修改日期或大小排序，则可以禁用此功能，且不会提供排序链接。此选项配置 `SuppressColumnSorting` 子指令。

## 显示文件描述
启用此项以在花哨的索引列表中显示文件的描述。此选项对应于 `SuppressDescription` 子指令。

## 输出 HTML 头部标签
如果使用头部文件（也在此页面配置）用于目录索引，您可以选择允许 Apache 输出包含足够内容以开始合法 HTML 页面的标准 HTML 前言。如果禁用此项，您的头部必须包含自己的前言才能成为合法的 HTML 页面。此选项配置 `SuppressHTMLPreamble` 子指令。

## 显示最后修改时间
默认情况下，Apache 将在生成的索引中显示每个文件的最后修改时间。取消选择此选项将导致 Apache 不这样做。此选项配置 `SuppressLastModified` 子指令。

## 显示文件大小
此选项与上一个选项类似，只是它允许您禁用在生成的索引中显示所列文件大小信息。此选项对应于 `SuppressSize` 子指令。

## 链接中包含图标
这将导致 Apache 将图标显示为链接的一部分。此选项配置 `IconsAreLinks` 子指令。

## 文件名宽度
在此处您可以配置 Apache 在索引中显示的文件名的字符数。此选项对应于 `NameWidth` 子指令。如果将其设置为 `*`，Apache 将长度设置为目录中最长文件名的长度。

## 描述宽度
在生成的索引中描述字段将显示的字符数。此选项对应于 `DescriptionWidth` 子指令。如上所述，如果此值设置为 `*`，描述长度将设置为目录中最长描述的长度。

## 先显示目录
您可以选择让 Apache 对列表进行排序，使目录在索引中先列出。此选项对应于 `FoldersFirst` 子指令。

## 目录索引文件
在此处配置 Apache 在进入目录时查找的文件名，如果其中一个存在，它将被显示为目录的索引，而不是自动生成的文件索引。此文件将显示给在 URL 末尾指定 `/` 请求服务器上任何目录的客户端。这可以是任何文件名或文件名列表，尽管按惯例使用的包括在文件名有限制的操作系统上的 `index.html` 或 `index.htm`。现在使用脚本后缀的索引页面也很常见，例如 `index.pl`、`index.cgi` 或 `index.php`。此选项对应于 `DirectoryIndex` [`http://httpd.apache.org/docs/mod/mod_dir.html#directoryindex`] 指令。

## 目录索引中忽略的文件
如果正在显示自动生成的索引，您可以指定不应在索引中列出的文件。此选项配置 `IndexIgnore` [`http://httpd.apache.org/docs/mod/mod_autoindex.html#indexignore`] 指令。

## 目录索引默认图标
当识别文件的类型时，Apache 会自动向索引列表添加图标。当文件类型的图标未知时，您可以在此处配置要显示的图标。此选项对应于 `DefaultIcon` [`http://httpd.apache.org/docs/mod/mod_autoindex.html#defaulticon`] 指令。

## 目录索引页眉文件
索引可以使用此选项附加自定义页眉文件。该文件可以是纯文本文件或 HTML 文件。此选项对应于 `HeaderName` 指令 [`http://httpd.apache.org/docs/mod/mod_autoindex.html#headername`]。

## 目录索引页脚文件
设置附加到索引末尾的文件路径。此选项对应于 `ReadmeName` 指令 [`http://httpd.apache.org/docs/mod/mod_autoindex.html#readmename`]。

## 按...排序目录索引
此选项允许您选择 Apache 将如何对索引页上的条目进行排序。顺序可以是升序或降序，并且可以根据文件的名称、最后修改日期、文件大小或文件的描述进行排序。此选项对应于 `IndexOrderDefault` [`http://httpd.apache.org/docs/mod/mod_autoindex.html#indexorderdefault`] 指令，默认按文件名的升序排序。

## 目录索引图标
在此您可以选择将在花哨的目录列表索引页面中文件名称链接旁边显示的图形图标。`Icon` 是指向图像文件的相对路径。`Alt` 文本是在客户端浏览器不支持图像时要显示的文本。`Match by` 是在决定显示哪个图标时要匹配的属性，它可以是 `Filename`、`MIME` 类型或 `Encoding`。`Filenames`、`Types` 或 `Encodings` 只是要为此图标类型显示而匹配的术语。此选项配置 `AddIcon` [`http://httpd.apache.org/docs/mod/mod_autoindex.html#addicon`]、`AddIconByEncoding` [`http://httpd.apache.org/docs/mod/mod_autoindex.html#addiconbyencoding`] 和 `AddIconByType` 指令 [`http://httpd.apache.org/docs/mod/mod_autoindex.html#addiconbytype`]。当根据文件名匹配 MIME 类型时，您可以使用通配符来匹配多种变体。例如，要匹配所有备份文件（如 `ispell` 和其他软件生成的），您可以使用文件匹配 `*~`，或者，对于 MIME 类型通配符示例，要匹配所有图像类型，您可以使用 `image/*`。通常建议尽可能基于 MIME 类型而不是文件扩展名进行匹配，因为它不太容易遗漏某些类型的文件或错误识别文件类型。

> NOTE 在添加文件名匹配图标时，有几个特殊名称可用于匹配目录和空白行（Apache 使用空白行来格式化列表）。它们分别是 `^*DIRECTORY^*` 和 `^*BLANKICON^*`。

## 目录索引 ALT 标签
与前一个选项类似，此选项允许您配置为文件显示的文本而不是图标。可能的值和通配符用法与前一个选项相同。这配置了 `AddAlt` [`http://httpd.apache.org/docs/mod/mod_autoindex.html#addalt`]、`AddAltByEncoding` [`http://httpd.apache.org/docs/mod/mod_autoindex.html#addaltbyencoding`] 和 `AddAltByType` [`http://httpd.apache.org/docs/mod/mod_autoindex.html#addaltbytype`] 指令。

## 目录索引描述
在此您可以定义将为给定文件扩展名显示的描述。其长度将受上面讨论的 `Description width` 选项限制。此选项配置 `AddDescription` [`http://httpd.apache.org/docs/mod/mod_autoindex.html#adddescription`] 指令。

## Imagemaps
`Imagemaps` 提供了一种使图像区域可点击的方法，其中每个区域导致不同的 URL。此页面上的选项规定了 `imagemap` URL 的默认路径、`imagemap` 中的点击要采取的操作以及错误条件的处理。

## Imagemaps 的默认基目录
此选项设置 `imagemaps` 的基目录。如果未设置，默认值为 `http://servername/`。这对应于 `ImapBase` [`http://httpd.apache.org/docs/mod/mod_imap.html#imapbase`] 指令。

## Imagemaps 的默认操作
设置在 `imagemap` 文件中使用的默认值。这将被 `imagemap` 文件中的默认指令覆盖。默认值为 `nocontent` 或不执行任何操作，这会向浏览器发送 204 No content 消息。浏览器应继续显示原始页面。此选项对应于 `ImapDefault` [`http://httpd.apache.org/docs/mod/mod_imap.html#imapdefault`] 指令。

## Imagemaps 的错误使用操作
