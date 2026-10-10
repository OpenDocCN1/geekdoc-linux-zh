
进入 `/path/to/xxx` 目录，找到 `xxx.json`。

在表达式 `cvar = avar + bvar` 中，加法运算符（`+`）将 `avar` 与 `bvar` 相加，得到它们的和 `cvar`

在 `List.of(arg0, arg1, arg2)` 中，`List` 接口的工厂方法 `of()` 接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用 `cmd` 命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

Wait need actual text. Let's redo properly.

[content]
- **阻止弹出窗口** —— 在 Firefox 中，默认阻止弹出窗口。要查看或更改如何处理弹出窗口，选择 Edit → Preferences 和 Content。Block Pop-Ups 选项被选中（阻止弹出窗口）或取消勾选（允许）。如果阻止了弹出窗口，你可以选择 Exceptions 来允许指定的站点。

有很多方法可以配置 Firefox 使其运行顺畅。以下章节描述了在 Firefox 中自定义你的浏览体验的一些方法。

## 第 9 章：使用互联网和 Web 375

### 设置导航器偏好

你可以在选项窗口中设置 Firefox 选项。要打开 Firefox 选项，点击编辑 -> 选项。选项窗口如如图 9-5 所示。

![](img/6a8f767dda2519b458f97c2e7f586576_416_0.png)

图 9-5：在 Firefox 选项窗口中更改网页设置。

以下列表显示了你可能想从 Firefox 窗口更改的一些偏好：

- *选择主页* — 要从“主页”标签页选择主页，你只需在位置框中输入 URL。它可以是本地文件（`file://`）或网页（`http://`）。你还可以拥有多个主页，每个主页会在 Firefox 启动时出现在单独的标签页上，用管道线符号分隔 URL（例如，`linuxtoys.net|redhat.com`）。

要填写页面位置，你也可以选择按钮。“使用当前页面”会将浏览器中所有标签页的当前页面添加为主页。“使用书签”按钮允许你从书签列表中选择主页。“选择空白页”将把你的主页设置为 `about:blank`。

- **保存信息** — 选择“隐私”来选择保存有关 Web 信息的方式。在“隐私”标签页中，你可以选择如何将数据保存到浏览历史、表单数据、密码、下载的文件和 cookies。你可以选择历史、表单数据、密码、下载历史、cookies 和缓存的网页。如果你在别人的机器上使用 Firefox 并希望保持浏览隐私，那么清除这些信息是一个好主意。

- **设置语言** — 如果网页有多种语言版本，可以通过选择“内容”类别并在“语言”下选择“选择”按钮，为特定语言设置显示偏好列表。

- **阻止或启用内容** — 你遇到的某些内容在浏览器中播放或显示可能是令人恼的或危险的。从“内容”标签页，可以设置允许或阻止弹出窗口、尝试安装扩展或主题的站点、图像显示、ava 内容和 javascript 内容。你还可以针对处理上述内容时设置的通用规则设置例外。

> 注意：Firefox 警报器会在遇到被报告为伪造的页面时显示“疑似伪造”消息，帮助你阻止网站。你可以选择不显示该页面或忽略警告。如果你怀疑某个未显示该消息的页面是伪造的，选择帮助 -> 报告伪造将该页面添加到 Google 网页伪造列表。

- **定义标签页浏览** — 使用“标签页”标签上的选项来确定在打开新内容或关闭浏览器时如何使用标签页。

- **下载管理器和文件夹** — 选择在下载完成时是否显示下载管理器。你也可以选择询问放置每个所选下载的位置，或选择默认文件夹以自动下载文件。选择“查看和编辑选项”来配置你采取的操作。

“高级”选项页可用于精调你的 Web 浏览体验。以下是一些可能让你感兴趣的高选项：

- **常规设置** — 高级部分“常规”标签页上的某些设置允许你更改辅助设置、浏览功能（如窗口自动调整大小和滚动）以及系统默认值。

- **选择连接设置** — 如果你直接访问互联网，不需要更改任何代理设置。但是，如果你需要通过代理服务器访问互联网，可以通过从“高级”标签页选择网络 -> 连接设置来识别该服务器（或多个服务器）的位置。要通过代理服务器访问 Web，你必须显式识别用于请求的每种内容内容的代理服务器（HTTP, SSL, FTP, Gopher 和 SOCKS）。

- **获取浏览器更新** — 从“更新”标签页，可以设置 Firefox 自动检查搜索引擎或已安装扩展和主题的更新。选择“更新历史”查看你为 Firefox 安装的更新历史。

- **选择安全设置** — 从“高级”部分的“加密”标签页，选择 Firefox 用于安全浏览时可以接受的协议（SSL 和 TLS）。还有一个“证书”部分，允许你管理证书以验证安全站点的真实性或对远程站点进行身份验证。（访问“保护 Firefox”部分获取更多关于使用 Firefox 保护 Web 浏览的信息。）

## 扩展 Firefox

Firefox 可以轻松地处理标准的 Web 内容（HTML、JPEG、文本文件）。与任何浏览器一样，某些内容需要添加插件或辅助应用程序才能播放或显示该内容。Firefox 还允许你添加扩展来增强 Firefox 的功能。

### 使用插件

在 Firefox 中，你可以通过在位置栏中输入 `about:plugins` 查看安装了哪些插件。由于 Firefox 交付在 Fedora 和 RHEL 系统中，你默认至少安装了一个 NPAPI 插件封装器。NPAPI 插件允许你使用某些并非为 Linux 构建的插件。

要找到 Linux 系统中适用于 Firefox 的插件，请搜索 Mozilla 插件页面（http://pluginindoc.mozdev.org/linux.html）。以下是一些你可能想添加到 Firefox 的插件：

- Adobe Acrobat 插件 (www.adobe.com/support/downloads) — 显示 Adobe Systems PDF（便携式文档格式）格式的文件。（如果未安装此插件，Firefox 将无法显示它们。）

- DjVu 插件 (sourceforge.net) — 此插件允许你查看压缩的图像文件。

- Adobe Flash Player (www.adobe.com/support/downloads) — 启用基于 Flash 内容播放。

- MPlayer (http://mplayer.org) — 允许在浏览器内播放视频内容。

- Java 运行时 (http://java.com/download) — 为运行 Java 和内容提供环境。

- CrossOver 插件 (www.codewavers.com) — 允许在 Linux 上使用 Windows 插件，如 QuickTime 和 Windows Media Player。

# 第 9 章：使用互联网和 Web 379

Flash、iTunes 和 Lotus Notes，以及 Microsoft Word、Excel 和 PowerPoint 预览器。（在你阅读此内容时，可能已经提供了对该内容后续版本的支持。）你还可以安装其他多媒体插件，以及用于配合这些插件的各种字体。

对于某些插件，系统会提示你想要将插件存放在何处。你可以选择将其安装为供系统上的所有用户使用，或仅供当前用户使用。要为当前用户添加插件，请将其放在 `~/.mozilla/plugins` 目录中。要让系统中所有运行 Firefox 的用户都能使用插件，请将插件放在 `/usr/lib/firefox-*` 目录。

> 注意：如果 Firefox 没有处理特定数据类型的插件，会弹出一个窗口，提示你使用桌面环境中的默认应用程序来处理该数据。GNOME 通过 `/usr/share/applications/defaults.list` 定义系统级默认应用程序。对于你自己的设置，可以这样更改打开特定文件类型的默认值：打开 Nautilus 管理器；右键点击你想更改的类型的任意文件；属性；选择“打开”选项卡中的“使用方式打开”；在列表中更改你想用于该文件类型的应用程序。如果你想添加它但它不在列表中，点击“添加”到列表。

虽然插件可以选择不同类型的内容，但也可以向浏览器添加扩展程序以增强浏览器本身的功能。

### 获取扩展

要扩展 Firefox 以处理由 Fedora 或 RHEL 提供的内容，请从 Mozilla Firefox 产品页面（http://www.mozilla.com/en-US/firefox/）开始。从那里，点击链接进入 Firefox 扩展（Add-ons）。以下是 Mozilla 提供的一些最流行的 Firefox 扩展：

> 注意：已知某些 Firefox 扩展会导致 Firefox 出现性能问题，主要是使用过多内存。如果你发现 Firefox 性能不佳，请关闭所有 Firefox 窗口，在终端中输入以下命令通过安全模式重启 Firefox：

```
firefox -safe-mode
```

请参考 http://kb.mozilla.org/Safe_Mode 了解更多关于使用安全方法调试 firefox 问题的信息。

- 下载工具 - 如果你想从 Web 浏览器下载组文件，FlashGot 是一个非常实用的工具。安装 FlashGot 后，你可以选择下载单个文件、通过高亮网页上的链接识别的文件，或从当前网页链接的所有文件。它还有一个“库（Gallery）”功能，允许你一次性识别下载范围的文件名。安装 FlashGot 后，你可以通过选择“工具 → FlashGot”来访问它，然后从菜单中选择一个功能。在 Fedora 中，FlashGot 将请求传递给 `kGet` 以完成下载。你可以获取其他工具作为 `wget` 使用。

## 第二部分：使用 Fedora 和 RHEL
