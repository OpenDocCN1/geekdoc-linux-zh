
# 第二部分：面向桌面用户的 Ubuntu

## 第 9 章：从 Windows 系统迁移

如果前两个项目中的任一项目缺失，请将你的 Windows 或 Mac OS 配置文件的内容复制到你的 `~/.mozilla/firefox` 目录。确保你复制的是 Windows 或 Mac OS 配置文件的内容，而不是目录本身。你的 `~/.mozilla/firefox` 目录必须包含一个 `profiles.ini` 文件，该文件标识了配置文件数据所在的目录。

#### 图 9-11：Internet Explorer 导入和导出向导

![图 9-11：Internet Explorer 导入和导出向导](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_386_0.png)

#### 图 9-12：选择从 Internet Explorer 导出的内容

![图 9-12：选择从 Internet Explorer 导出的内容](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_386_1.png)

图 9-12 显示的对话框允许你选择想要从 Internet Explorer 导出的信息类型：收藏、Cookies 或 RSS Feed（后者仅在从 IE7 导出时显示）。要将收藏导出为 HTML 文件，请选择“导出收藏夹”并点击“下一步”继续。将显示图 9-13 所示的对话框。

#### 图 9-13：选择从 Internet Explorer 导出的收藏夹项目

![图 9-13：选择从 Internet Explorer 导出的收藏夹项目](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_387_0.png)

图 9-13 显示的对话框允许你选择想要导出为 HTML 的收藏夹文件夹。要导出所有的收藏夹，请如图 9-13 所示选择顶层收藏夹文件夹。点击“下一步”继续。将显示图 9-14 所示的对话框。

#### 图 9-14：选择 Internet Explorer 导出项目的保存位置

![图 9-14：选择 Internet Explorer 导出项目的保存位置](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_387_1.png)

图 9-14 显示的对话框允许你指定包含收藏夹（讽刺地称为 `bookmark.htm`）的文件的保存位置，或者选择性地将其直接导出到另一个应用程序。我们的目标是将它们保存到文件（这是默认操作），请保持“导出到文件或地址”单选按钮被选中，如果你想使用除默认以外的名称，可以修改文件名。点击“下一步”继续。

将显示一个最后的对话框，需要你点击“完成”以开始导出过程。导出过程完成后，将显示一个确认对话框。点击“确定”关闭确认对话框，这将关闭“导入和导出”对话框。

将包含收藏夹的文件复制到运行你想导入书签浏览器的系统中。如果该系统不存在或当前无法访问，请确保你刚刚创建的文件位于一个可以在你创建 Windows 系统备份时对其进行备份的位置。

### 导出 Safari 书签

奇怪的是，Apple 为 Mac OS X 系统提供的 Safari 浏览器并没有自动提供将其书签保存为 HTML 的功能。好消息是，Simone Mangani 写了一款名为 Safari Bookmark Exporter (http://homepage.mac.com/simx/sbe.html) 的优秀（免费）应用程序，它可以实现这一点。下载该应用程序的磁盘镜像后，你可以安装或直接从镜像运行它。将显示类似于图 9-15 所示（在 Mac OS X 系统上截图）的对话框。

#### 图 9-15：初始的“Safari Bookmark Exporter”对话框

![图 9-15：初始的“Safari Bookmark Exporter”对话框](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_388_0.png)

如果 Safari 正在你的 OS X 系统上运行，请点击“不要对活动浏览器进行警告”按钮。接下来，在“分析书签（Analyze Bookmarks）”按钮下方，通过浏览器/文件格式名称选择一个输出目标——你的选择主要决定了 Safari Bookmark Exporter 将保存包含书签的文件的位置。我通常会选择 Firefox/Firebird/Phoenix，仅因为此选项对 Firefox 有用，尽管 Simple HTML 也是一个合理的选择。点击“导出书签”显示一个对话框，允许你识别想要保存书签的位置。如果你选择 Firefox/Firebird/Phoenix 作为你的浏览器，建议的保存位置是将输出文件保存到你的 Firefox 配置文件目录，你可能不想这样做，因为这会覆盖任何同名的文件。我通常将这些文件保存到我的家目录，并命名为 `safari-bookmarks-export.html`，这可以清晰地看出文件包含的内容。

### 保存 Safari 书签的快速技巧

如果你不想为了一次性操作而下载并安装 Safari Bookmark Exporter 应用程序，可以使用 Safari 内部的一些黑技巧（hack）将你的 Safari 书签保存为 HTML 文件。因为这确实是一种黑技巧，它可能在所有新版本的 Safari 中不起作用，但值得一试：

1. 退出 Safari 并启动终端（Terminal）应用程序。
2. 在终端窗口执行以下命令：`defaults write com.apple.Safari IncludeDebugMenu 1`
3. 启动 Safari。
4. 选择新“调试（Debug）”菜单中的“导出书签”命令，并识别想要保存 `Safari Bookmarks.html` 文件的位置。

然后你可以按照本文稍后描述的方法，将此文件导入到 Firefox 浏览器中。

### 将书签导入 Firefox

要在 Firefox 中导入包含书签的 HTML 文件，首先选择书签菜单中的“从 HTML 导入（Import from HTML...）”命令。选择包含书签的文件并点击“打开”。书签现在将添加到你的书签栏中。

#### 图 9-16：从 HTML 导入书签

![图 9-16：从 HTML 导入书签](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_389_0.png)

#### 图 9-17：从 Firefox 导入书签

![图 9-17：从 Firefox 导入书签](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_390_0.png)

- DOC, XLS, PPT：你可以使用 OpenOffice 工具打开由 Microsoft Office 应用程序创建的文件。微软新的基于 XML 的 DOCX、XLSX 及相关格式仅由 OpenOffice 3.0（及更高版本）工具支持。
- PDF 文件：Ubuntu 提供了 Evince 来显示 PDF 文件。该应用程序无法让你编辑 PDF 文件、填充 PDF 等。大多数 Ubuntu 应用程序都允许你通过选择“打印到文件”选项并指定 PDF 输出来创建 PDF 文件。在 Ubuntu 仓库中可以找到 `pdedit`，它可以编辑 PDF 文件。
- Linux 替代方案项目：www.linuxalt.com
- Linux 应用查找：www.linuxappfinder.com/alternatives
- Windows 软件的 Linux Equivalent：www.linuxlinks.com/article/200707011340544/Equivalents.html
- Windows 软件的 Linux Equivalent：http://wiki.linuxquestions.org/wiki/Linux_software_equivalent_to_Windows_software
- Linux 中 Windows 软件的等效/替换/类似物表：www.linuxrsp.ru/win-linux-soft-table-eng.html

如上所示，这个列表可以无限延续下去。要查看与 Windows 应用等效的 Linux 应用优秀总结，请访问以下站点：

除了这些 Linux 专用站点外，开源替代方案（www.osalt.com）列出了运行在其他开源操作系统（包括 Linux 等）上的 Windows 软件的等效应用程序。

关于使用、虚拟化以及能够让你在 Ubuntu 系统上运行实际 Windows 软件的类似技术的信息，请参阅第 24 章“使用虚拟机和模拟器”。是的，这是可以做到的！

### 总结

Linux 丰富的软件资源让 Ubuntu 成为你的日常主力操作系统（即你完成所有工作的系统）——变得完全可行。但你在现有的 Windows 或 Mac OS 上积累的所有邮件、浏览器收藏夹/书签和数据文件该怎么办？本章解释了从 Microsoft Windows 或 Mac OS 系统迁移电子邮件和浏览器设置到 Ubuntu 系统的不同方法，讨论了备份 Windows 或 Mac OS 系统以方便迁移的好方法，识别了在进行最终备份之前应该执行的一些任务，并讨论了 Internet Explorer、Outlook 和 Outlook Express 等应用程序存储数据的关键方向。它还讨论了完全迁移到 Ubuntu 系统的其他考虑因素，例如确保你能找到可以处理现有数据文件的应用程序。
