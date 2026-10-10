
`slrn` 新闻阅读器是基于屏幕的。命令显示在屏幕顶部，可以使用列出的键执行。存在不同类型的屏幕，分别用于新闻组列表、文章列表和内容，每种都有各自的一组命令。初始屏幕列出你订阅的新闻组，并提供发布、列出和订阅新闻组的命令。当你第一次启动 `slrn` 时，你必须在家中目录下创建一个 `*.jnewsrc*` 文件。使用以下命令：`slrn -f .jnewsrc -create`。此外，你还必须设置 **`NNTPSERVER`** 变量并确保其已导出。

`slrn` 新闻阅读器有一个名为 `slrnpull` 的新实用程序，你可以使用它自动下载指定新闻组中的文章。这允许你离线查看所选的新闻组。`slrnpull` 实用程序被设计为 Leafnode 的简单单用户版本；它将访问新闻服务器并下载其指定的新闻组，使这些内容在用户选择查看时可通过 `slrn` 访问。新闻组文章下载到 **`SLRNPULL_ROOT`** 目录。在 Fedora 上，这是 `/var/spool/slrnpull`。要下载的选定新闻组输入到放置在 **`SLRNPULL_ROOT`** 目录中的 `slrnpull.conf` 配置文件中。在此文件中，你可以指定每个组下载多少篇文章以及它们的过期时间。要将 `slrn` 与 `slrnpull` 一起使用，你需要进一步配置 `.slrnrc` 文件以引用存放新闻组文件的 `slrnpull` 目录。

> **注意** 几个基于 Windows 的新闻阅读器（如流行的 NewsbIN）可以在 Linux 上运行，使用 Fedora 上的 Wine Windows 仿真。你可以使用 Pirut（添加/删除应用程序）下载和安装 Wine。要使新闻阅读器正常工作，你必须遵循配置说明，通常需要特定的 Windows DLL。对于 NewsbIN，请查看 NewsbIN 的 Linux 论坛。记得将 DLL 添加到你的 `.wine/drive_c/Windows/System32` 目录中。此外，对于 64 位 Fedora Linux 系统，你需要使用“Windows XP x64”系统中的 DLL。

## 新闻传输代理

Usenet 新闻通过互联网以每日新闻源的形式提供，包含数千个新闻组的文章和帖子。该新闻源被发送到站点，这些站点然后通过新闻阅读器为其他系统提供新闻访问权限。这些站点作为新闻服务器运行；用于访问它们的新闻阅读器是其客户端。新闻服务器软件，即*新闻传输代理*，为新闻阅读器提供新闻，使你能够阅读新闻组。

并发布文章。对于 Linux 系统，三种流行的新闻传输代理是 INN、Leafnode 和 Cnews。Cnews 和 Leafnode 都小巧、简单，适用于小型网络。INN 功能更强大，结构也更复杂，专为大型系统设计（更多详情请参阅 www.isc.org）。

Usenet 上的每日新闻流通常体积庞大，在时间和内存方面都会消耗新闻服务器的大量资源。因此，您可能不希望在自己的 Linux 系统上接收此类新闻流。如果您正在管理一个 Linux 系统网络，可以将其中一台指定为新闻服务器，并在其上安装新闻传输代理以接收和管理 Usenet 新闻流。网络中其他系统上的用户可以使用自己的新闻阅读器访问该新闻服务器。

如果您的网络已经拥有新闻服务器，则完全不需要安装新闻传输代理。您只需使用新闻阅读器远程访问该服务器即可（参见前文中的 **`NNTPSERVER`**）。对于 ISP（互联网服务提供商）而言，此类提供商通常运营自己的新闻服务器，您同样可以使用自己的新闻阅读器（如 KNode 和 Pan）进行远程访问。不过请记住，新闻阅读器必须花费时间下载选定新闻组的文章，以及所有新闻组的更新信息。

您还可以使用新闻传输代理运行仅面向本地系统或局域网用户的本地新闻版本。为此，安装 INN、Leafnode、`slrnpull` 或 Cnews，并配置它们仅管理本地新闻组。您系统上的用户随后即可发布文章并阅读本地新闻。

此页有意留白

# 第 14 章

# Web、FTP 和 Java 客户端

大多数 Linux 发行版都提供强大的 Web 和 FTP 客户端，用于访问互联网。许多客户端在安装后自动就绪，当您首次启动 Linux 系统时即可使用。Linux 还包含完整的 Java 开发支持，允许您运行和构建 Java 小程序（applets）。本章将介绍 Linux 上一些更流行的 Web、Java 和 FTP 客户端。Web 和 FTP 客户端连接到运行服务器的站点，使用 Web 页面和 FTP 文件向用户提供相关服务。

## Web 客户端

万维网（WWW，或简称 Web）是一个分布式数据库，包含不同类型的信息，分布在互联网上的许多不同站点。*超文本数据库*由链接到其他项的条目组成，这些条目反过来又可能链接到其他项，以此类推。在检索某一项时，您可以使用该项来检索任何相关项。例如，您可以检索一篇关于亚马逊雨林的文章，然后利用它检索该雨林的地图或图片。就此而言，超文本数据库就像一个相互连接的数据网络，您可以从一个数据项追踪到另一个数据项。信息以称为*Web 页面*的页面形式显示。在 Web 页面上，某些关键词或图形被高亮显示，形成指向其他 Web 页面或项目（如图片、文章或文件）的链接。

在您的 Linux 系统上，您可以从多个 Web 浏览器中选择，包括 Firefox、Konqueror、Epiphany 和 Lynx。Firefox、Konqueror 和 Epiphany 是基于 X Window System 的浏览器，提供完整的图片、声音和视频显示功能。大多数发行版还包括 Lynx 浏览器，这是一款行模式浏览器，仅显示文本行。K Desktop 将 Web 浏览器功能集成到其文件管理器中，使目录窗口能够作为 Web 浏览器运行。基于 GNOME 的浏览器（如 Epiphany 和 Mnemonic）也设计为易于增强扩展。

Web 浏览器和 FTP 客户端常用于执行安全交易，如登录远程站点、订购物品或传输文件。目前，此类操作通过安全套接字层（SSL）提供的加密方法加以保护。有关 SSL 及其对应技术 SSH（安全外壳）的更多信息，请参阅第 19 章和第 23 章。如果您使用浏览器进行安全交易，该浏览器必须支持 SSL。大多数浏览器（如 Mozilla 和 ELinks）都包含 SSL 支持。对于 FTP 操作，您可以使用 ftp 的 SSH 版本 `sftp`，或 Kerberos 5 版本（请参阅第 19 章）。Linux 发行版将 SSL 作为标准安装的一部分包含在内。

## URL 地址

互联网资源使用通用资源定位符（URL）进行访问。URL 由三个元素组成：传输协议、主机名和路径名。传输协议和主机名由冒号和双斜杠（://）分隔。*路径名*始终以单个斜杠开头：

`transfer-protocol://host-name/path-name`

*传输协议*通常是 HTTP（超文本传输协议），指示 Web 页面。传输协议的其他可能值是 **`ftp`** 和 **`file`**。顾名思义，**`ftp`** 发起 FTP 会话，而 **`file`** 显示您系统上的本地文件，例如文本文件或 HTML 文件。表 14-1 列出了各种传输协议。

*主机名*是特定 Web 站点所在的计算机。您可以将其视为该 Web 站点的地址。根据惯例，大多数主机名以 www 开头。在下一个示例中，URL 定位了 **`tldp.org`** Web 站点上名为 **`guides.html`** 的 Web 页面：

`http://tldp.org/guides.html`

如果您不想访问特定的 Web 页面，可以省略文件引用，这样您将自动访问该 Web 站点的主页。若要直接访问某个 Web 站点，请使用其主机名。如果 Web 站点未指定主页，顶级目录中的文件 **`index.html`** 通常用作主页。在下一个示例中，用户打开了 Red Hat 的主页：

`http://www.redhat.com/`

路径名指定了在主机系统上可以找到资源的目录，以及资源文件的名称。例如，`/pub/Linux/newdat.html` 引用了位于 `/pub/Linux` 目录中名为 **`newdat`** 的 HTML 文档。

资源文件的扩展名指示要对其执行的操作类型。图片具有 **`.gif`** 或 **`.jpeg`** 扩展名，会被转换以用于显示。声音文件具有 **`.au`** 或 **`.wav`** 扩展名，会被播放。以下 URL 引用了一个 **`.gif`** 文件。浏览器不会显示 Web 页面，而是调用图形查看器来显示该图片。表 14-2 提供了一些常见文件扩展名的列表。

`http://www.train.com/engine/engine1.gif`

**表 14-1** Web 协议

| 协议 | 描述 |
|---|---|
| **`http`** | 使用超文本传输协议访问 Web 站点。 |
| **`ftp`** | 使用文件传输协议进行匿名 FTP 连接。 |
| **`telnet`** | 建立 Telnet 连接。 |
| **`news`** | 阅读 Usenet 新闻；使用网络新闻传输协议（NNTP）。 |

**表 14-2** Web 文件类型

| 文件类型 | 描述 |
|---|---|
| **`.html`** | 使用超文本标记语言（HTML）格式化 Web 页面文档 |
| **`.gif`** | 使用 GIF 压缩的图形 |
| **`.jpeg`** | 使用 JPEG 压缩的图形 |
| **`.png`** | 使用 PNG 压缩（便携式网络图形）的图形 |
| **`.au`** | Sun (Unix) 声音文件 |
| **`.wav`** | Microsoft Windows 声音文件 |
| **`.aiff`** | Macintosh 声音文件 |
| **`.QT`** | QuickTime 视频文件，多平台通用 |
| **`.mpeg`** | 视频文件 |
| **`.avi`** | Microsoft Windows 视频文件 |

## Web 浏览器

大多数 Web 浏览器旨在访问多种不同类型信息。Web 浏览器可以访问远程 Web 站点上的 Web 页面，或您自己系统上的文件。某些浏览器还可以访问远程新闻服务器或 FTP 站点。站点的信息类型由关键字指定：Web 站点使用 **`http`**，新闻服务器使用 **`nttp`**，FTP 站点使用 **`ftp`**，您自己系统上的文件使用 **`file`**。如前所述，Linux 上有多种流行浏览器可供选择。此处介绍三种具有特色的浏览器：Mozilla、Konqueror 和 Lynx。Mozilla 是基于 X Window System 的 Web 浏览器，能够显示图形、视频和声音，并可作为新闻阅读器和邮件客户端运行。Konqueror 是 K Desktop 的文件管理器。KDE 将完整的 Web 浏览功能集成到 Konqueror 文件管理器中，使您能够使用同一应用程序无缝访问 Web 和文件系统。Lynx 和 ELinks 是基于命令行的浏览器，不具备图形功能，但在其他方面都是功能齐全的 Web 浏览器。

若要搜索 FTP 站点上的文件，您可以使用 Web 站点提供的搜索引擎，例如 Yahoo!、Google 或 Lycos。这些引擎通常同时搜索 Web 页面和 FTP 文件。若要查找您想要在互联网上访问的特定 Web 页面，可以使用这些搜索引擎中的任意一个，或从众多 Web 门户网站执行搜索。Web 搜索已成为大多数 Web 站点的一项标准服务。在 Web 站点内部对文档执行的搜索可能使用由 ht: /Dig 等索引程序建立和维护的本地搜索索引。使用 ht:/Dig 的站点采用标准的 Web 页面搜索界面。超文本数据库被设计为可访问任何类型的数据，无论是文本、图形、声音，甚至是视频。您是否实际能够访问此类数据，在很大程度上取决于您使用的浏览器类型。

## Mozilla 框架

Mozilla 项目是一个基于原始 Netscape 浏览器代码的开源项目，它为基于 Web 的应用程序提供开发框架，主要包括 Web 浏览器和电子邮件客户端。最初，Mozilla 项目的目标是提供一款名为 Mozilla 的终端用户 Web 浏览器。如今，其目的已转变为提供一个开发框架，任何人都可以使用它来创建 Web 应用程序，尽管该项目也提供自己的浏览器。表 14-3 列出了一些 Mozilla 资源。

目前，该开发框架被用于 Mozilla 产品（如 Firefox Web 浏览器和 Thunderbird 邮件客户端），同时也用于非 Mozilla 产品（如 Netscape、Epiphany 和 Galeon Web 浏览器）。此外，该框架易于扩展，支持以插件和扩展形式存在的众多附加组件。Mozilla 项目网站是 www.mozilla.org，常用于插件和扩展开发的网站是 www.mozdev.org。

Mozilla 项目的第一代产品是 Mozilla Web 浏览器，它仍然可用。与最初的 Netscape 类似，它集成了邮件客户端和新闻阅读器，所有功能均在一个集成界面中。第二代产品将这个集成包拆分为独立的单独应用程序：Firefox Web 浏览器和 Thunderbird 电子邮件/新闻阅读器客户端。此外，还有正在开发中的 Mac OS X 版本的 Camino Web 浏览器和 Sunbird 日历应用程序。

1998 年，Netscape 根据 Netscape 公共许可证（NPL）自由发布了其源代码。Mozilla 采用类似于 Linux、KDE 和 GNOME 的开源模式进行开发。开发人员可以通过 Internet 向 Mozilla 网站提交修改和添加。Mozilla 的版本被称为“里程碑（Milestones）”。目前，Mozilla 产品根据 NPL 许可证（用于 Mozilla 代码的修改）和 MPL 许可证（Mozilla 公共许可证，用于新增内容）双重发布。

## Firefox Web 浏览器

Firefox 是基于名为 Mozilla 的 Netscape 核心源代码的下一代浏览器。在当前的发行版中，Red Hat 和 Fedora 使用 Firefox 作为其主要浏览器，取代了 Netscape。Firefox 是一款精简的浏览器，具有快速的 Web 访问速度和针对侵入式间谍软件的 Secure 保护。

Firefox 是一个 X 窗口系统应用程序，你可以从任何桌面进行操作，包括 GNOME、KDE 和 Xfce。在 Red Hat Fedora 上，Firefox 默认安装，主菜单中的 Internet 菜单项中有一个菜单条目，不同的桌面面板上也有其图标。

| 网站 | 描述 |
| :--- | :--- |
| www.mozilla.org | Mozilla 项目 |
| www.mozdev.org | Mozilla 插件和扩展 |
| www.oreillynet.com/mozilla | Mozilla 文档和新闻 |
| www.mozillazine.org | Mozilla 新闻和文章 |
| www.mozillanews.org | Mozilla 新闻和文章 |
| www.bugzilla.org | Mozilla 错误报告跟踪系统 |

**表 14-3** Mozilla 资源

打开时，Firefox 在屏幕顶部显示一个用于输入 URL 地址的区域，以及一系列用于各种网页操作（如页面导航）的按钮。顶部菜单栏上的下拉菜单提供访问 Firefox 功能（如工具、查看和书签）的途径。

URL 框右侧是一个搜索框，你可以使用不同的搜索引擎来搜索 Web、选定网站或特定项目。弹出式菜单允许你选择搜索引擎。目前包括 Google、Yahoo、Amazon 和 eBay，以及用于查找单词定义的 Dictionary.com。Firefox 还具有按钮链接和标签页功能。你可以将 URL 从 URL 框拖放到按钮链接栏，以创建一个可以快速访问该网站的按钮。这对于经常访问的网站很有用。

为了轻松浏览，Firefox 提供标签页面板来显示 Web 页面。要打开一个空白标签页面板，请按下 CTRL-T 或从文件菜单中选择“新建标签页”。要在该面板中显示页面，请将其 URL 从 URL 框或书签列表拖放到面板中。你可以同时打开多个面板，通过点击它们的标签页从一个页面切换到下一个。你可以通过右键点击链接栏并选择“在标签页中打开”，选择将所有链接按钮作为标签页面板打开。

Firefox 将你想要保留的 Web 页面 URL 称为*书签*，标记你想要直接访问的页面。书签菜单允许你添加你喜爱的 Web 页面。然后你可以查看书签并选择一个进行查看。你还可以编辑书签列表，添加新的或移除旧的。历史记录是你之前访问过的 URL 列表。URL 框还有一个弹出式菜单，列出了你之前的历史站点。书签和历史记录可以作为侧边栏查看，可以从查看菜单中选择。

当你使用 Firefox 下载文件时，下载由下载管理器管理。你可以同时下载多个文件。进度可以在下载管理器窗口中显示，可以从工具菜单访问。你可以随时取消下载，或者暂停下载，稍后继续。右键点击下载条目将显示它下载自的网站以及你保存它的目录。要删除条目，请点击“移除”。要清除整个列表，请点击“全部清除”。

Firefox 中的首选项菜单（编辑 | 首选项）允许你设置几种不同的选项。Firefox 还支持高级功能，如 Cookie、表单、图像和密码管理。你可以选择抑制来自特定网站的 Cookie，自动填写表单，不显示网站图像，并为选定网站设置登录信息（如用户名和密码）。你可以为通用功能、隐私、Web 和下载管理以及高级功能设置首选项。在通用首选项中，你可以确定主页、页面字体和颜色，以及连接设置（如代理信息）。对于隐私，你可以控制保存的信息（如要记住的历史站点数量和历史记录），设置保存 Cookie 的策略，并设置缓存大小。所有这些都可以手动清除。在 Web 功能下，你可以控制弹出窗口，允许软件安装，并启用 JavaScript。下载管理器面板允许你配置下载操作，让你指定默认下载目录，是否自动提示输入目录，以及对于某些类型的文件（如 Adobe PDF 文件使用 Adobe Acrobat），你可能希望自动使用的插件。高级面板让你控制更复杂的浏览功能，如滚动、安全级别和证书管理。

如果你所在的网络通过防火墙连接到 Internet，你必须使用代理屏幕输入网络防火墙网关计算机的地址。*防火墙*是一台作为网络受控 Internet 网关的计算机。存在几种类型的防火墙。其中限制最严格的一种使用称为*代理*的程序。

![](img/ab68ea377332b50bf70ef1316c8175b6_364_0.png)

这些代理接收来自用户的 Internet 请求，然后代表他们发起这些请求。没有直接连接到 Internet。

> **注意**：Privoxy Web 代理过滤 Web 内容以保护用户隐私，拦截不必要的广告或阻止侵入式 Cookie。Privoxy 将执行其操作文件中列出的规则，例如位于 `/etc/privoxy` 目录中的 `action.default`。你可以使用 **服务** 工具或 `service` 命令启动 Privoxy。要让浏览器使用 Privoxy，请配置它以运行 Privoxy 的主机作为代理。

## K 桌面文件管理器：Konqueror

如果你使用的是 K 桌面，你可以将文件管理器窗口用作 Web 浏览器。K 桌面的文件管理器被自动配置为充当 Web 浏览器。它可以显示 Web 页面，包括图形和链接。K 桌面的文件管理器支持标准的 Web 页面操作，例如在已访问页面之间前进和后退。点击链接将访问并显示引用的 Web 页面。在这方面，Web 无缝地集成到了 K 桌面中。

## GNOME Web 浏览器：Galeon 和 Epiphany

还有其他几种基于 GNOME 的 Web 浏览器也可用。Epiphany、Galeon 和 KazeKuhase 支持标准的 Web 操作。Epiphany 是一款旨在具有简洁界面且速度快的 GNOME Web 浏览器。你可以在 `epiphany.mozdev.org` 了解更多关于 Epiphany 的信息。Epiphany 随 Red Hat 和 Fedora 一起提供。Epiphany 作为具有简洁界面的简单浏览器运行良好。它还集成了桌面功能，配有一个即使关闭 Epiphany 后也会继续运行的下载小部件。Epiphany 还支持标签页面板，以便访问多个 Web 站点。Galeon 是一款快速、轻量级浏览器，同样基于 Mozilla 浏览器引擎（Gecko）。KazeKuhase 强调可定制界面，带有下载框和 RSS 书签。

对于 GNOME，你还可以下载许多支持工具，例如用于显示新闻源的 RSSOWL 和用于控制基于 Web 的下载的 GNOME 下载管理器（Gwget）。X 客户端下载器（Downloader for X client）对于 FTP 和 Web 文件下载都很有用。它具有众多功能，让你可以控制下载速度，以及下载子目录。虽然它不是 Red Hat Fedora 发行版的一部分，但你可以从 `rpmfind.net` 下载它。

> **注意**：Epiphany 和 Galeon 都可以通过“添加/移除软件”中的图形化 Internet 浏览面板下载。

## Lynx 和 Elinks：行模式浏览器

Lynx 是一个行模式浏览器，可以在没有 X 窗口系统的情况下使用。Web 页面仅以文本形式显示。文本页面可以包含指向其他 Internet 资源的链接，但不显示任何图形、视频或声音。除了显示限制外，Lynx 是一个功能齐全的 Web 浏览器。你可以使用 Lynx 下载文件或建立 Telnet 连接。Web 上的所有信息仍然对你可访问。由于它不需要基于图形的浏览器所需的大量开销，Lynx 可以运行得更快，快速显示 Web 页面文本。要启动 Lynx 浏览器，你在命令行输入 `lynx` 并按下 ENTER 键。

大多数发行版随附的另一个实用基于文本的浏览器是 ELinks。ELinks 是一个强大的基于屏幕的浏览器，包含诸如框架、表单和表格支持等功能。它还支持 SSL 安全加密。要启动 ELinks，请在终端窗口中输入 `elinks` 命令。

## 创建您自己的网站

要创建您自己的网站，您需要访问 Web 服务器。Red Hat 在其 Linux 系统上自动安装 Apache Web 服务器。您也可以租用远程服务器上的 Web 页面空间——许多 ISP 都提供此服务，有些甚至是免费的。在 Red Hat 系统上，为您的网站页面设置的 Apache Web 服务器目录是 `/var/www/html`。其他服务器为您提供一个用于主页的目录。将您创建的 Web 页面放在该目录中。您将您的主页放在这里。

Web 页面的创建并不困难。从一个页面到另一个页面的链接可以引导用户浏览您的网站。您甚至可以创建指向其他网站上的 Web 页面或资源的链接。有许多优秀的文本资料可用于 Web 页面创建和管理。

Web 页面是使用 HTML（超文本标记语言）或较新的扩展版本 XML（扩展标记语言）创建的。它们是标准通用标记语言（SGML）的子集。创建 HTML 或 XML 文档的问题是在文本文件中插入 HTML 或 XML 标签。在这方面，创建 Web 页面与使用基于标签的单词处理器一样简单。您使用 HTML 标签来格式化文本以便作为 Web 页面显示。XML 标签可以包括有关特定连接的更详细信息，例如对象数据或事务特性。Web 页面本身是一个文本文件，您可以使用任何文本编辑器（如 Vi）创建它。如果您对 Unix 系统上的基于标签的单词处理熟悉，您会发现它在概念上与 `nroff` 类似。某些 HTML 标签指示标题、列表和段落，以及对参考 Web 资源的链接。

除了手动输入 HTML 或 XML 代码外，您可以使用 Web 页面编辑器。Web 页面编辑器提供了一个图形界面来构建 Web 页面。特殊的 Web 页面创建程序可以轻松帮助您创建复杂的 Web 页面，而无需显式输入任何 HTML 标签。请记住，无论您使用什么工具创建您的 Web 页面，Web 页面本身都将是一个 HTML 文档。作为 KDE 项目的一部分，KDE Web Dev (www.kdewebedev.org) 提供了几个 KDE Web 开发应用程序，如 Quanta Plus Web 编辑器和 Kommander 对话框构建器。

> **注意：** KDE 桌面和 GNOME 的许多标准编辑器都包含 Web 页面构建功能。许多允许您插入链接或格式化标题。例如，KEdit 程序支持基本的基于文本的 Web 页面组件。您可以添加标题、链接或线条，但不能添加图形。

## Linux 中的 Java

要开发 Java 应用程序、使用 Java 工具并运行许多 Java 产品，您必须在系统上安装 Java 2 软件开发套件 (SDK) 和 Java 2 运行时环境 (JRE)。它们共同组成了 Java 2 平台，标准版 (JSE)。Sun 目前支持并分发这些产品的 Linux 版本。您可以从 Sun 的 `java.sun.com/j2se` 下载并在您的系统上安装它们。Java 包和应用程序在表 14-4 中列出。

### jpackage、Sun 和类 Java (java-gcj-compat)

Fedora 包含众多免费的 Java 应用程序和支持，例如 Jakarta。请查看 `fedoraproject.org/wiki/JavaFAQ` 获取有关 Java 在 Fedora 上如何实现的信息。您应该使用 Fedora 版本的 Java 包，因为它们已专门修改以用于 Fedora。但是，主要的 Java 运行时环境和 SDK 未包含在内。相反，您可以使用包含的一组兼容的 GNU 包（类 Java）来运行 Java applet，从 JPackage 安装 JRE 和 SDK，或从 Sun 下载并安装原始的 JRE 和 SDK。这些选项并不互斥。

Fedora 现在包含一个类 Java 的支持包集合，该集合允许使用 Java 运行时操作。该集合没有官方名称，尽管它被称为 *java-gcj-compat*，以及类 Java。此集合提供与 Fedora 一起包含的免费和开源环境，由三个包组成：GNU Java 运行时 (`libgcj`)、Eclipse Java 编译器 (`ecj`) 以及一组包装器和链接 (*java-gcj-compat*)。

**表 14-4：Java 包和 Java Web 应用程序**

| 应用程序 | 描述 |
| :--- | :--- |
| Java 2 软件开发套件 (SDK) | 包含编译器、解释器、调试器等更多功能的 Java 开发环境，`java.sun.com/j2se`。SDK 是 Java 2 平台的一部分。从 JPackage 或直接下载 Linux 端口。 |
| Java 2 运行时环境 1.4 (J2RE) | 用于运行 Java applet 的 Java 运行时环境。从 `java.com` 或 `jpackage.org` 下载 Linux 端口。 |
| Java 3D for Linux | Sun 为 3-D Java 程序提供的 3-D 应用程序编程接口。 |
| 类 Java 环境 | 类 Java 自由和开源环境，由 GNU Java 运行时 (`libgcj`)、Eclipse Java 编译器 (`ecj`) 和支持的包装器和链接 (*java-gcj-compat*) 组成。包含在 Fedora 中 (`fedoraproject.org/wiki/JavaFAQ`)。 |
| Java Advanced Imaging (JAI) for Linux | Java Advanced Imaging API。 |
| Java 1.1 开发套件 (JDK) 和 Java 1.1 运行时环境 (JRE) for Linux | 旧的 Java 1.1 开发环境，带有编译器、解释器、调试器等。通过 `jpackage.org` 为您的发行版更新下载 Linux 端口。 |
| Java 系统 Web 服务器 | 使用 Java 实现的 Web 服务器。在 `java.sun.com` 的 Java 网站上可用（商业版）。 |
| GNU Java 编译器 | GNU 公共许可 Java 编译器 (GJC) 用于编译 Java 程序，`gcc.gnu.org/java`。包含在 Fedora 中 (`libgcj`)。 |
| Jakarta 项目 | Apache 软件基金会用于开源 Java 应用程序的项目，`jakarta.apache.org`。 |

Fedora 建议您从 JPackage 下载额外的 Java 和 Java 应用程序，该组织设计其 Java 包以避免冲突并与指定的 Linux 发行版兼容。使用 JPackage 版本的 Java，您可以安全地安装和卸载众多的 Java 应用程序和支持工具。使用 JPackage 的最佳方法是下载其 Yum 仓库配置文件。请务必选择适合 Fedora 发行版的那一个（如果可用）。不幸的是，由于许可证限制，JPackage 必须对主要 JRE 以及 SDK Java 应用程序收费。这些包含在其 Java 包中。或者，您可以直接从 Sun 免费下载并安装 JRE 或 JDK。如果您安装了来自 JPackage 的替代 Java 环境，您可以使用 `alternatives` 命令在它们之间切换。

> **注意：** 检查 `fedoraproject.org/wiki/JavaFAQ` 中可能的兼容性问题。

### 安装 Java 运行时环境：JRE

许多 Web 站点将运行需要 Java 运行时环境 (JRE) 的应用程序。Fedora 未预装 Java 运行时环境。但是，类 Java 已经支持兼容的应用程序，如 Office.org 和 Eclipse。对于 Sun 的 Java，您需要在 Linux 系统上下载并安装 JRE。您可以从 Sun Java 站点 (`www.java.com`) 或 JPackage 获取副本。SDK 和 JRE 以自解压压缩存档的形式提供，扩展名为 `.bin`。这些文件实际上是带有嵌入式压缩存档的 shell 脚本。（另有单独的说明。）由于文件名冲突，您不应使用 Sun RPM 包 (`.bin.rpm`)。相反，您应该下载 `.bin` 包并将其提取到 `/opt` 目录中。或者，您可以使用来自 JPackage 的 RPM 包。您必须使用 `chmod` 命令使自解压 bin 文件可执行。以下命令将 JRE 文件 `jre-1_5_0_02-linux-i586-rpm.bin` 更改为可执行文件。首先会提示您接受许可协议。

```bash
