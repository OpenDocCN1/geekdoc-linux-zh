
这些应用对他们很有用，或者他们安装了工作需求必需的应用程序。

## 3.2 建立功能连续性

本章包含了有助于保留现有应用程序功能的方法。迁移后，大多数用户将不得不切换到不同但功能等效的应用。为了弥补这种可能导致生产力损失的差距，为习惯于新应用程序的用户制定一项策略是有益的。

### 3.2.1 桥接应用程序

某些在 Linux 上原生运行的应用程序在 Windows 上也可以原生运行。这些应用程序提供了一个机会，可以减少由于将操作系统迁移到 Linux 引起触发的过渡影响和培训需求。因此，可以在实际迁移操作系统本身之前，先迁移到将在 Linux 平台上支持的应用程序。

> **重要：** 本节描述的方法可以为缓解用户中断和挫败感提供一种极其重要的途径，并最大限度地减少完成迁移所需的应用程序重新培训。

这种迁移前更改的优势在于，允许用户在操作系统实际迁移完成之前习惯新的应用程序。

在安装新的操作系统之后，用户在对这些应用程序进行切换时，在应用程序方面完全不会经历任何变化。

第 54 页的表 3-1 提供了几个可以作为 Microsoft Windows 和 Linux 之间“桥接”应用程序的示例。第二列列出的 Linux 等效应用是在可以在 Microsoft Windows 和大多数主流 Linux 发行版上原生运行的应用程序示例。因此，它们允许应用程序迁移在操作系统迁移之前发生。

### 表 3-1 示例桥接应用程序

| Windows 中使用的应用程序 | 桥接应用程序 |
|---|---|
| Microsoft Internet Explorer | Mozilla 或 Mozilla Firefox |
| Microsoft Outlook 或 Outlook Express | Mozilla, Thunderbird, 或 Evolution |
| Microsoft Word | OpenOffice.org^a Writer |
| Microsoft Excel® | OpenOffice.org Spreadsheet |
| Microsoft Powerpoint | OpenOffice.org Impress |
| Jasc Paint Shop Pro, Adobe Photoshop | The GIMP^b |
| 消息客户端 (MSN, Yahoo, ICQ, AIM) | GAIM^c |
| IBM Sametime 7.5^d,e | (支持原生 Windows 和 Linux) |
| IBM Lotus Notes 7.4^f | (支持原生 Windows 和 Linux) |

a. http://www.openoffice.org
b. http://www.gimp.org
c. http://gaime.sourceforge.net
d. IBM Lotus Sametime 和 IBM Lotus Notes 将从这些版本开始提供针对 Windows 和 Linux 的原生版本。
e. http://www.ibm.com/software/sw-lotus/products/product3.nsf/wdocs/st7home
f. http://www.ibm.com/software/sw-lotus/products/product4.nsf/wdocs/linux

### 3.2.2 功能等效的实用程序应用程序

文件系统浏览器、压缩程序和查看器等实用程序应用程序提供的功能使得这些工具的设计与操作系统结合得更紧密。它们不能被视为“桥接应用程序”，正如我们在上一节中列出的应用程序所描述的那样。Linux 被认为正接近 Windows 的等效性之一，是实用程序应用程序上有许多选择。在许多情况下，这些应用程序的功能集实际上比今天 Windows 中使用的等效实用程序应用程序更强大。

第 55 页的表 3-2 提供了 Linux 中可用的等效实用程序应用程序示例。

### 表 3-2 Linux 中等效实用程序应用程序示例

| 文件管理器 (Windows Explorer) | Konqueror (KDE) Nautilus (GNOME) |
|---|---|
| 压缩程序 (如 WinZip) | KArchiver, Ark (KDE) FileRoller (GNOME) |
| 查看器 (如 Adobe Reader) | Konqueror, KView (KDE) Nautilus, Evince (GNOME) Linux 版 Adobe Reader |
| 多媒体播放器 (如 Windows Media® Player) | xmms, xine, RealPlayer, totem, amaroK, JuK (KDE) Rhythmbox, Banshee (GNOME) |

### 3.2.3 Web 应用程序

遗憾的是，你可能找不到满足每个要求的桥接应用程序（理想情况）或功能等效应用程序。例如，提供 ERP 或 CRM 的应用程序特别可能具有厚客户端实现，而 Windows 和 Linux 之间没有跨平台的等效实现。企业应用程序供应商并没有通过为每个操作系统开发单独的厚客户端来实现来实现，而是将 Web 浏览器作为将其应用程序扩展到替代客户端平台（如 Linux）的容器。

如果基于浏览器的解决方案不可行，就无法通过先过渡到跨平台 Web 客户端界面来桥接应用程序到新桌面的方法。在这种情况下，你可能必须将应用程序迁移到支持多平台客户端的新版本，或者你可能需要考虑切换到另一个满足跨平台客户端要求的软件供应商。

### 3.2.4 构建到服务器的桥梁

在最后三个节中，我们展示了通过切换到移植应用程序或 Web 客户端来让用户更容易更改的方法。弥补功能差距的另一种可能性是将应用程序从客户端移回服务器作为主要的处理主机。

基于服务器的计算（例如，基于终端服务的客户端应用程序远程托管）可以产生许多优势。关于此类一些方法的介绍将在 154 页的 7.2 “远程工具”中进行更详细的讨论。无论安装哪种操作系统或使用何种客户端，你都应该能够确保在终端应用程序中交付相同的应用程序界面。
