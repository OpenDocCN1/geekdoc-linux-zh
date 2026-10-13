
要浏览网页，只需网页浏览器和互联网连接。假设你已处理好互联网连接，那么只需了解 Red Hat Linux 中的网页浏览器。

## 查看 Red Hat Linux 中的网页浏览器

Red Hat Linux 附带 Mozilla 网页浏览器。Mozilla 是 Netscape Communicator 的开源版，正取代 Netscape 成为 Red Hat Linux 的主要浏览器。

Red Hat Linux 还包含其他浏览器。我会简要提及，后续主要聚焦 Mozilla。主要浏览器如下：

- `Mozilla`：老牌工作马 Netscape Communicator 的重生版，更好。包含邮件和新闻阅读器。浏览器称为 Mozilla Navigator，或简称 Navigator。
- `Epiphany`：GNOME 浏览器，使用部分 Mozilla 代码绘制网页，界面更简单。默认未安装，应在本书附带 DVD 上。找不到可从 `epiphany.mozdev.org` 下载。
- `Konqueror`：KDE 浏览器，同时是文件管理器和通用查看器。

除此三款外，还有许多应用可下载显示网页。

## 启动 Mozilla

从 GNOME 桌面可通过两种方式启动 Mozilla：

- 在 GNOME 或 KDE 面板点击 Web 浏览器图标（地球和鼠标）。
- 选择 主菜单→Internet→Mozilla Web Browser。

启动后显示浏览器窗口及默认主页，可配置为其他页面。

## 学习 Mozilla 用户界面

Figure 2-4 显示 Wiley 网站页面及 Mozilla 浏览器窗口主要元素。

Mozilla 界面功能丰富，易于掌握。可关闭繁杂项目，也可先从基础开始逐步扩展。

点击关闭侧边栏

![](img/a7eec43a54473e95dc5ea333fecf1bd7_393_0.png)

Figure 2-4:

Mozilla 网页浏览器运行中。

From www.dummies.com. Copyright © 2003 by Wiley Publishing, Inc. All rights reserved.

Reproduced here by permission of the publisher.

## Mozilla 工具栏

从窗口顶部起为标准菜单栏，其后为导航工具栏，再为较细的个人工具栏，含 Home、Bookmarks 等图标。个人工具栏下方垂直分为侧边栏和显示当前网页的主区域。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_393_1.png)

注意侧边栏上的 X 按钮，点击后侧边栏消失。建议关闭以显示更多网页内容。

无侧边栏时窗口更简洁（图 2-5）。可清晰看到菜单栏及导航工具栏、个人工具栏。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_394_0.png)

Figure 2-5:

关闭侧边栏以简化 Mozilla 用户界面。

From www.dummies.com. Copyright © 2003 by Wiley Publishing, Inc. All rights reserved.

Reproduced here by permission of the publisher.

菜单栏下方导航工具栏按钮功能：

- `Back`：返回上一页。
- `Forward`：前进到后退来源页。
- `Reload`：重新加载当前页。
- `Stop`：停止加载。
- `Location text box`：显示当前页 URL，可输入 URL 访问。
- `Search`：用当前页 URL 作为搜索串搜索 Netscape 搜索站点（`search.netscape.com`）。
- `Print`：打印当前页，可预览。
- `Mozilla icon`：前往 Mozilla.org 网站（`www.mozilla.org`）。

其下为个人工具栏，含 Home 和 Bookmarks：

- `Home`：到主页。
- `Bookmarks`：显示菜单，可添加书签和管理。

个人工具栏还有 Red Hat Network 链接，可注册接收 Red Hat Linux 更新。其余链接按文件夹组织，点击文件夹显示下拉列表。

## 状态栏

窗口底部为状态栏，中间显示 Mozilla 加载网页时的状态信息。

左侧有多个图标，悬停显示气泡帮助。点击可打开其他 Mozilla 窗口。表 2-1 说明图标功能。

**表 2-1 Mozilla 状态栏上的图标**

| 当点击此图标时 | 其执行以下操作 |
|---|---|
| [icon] | 打开另一个 Navigator 窗口。 |
| [icon] | 打开 Mozilla Mail 窗口阅读邮件和新闻组。 |
| [icon] | 打开 HTML 编辑器窗口准备 HTML 文档。 |
| [icon] | 打开地址簿窗口查找地址。 |
| [icon] | 打开 ChatZilla 窗口加入 IRC 频道聊天。 |

![](img/a7eec43a54473e95dc5ea333fecf1bd7_395_0.png)

状态栏右上角状态信息右侧有两个图标。左侧表示在线，点击可离线。右侧为安全挂锁。Mozilla 支持使用 SSL 协议传输加密数据的 HTTPS。当连接支持安全 HTTP 的服务器时挂锁锁定，否则打开表示不安全。安全 URL 以 `https://` 开头。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_396_0.png)

状态栏中间显示状态信息。下载完成后显示耗时秒数。

## Mozilla 菜单

菜单使用较少，但了解其功能有帮助。表 2-2 为概览。

表 2-2 Mozilla 菜单

| 此菜单 | 使你能够执行以下操作 |
|---|---|
| File | 打开文件或网页位置，关闭浏览器，通过邮件发送网页或链接，编辑网页，打印当前页，退出 Mozilla。 |
| Edit | 复制粘贴，查找当前页文本，编辑首选项。 |
| View | 显示/隐藏工具栏，重新加载页面，调整文本大小，查看 HTML 代码，查看页面信息。 |
| Go | 在访问历史中后退/前进，或跳转到最近访问页面。 |
| Bookmarks | 添加书签，管理书签，向个人工具栏文件夹添加链接。 |
| Tools | 搜索网页，管理图像加载、Cookie、存储密码等。 |
| Window | 打开其他 Mozilla 窗口，如 Mozilla Mail、Navigator、地址簿、编辑器。 |
| Help | 获取 Mozilla 在线帮助。 |

## 更改你的主页

主页是 Mozilla 启动时加载的页面。默认从 Mozilla.org 网站加载。更改很简单。

首先找到你想要设为主页的页面。你可以用任何方式到达该页面。你可以在搜索引擎上搜索想要的页面，也可以在位置文本框中输入 URL，甚至可能偶然进入一个你想设为主页的页面。无所谓。

当你正在查看感觉适合作为主页的网页时，从 Mozilla 菜单中选择 编辑→首选项。首选项窗口出现（如图 2-6 所示）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_397_0.png)

图 2-6：

点击“使用当前页面”按钮将当前网页设为主页。

在图 2-6 的右侧，注意到“主页”单选按钮是开启的。这意味着启动时 Mozilla Navigator 应显示主页。然后是主页的 URL，下面有一个“使用当前页面”按钮。点击该按钮即可将当前页面设为主页。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_397_1.png)

你可以使用首选项窗口设置许多其他选项。虽然我没有解释所有选项，但你可以随意点击来探索从此窗口可以做的一切。例如，你可以点击“选择文件”按钮，从本地系统中选择一个文件作为主页。

## 更改 Mozilla 的外观

Mozilla 支持主题。主题基本上是 Mozilla 用户界面的外观和感觉（包括背景和按钮的外观）。默认主题称为 Classic 主题，它提供与 Netscape 以前类似的外观和感觉。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_398_0.png)

Mozilla 还附带一个名为 Modern 的主题，你可以从网络上下载许多其他主题。访问 `themes.mozdev.org` 浏览一些可用的主题并下载你想要尝试的主题。你也可以通过从 Mozilla 菜单中选择 查看→应用主题→获取新主题 来获取新主题。

更改主题很容易。如果你想在选择主题之前先看到所选主题，请按以下步骤操作：

- 1. 从 Mozilla 菜单中选择 编辑→首选项。
- 首选项窗口出现。
- 2. 点击窗口左侧“外观”旁边的加号。
- “外观”项目展开。
- 3. 点击“主题”项目。
- 右侧现在显示可用的主题。
- 4. 点击你想要的主题。
