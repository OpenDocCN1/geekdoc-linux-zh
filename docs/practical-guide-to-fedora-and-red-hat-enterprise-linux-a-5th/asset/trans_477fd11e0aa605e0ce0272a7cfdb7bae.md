

## 控制内容的指令

### AddHandler
*创建文件名扩展名与内置 Apache 处理程序之间的映射。*

```
AddHandler handler extension [extension] ...
```

其中 *handler* 是内置处理程序的名称，*extension* 是映射到 *handler* 的文件名扩展名。处理程序是内置于 Apache 中且与已加载模块直接相关的操作。当客户端请求具有指定文件名扩展名的文件时，Apache 会使用相应的处理程序。

例如，以下 AddHandler 指令使 Apache 使用 cgi-script 处理程序来处理文件名扩展名为 .cgi 的文件：

```
AddHandler cgi-script .cgi
```

上下文：服务器配置，虚拟主机

默认值：无

Fedora/RHEL：type-map 变量

### Alias
*将 URI 映射到目录或文件。*

```
Alias alias pathname
```

其中 *alias* 必须匹配客户端请求的 URI 的一部分以调用别名，而 *pathname* 是别名目标的绝对路径名，通常是一个目录。

例如，以下别名使得当客户端请求 http://www.example.com/pilk.jpg 时，Apache 提供 /usr/local/pix/milk.jpg：

```
Alias /pix /usr/local/pix
```

在某些情况下，你需要使用 <Directory> 容器（第 855 页）来授予对别名内容的访问权限。

上下文：服务器配置，虚拟主机

默认值：无

Fedora/RHEL：提供两个别名，一个用于 /icons/，另一个用于 /error/

### ErrorDocument
*指定 Apache 在发生指定错误时采取的操作。*

*ErrorDocument code action*
其中 **code** 是该指令定义响应的错误代码（第 882 页），而 **action** 是以下之一：

-   **string:** 定义 Apache 返回给客户端的消息。
-   **absolute pathname**：指向本地脚本或其他内容，Apache 会将客户端重定向到该内容。
-   **URL**：指向外部脚本或其他内容，Apache 会将客户端重定向到该内容。

如果你未针对给定的错误代码指定此指令，当发生该错误时，Apache 会返回硬编码的错误消息。有关 *ErrorDocument* 指令如何在系统首次安装时返回 Fedora/RHEL 测试页面的解释，请参阅第 872 页。

以下是一些 *ErrorDocument* 指令的示例：

```
ErrorDocument 403 "Sorry, access is forbidden."
ErrorDocument 403 /cgi-bin/uh-uh.pl
ErrorDocument 403 http://errors.example.com/not_allowed.html
```

上下文：服务器配置，**虚拟主机**，目录，**.htaccess**

默认值：无；Apache 返回硬编码的错误消息

Fedora/RHEL：403 ***/error/noindex.html***；请参阅第 872 页的“Fedora/RHEL 测试页面”。

### IndexOptions
*指定 Apache 如何显示目录列表。*

*IndexOptions [*|*+]*option* [*|*+option]* ...*
其中 **option** 可以是以下选项的任何组合：

-   **DescriptionWidth=n:** 将描述列的宽度设置为 **n** 个字符。使用 **\*** 代替 **n** 以适应最宽的描述。
-   **FancyIndexing:** 在目录列表中，显示作为链接的列标题。点击其中一个链接时，Apache 会根据列的内容对显示内容进行排序。第二次点击会反转顺序。
-   **FoldersFirst:** 对列表进行排序，使目录位于普通文件之前。仅与 FancyIndexing 一起使用。
-   **HTMLTable**: 以表格形式显示目录列表。
-   **IconsAreLinks**: 使图标可点击。仅与 FancyIndexing 一起使用。
-   **IconHeight=n**: 将图标的高度设置为 **n** 像素。仅与 IconWidth 一起使用。
-   **IconWidth=n**: 将图标的宽度设置为 **n** 像素。仅与 IconHeight 一起使用。
-   **IgnoreCase**: 在排序名称时忽略大小写。
-   **IgnoreClient**: 忽略客户端在 URL 中提供的选项。
-   **NameWidth=n**: 将文件名列的宽度设置为 **n** 个字符。使用 * 代替 **n** 以适应最长的文件名。
-   **ScanHTMLTitles**: 从 HTML 文档中提取并显示标题。仅与 FancyIndexing 一起使用。通常不使用，因为它对 CPU 和磁盘密集。
-   **SuppressColumnSorting**: 抑制可用于对列进行排序的可点击列标题。仅与 FancyIndexing 一起使用。
-   **SuppressDescription**: 抑制文件描述。仅与 FancyIndexing 一起使用。
-   **SuppressHTMLPreamble**: 即使指定文件存在，也抑制 HeaderName 指令指定的文件的内容。
-   **SuppressIcon**: 抑制图标。仅与 FancyIndexing 一起使用。
-   **SuppressLastModified**: 抑制修改日期。仅与 FancyIndexing 一起使用。
-   **SuppressRules**: 抑制水平线。仅与 FancyIndexing 一起使用。
-   **SuppressSize**: 抑制文件大小。仅与 FancyIndexing 一起使用。
-   **VersionSort**: 以自然方式对版本号（在文件名中）进行排序；除了数字子串以外的字符字符串不受影响。

作为一个例子，假设客户端请求一个指向目录的 URI（例如 http://www.example.com/support/），并且该目录中不存在 DirectoryIndex 指令（第 853 页）指定的任何文件。如果目录层级由 .htaccess 文件控制，并且 AllowOverride（第 869 页）已设置为允许索引，那么 Apache 将根据此指令指定的选项显示目录列表。

如果此指令在目录中出现多次，Apache 会合并来自这些指令的选项。使用 + 和 - 将选项与上层目录的选项合并。（除非你对所有选项都使用 + 或 -，否则 Apache 会丢弃在上层目录中设置的任何选项。）例如，以下指令和容器将 /custsup/download 的选项设置为 VersionSort；由于第二个 <Directory> 容器中的 VersionSort 前没有 + 或 -，Apache 会丢弃 download 目录中的 FancyIndexing 和 IgnoreCase：

```
<Directory /custsup>
    IndexOptions FancyIndexing
    IndexOptions IgnoreCase
</Directory>

<Directory /custsup/download>
    IndexOptions VersionSort
</Directory>
```

由于 VersionSort 前出现了 +，下一个指令和容器将 /custsup/download 的选项设置为 FancyIndexing、IgnoreCase 和 VersionSort：

```
<Directory /custsup>
    IndexOptions FancyIndexing
    IndexOptions IgnoreCase
</Directory>

<Directory /custsup/download>
    IndexOptions +VersionSort
</Directory>
```

上下文：**服务器配置**，**虚拟主机**，**目录**，**.htaccess**

默认值：无；仅列出文件名

Fedora/RHEL：FancyIndexing VersionSort NameWidth=* HTMLTable

仅 Fedora：Charset=UTF-8

### ServerRoot directory
*指定服务器文件的根目录（不是内容）。*

其中 *directory* 指定构成服务器的文件的根目录的路径名。Apache 会在 **httpd.conf** 中的相对路径名前添加 *directory*。此指令不指定 Apache 提供的内容的存储位置；DocumentRoot 指令（第 852 页）执行此功能。除非你移动了服务器文件，否则不要更改此值。

-   上下文：**服务器配置**
-   默认值：/usr/local/apache
-   Fedora/RHEL：/etc/httpd

### ServerTokens
*指定 Apache 返回给客户端的服务器信息。*

```
ServerTokens Prod | Major | Minor | Min | OS | Full
```

*Prod:* 返回产品名称（**Apache**）。也称为 **ProductOnly**。

*Major:* 返回服务器的主发行版号（**Apache/2**）。

*Minor:* 返回服务器的主次发行版号（**Apache/2.2**）。

*Minimal:* 返回完整版本（**Apache/2.2.8**）。也称为 **Min**。

*OS:* 返回操作系统名称和完整版本（**Apache/2.2.8 (Fedora)**）。提供的信息比 *Full* 少，这可能有助于防止恶意用户。

*Full:* 与 OS 相同，此外还发送非 Apache 组模块的名称和版本（**Apache/2.2.8 (Fedora) PHP/5.2.4**）。

除非你希望客户端出于某种原因了解你正在运行的软件的详细信息，否则请将 **ServerTokens** 设置为尽可能少地透露信息。

-   上下文：**服务器配置**
-   默认值：Full
-   Fedora/RHEL：OS

