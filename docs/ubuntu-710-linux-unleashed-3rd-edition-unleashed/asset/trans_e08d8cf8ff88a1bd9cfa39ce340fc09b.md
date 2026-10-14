

## 注意事项

马萨诸塞州决定将 PDF 和 OpenDocument 作为标准格式，这对开源世界产生了巨大的影响。这是 OpenDocument 这一已达成一致的开放标准首次以这种方式被指定。这意味着任何希望与州政府开展业务的人都必须使用基于 OpenDocument 的文件格式，而不能使用微软使用的专有格式。对微软来说不幸的是，其任何应用程序都不支持 OpenDocument，这使得它们对希望与州政府合作的人来说毫无用处。尽管微软是开发并批准了 OpenDocument 标准的 OASIS 的创始成员之一！

## 与 Gnome Office 协作

GNOME 可用的另一套办公软件是 Gnome Office，它是一组独立的应用程序。与 OpenOffice.org 不同，Gnome Office 没有一套连贯的应用程序，这意味着你必须习惯使用一个与电子表格没有任何集成、也不能直接与演示文稿包协作的文字处理器。然而，如果你只需要一两个组件，值得研究一下 Gnome Office。

## GTK 控件集

开源开发者总是试图让人们更容易构建应用程序并协助开发。为此，有许多小部件或工具包可供其他开发者使用，以便快速创建和部署 GUI 应用程序。这些小部件控制诸如下拉列表、另存为对话框、窗口按钮以及整体外观和感觉等内容。不幸的是，而 Windows 和 Apple 开发者只需担心各自的一套小部件，Linux 却有大量不同的小部件，包括 GTK+、QT 和 Motif。更糟糕的是，这些小部件彼此不兼容，使得将已完成的应用程序从一个小部件集轻松迁移到另一个小部件集变得困难。

GTK 是 GIMP Tool Kit 的缩写。GIMP（The GNU Image Manipulation Program）是一款图形应用程序，非常类似于 Adobe Photoshop。通过使用基于 GTK 的术语，我们可以节省数百字的输入，并帮助推进我们对 GNOME Office 的讨论。你也可能会在这些章节中看到对 QT 和 Motif 以及其他小部件集的类似引用。

以下是 Ubuntu 中可用的 Gnome Office 套件的主要组件：

- AbiWord—此文字处理程序使你能够撰写、格式化和组织文本文档，并与 Microsoft Word 文件格式具有一定的兼容性。它使用插件（添加诸如语言翻译等功能的程序）来增强其功能。
- Gnumeric—此电子表格程序使你能够以电子表格格式操作数字。对除最冷僻的 Microsoft Excel 函数之外的所有函数的支持意味着用户在与 Excel 用户交换电子表格时应不会遇到太大困难。
- The GIMP—此图形应用程序允许你创建通用用途的图像。它可以导入和导出所有常见的图形文件格式。GIMP 类似于 Adobe 的 Photoshop 应用程序，并在第 7 章“多媒体应用程序”中进行了描述。
- Evolution—Evolution 是一款邮件客户端，其界面类似于 Microsoft Outlook，提供电子邮件、调度和日历功能。它在第 5 章“在互联网上”中进行了描述。

被称为 Gnome Office 的松散关联的应用程序集合包括几个与 Ubuntu 已提供的应用程序功能重复的额外应用程序。这些额外的 GNOME 应用程序未包含在 Ubuntu 的默认安装中，以消除冗余。它们都可在 Gnome Office 网站上获取，网址为 http://www.gnome.org/gnome-office/。The GIMP 和 Evolution 在 Ubuntu 中默认可用。你必须使用 yum 或 pirut 来获取剩余组件。

Ubuntu 将 AbiWord 编辑器作为其 Extras 的一部分提供，如图 6.14 所示。AbiWord 可以导入 XML、Microsoft Word、RTF、UTF8、纯文本、WordPerfect、KWord 以及其他几种格式。AbiWord 以其使用插件或集成辅助应用程序而著称，这些插件扩展了其功能。这些插件增加了语言翻译、HTML 编辑、同义词库、Linux 命令 shell 以及在线词典等其他功能和特性。如果你只需要一个简单而强大的文字处理应用程序，你应该查看 AbiWord。

AbiWord 未在 Ubuntu 中默认安装，因此你需要使用 apt-get 或 synaptic 安装它。该软件包简单地称为 abiword-gnome，尽管你可能希望安装元软件包 gnome-office，它将包含其他 Gnome Office 应用程序。

安装 Abiword 后，它将出现在应用程序菜单中，位于 Office 子菜单下。只需单击图标即可启动应用程序。

如果你熟悉 Microsoft Works，AbiWord 界面会让你感到熟悉，因为其设计者基于 Works 设计了该界面。

你可以使用 Gnumeric 电子表格应用程序执行财务计算并绘制数据，如图 6.15 所示。它可以导入逗号或制表符分隔的文件、文本或 Gnumeric XML 格式的文件，仅以 XML 或文本格式保存文件。你需要使用 apt-get 或 synaptic 以与 Abiword 相同的方式安装 Gnumeric。如果你已经安装了 gnome-office 软件包，Gnumeric 将在应用程序、Office 下作为 Gnumeric Spreadsheet 可用。

