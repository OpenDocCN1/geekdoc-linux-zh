
## VirtualScriptAliasIP

`VirtualScriptAliasIP` 指令允许您定义一个使用插值目录路径的脚本别名（类似于使用 `ScriptAlias` 指令所做的那样）。

-   **语法：** `VirtualScriptAliasIP alias interpolated_directory`
-   **上下文：** 服务器配置，虚拟主机

例如，在以下指令中，当 Apache 接收到对 `http://www.domain.com/cgi-bin/script_name` 的请求时，它会将该请求转换为 `/www/IP_address/cgi-bin/script_name`

```
VirtualScriptAliasIP /cgi-bin/ /www/%0/cgi-bin
```

## 其他模块

本节中的模块（如表 5-11 所示）不属于任何特定类别。

表 5-11
其他模块

| 模块 | 用途 |
| :--- | :--- |
| mod_so | 支持在运行时加载模块。 |
| mod_imap | 图像映射文件处理程序。 |
| mod_proxy | 将 Apache 变为缓存代理服务器。详情参见第 10 章。 |
| mod_isapi | Windows ISAPI 扩展支持。详情参见第 21 章。 |
| mod_file_cache | 在内存中缓存文件以加快响应速度。 |
| mod_dav | 提供 1 类和 2 类基于 Web 的分布式创作和版本管理（WebDAV）功能。 |
| mod_example | 供模块开发者学习如何编写 Apache 模块的示例。对除 C 程序员外的其他人没有用处。 |

## mod_so

`mod_so` 模块允许 Apache 加载其他模块所需的可执行代码，或在服务器启动期间加载其他模块。除了该模块本身，您可以将所有模块编译为 DSO（动态共享对象）模块。

### LoadFile

`LoadFile` 指令在启动期间加载指定的文件。通常，使用此指令加载其他模块所需的动态链接库（DLL）文件（仅限 Windows）。

-   **语法：** `LoadFile filename [filename...]`
-   **上下文：** 服务器配置

### LoadModule

`LoadModule` 指令加载已编译为 DSO 的模块。

-   **语法：** `LoadModule module_filename`
-   **上下文：** 服务器配置

## mod_imap

`mod_imap` 模块在 Apache 中默认编译。它提供图像映射支持，该功能曾由 CGI 程序 `imagemap` 提供。您可以使用 `AddHandler` 指令为任何文件扩展名指定 `imap-file` 处理程序（内置于该模块中）。例如，以下指令使 Apache 将所有 `.map` 扩展名的文件视为图像映射，并使用 `mod_imap` 模块处理这些文件：

```
AddHandler imap-file map
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_182_0.png)

`mod_imap` 模块仍支持旧格式：

```
AddType application/x-httpd-imap map
```

但是，不建议使用旧格式，因为未来可能会取消对其支持。

图像映射文件的内容可以具有以下任一语法：

```
directive value [x,y ...]
directive value "Menu text" [x,y ...]
directive value x,y ... "Menu text"
```

图像映射文件中允许的指令如下：

-   `base` — 映射文件中使用的相对 URL 被视为相对于此指令值。请注意，如果在映射文件中找到 `ImapBase` 指令设置，则会被此指令覆盖。默认值为 `http://server_name/`。`base_uri`，与 `base` 同义。
-   `default` — 指定当坐标不符合任何多边形、圆形或矩形，且未给出任何 point 指令时要采取的操作。此指令的默认值为 nocontent，表示告知客户端保持显示当前页面。
-   `poly` — 使用至少 3 个点到最多 100 个点的多边形来定义。如果用户提供的坐标落在多边形内，则此指令被激活。
-   `circle` — 使用中心坐标和圆上一点来定义圆形。如果用户提供的坐标落在圆内，则此指令被激活。
-   `rect` — 使用两个对角坐标来定义矩形。如果用户提供的坐标落在矩形内，则此指令被激活。
-   `point` — 定义单个点坐标。当不满足其他指令时，使用距离用户提供坐标最近的 point 指令。

值为绝对或相对 URL，或以下列表中的特殊值之一。坐标 $(x,y)$ 由空白字符分隔。双引号内的文本（如第二种语法所示）在生成图像映射菜单时用作链接文本。任何以 # 字符开头的行都被视为注释，并被 Apache 忽略。

坐标以 $x,y$ 格式书写，每个坐标由空白字符分隔。引号内的文本字符串在生成菜单时用作链接。如果没有这样的字符串，则 URL 即为链接，如下面的图像映射文件所示：

```
# Comments go here
# Version 1.0.0
base http://www.yoursite.com/some/dir
rect thisfile.html "Customer info" 0,0 100,200
circle http://download.yoursite.com/index.html 295,0 100,22
```

如果该图像映射文件名为 `imap.map`，则可以从其他 HTML 文件中以如下方式引用：

```
<A HREF="/path/to/imap.map"><IMG ISMAP SRC="/path/to/imap.gif"></A>
```

### ImapMenu

`ImapMenu` 指令确定在请求没有有效坐标的图像映射文件时的操作。

-   **语法：** `ImapMenu (None, Formatted, Semi-formatted, Unformatted)`
-   **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
-   **覆盖：** Indexes

`ImapMenu` 允许以下操作：

| 操作 | 执行内容 |
|---|---|
| None | 不生成菜单，并执行默认操作。 |
| Formatted | 生成最简单的菜单。忽略注释。打印一级标题，然后是一条水平线，接着是链接——每个链接占一行。 |
| Semi-formatted | 在半格式化菜单中，打印注释，将空行转换为 HTML 换行符，且不打印标题或水平线。 |
| Unformatted | 在未格式化菜单中，打印注释，并忽略空行。 |

### ImapDefault

`ImapDefault` 指令定义图像映射的默认操作。此默认设置可以使用图像映射文件中的 `default` 指令进行覆盖。

-   **语法：** `ImapDefault {Error, Nocontent, Map, Referer, URL}`
-   **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
-   **覆盖：** Indexes

下表显示了 `ImapDefault` 指令每个可能值的含义。

| 值 | 执行内容 |
|---|---|
| URL | 相对或绝对 URL。相对 URL 相对于基准解析。 |
| Map | 与图像映射文件自身的 URL 相同。除非 ImapMenu 设置为 none，否则将创建菜单。 |
| Menu | 与 Map 相同。 |
| Referer | 与引用文档的 URL 相同。如果不存在 Referer: 头，则默认为 http://servername/。 |
| Nocontent | 发送状态代码 204 以告知客户端保持显示当前页面。对于 base 无效。 |
| Error | 发送状态代码 500 以告知客户端服务器错误。 |

### ImapBase

`ImapBase` 指令设置图像映射文件中使用的默认基准。此 `base` 设置可以使用图像映射文件内的 `base` 指令进行覆盖。如果不存在此指令，`base` 默认为 `http://servername/`。

-   **语法：** `ImapBase { Map, Referer, URL }`
-   **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
-   **覆盖：** Indexes

## mod_file_cache

`mod_file_cache` 模块允许 Apache 缓存经常使用且不太经常更改的静态文件。使用此模块，您可以将文件加载到内存中或预先打开文件，从而减少每次请求的磁盘 I/O。这意味着 Apache 无需为每个请求从磁盘读取文件。此模块并非在所有平台上都有效，并且仅当您确定频繁请求的文件不会更改时，才应使用它。如果缓存文件或预先打开的文件发生更改，在重启服务器之前，Apache 服务器无法处理该更改。

### MMapFile

`MMapFile` 指令允许您通过 `mmap()` 系统调用将文件加载到内存中。文件加载到内存后，服务器将无法检测到物理文件中的任何更改。因此，使用此指令时要小心。如果您更改了已加载到内存中的文件，请务必重启 Apache 服务器。

-   **语法：** `MMapFile filename [filename] [...]`
-   **上下文：** 服务器配置

### CacheFile

`CacheFile` 指令预先打开文件并缓存文件句柄，这样当请求到来时，Apache 无需执行系统调用来打开和读取文件。文件缓存后，对该文件的任何更改都需要重启 Apache 服务器。

-   **语法：** `CacheFile filename [filename] [...]`
-   **上下文：** 服务器配置

## mod_dav

`mod_dav` 模块允许您使用 HTTP 1.1 协议的 WebDAV 扩展。要了解有关这些扩展的更多信息，请访问 `www.webdav.org`。

