
| Chrome | Google Chrome 浏览器 http://www.google.com/chrome |
| lynx | 基于文本的命令行 Web 浏览器 http://lynx.isc.org |
| elinks | 基于文本的命令行 Web 浏览器 http://elinks.or.cz |

表 7-1: Web 浏览器

## 启用 Flash 插件

Adobe Flash 插件由 RHEL 补充仓库提供。请确保在您的 RHN 账户启用此软件通道。然后您可以使用 `PackageKit` 下载并安装 Flash 插件。选择 Red Hat Enterprise Linux 补充（Supplementary）类别，然后选择多媒体（Multimedia）子标题，并选择 `flash-plugin` 包。

## Firefox：Mozilla 框架

Mozilla 项目是一个基于原始 Netscape 浏览器代码的开源项目，为 Web 应用（主要是 Web 浏览器和电子邮件客户端）提供开发框架。最初，Mozilla 项目的目标是提供名为 Mozilla 的终端用户浏览器。其目的已变为提供一个任何人都可以用来创建 Web 应用的开发框架，尽管该项目也提供自己的框架。表 7-2 列出了

| Web Site | 描述 |
| :--- | :--- |
| www.mozilla.org | Mozilla 项目 |
| www.mozdev.org | Mozilla 插件和扩展 |
| www.oreillynet.com/mozilla | Mozilla 文档和新闻 |
| www.mozillazine.org | Mozilla 新闻和文章 |
| www.mozillews.org | Mozilla 新闻和文章 |

表 7-2: Mozilla 资源

目前该框架用于 Mozilla 产品，如 Firefox Web 浏览器和 Thunderbird 邮件插件。此外，该框架易扩展，支持以插件和扩展形式存在的众多附加组件。Mozilla 项目网站为 www.mozilla.1998，用于插件和扩展开发的网站为 www.mozdev.org。Netscape 在 Netscape 公共许可 (NPL) 下免费提供其源代码。Mozilla 基于类似于 Linux、KDE 和 GNOME 的开源模型开发。Mozilla 产品根据 NPL 许可发布修改的代码，并根据 MPL 许可（Mozilla 公共许可）发布新增内容。

## Firefox Web 浏览器

RHEL 使用 Firefox 作为其主要浏览器（见图 7-1）。Firefox 是一个具有快速访问特性的高效浏览器。Firefox 是一个可以在任何桌面（包括 GNOME 和 KDE）上操作的 X Window 系统。Firefox 默认安装，在主菜单的“Internet”中有一个条目，并在桌面上有一个图标。打开时，Firefox 在屏幕顶部显示一个用于输入 Web 地址的区域，以及一个包含一系列用于网页浏览和页面操作按钮的导航栏。菜单栏上的菜单提供了工具、视图、历史和书签等功能。底部的状态栏显示当前页的状态。

地址栏右侧是一个框，您可以使用不同的搜索引擎搜索 Web、选定站点或特定项目。弹出菜单允许您选择搜索引擎。目前包括 Google、Yahoo 和 Amazon。Firefox 还具有按钮链接和标记标签页。您可以将 Web 地址从地址栏拖动到按钮链接栏，以创建一个快速访问该站点的按钮。这用于经常访问的站点。

为了方便浏览，Firefox 具有用于显示网页的标签页面板。要打开空标签页面板，按 `CTRL-T` 或从“文件”菜单中选择“新标签页”。要在该面板中显示页面，请将其地址从地址框或书签列表拖到面板中。您可以同时拥有多个标签页面板来显示网页。

# 第二部分：应用程序

“连接”（Connection）功能的设置，你可以在此处设置网络连接，例如直接连接到互联网或代理设置。在这里，你还可以设置离线存储大小。加密（Encryption）选项卡则用于管理证书、设置验证方法、查看和撤销。

如果你处于通过防火墙连接到的网络中，应该使用“连接设置”对话框输入网络防火墙网关计算机的地址。可以通过“高级（Advanced）”选项卡下的“网络（Network）”选项卡打开连接设置对话框，并点击设置按钮，“配置 Firefox 如何连接互联网”。存在多种类型的防火墙。限制性强的防火墙使用程序代理，它们接收用户的互联网请求，然后代表用户执行这些请求。没有直接连接到互联网。

![](img/99301381a0d2790a6cdc2798147cbdad_211_0.png)

# 图 7-2：Firefox 偏好

首选项（Preferences）选项卡上的“管理附加项”（Manage Add-ons）按钮会打开附加项窗口，该窗口包含获取附加项（Get Add-ons）、扩展（Extensions）、主题（Themes）、语言（Languages）和插件（Plugins）等选项卡（见图 7-3）。点击其中之一可以打开简要描述并显示“添加到 Firefox”按钮，点击该按钮可以打开下载安装对话框。从“附加项”选项卡中，你可以点击“浏览所有附加项”链接访问“Firefox 附加项”网站。“扩展”选项卡列出了扩展，并配有偏好、禁用和卸载等按钮。在“插件”选项卡上，你可以禁用或启用如 DivX、iTunes、Quicktime 和 Skype 等嵌入应用程序。

Firefox 还支持配置（Profiles）。你可以设置不同的 Firefox 配置，每个配置都有自己的偏好和书签。这对于可能连接到不同网络或用于不同用途的电脑笔记本笔记本非常有用。你可以通过启动配置管理器来选择和创建配置。在终端窗口中使用 `-P` 输入 `firefox` 命令。

```
firefox -P
```

![](img/99301381a0d2790a6cdc2798147cbdad_212_0.png)

### 图 7-3：Firefox 附加项管理

系统已设置了一个默认配置。你可以创建一个新配置，运行配置向导以提示配置名称和要使用的文件夹。选择一个要使用的配置并点击“启动 Firefox”。下次启动 Firefox 时将使用你上一次使用的配置。你可以选择在启动时提示使用哪种配置，否则运行 `firefox -P` 命令来更改配置。

### Chrome

Google 的 Chrome Web 浏览器提供了早期且安全的 Web 访问方式，并与 Google 深度集成（见图 7-4）。你可以从 http://www.google.com/chrome 下载它。下载页面会显示你正在使用 Linux，并提供适用于 Fedora 和 Ubuntu 的选项。为你的系统选择适用于你架构的 Fedora RPM Chrome 包（32 位或 64 位）。然后你可以通过在下载对话框中选择“软件包安装器”（Package Installer）直接安装，它将使用 `PackageKit` 安装软件。安装过程还会下载并配置 chrome 存储库访问文件 `google-chrome.repo`，允许你使用 `PackageKit` 删除、更新和重新安装 Chrome (`google-package chrome`）。

你可以通过“应用程序 | 互联网 | Google Chrome”访问 Chrome。“开始使用 Google”（Get started with Google）选项卡提供了指向“Google Chrome 帮助中心”的链接，该中心提供详细的文档和支持。标签页具有优先级。Chrome 窗口顶部是已打开的 Web 页面标签页，末尾有一个 `+` 按钮用于打开新标签页。Chrome 具有一个简单的工具栏，带有导航按钮和书签按钮（星形图标）。要关闭标签页，点击地址栏上的 `x`；页面按钮显示 Web 页面操作（如搜索、打印和缩放）的下拉菜单。工具按钮（扳手图标）显示浏览器操作菜单项，如新标签页、全屏、历史记录、书签管理器、下载和扩展。要配置 Chrome，请从此菜单中选择“偏好”以打开 Chrome 偏好对话框。在这里，你可以设置主页、默认搜索服务（基础设置选项卡）、主题、密码和自动填充选项（个人信息选项卡），以及隐私和代理设置（底层设置选项卡）。

![](img/99301381a0d2790a6cdc2798147cbdad_213_0.png)

图 7-4：Chrome Web 浏览器 (Google)

## 第 7 章：网络应用 215

三个软件包：GNU Java 运行时 (`libgcj`)、Eclipse Java 编译器 (`ecj`) 以及一组包装器和链接 (`java`)。`java` 和 `libgcj` 包是默认安装的。

| 应用 | 描述 |
| --- | --- |
| Java 2 软件开发包 (SDK), JDK | 开源 Java 开发环境，包含编译器、解释器、调试器等。http://openjdk.java.net。Java 2 平台的一部分。作为 Red Hat Enterprise Linux 6 发行版的一部分包含 `java-1.6.0-openjdk-dev` 中。 |
