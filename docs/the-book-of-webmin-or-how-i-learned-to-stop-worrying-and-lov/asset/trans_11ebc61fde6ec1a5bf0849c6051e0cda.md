

## Regexp 文档目录别名

此选项与上面非常相似，只是它允许使用正则表达式来匹配要翻译的路径。此选项对应于 AliasMatch [http://httpd.apache.org/docs/mod/mod_alias.html#aliasmatch] 指令。有关正则表达式的更多信息，请参阅 regex 手册页。

## URL 重定向

此选项将旧 URL 重定向到新 URL。新 URL 将返回给客户端，客户端将尝试使用新地址再次获取。您还可以为重定向指定状态消息，可以是以下所述的几个 HTTP 状态代码之一。此选项配置 Redirect [http://httpd.apache.org/docs/mod/mod_alias.html#redirect] 指令。

## 重定向状态代码

| Code | Description |
|------|-------------|
| 301 | 永久移动。 |
| 302 | 临时移动。 |
| 303 | 查看其他，意味着资源已被替换。 |
| 410 | 对象不再可用。使用此状态时，重定向 To URL 应省略。 |

## Regexp URL 重定向

此选项的行为与上面完全相同，只是 From 字段可以包含用于匹配的正则表达式。此选项对应于 RedirectMatch [http://httpd.apache.org/docs/mod/mod_alias.html#redirectmatch] 指令。

## 永久 URL 重定向

此选项的行为与上面 URL 重定向相同，状态为 301（永久移动）。对应于 RedirectPermanent [http://httpd.apache.org/docs/mod/mod_alias.html#redirectperm] 指令。

## 临时 URL 重定向

此选项的行为与上面 URL 重定向相同，状态为 302（临时移动）。对应于 RedirectTemp [http://httpd.apache.org/docs/mod/mod_proxy.html#redirecttemp] 指令。

## 将本地映射到远程 URL

此选项允许将远程服务器映射到本地服务器的空间上；本地服务器不充当常规代理，而是看起来是远程服务器的镜像。例如，如果本地 URL 为 /mirror/otherdomain 而远程 URL 为 http://www.otherdomain.com，则用户将能够通过 http://www.thisdomain.com/mirror/otherdomain 访问 http://www.otherdomain.com。此选项对应于 ProxyPass [http://httpd.apache.org/docs/mod/mod_proxy.html#proxypass] 指令。

## 将远程 Location 头映射到本地

此选项提供与上一个选项大致相反的功能。它调整 HTTP 间接响应的 location 头，这在使用 Apache 作为反向代理时是必要的，以避免反向代理被重定向请求绕过。此选项配置 ProxyPassReverse [http://httpd.apache.org/docs/mod/mod_proxy.html#proxypassreverse] 指令。

## 目录索引

Apache 中的索引只是在客户端浏览服务器上的目录而不是对象或文档时显示的页面。例如，如果有人浏览我服务器上的 Squid 补丁目录，该目录位于 http://www.swelttech.com/pengies/joe/patches/，Apache 将提供一个索引页面。如果目录中没有与 Apache 的索引页面定义匹配的文件，它将改为生成包含文件列表的索引页面，或者如果禁止生成索引，则提供错误页面。此页面允许您配置 Apache 在显示索引页面时的行为。

## 目录索引选项

此选项设置 Apache 生成的索引的外观和包含的信息。此选项配置 IndexOptions [http://httpd.apache.org/docs/mod/mod_autoindex.html#indexoptions] 指令。以下选项可用：

- **显示花哨的目录索引** 这会打开目录的花哨索引，这意味着文件和目录将提供图标。这配置了 FancyIndexing 子指令。
- **显示 HTML 标题作为描述** 如果目录中的文件包含 HTML 标题信息，则这些标题将作为其各自文件的名称显示。此选项配置 ScanHTMLTitles 子指令。
- **图标高度** 这设置花哨目录列表中图标的高度。这对应于 IconHeight 子指令。
- **图标宽度** 这设置花哨目录列表中图标的宽度。这对应于 IconWidth 子指令。
- **允许用户对列进行排序** 默认情况下，Apache 将生成可通过单击列标题进行排序的列表。如果您不希望用户能够按最后修改日期或大小排序，则可以禁用此功能，且不会提供排序链接。此选项配置 SuppressColumnSorting 子指令。
- **显示文件描述** 启用此项以在花哨的索引列表中显示文件的描述。此选项对应于 SuppressDescription 子指令。
- **输出 HTML 头部标签** 如果使用头部文件（也在此页面配置）用于目录索引，您可以选择允许 Apache 输出包含足够内容以开始合法 HTML 页面的标准 HTML 前言。如果禁用此项，您的头部必须包含自己的前言才能成为合法的 HTML 页面。此选项配置 SuppressHTMLPreamble 子指令。

## 显示最后修改时间

默认情况下，Apache 将在生成的索引中显示每个文件的最后修改时间。取消选择此选项将导致 Apache 不这样做。此选项配置 SuppressLastModified 子指令。

## 显示文件大小

此选项与上一个选项类似，只是它允许您禁用在生成的索引中显示所列文件大小信息。此选项对应于 SuppressSize 子指令。

## 链接中包含图标

这将导致 Apache 将图标显示为链接的一部分。此选项配置 IconsAreLinks 子指令。

## 文件名宽度

在此处您可以配置 Apache 在索引中显示的文件名的字符数。此选项对应于 NameWidth 子指令。如果将其设置为 *，Apache 将长度设置为目录中最长文件名的长度。

## 描述宽度

在生成的索引中描述字段将显示的字符数。此选项对应于 DescriptionWidth 子指令。如上所述，如果此值设置为 *，描述长度将设置为目录中最长描述的长度。

## 先显示目录

您可以选择让 Apache 对列表进行排序，使目录在索引中先列出。此选项对应于 FoldersFirst 子指令。

## 目录索引文件

在此处配置 Apache 在进入目录时查找的文件名，如果其中一个存在，它将被显示为目录的索引，而不是自动生成的文件索引。此文件将显示给在 URL 末尾指定 / 请求服务器上任何目录的客户端。这可以是任何文件名或文件名列表，尽管按惯例使用的包括在文件名有限制的操作系统上的 index.html 或 index.htm。现在使用脚本后缀的索引页面也很常见，例如 index.pl、index.cgi 或 index.php。此选项对应于 DirectoryIndex [http://httpd.apache.org/docs/mod/mod_dir.html#directoryindex] 指令。

## 目录索引中忽略的文件

如果正在显示自动生成的索引，您可以指定不应在索引中列出的文件。此选项配置 IndexIgnore [http://httpd.apache.org/docs/mod/mod_autoindex.html#indexignore] 指令。

## 目录索引默认图标

当识别文件的类型时，Apache 会自动向索引列表添加图标。当文件类型的图标未知时，您可以在此处配置要显示的图标。此选项对应于 DefaultIcon [http://httpd.apache.org/docs/mod/mod_autoindex.html#defaulticon] 指令。

