
# 第 22 章 电子邮件与网页浏览 613

（例如，`cat index.html | w3m -T text/html`）。使用 `Page Up` 和 `Page Down` 键翻页文档。在链接上按 `Enter` 跳到该链接。按 `B` 返回上一个链接。分别使用 `/`（斜杠）和 `?`（问号）键向前向后搜索。

w3m 似乎是这些浏览器中最复杂的。它具有默认字体选择功能，并且似乎很好地处理框架；其色彩的使用使其易于使用。链接浏览器允许你使用鼠标剪切和粘贴文本。

你可以通过输入文件名来启动任何基于文本的 Web 浏览器，如果你有活动连接，可以将 Web 地址作为命令名的选项。例如，要用 w3m 浏览器读取 w3m 文档（HTML 格式），请在终端窗口或 shell 界面中输入以下内容：

```
$ /usr/share/doc/w3m/*MANUAL.html
```

屏幕将显示 W3M 手册的 HTML 版本。或者你也可以给 w3m 一个网页的 URL，如下：

```
$ w3m.handsonhistory.com
```

页面打开后，你就可以查看页面并移动到包含其中的链接了。首先使用方向键移动并选择链接。使用 `Page Up` 和 `Page Down` 键翻阅文本。

## 运行 Firefox 浏览器

Firefox 是 Mozilla 最新的 Web 浏览器，旨在为 Web 浏览器设定新的方向和标准。尽管 Firefox 最近刚升级到 1.0 版本（标志着正式发布），但它已经是 Fedora 和其他 Linux 系统的默认 Web 浏览器。

Firefox 正被誉为 Microsoft Internet Explorer 的首选替代方案。因此，除了用于 Linux 系统外，数百万份副本已下载到 Windows 系统。Mozilla 项目在 Mozilla.org 网站（www.mozilla.org/products/firefox/switch）上为从 Internet Explorer 切换过来提供了帮助和鼓励。

Firefox 包含了与 Firefox Navigator 相同的渲染引擎（cko），但用户界面和许多安全特性都是全新的。Firefox 还具有更快的性能，并且占用的内存更少。因为它没有包含所有的邮件、新闻、IRC 和类似的客户端（这些可以从 Mozilla 单独获取），它的加载和启动速度应该比 Mozilla Navigator 快。如果你正在使用 Mozilla 以外的应用程序提供这些功能，那么 Firefox 可能适合你。

## 614 第四部分 ♦ 运行应用程序

Firefox 随书中提供的几个 Linux 发行版。你可以在 www.mozilla.org/products/firefox 下载最新的 Firefox 版本。在编写此时，Firefox 1.5 即将完成。

Damn Small Linux 发行版的一个不错特性是它提供了一个菜单选择，允许从可启动的 Linux 环境下载并启动 Firefox。选择 MyDSL 图标，然后从网络按钮选择 Firefox Web Browser。

## 扩展 Firefox

Firefox 能够轻松处理大多数标准的 Web 内容（HTML、JPEG、文本文件）。对于任何浏览器，某些内容都需要添加插件或辅助程序才能播放或显示该内容。Firefox 还允许你添加扩展，以增强 Firefox 的功能。

大多数适用于 Mozilla Navigator 的插件也将同样适用于 Firefox。请参阅本章之前关于 Mozilla 插件的描述，以获取有关为 Mozilla 和 Firefox 浏览器添加插件的信息。

除了插件，Firefox 还允许你添加扩展和主题，可以从 Mozilla 的 Firefox 产品页面（www.mozilla.org/products/firefox）开始。从那里，点击“获取扩展和主题”。接下来的章节将描述一些流行的 Firefox 扩展和主题。

## 添加 Firefox 扩展

这里是 Mozilla.org 提供的一些最流行的 Firefox 扩展：

- **下载工具 (FlashGot)** —— 如果你喜欢从浏览器下载组文件，FlashGot 可以是一个非常实用的工具。安装 FlashGot 后，你可以选择单个文件、通过高亮网页上的链接识别出的文件，或从当前网页链接的所有文件。它有一个“构建图库”（Build Gallery）功能，可以让你一次性识别一系列文件名。

- 安装 FlashGot 后，你可以通过选择 `Tools > FlashGot` 在 Firefox 中访问它，然后从菜单中选择一个功能。在 Fedora Core 中，Firefox 将请求传递给 KGet 以完成下载。你可以获取其他工具来代替 KGet。

- **选择性拦截广告 (Adblock)** —— 使用 Adblock，你可以选择性地防止广告在网页上显示。安装 Adblock 后，Firefox 右下角会出现一个 Adblock 按钮。点击它可以看到一个包含当前页面上你想拦截的项目的窗口。在图像上点击右键并选择 Adblock image 以拦截来自特定网站（例如 www.example.com/*）的广告。从 Firefox 中打开 Adblock 偏好（`Tools > Adblock > Preferences`）来查看、编辑或删除被拦截的网站。

## 第 22 章 ♦ 电子邮件与网页浏览 615

- * 标签页浏览 (Tabbrowser Preferences) —— 虽然 Firefox 已经提供了一些使用标签页在同一个 Firefox 窗口中打开多个网页的好功能，但 Tabbrowser Preferences 将这些功能更进一步。选择 `Edit ✎ Tabbed Browsing`。标签页浏览让你精炼 Firefox 中的工作。你可以设置选择标签页的方式（例如鼠标悬停而非点击）、将标签页放在底部，或选择是否在新标签页中加载主页。

- * 关注你的天气 (ForecastFox) —— 通过 Firefox，你选择的任何区域的最新天气只需点击一下。在安装 ForecastFox 并重启 Firefox 后，会弹出一个窗口让你配置 Firefox。选择你想要关注的天气区域。Firefox 右下角会出现天气图标。将鼠标悬停在图标上可以查看来自 www.weather.com 的详细天气报告。

- * 检查速度 (Bandwidth Test) —— 使用 Firefox，你选择的任何区域的最新天气只需在 Firefox 中点击一下。在安装 ForecastFox 并重启 Firefox 后，会弹出一个窗口让你配置 Firefox。选择你想要关注的天气区域。Firefox 右下角会出现天气图标。

- 选择性拦截广告 (Adblock) —— 使用 Adblock，你可以选择性地防止广告在网页上显示。安装 Adblock 后，Firefox 右下角会出现一个 Adblock 按钮。点击它可以看到一个包含当前页面上你想拦截的项目的窗口。在图像上点击右键并选择 Adblock image 以拦截来自特定网站（例如 www.example.com/*）的广告。从 Firefox 中打开 Adblock 偏好（`Tools > Adblock > Preferences`）来查看、编辑或删除被拦截的网站。

- 检查速度 (Bandwidth Test) —— 使用 Bandwidth Test，在 Firefox 中，你可以检查你的连接速度。

