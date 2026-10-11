
## 表 13.12 httpd.conf 中 IndexOptions 指令可用的值（续表）。

| 选项 | 用途 | 示例 |
| :--- | :--- | :--- |
| ScanHTMLTitles | 指定从列出的任何 HTML 文件中提取 <TITLE> 标签的内容，并将其用作文件描述符。必须激活 **FancyIndexing**。 | ScanHTMLTitles |
| SuppressColumnSorting | 指定不使索引列表中的列头可点击。这将导致无法点击列头以反向排序内容。必须激活 **FancyIndexing**。 | SuppressColumnSorting |
| SuppressDescription | 指定不显示文件描述。必须激活 **FancyIndexing**。 | SuppressDescription |
| SuppressHTMLPreamble | 指定在索引列表开始时仅包含 **HeaderName** 文件的内容（如果使用了该文件），而不是同时包含文件的头部信息。 | SuppressHTMLPreamble |
| SuppressLastModified | 指定不在索引列表中显示文件最后修改的时间。必须激活 **FancyIndexing**。 | SuppressLastModified |
| SuppressSize | 指定不在索引列表中显示文件大小。 | SuppressSize |

接下来我们继续介绍更多的图标语句：

```
AddIconByEncoding (CMP, /icons/compressed.gif) x-compress x-gzip
```

**AddIconByEncoding** 语句以通用形式使用如下：

```
AddIconByEncoding *icon* *MIME-encoding*
```

该指令的 *icon* 部分可以包含两种不同的格式。第一种是直接指向图标的路径，例如 /icons/compressed.gif。第二种是刚才演示的格式，通常如下所示：

```
(ALT, /path/icon)
```

在这两种情况下，*path* 都是 URL 路径。这意味着它是相对于 DocumentRoot 的，但你必须将其作为绝对 URL 来书写，因此它必须以斜杠开头。格式中的 *ALT* 部分指的是 HTML **ALT** 项，它通常用作 <IMG> 标签中为文本浏览器提供的线索。

## 13. Apache Web 服务器

*MIME-encoding* 部分代表用于对文件进行编码或加密包装的方法。使用这种方法可以使文件传输得更快，同时在接收端机器上仍然完整且可理解。默认列出的两种编码是当今 Web 上通常使用的仅有的两种。

以下是下一个指令集：

```
AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*
```

**AddIconByType** 的使用格式与 **AddIconByEncoding** 完全相同。然而，在这种情况下，可用的类型比此处列出的要多得多。所有可用 MIME 媒体类型的当前列表由互联网号码分配机构（IANA）在 www.isi.edu/in-notes/iana/assignments/media-types/media-types 提供。

当你按类型添加时，你是在告诉 Apache 猜测文件类型。如果你想明确指定哪种文件类型使用哪种图标，请使用 **AddIcon** 指令。以下显示了前四条 **AddIcon** 行：

```
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
AddIcon /icons/world2.gif .wrl .wrl.gz .vrml .vrm .iv
```

**AddIcon** 指令以这种格式使用：

```
AddIcon icon ext
```

该指令中的 *icon* 部分是你所分配图标的路径——以绝对格式书写，但实际上相对于 DocumentRoot。为了告诉 Apache 使用此图标来显示特定类型的文件，请在 *ext* 部分放置一个以空格分隔的扩展名列表。

即使是经验丰富的 Web 管理员也无法预见到用户或客户端可能在其 Web 站点中包含的所有文件扩展名。**DefaultIcon** 指令允许你确保至少为未知文件使用某种图标：

```
DefaultIcon /icons/unknown.gif
```

接下来是更多图标索引信息：

```
#AddDescription "GZIP compressed document" .gz
#AddDescription "tar archive" .tar
#AddDescription "GZIP compressed tar archive" .tgz
```

**AddDescription** 指令将文本字符串分配给描述文件存储的格式。它是 **FancyIndexing** 指令的子选项之一。接下来是不同的索引列表详情对。你可以使用 **HeaderName** 指令来告诉 Apache 在列表顶部插入哪个文件名（如果存在），并使用 **ReadmeName** 来布置在底部显示哪个文件名。默认情况下，这些设置为以下值：

```
ReadmeName README
HeaderName HEADER
```
接下来是：

```
IndexIgnore .??* *~ *# HEADER* README* RCS
```

**IndexIgnore** 指令用于告诉 Apache 在目录中哪些项目不应在文件列表中显示。该指令的一个条目可以是以下格式之一：

-   文件扩展名。例如，.bak。
-   带通配符的部分文件名。例如，Index??。
-   完整文件名。例如，personal.txt。

某些 Web 浏览器实际上可以在加载时解压信息。目前只有某些版本的 Mosaic ([www.ncsa.uiuc.edu/SDG/Software/Mosaic/ NCSAMosaicHome.html](http://www.ncsa.uiuc.edu/SDG/Software/Mosaic/ NCSAMosaicHome.html)) 支持此功能，但希望未来会有更多浏览器支持。**AddEncoding** 指令会自动压缩发送给能够处理此功能的浏览器的信息。**AddEncoding** 的默认设置如下：

```
AddEncoding x-compress Z
AddEncoding x-gzip gz
```

**AddLanguage** 指令允许你设置在特定语言的文档末尾添加哪些扩展名。此功能对于设置多语言站点的人极有帮助。你使用此指令的格式如下：

```
AddLanguage language_code .extension
```

以下是 Apache 的默认设置：

```
AddLanguage en .en
AddLanguage fr .fr
AddLanguage de .de
AddLanguage da .da
AddLanguage el .el
AddLanguage it .it
```
你还可以设置哪些语言比其他语言更常被请求——按从最流行到最不流行的顺序——使用类似以下的行：

```
LanguagePriority en fr de
```
在此之后是：

```
<IfModule mod_php3.c>
    AddType application/x-httpd-php3 .php3
    AddType application/x-httpd-php3-source .phps
</IfModule>
```

此时你熟悉 <IfModule> 语句了。AddType 指令在表 13.6 中有简要说明。AddType 将 MIME 文件类型分配给特定的文件扩展名。因此，在此语句中，如果加载并激活了 php3 模块（你可以嵌入到 HTML 代码中的脚本语言，即超文本预处理器），则为 .php3 扩展名和 .phps（PHP3 源代码）扩展名定义了 MIME 类型。

你使用 AddType 的格式如下：

```
AddType MIME-encoding-type extension
```
下一个与 PHP 相关的语句是：

```
<IfModule mod_php.c>
    AddType application/x-httpd-php .phtml
</IfModule>
```
此模块是较旧的 PHP 实现。如果你加载并激活了它，则分配了一个新的 MIME 类型。Apache 将识别 .phtml 文件为 PHP。

在此之后是一系列被注释掉的 AddType 和 AddHandler 指令，这些指令在之前的表 13.6 中已简要介绍。AddHandler 允许你告诉 Apache 在遇到特定扩展名时运行某些程序（处理程序）。该指令的使用格式如下：

```
AddHandler program extension
```
另一个允许你指定在特定时间发生什么的指令是 **Action**。该指令的使用格式如下：

```
Action type script
```
*type* 是处理程序或 MIME 内容类型；*script* 是遇到此类型时要运行的 CGI 脚本。

现在你来到了 **Meta** 类指令。两个被注释掉的 **Meta** 指令如下：

-   **MetaDir**——包含你的元文件集合的目录
-   **MetaSuffix**——你用于元文件的后缀
接下来是一节专门针对 **ErrorDocument** 指令的被注释项目部分。你使用此指令的格式如下：

```
ErrorDocument code message
```
*code* 是你分配的错误编号。对于 *message*，你有多个选项：

-   指向外部错误页的 URL
-   指向内部错误页的 URL
-   前面带双引号的错误消息，但没有结束引号
以下是最后部分：

```
BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "MSIE 4\\.0b2;" nokeepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4\\.0" force-response-1.0
BrowserMatch "Java/1\\.0" force-response-1.0
BrowserMatch "JDK/1\\.0" force-response-1.0
```
**BrowserMatch** 指令的使用格式如下：

```
BrowserMatch expression variable
```
*expression*——通常写作为正则表达式，或 regexp——尝试匹配特定的浏览器品牌或版本，具体取决于你要查找的内容。然后，出于浏览器兼容性目的，它会激活某些 HTTP 环境变量。另一个元素 *variable* 指的是如果你希望表达式匹配浏览器类型时想要操作的变量名称。有关 *variable* 可用格式，请参见表 13.13。

