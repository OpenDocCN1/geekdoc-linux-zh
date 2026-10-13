
对于此版本的 Mozilla，目前没有许多插件可供 Fedora 使用。请查看帮助（Help）→插件（Plug-ins）。你可能会看到一个插件：`MozPlugger`。如果尚未安装 `MozPlugger`，你可以从随书附带的 DVD 中安装。`MozPlugger` (`http://fredrik.hubbe.net/plugger.html`) 是一种多媒体插件，通过依赖外部程序播放 SGI 电影、TIFF、DL、IF 动画、MIDI、Soundtrack、AU、WAV 和 Commodore 64 音频文件。最近，`MozPlugger` 还支持用于显示各种 Microsoft 办公文件类型的插件。

大多数适用于 Firefox 的插件（本章稍后将“使用插件”部分）也可以在 Mozilla 中工作。未来可能会添加更多供 Fedora 使用的插件。Mozilla 提供了一个非常棒的网站，用于获取在 Mozilla 中运行的 Linux 插件：

# 第9章：使用互联网和 Web 355

`http://pluginindoc.mozdev.org/linux.html`。该网站包含下载插件的链接以及安装说明。

当你下载插件时，请按照插件随附的说明进行安装。如果插件是 RPM 文件格式，请按照你在 Red Hat Linux 中安装任何其他软件软件包的方式进行安装（使用 `rpm -Uvh package` 命令）。否则，只需将插件（`.so` 文件）复制到系统插件目录（`/usr/lib/mozilla/plugins/`）或你的个人插件目录（可能是 `~/mozilla/plugins/`）。当你重启 Mozilla 时，插件将自动从这些位置加载。

> 注意：`CrossOver Plugin` 是一款商业产品，允许你在 Mozilla 中使用许多 Windows 插件。详细信息请参阅本章后面“使用插件”部分中关于 `CrossOver Plugin` 的介绍。

## Mozilla Navigator 控件

如果你使用过 Web 浏览器，这些控件可能正如你预期的那样：地址栏、前进和后退按钮以及文件编辑菜单等。Mozilla 中还有一些你可能不习惯看到的控件。以下是一些示例：

- **使用侧边栏** — 按 F9 功能键切换侧边栏的开启和关闭。点击“相关内容”、“搜索”、“书签”或“历史记录”标签（或如前所述添加你自己的标签）。添加你自己的书签，从历史列表中返回页面，或搜索 Web 内容。

- **发送 Web 内容** — 你可以向选定的接收者发送包含当前 Web 页面（文件 → 发送页面）或当前 Web 页面的 URL（文件 → 发送链接）的电子邮件。

- **在网上搜索** — 你可以通过多种不同的方式在互联网上搜索关键词短语。选择工具 → 搜索 Web 来打开一个 Netscape 网站，你可以在其中搜索互联网。在地址栏中输入一个或多个关键词，然后点击搜索。当然，你也可以像之前描述的那样使用侧边栏进行搜索。

- **查看页面信息** — 你可以通过选择查看 → 页面信息来查看关于 Web 页面的位置、其每个组件的位置、页面修改日期以及其他信息。图 9-5 显示了 Web 页面的页面信息窗口。点击“链接”标签可以查看该页面指向 Web 其他内容的链接。点击“安全”标签可以查看页面上使用的验证和加密信息。

## 356 第二部分：使用 Fedora RHEL

![](img/8aa80810fdd3df400bb7ee72b296baad_379_0.png)

## 改进 Mozilla 浏览

你用 Mozilla 访问的每个网站并不并不都能完美运行。有些网站不遵循标准，使用不可读的字体，选择难以阅读的颜色，或者要求你使用特定类型的浏览器来查看其内容。为了改进你的浏览体验，你可以为 Mozilla 添加一些功能。

### 添加偏好工具栏

如果你曾遇到过要求使用特定类型或版本的浏览器，或者颜色导致页面无法阅读的网页？名为 `PrefBar2` 的 Mozilla 工具栏可以让你尝试欺骗网站，让它们认为你正在运行不同的浏览器。它还允许你选择设置，以改进难以阅读页面上的颜色、字体和其他属性。

你可以从 Mozdev.org 网站 (`prefbar.mozdev.org`) 下载这个精巧的小工具栏。点击安装链接；安装完成后，重启 Mozilla。

> 提示。你必须拥有 `/usr/lib/mozilla-1.7.3` 的权限，安装链接才能生效。这可能需要你以 root 身份登录、启动 Mozilla、安装偏好工具栏，然后注销 root。

默认按钮组允许你执行以下操作：

- 颜色 — 在默认颜色与网页设置的颜色之间切换。

- 图像 — 在显示的页面上切换加载或不加载图像的状态。

- JavaScript — 允许或禁止在 Mozilla Navigator 中运行 JavaScript 内容。

- 清除缓存 — 删除内存和磁盘中的所有缓存内容。

- 杀死 Flash — 杀死当前页面所有的嵌入 Flash 内容。

- 真实 UA — 选择让你的浏览器识别为自身（Mozilla 当前版本）或以下任何一种：Mozilla 1.0（适用于 Windows 98）、Netscape Navigator 4.7（适用于 Macintosh）、Netscape 6.2（适用于 Windows）、Internet Explorer 5.0（适用于 Macintosh）或 Internet Explorer 6.0（适用于 Windows XP）。

用户代理 (`UA`) 设置在处理需要 Internet Explorer (`IE`) 的网站时（通常是 Windows 或 macOS 上的 IE）非常有用。`IE 6.0 WinXP` 设置足以让 Mozilla 运行在 Microsoft Exchange 网络直播服务上，该服务通常设置为需要 IE。如果你在一个主要使用 Windows 的组织中运行 Linux，安装偏好工具栏将列出你可能无法访问的页面。

点击“自定义”（Custom）按钮向偏好工具栏添加更多按钮。你可以添加按钮来清除历史记录或地址栏条目。你甚至可以添加“弹出窗口”（Popups）按钮，防止页面从 Mozilla 中打开弹出窗口。

许多偏好会立即生效。其他设置可能需要你重启 Mozilla。

### 添加 Java 支持

如果你想显示某些 Java 内容，但只看到破碎的拼图和一个提示你需要插件的失败信息。请参见“使用插件”部分了解 `JSE` 环境。

## 使用 Mozilla 玩花样

Mozilla 内置了一些实用功能，可以让你的浏览更加愉快。以下是其中一些特性：

### 使用标签页浏览

与 Firefox 一样，每个标签页的标签都会出现在顶部。要关闭标签、创建新标签、书签一组标签或刷新标签，请右键点击顶部的某个标签。下拉菜单允许你选择所需的功能。

在标签页中打开链接的最简单方法之一是在 HTML 页面上右点击链接。选择“在新标签中打开链接”。

### 使用 DOM 检查器

如果你正在调试自己创建的 Web 页面，文档对象模型（DOM）检查器对于检查页面结构非常有用。要打开 DOM 检查器，在 Mozilla 或 Firefox 控件中选择：

在 DOM 检查器窗口中输入要检查的 Web 面的 URL。代表头、体、表格、字体等的节点出现在左列。每个节点的值出现在右列。点击节点名称，页面上的相应区域将被高亮，并在右侧显示节点值。

### 调整网页大小

有一个方便的快捷键，可以快速调整 Mozilla 或 Firefox 中大多数网页的字体大小。按住 `Ctrl` 键并按 `(+)` 或 `(-)` 键。网页上的文字（大多数情况下）会变大或变小。那个字体极小的页面突然变得可读了。

## 使用 Mozilla Firefox 浏览

通过 Firefox 浏览器（见图 9-6），Mozilla 项目已直接挑战 Internet Explorer。Firefox 非常轻量（因此运行速度快）、功能丰富且优先考虑。如果你还没有切换到 Fedora，你可以在 Windows、Mac OS X 和其他 Linux 系统上获取 Firefox。如果你有随书的 Fedora Core DVD，你现在就可以尝试 Firefox。

由于 Firefox 是 FC4 和 RHEL4 的默认浏览器，如果你执行了包含桌面的安装，Firefox 应该已经安装。（如果还没有，你需要从 FC4 DVD 安装 `firefox` 软件包。）从你的 FC4 桌面启动 Firefox，只需选择

# 第9章：使用互联网和 Web 359

点击你面板上的地球仪图标，或从应用程序菜单中选择 Internet -> Firefox Web 浏览器。

![](img/8aa80810fdd3df400bb7ee72b296baad_382_0.png)

图 9-6：Firefox 可以轻松地进行搜索、标签页浏览并安全地获取插件。

Firefox 将其一些最佳功能直接放在主窗口中（如图 9-6 所示）。以下是一些示例：
