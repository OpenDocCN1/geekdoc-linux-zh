
# Linux 业务桌面迁移

Konqueror 是 KDE 桌面环境不可或缺的一部分，虽然它是一个 Web 浏览器，但同时也作为文件管理器和通用查看应用程序。尽管它是 KDE 桌面的一部分，但它也可以在 GNOME 等其他桌面环境中运行。无论如何，由于其多功能性，它是开源领域最优秀的工具之一。初看之下，Konqueror 看起来与 Mozilla Firefox 非常相似，但检查后会发现，Konqueror 拥有更广泛的功能集。它与 Windows Explorer 有相似之处，但没有将 Web 浏览器/文件管理器与操作系统紧密结合带来的安全风险。Konqueror 支持基于标签的浏览，并具有与 Firefox 类似的集成搜索栏。Konqueror 使用 KHTML 渲染引擎，该引擎也用于苹果的 Safari 浏览器。除了网页浏览，Konqueror 还能执行许多任务：

- **文件管理器：** Konqueror 是 Linux 上最强大的图形化文件管理器。它具有操作文件并以多种视图提供文件的能力。
- **可定制应用程序：** 与 Firefox 类似，Konqueror 可以使用 Konqueror XML 配置扩展附加功能，添加工具栏和小部件，使 Konqueror 更加实用。
- **通用文件查看器：** Konqueror 可查看多种不同的文件格式。对图像点击右键可以允许你直接在 Konqueror 中查看图形。此外，还可以使用 `Kparts` 库查看演示文稿和文档。

图 7.11 显示了 Konqueror 如何桥接文件管理器和 Web 浏览器之间。

![](img/72e1c6125676a623b5032cfdab8d797c_216_0.png)

**图 7.11** Konqueror 可以使用分屏视图并排显示网页，或在网页旁边显示文件系统。

一个显著的区别是，Konqueror 的设置跨越系统，在你熟悉调整环境的适当方法时可能需要花一点寻找。虽然 Konqueror 菜单的许多地方都可以调整不同的设置，但最核心的地方是在“设置（Settings）”菜单下。在这里，你可以配置 Konqueror 的外观、感觉及其行为。

## 使用 Konqueror 作为网络工具

在导航文件夹与网页时，你将获得不同的呈现。使用 Web 视图查看文件夹可能并不实用。侧边栏提供了快捷方式和特殊功能，可以更容易找到你正在搜索的内容。你可以使用 Konqueror 定位网络，或作为使用 `fish` 协议的图形化 `SSH` 工具。

Konqueror 提供了一些基于标准的浏览器；它还具有一些独特的功能，使其与网站及系统的其他部分相互操作。你可能希望使用 Mozilla 浏览器之一进行大多数网页浏览，这也是你安装插件的方式。以下是一些帮助提升 Konqueror 浏览体验的技巧和提示。

- **使用 Netscape 书签：** 如果你使用 Netscape 或 Firefox，一个非常有用的功能是点击“书签（Bookmarks）”菜单并选择“编辑书签”。书签编辑器中有一个选项允许你勾选“在 Konqueror 中显示 Netscape 书签”。这将使你能够使用与其他浏览器中相同的书签。
- **使用插件：** 可以单独为 Konqueror 安装书签，但使用 Firefox 的插件服务来定位并安装插件，然后指向 Konqueror 会更简单。一旦安装了插件，转到 Konqueror 设置并选择“配置 Konqueror”。选择“插件（Plug-ins）”选项；在这里你可以添加你的 Firefox 或 Netscape 插件（可能位于 `/home/USER/firefox/plugins` 或 `/usr/lib/mozilla/plugins`）。一旦 Konqueror 扫描了插件，在你在使用程序时它们应该是可。
- **浏览器识别：** 一些网站尝试判断你使用的是 Internet Explorer 还是其他浏览器。你可以通过“工具（Tools） -> 配置 Konqueror -> 用户代理（User Agent）”将你的浏览器识别设置为另一个浏览器。这是由于开发者没有遵守浏览器如何识别自身的严格标准。

除了作为 Web 浏览器有用外，Konqueror 还可以作为网络工具发挥多种功能，包括 `ssh` 前端或 `ftp` 客户端。

- **图形 SSH 客户端：** `Fish` 允许用户通过拖放文件通过 `SSH` 访问文件。`SSH` 是安全连接 Linux 计算机流行方式，但它通常在命令行运行。要访问运行 `SSH` 守护进程的另一个 Linux 服务器，输入 `fish://ip_address`，其中 IP 地址是另一台计算机的网络地址。用户将访问服务器之间的安全通道。
- **FTP 客户端：** 通过在你的 `ftp` 位置加上 `ftp` 前缀，Konqueror 可以轻松地作为 `ftp` 客户端工作。如果需要身份验证，Konqueror 将提示你输入用户名和密码。

## 其他 Konqueror 功能

Konqueror 拥有许多超出你对浏览器和文件管理器预期的功能。其中许多功能归功于 Konqueror 作为 KDE 桌面核心的受欢迎。然而，Konqueror 还有一些额外的优势。Konqueror 不仅仅是一个 Web 浏览器或文件管理器；它是 KDE 桌面的核心功能之一（当然，它在 GNOME 下也可以运行）。例如，如果你想查看文档，可以在位置栏中输入文件位置，文档将在 Konqueror 框架中打开。另一个用于比较文档的功能是，你可以在 Konqueror 的分屏视图中打开它们并并排比较。Konqueror 的另一个功能属于系统管理。`FSView` 工具通过“视图（View） -> 视图模式（View Mode） -> 文件大小视图（File Size View）”在 Konqueror 中提供了文件系统的图形视图，让你看到单个文件占用的空间，如图 7.12 所示。

Konqueror 是 Linux 桌面的核心技术之一（尽管是原生的 KDE），你将发现它提供了超越任何应用程序分类的广泛功能。

## Opera

多年来，Opera 作为从 PC 操作系统到移动设备的平台浏览器，一直拥有创新者的声誉。虽然 Firefox 是最近的浏览器宠儿，但 Opera 在 Windows 和 Linux 上已经存在很长时间了。Opera 浏览器具有许多与 Firefox 和

![](img/72e1c6125676a623b5032cfdab8d797c_219_0.png)

图 7.12 FSView 在 Konqueror 内部提供了 Linux 文件系统空间的使用视图。

Konqueror 拥有这些功能，但它也以资源占用极轻量和具有创新性闻名，并拥有独特的功能。

- **平铺式浏览或标签页浏览：** Opera 提供平铺式或标签页浏览两种选择。
- **KIiosk 模式：** Opera 的一个有趣功能是它可以作为代理来锁定桌面。

*Opera 浏览器并非没有限制。你可以免费下载它，只需忍受广告，如图 7.13 所示。*

![](img/72e1c6125676a623b5032cfdab8d797c_220_0.png)

图 7.13 Opera Web 浏览器是另一个跨平台浏览器，可以在迁移到 Linux 之前在 Windows 上使用。

## 插件

Linux Web 浏览器的一个陷阱是，许多网站使用了专为 Windows 设计的的特殊插件。那些没有使用基于标准的技术的插件通常无法按预期运行。在大多数情况下，最常见的插件（如 Macromedia 的 Flash 插件、Adobe Reader 和 Real Player）是可以正常工作的。然而，你可能会遇到专有格式的问题。对插件的支持在不断变化，因此最好参考你浏览器的支持网站以获取最新动态。

在 Linux 上安装 Java 插件并不是一个非常直观的过程。Sun 确实提供了 Java 插件的 RPM 包，但取决于你的安装类型，你可能需要创建一个符号链接（Linux 等同于 Windows 快捷方式）。Linsphere 许可了在其版本的流行的开源 Xine 多媒体播放器中播放 Windows 媒体文件所需的代码，可以在浏览器中播放 Windows 媒体文件，但并非所有文件都受到数字权利管理（DRM）的保护。多媒体领域争议最大的方面之一（特别是对于 Linux 桌面用户来说）是 Windows 和 Apple OSX 下使用的数字权利管理在 Linux 下无法工作。你可能通过在 Linux 下的虚拟机中运行 Windows 副本来最容易地解决这个问题。如果需求适中，你可以使用在 Wine 下运行的 Windows Media Player，Wine 是在 Linux 和其他 Unix 系统上运行的 Windows API 替代品。
