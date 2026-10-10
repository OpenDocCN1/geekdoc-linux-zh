
# 序言

Netscape/Mozilla 与我见或处理过的任何东西完全不同。首先，这个新版本的 Netscape 不仅仅是一个浏览器，它还是能够托管应用程序的平台。`Netscape` 随附的主要示例有 `AIM`、`邮件/新闻客户端`、一个名为 `Composer` 的所见即所得 HTML 编辑器、`Chatzilla IRC` 客户端以及浏览器本身。扩展程序，如今天 Firefox 可用的扩展，与此密切相关。

我们并没有使用 `C` 或 `C++` 结合如 `MFC` 或 `Gtk+` 等原生平台 GUI 工具包提供的 API 为这些应用程序构建图形用户界面（GUI），而是使用了 `Netscape/Mozilla` 开发的技术。使用静态扩展标记语言（`XML`）文件来描述用户界面的布局，就像使用 `HTML` 描述 Web 页面的布局一样。为此目的开发的 XML 方言被称为 XML 用户界面语言（`XUL`）。`JavaScript` 代码通过类似于链接到 HTML 元素的属性的方式，用于响应菜单选择和点击。

要在 `Netscape/Mozilla` 上构建应用程序，只需要 `XML` 和 `JavaScript` 的组合；因为 `JavaScript` 和 `XML` 本身是可移植的，所以使用它们设计的接口也是。当 `JavaScript` 不足以完成工作时（任何应用程序都是如此），`JavaScript` 代码可以调用位于共享库中的 `C++` 函数。这些函数通过两种技术在 `Netscape/Mozilla` 架构中直接支持：`XPConnect` 和 `XPCOM`。这些技术允许合格的开发者使用接口描述语言定义平台无关的接口。

使用 `XPCOM` 和 `XPConnect`，`JavaScript` 代码可以查询组件是否存在。顺利，`JavaScript` 将获得一个用 `C++` 编写的对象，并能够实现 `JavaScript` 程序员梦寐以求的功能。这些接口本质上是高度平台无关的。

然而，不仅仅是 `Netscape/Mozilla` 的架构让浏览器以及相关应用程序（`AIM`、`Mail`、`Composer`）具有了移植性。要实现这种工作，不仅需要坚固的架构，还需要一套政策和程序文化，将跨平台开发置于优先事项的顶位——此外还需要大量的自律来确保这些最佳实践得到遵循。`Tinder` 和 `Bugzilla` 等工具（这两者在书中均有描述）都得到了 `Netscape` 和 `Mozilla` 的投资，而这些投资获得了丰厚的回报。

工程师被迫考虑其他平台，而不仅仅是自己的平台；而且在仅一个平台上进行日常测试时出现的回归问题可能会停止所有平台的开发，而不仅仅是受影响的那一个，因为 `Netscape` 和 `Mozilla` 意识到，实现移植性的唯一真正途径就是处理眼下的问题。

本书的很大一部分内容脱离了代码，描述了这些最佳实践：无论你的架构支持跨平台的能力如何，你都必须对你计划支持的所有平台投入同等水平的关注和奉献进行开发，它们才能以同样的质量到达终点。

正如我们编写的程序由数据结构和算法组成一样，在我看来，移植性在很大程度上取决于架构和流程，这一信念是你现在手中这本书的基础。

## 书籍结构

本书由一系列主题章节组成。这些章节中的大部分由一组项目组成，每个项目涵盖一个支持章节整体主题的特定话题。

在书的开头，你将发现一些章节包含了最佳实践的项目，这些实践必须传达给整个开发组织，包括管理层、开发人员和测试人员。随后的章节涵盖了管理层应该注意的软件工程主题，但这些章节主要是为将实现代码的读者编写的。总之，这些初始章节中介绍了 23 个项目。

用户界面的实现是跨平台桌面应用开发中的主要关注点。项目 23 用于介绍这一话题。因此，本书的最后两个章节致力于跨平台 GUI 相关主题。

其中第一个章节提供了 `wxWidgets` 跨平台工具包的全面介绍和教程。在读完我对 `wxWidgets` 的介绍后，你可能想查看 Julian Smart 等人 Prentice Hall 出版的该主题的详细著作《使用 wxWidgets 进行跨平台 GUI 编程》`Cross-Platform GUI Programming with wxWidgets`。`wxWidgets` 并不是你项目中唯一可跨平台 GUI 工具。另一个非常流行的跨平台 GUI 工具包 `Qt` 未在书中介绍。然而，如果你对 `Qt` 感兴趣，目前有几本书详细涵盖了该主题，也许最著名的是 Jasmin Blanchette 和 Mark Summerfield 由 Prentice Hall 出版的《使用 Qt 4 进行 C++ GUI 编程》`C++ GUI Programming with Qt 4`（另见他们针对 Qt 3 的书）。

本书的最后一章——第 9 章“用 C++ 开发跨平台 GUI 工具包”，从对跨平台 GUI 工具包 `XPToolkit` 的介绍开始，它是 `Netscape` 和 `Mozilla` 跨平台浏览器套件的主要组件。随后，它将介绍我专门为本书创建的工具包 `Trixul` 的实现。

`Trixul` 具有许多我们在 `Netscape` 构建跨平台 GUI 时所用的 `Netscape/Mozilla XPToolkit` 的许多属性。例如，`XPToolkit` 和 `Trixul` 都允许你使用 `XML` 和 `JavaScript` 描述界面，两者都支持基于组件的模型，允许界面调用 `C` 或 `C++` 共享库，并且都具有高度的可移植性。

然而，`Trixul` 与 `Mozilla` 提供的工具之间有两个主要区别：第一，`Trixul` 是一个桌面 GUI 工具包，而 `XPToolkit` 应用在 Web 浏览器的环境中执行。第二，`Trixul` 的整体设计（我认为）比 `XPToolkit`（我确定）要简单得多，这让我能够很好地描述工具包的架构及其设计背后的概念，否则我可能无法做到这一点。

我并不真正期望你会为你的项目设计一个自定义的跨平台 GUI 工具包，但观察 `Trixul` 是如何设计和实现的可以学到很多东西。

在很大程度上，章节都编写得可以按任何顺序阅读。如果你是技术管理人员，我建议仔细阅读以下章节：

- 第 5 章“操作系统”

### 关于 Trixul 的说明

`Trixul` 是我为了协助本书而的一个开源项目。在写本书时，该项目还处于婴儿阶段。如果你喜欢 `Trixul` 并兴趣为其开发做出贡献，或进行移植工作，我非常希望听到你的消息。你可以访问 `www.trixul.com` 或 SourceForge 上的页面 `http://sourceforge.net/projects/trixul` 了解更多信息。

`Andrew Oram and Steve Talbot, Managing Projects with make (Sebastopol, CA: O’Reilly Media, Inc., 1993).`

`Eric S. Raymond, The Art of UNIX Programming (Reading, MA: Addison-Wesley, 2003).`

`Julian Smart, et al., Cross-Platform GUI Programming with wxWidgets (Upper Saddle-River, NJ: Prentice Hall, 2006).`

`Bjarne Stroustrup, The C++ Programming Language (Reading, MA: Addison-Wesley, 2000).`

# 致谢

正如你可能想象的那样，写书是一项非常孤独的努力。然而，实际上，出版一本书绝非单打独斗——它需要许多人的才华、时间和奉献，才能将我的想法从概念到完成最终呈现在纸上。本着这种精神，我想感谢以下人员在帮助我完成这本书方面所做出的贡献。

首先，感谢 Prentice Hall 的 `Greg Doch` 信任我，并给了我一个再次将我的想法写在纸上的机会。他的助理 `Michelle Housley` 在过程中提供了许多必要的支持。我还要感谢培尔教育（Pearson Education）的团队，他们帮助将我的手稿变成了最终形式，包括 `Keith Kline`。

我特别感谢 `Anne`，她愿意配合我处理我所要求的许多“微小”修改，这些修改给她造成了额外的工作（更不用说每次收到我发来的带有“最新修正”的新邮件时了）。我心里毫无疑问，这些请求确实增加了她的工作量，但她仍然仔细地考虑并准确执行了我的每一项请求，完美无缺且从无怨言。她应该得到额外的“感谢”。

按照惯例，所有未被他们发现的错误仍由我本人负责。（关于这一点，请访问 `www.crossformbook.com` 查看该版本的勘误表。）
