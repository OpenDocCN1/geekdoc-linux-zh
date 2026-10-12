
## 特性，且将安全性作为高优先级来构建。

如果你尚未切换到 Fedora，你可以获取 Windows、Mac OS X 以及其他 Linux 系统的 Firefox。如果你拥有随本书附带的 Fedora Core 3 DVD，你可以立即试用 Firefox。

如果你的 Fedora Core 3 系统已安装 Firefox（你需要从 DVD 安装 firefox 软件包），可以通过选择红帽菜单中的 **Internet → Firefox Web Browser** 来打开它。

![](img/b22364e57409c2481ba806e4e6b9309c_351_0.png)

**图 9-5**：Firefox 让搜索、标签浏览以及安全地获取插件变得简单。

Firefox 最卓越的特点在于它赋予你控制 Web 浏览器行为的能力，并使决策过程易于处理。例如，在浏览过程中，如果 Firefox 遇到弹出式窗口，它会提供选项允许该弹出窗口或允许来自该站点的所有弹出窗口。如果遇到需要特殊软件（如插件）才能播放的数据，它会帮助你搜索所需的软件并决定是否需要播放器。

关于主要特性，以下是你在 Firefox 中预期会找到的一些亮点：

- **标签浏览** — 无需打开多个窗口来同时访问多个 Web 页面，Firefox 包含一种非常高效的标签浏览功能。选择 **File → New Tab**。然后输入你想要的新 Web 页面的 URL。图 9-5 显示了 Firefox 窗口及其两个打开的浏览标签。
- **动态书签** — 对于提供 RSS 新闻和博客标题的 Web 站点，Firefox 屏幕右下角会出现一个小 RSS 标志（见图 9-5）。

尝试访问如 [http://slashdot.org](http://slashdot.org) 这样的站点。点击 RSS 按钮并选择 **Subscribe to Slashdot RSS...**。当提示时，选择为该站点添加一个书签。选择 **Bookmarks**，然后将鼠标指针悬停在新的书签上。在书签的右侧，会显示该站点今天可用的文章列表。你可以直接点击感兴趣的文章。或者，你可以选择 **Open in Tabs** 在单独的标签页中打开所有文章。

> **注意：** 如果你访问一个你知道是 RSS 站点的 Web 站点，但你想要的标题以 XML 代码形式出现，这意味着该页面没有向 Firefox 识别自己为 RSS 站点。你仍然可以通过选择 **Bookmarks** → **Manage Bookmarks** 为该站点添加动态书签。在 **Bookmarks Manager** 屏幕中，选择 **File** **New** **Live Bookmark**。当提示时，输入动态书签的名称，然后将 RSS 页面的位置键入（或剪切并粘贴到） **Feed Location** 框中，并点击 **OK**。该新的动态书签以及该站点今天的文章将出现在你的书签列表中。

- **查找文本** — 点击 **Edit** → **Find in This Page** 以打开窗口底部的工具栏，用于在当前页面中搜索文本字符串。这允许你搜索页面文本，而不必让一个小的弹出窗口挡住视线。输入文本字符串后，点击 **Find Next** 或 **Find Previous** 以搜索该字符串。你还可以点击 **Highlight** 高亮页面上该字符串的所有实例。
- **拦截弹出窗口** — 在 Firefox 中，默认情况下会拦截弹出窗口。如果你浏览到一个试图打开弹出窗口的页面，Firefox 会告知你“Firefox 阻止了该站点打开弹出窗口。点击此处查看选项...”你可以选择允许来自此站点的弹出窗口，编辑你的弹出窗口拦截选项，或仅显示遇到的特定弹出窗口。
- 要查看或更改 Firefox 如何处理弹出窗口，请选择 **Edit** → **Preferences** 并选择 **Web Features**。**Block Pop-up Windows** 选项要么被选中（以拦截弹出窗口），要么未被选中（以允许弹出窗口）。如果弹出窗口被拦截，你可以选择 **Allowed Sites** 来添加你允许其弹出窗口的特定站点。
- **高级安全特性** — 使用 Firefox，你可以大量控制哪些内容可以播放以及哪些软件可以下载到你的计算机。你可以从 **Preferences** 窗口（选择 **Edit** → **Preferences**）查看或更改许多安全特性。**Web Features** 主题允许你选择启用 Java 或 JavaScript、加载图像或允许 Web 站点安装软件。**Privacy** 主题允许你管理 Cookie、密码、历史记录和缓存信息。

前往 Mozilla Firefox 站点（[www.mozilla.org/products/firefox](http://www.mozilla.org/products/firefox)）获取更多关于 Firefox 的信息。有关从 Internet Explorer 过渡到 Firefox 的帮助，Foxfire 站点提供了相关资源：[www.mozilla.org/products/firefox/switch.html](http://www.mozilla.org/products/firefox/switch.html)。

## 使用基于文本的 Web 浏览器

如果你成为一名 Linux 管理员或高级用户，随着时间推移，你不可避免地会发现自己需要在远程登录的计算机或没有桌面 GUI 可用的环境中工作。在那种状态下的某个时刻，你很可能想要查看 HTML 文件或 Web 页面。为了解决这个问题，Fedora Core 包含几个基于文本的 Web 浏览器。

使用基于文本的 Web 浏览器，你可以从 shell 访问来自 Web、你的本地文件系统或你远程登录的计算机上的任何 HTML 文件。如果你只想瞄一眼 Web 页面的内容，就不必启动 GUI 或阅读几页 HTML 标记。除了调用 Web 页面、在这些页面间移动以及跟随链接到其他页面之外，这些基于文本的浏览器中的一些甚至可以在终端窗口中显示图形！

你使用哪个基于文本的浏览器取决于你对哪个更熟悉。可用的浏览器包括：

- **links** — 使用 `links`，你可以打开文件或 URL，然后遍历打开的页面中的链接。使用向前搜索（*string*）和向后搜索（*string*）功能在页面中查找文本字符串。使用上下箭头在链接之间前后移动。然后按 Enter 键转到当前链接。使用左右箭头键在你访问过的页面之间前后移动。按 Esc 键查看功能菜单栏。
- **lynx** — `lynx` 浏览器附带一套很好的帮助文件（按 ? 键）。使用空格键在页面间移动。虽然 `lynx` 可以显示包含框架的页面，但它无法按预期位置显示它们。使用方向键显示选定的链接（右箭头），返回上一个文档（左箭头），选择上一个链接（上箭头）以及选择下一个链接（下箭头）。
- **w3m** — `w3m` 基于文本的 Web 浏览器可以显示包含文本、链接、框架和表格的 HTML 页面。它甚至尝试显示图像（尽管有点不稳定）。有英语和日语的帮助文件可供使用（在运行 `w3m` 时按 H 键）。你也可以使用 `w3m` 以纯文本形式翻页浏览 HTML 文档（例如，`cat index.html | w3m -T text/html`）。使用 Page Up 和 Page Down 键翻页浏览文档。在链接上按 Enter 键转到该链接。按 B 键返回上一个链接。分别使用 / 和 ? 键向前和向后搜索文本。

> **注意。** 你需要安装 elinks 软件包来获取 links，安装 lynx 软件包来获取 lynx，安装 w3m 软件包来获取 w3m。

在这些浏览器中，`w3m` 命令似乎是最先进的。它具有漂亮的默认字体选择，似乎能整洁地处理框架，并且其颜色使用也很方便。`links` 浏览器允许你使用鼠标剪切和粘贴文本。

你可以通过提供文件名或（如果你有活动的网络连接）Web 地址来启动这些基于文本的 Web 浏览器中的任何一个。例如，要在 `w3m` 浏览器中阅读 `w3m` 文档（其为 HTML 格式），你可以从终端窗口或其他 shell 界面输入以下内容：

