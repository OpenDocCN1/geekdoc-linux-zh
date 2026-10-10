
许多工作站存在的唯一目的是执行少数常见的任务——文字处理、使用电子表格进行数值计算、准备演示文稿以及制作图表或其他业务图形。这些任务非常重要，以至于处理它们的程序通常被捆绑在一起，成为一个被称为*办公套件*的包。在 Windows 世界中，最常见的办公套件是 Microsoft Office，但这个包不适用于 FreeBSD。本章描述了 FreeBSD 可用的办公工具，从可用工具概览开始，接着总结 FreeBSD 办公工具的常见功能和怪癖，最后以使用最强大的 FreeBSD 办公工具之一 OpenOffice.org 的示例会话结束。当然，办公套件足够复杂，本章无法比介绍这些程序做得更多。如需更多信息，请参阅相关程序的文档。

# 第 25 章：办公工具

## FreeBSD 可用的办公工具

FreeBSD 上有相当多的办公程序。三套程序很受欢迎：GNOME Office、KOffice 和 OpenOffice.org。也有不属于特定套件的程序，并且你可能能够像使用套件一样有效地使用这些独立程序。

### GNOME Office

GNOME Office 并非作为单一集成的程序组来构思的；相反，GNOME Office 开发人员已经吸收了最初作为独立包开始生命周期的程序。然而，GNOME Office 组件确实使用某些公共库，例如 GIMP Tool Kit (`GTK+`)，它最初是作为 GNU Image Manipulation Program (`GIMP`) 的 GUI 工具包开发的，但后来被 GNOME 和许多其他程序采用。正在进行中的工作旨在提供数据共享，并在尽可能提供组件程序之间的集成文件格式。这并不是说这些程序构成了一个排他性的俱乐部或必须作为一组使用；你可以只安装一个 GNOME Office 组件并使用它，而不使用其他 GNOME Office 组件，也许可以在它和一些无关的程序之间传输文件。

你可以在 `http://www.gnome.org/gnome-office/` 找到 GNOME Office 组件的完整列表。该列表包括 14 个类别中的组件：电子表格、文字处理器、通信、浏览、矢量图形、光栅图形、图像查看器、电子邮件和群件、绘图、制表、项目管理、财务、演示文稿和数据库工具。某些类别包含多个程序。最引人注目的 GNOME Office 组件是

- **Gnumeric** 此程序是一个电子表格应用程序。`Gnumeric` 开发人员声称已经实现了 Microsoft Excel 中可用函数的 95%。该程序的文件名是 `gnumeric`。

- **AbiWord** 该程序是 GNOME 办公套件的 word 处理器。最初是作为跨平台工具开发的，`AbiWord` 可用于类 UNIX 系统（自然包括 FreeBSD）、Windows 和 BeOS。该程序的文件名为 `AbiWord`（`abiword` 作为链接）。

- **Galeon** 在第 24 章中提到的 `Galeon` Web 浏览器，被视为 GNOME 办公套件的一部分。该程序的文件名为 `galeon`。

- **The GIMP** GNU 图像处理程序（`GIMP`）是 FreeBSD 上功能最强大的位图图像编辑器，它也是 GNOME 办公套件的正式组成部分。第 26 章将更详细地介绍 `GIMP`。该程序的文件名为 `gimp`。

- **Dia** 该程序旨在创建图表，例如流程图、电路图等等。其角色大致类似于 Windows 程序 Visio，但 `Dia` 尚未像 Visio 那样成熟。该程序的文件名为 `dia`。

- **Guppi** 该程序是一个数据绘图程序——它接收其他程序生成的数据，并根据这些数据创建图表。因此，它在科学和商业事务中可能非常有价值。该程序的名称是 `guppi-gnumeric`。

- **Balsa** 该程序是一个电子邮件客户端，类似于第 24 章中描述的某些程序。该程序的文件名为 `balsa`。

- **Evolution** 该程序是 GNOME 办公套件的第二个电子邮件客户端。`Evolution` 支持的功能远多于 `Balsa`。该程序的文件名为 `evolution`。

- **Gnucash** 个人财务管理工具在家庭用户中变得很流行，而 `Gnucash` 可能是 FreeBSD 世界中最受欢迎的此类程序。该程序的文件名为 `gnucash`。

- **GNOME-DB** 数据库保存着关于几乎所有事物的关键信息，`GNOME-DB` 是 GNOME 办公套件的数据库访问和操作工具。该程序的文件名为 `gnomedb--fee`。

- **OpenOffice.org** GNOME 办公网站声称 `OpenOffice.org` 是一个尚未完全集成的组件。在 2002 年，我更喜欢将 `OpenOffice.org` 视为一个竞争的办公套件，并且在本章稍后的“OpenOffice.org”部分将其以此形式呈现。主程序的文件名为 `office`，但子组件也可以通过其他名称启动。

与一些集成的办公套件不同，GNOME 办公工具是独立安装的。大多数它们都作为 FreeBSD 软件包或 ports 在 `gnome` 区域中可用。值得注意的例外包括 `AbiWord`（可从 `editors` 区域获取）；`Sketch`（可从 `graphics` 区域获取）；以及 `Guppi`（可从 `math` 区域获取）。

GNOME 办公的优点包括 `GIMP`，它经常被与 Adobe Photoshop 进行有利的比较；`Gnucash`，其功能接近 Quicken；`Gnumeric`，这是 FreeBSD 上非常流行的电子表格；以及（在它确实成为 GNOME 办公组件的程度上）`OpenOffice.org`，它是 FreeBSD 中最接近完全替代 Microsoft Office 的产品。其他一些程序，如 `AbiWord`，虽然功能正常，但缺乏习惯于 Windows 应用程序的用户所期望的功能范围。当然，这并不总是坏事；UNIX 哲学传统上是将许多小程序组合起来，以提供在 Windows 世界中较大程序所拥有的功能。此外，大型办公包也因其巨大的资源需求而受到批评。

### KOffice

KOffice 之于 K 桌面环境（KDE），就相当于 GNOME 办公之于 GNOME。不过，KOffice 是从头开始设计作为 KDE 的办公套件的，而 GNOME 办公则是从许多独立项目的种子生长而来的。

KOffice 的主要网站是 `http://www.koffice.org`，你可以在那里找到有关该项目的更多信息。

KOffice 包含的组件和组件类型比 GNOME 办公少，但最重要的组件类型在两个套件中都有体现。KOffice 包括以下程序：

1. **KWord** 该程序是 KOffice 的 word 处理器。`KWord` 是一个基于框架的 word 处理器，提供了比 `AbiWord` 更多的功能。

2. **KSpread** 该程序是 KOffice 的电子表格。它实现的函数不如 Microsoft Excel 或 `Gnumeric` 多，但它基本上是一个可靠的产品。

3. **KPresenter** 该程序处理演示文稿。`KPresenter` 演示文稿的在线示例可在 `http://www.kde.org/kdslides/` 获取。

4. **Kivio** 该程序是一个类似于 Windows 程序 Visio 或 GNOME 办公的 `Dia` 的流程图程序。`KVivio` 提供了一个插件脚本系统，使你能够以各种方式扩展该程序。例如，你可以使用此功能向 `KVivio` 提供 C++ 头文件，让它生成类图。

5. **Kontour** 矢量绘图程序在办公套件中很常见，`Kontour` 是 KOffice 在此领域的进入者。

6. **Krita** 该程序是 KOffice 的位图图像编辑程序。KOffice 网页将该程序与 `GIMP` 和 Adobe Photoshop 进行了比较，但在 2002 年，`Krita` 仍然非常新，其功能远未达到 `GIMP` 或 Photoshop 的水平。

7. **Kugar** 该程序有助于自动化商业报告的制作。它是唯一的在 GNOME 办公中没有对应组件的 KOffice 组件。

8. **KChart** 该程序是另一个图形工具，但它根据数据文件生成图表、图形等。

> **注意** 尽管 KOffice 的组件比 Sun Gnome Office 少，但这一事实有点误导性，因为一些 GNOME 办公应用程序有非 KOffice 官方部分的 KDE 对应物。例如，`KMail` 和 `Konqueror` 分别是 KDE 的邮件阅读器和 web 浏览器。与 GNOME 的对应物 `Balsa` 和 `Galeon` 不同，它们不是 KOffice 的一部分。

总体而言，KOffice 组件足以在许多环境中使用。它们缺乏某些竞争程序中的一些更高级的功能。例如，`KWord` 缺乏修订跟踪和语法检查器。不过，KOffice 开发人员旨在提供习惯于 Microsoft Windows 办公套件的用戶所期望的所有功能，因此这些不足之处有望随着时间推移而缩小。

### OpenOffice.org
