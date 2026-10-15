
Alpha、Beta 和候选发布（Release Candidate）版本。在版本 1.4 完成之前，1.4alpha 和 1.4beta 版本是 1.3 版本的衍生，它们比 1.3 更完善，但均未完全完成，也没有作为 1.4 版本发布。候选发布版本是接近完成的 Beta 版本，如果它们通过了最后的测试，就可能成为最终发布版本。

Talkback 版本（Talkback releases）。发布的其他版本可能包含 Talkback 技术，该技术会在浏览器崩溃时捕获状态并将结果通过电子邮件发回给 mozilla.org。这用于计算平均故障间隔时间（mean-time-between-failures）工程指标以及调试目的。

夜快版（Nightly）和调试版（debug releases）。每晚生成的版本包含最新的更改，是这些工作可能性最低的版本。它们在编译时开启了额外的调试功能，高级技术用户将其作为分析工具使用。包含调试功能的平台和应用程序。

自定义版本（Custom versions）。由于源代码是免费提供的，使用合适的计算机就可以编译该平台。许多时间选项可以改变最终二进制文件中包含的功能集。通过修改默认功能集，自定义平台面临着风险。这种风险在于，大部分进展都假设默认功能始终可用。特殊的自定义版本必须必须接受这样一个事实：它们可能跟不上平台主流的变化，并且无法运行某些 Mozilla 应用程序。

本书使用了标准平台的最终版本、次版本或大版本。

### 1.1.2 示例应用程序

构建在 Mozilla 平台上的某些较知名 Web 应用如下：

- Netscape 7.0。这是 Mozilla 的商业版，包含了支持 AOL Time 在 Web 和互联网领域业务目标的功能。其主要的技术差异在于：支持 AOL 名称标识；与 AOL 服务器端设施集成；缺乏弹出窗口抑制功能；自定义 cookie 处理；以及对用户界面的通用清理。Netscape 7.0 基于 Mozilla 1.01。Netscape 6.x 也是基于 Mozilla 的；但它是基于 0.94 版本，且存在大量 Bug。

- Compverse 7.0。AOL 同样拥有这一较旧的基于 Web 和互联网的服务，它仍然拥有庞大的用户群。7.0 版本是一个基于 Mozilla 1.0 的工具。

- 适用于 MacOS X 的 AOL 8.0。这是 AOL 的旗舰 Web 和互联网客户端，拥有非常大的用户群和高度自定义的界面。通过 8.0 版本，AOL 的 Macintosh 版本已从 Internet Explorer 迁移到 Mozilla 1.01。

## 基础概念 第1章

## Mozilla 浏览器。这个 mozilla.org Web 浏览器比经典浏览器（Classic Browser）更紧凑、更高效。

OEOne 和 ActiveState 提供了两个非 Web 应用的示例。

OEOne (`www.oeone.com`) 的产品旨在让新手轻松使用个人电脑。他们的 OEOne HomeBase 是 Linux 和 Mozilla 平台增强版（Penzilla）的结合。它提供了一个与计算机交互的完整系统。图 1.1 显示了这个基于 Mozilla 的桌面的布局。

ActiveState (`www.activestate.com`) 为软件开发者生产集成开发环境（IDE）工具。Komodo 项目基于 Mozilla 平台。图 1.2 是该产品的截图。

除了 Web 和非 Web 应用外，高度自定义的应用也是可能的。标准的 Mozilla 平台在每个桌面上都提供相同的界面，这涉及到一些妥协。曾多次尝试创建与某个特定平台外观和感受完全匹配的浏览器产品。这些深度定制的 Mozilla 分肢使用了本书未涵盖的嵌入技术：

![](img/319913ee3703286e2c03d285fbfc49c7_33_0.png)

图 1.1 OEOne HomeBase 桌面。经 OEOne 公司 (`www.oeone.com`) 许可。

## AppDevMozilla-01 第 7 页 2003年12月4日 星期四 下午 6:22

## 1.1 理解 Mozilla 产品名称

![](img/319913ee3703286e2c03d285fbfc49c7_34_0.png)

图 1.2 ActiveState 的 Komodo 2.0 IDE。经 ActiveState (`www.activestate.com`) 许可与谢意。

**Chimera。** 一种基于 Cocoa 界面的 Macintosh MacOS X 浏览器，具有传统菜单。

**Galeon, Nautilus。** 与 GNU/Linux GNOME 桌面紧密集的浏览工具。标准平台通过即将对 GTK 2.0 的支持来解决集成问题。

**Meleon。** 一种 Microsoft Windows 浏览器，将 Mozilla 转换为 ActiveX 控件。工具栏与简单的 Internet Explorer 非常相似。

基于 Mozilla 平台的应用程序数量正在稳定增长，大约每个月都会发布公告。mozilla.org 是获取新产品公告的好地方。

### 1.1.3 术语

Mozilla 文化和 mozilla.org 文档包含一些俚语。涵盖所有术语是一项徒劳的任务。参考 `www.mozilla.org/docs/argon.html`，以下是更可见的术语：

- **XP.** 跨平台（Cross platform），意味着可移植的，如 `XPCOM`, `XPInstall`, `XPIDL`。

- **FE.** 前端（Front end），Mozilla 的图形显示部分。

- **BE.** 后端（Back end），Mozilla 的网络部分。

- **I18n.** 国际化（Internationalization） = 18 个字母。

- **L10n.** 本地化（Localization） = 10 个字母。针对特定区域语言的定制。

- **The tree（树树）。** Mozilla 源代码和编译系统。

- **Bloat.** 臃肿（倾向于增加冗余内容）。

# 基础概念 第1章

XML 的应用广泛；尽管如此，任何人都可以随时创建新的 XML 应用程序。这是一种高度灵活的。此外，XML 标准允许将 XML 应用程序的部分实例（称为文档片段）混合在一个文档中。一个文档可以同时包含 HTML 和 SVG。这是非常灵活的。

灵活性是一个流动的状态，为创新提供了肥沃的土壤。文档作者可以自由创建特定 XML 应用程序的任何实例，这是常识。软件开发者可以自由创建任何 XML 应用程序定义。新的应用程序定义可以作为新内容或新区域系列新文档的基础。

Mozilla 受益于其灵活性。它实现了几个创新的 XML 应用程序，特别是 XL（XML 用户界面语言）和 XBL（XML 绑定语言），许多特殊用途的 XML 文档都基于这些语言。它允许程序员生成通用的 XML 内容并创建特定的应用程序，如 RDF 和 XHTML。

## 1.2.3 超越英语

XML 的另一个优势是它能够通用的表达。

Unicode 标准是人类书写使用的每个字符的列表。当 Unicode 引用和字体结合时，就可以显示一个字符（也称为字形）。XML 文档可以引用 Unicode 标准中的任何项目，因此 XML 是用地球上任何语言表达信息的有用方式。

现代计算世界的早期成功发生在西方的英语国家，有些在加利福尼亚大学伯克莱分校，有些在 AT&T。当时似乎八位（字节字节）足以捕捉普通英语文本中的所有字形。这导致了 ASCII 字符集、C 语言的 `char` 类型以及 UNIX 操作系统中的处理被固定为一个字节。这一遗留为 Unicode 标准制造了障碍，因为每个字符需要两个字节。XML 是绕过这一障碍的方法之一，因为它从一开始就采用基于 Unicode 标准的新格式。

Mozilla 是一个依靠 XML 和 Unicode 技术处理国际问题的工具示例。它主要支持的语言 JavaScript 也是基于 Unicode 的。

## 1.2.4 层次化思维

XML 的最终优势在于它的内部结构。根据 XML 标准创建的文档由相互嵌套在内部的片段组成，以层次化的方式。层次化组织是人类易于理解的概念。正如谜语所说，圣伊夫的男人有七个妻子，每个妻子七个袋子，每个袋子里装有七只猫，每只猫有七只小猫。

这就是层次化思维。

简单的概念在计算机计算中尤为重要，因为与计算机工作是一项抽象任务。即使在计算机之外（例如本书），层次化组织也为复杂的信息流带来了秩序。对于计算机程序员来说，XML 的层次化本质是表达解决方案并完成工作的一种简单方法。

## 1.3 平台概念

现在让我们转向 Mozilla 平台本身的本质。软件平台是程序员用作踏脚石的软件。通过站在平台特性之上（创建高层级功能的任务变得更简单）。程序员不需要花时间使用 C 等语言来制作基本功能。
