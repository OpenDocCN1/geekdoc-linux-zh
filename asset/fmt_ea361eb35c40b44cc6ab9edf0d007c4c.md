
After the purchase of StarOffice, Sun Microsystems released a large part of the StarOffice code under the GNU Public License, and development began on what has become OpenOffice.org, which is freely available under the GPL. Sun continued development on StarOffice and released a commercial version as StarOffice 6.0. The significant differences between the free and commercial versions of the software are that StarOffice provides more fonts and even more import/export file filters than OpenOffice.org (these filters cannot be provided in the GPL version because of licensing restrictions) and StarOffice provides its own relational database, Software AG’s Adabas D database. The StarOffice counterpart to OpenOffice.org 2.4 is StarOffice 8.

## Configuring OpenOffice.org

The installation of OpenOffice.org is done on a systemwide basis, meaning that all users have access to it. However, individual users have to go into OpenOffice.org to configure it for their individual needs. This initial configuration happens transparently the first time you load any of the OpenOffice.org components, and might mean the application takes a little longer to load as a result. Be patient, and your desired application will appear.

TIP

OpenOffice.org is constantly improving its productivity applications. You can check the OpenOffice.org website (`http://www.openoffice.org/`) for the latest version. The website provides a link to download the source or a pre-compiled version of the most current working installation files. A more current version might offer file format support that you need. Should you need a Windows-compatible version, you will also find it at the website.

Shown in Figure 6.1 is the Office menu, which is found under Applications. You can see the entries for Database (Base), Presentation (Impress), Spreadsheet (Calc), and Word Processor (Writer).

![](img/8f9e74e2b343ff525bebfb720a3d8441_165_0.png)

FIGURE 6.1 The OpenOffice.org suite provided by Ubuntu is simple to configure and use.

与许多 Linux 应用程序一样，OpenOffice.org 提供的配置选项数量之多可能会让你感到有些不知所措。值得庆幸的是，这些选项经过了大量思考后进行了组织，你可以通过点击 Tools 菜单并选择 Options 来访问它们。无论你使用哪个程序打开此对话框，结果都一样；无论是从 Writer、Impress 还是 Calc 调出，它都显示相同。它充当所有 OpenOffice.org 应用程序的中央配置管理工具。你可以用它为所有 OpenOffice.org 应用程序设置全局选项，或为每个单独组件设置特定选项。例如，在图 6.2 中，你可以更改用户详细信息和信息，并且这会在所有 OpenOffice.org 应用程序中得到体现。

![](img/8f9e74e2b343ff525bebfb720a3d8441_166_0.png)

图 6.2 你可以从此对话框为所有 OpenOffice.org 应用程序设置用户详细信息。

### TIP

两个网站提供了有关 OpenOffice.org 功能的额外信息：

`http://lingucomponent.openoffice.org/download_dictionary.html`—该网站提供安装拼写和连字符词典的说明和文件，这些词典未随 OpenOffice.org 提供。

`http://sourceforge.net/projects/ooextras/`—该网站提供模板、宏和剪贴画，这些内容未随 OpenOffice.org 提供。

OpenOffice.org 仍在不断完善中，但当前版本与 Sun 版本的 StarOffice 8 不相上下。你可以浏览 OpenOffice.org 网站获取文档和常见问题的答案并提供反馈。

## 使用 OpenOffice.org Writer

在构成 OpenOffice.org 的所有应用程序中，你最有可能定期使用的就是 Writer，即 OpenOffice.org 文字处理器。Writer 的视觉风格与 Microsoft Word 非常相似，在其商业的且价格高昂得多的竞争对手之上具有许多优势。在本节中，你将学习如何开始使用 Writer 并利用其强大的格式和版式工具。

> NOTE
>
> 你可能有兴趣知道，Writer 是撰写和编辑本书时选用的主要文字处理器。

### 开始使用 Writer

你可以通过进入 Applications、Office 菜单并选择 OpenOffice.org Word Processor 来访问 Writer。几秒钟后 Writer 打开，出现一个空白文档和一个闪烁的光标等待你的指令。很容易就想直接跳进去开始输入文档，但开始工作前进行一些初始配置是值得的。

首先，确保选项已设置为你的需求。点击 Tools 菜单并选择 Options 以调出 Options 对话框，如图 6.2 所示。初始屏幕允许你使用姓名、地址和联系方式个性化 OpenOffice.org，但还有可配置的功能选项，你可能也想更改。首先，通过点击 Paths 选项检查你的默认路径是否正确。你可能希望将 My Documents 路径，如图 6.3 所示，改为比仅仅 Documents 目录更具体的路径。

![](img/8f9e74e2b343ff525bebfb720a3d8441_167_0.png)

图 6.3 点击 Edit 按钮选择你的默认文档目录。

你可能还想更改 OpenOffice.org，使其默认以 Microsoft Word 格式保存，如果你需要的话。这可以在图 6.4 所示的 Load/Save General 选项下完成，如果你重视你的工作，改变 Autorecovery 设置使其每隔几分钟保存一次是个好主意。

![](img/8f9e74e2b343ff525bebfb720a3d8441_168_0.png)

图 6.4 确保你正在使用最适合你的文件格式。

从上到下，它们是

- `General`—指定影响 Writer 一般使用的选项。
- `View`—指定你希望 Writer 显示的内容。
- `Formatting Aids`—指定是否希望看到非打印字符。
- `Grid`—创建可用于将框架和图像就位吸附的网格。
- `Basic Fonts`—在此选择文档的默认字体。
- `Print`—指定打印文档时 Writer 的确切输出内容。
- `Table`—设置在 Writer 中绘制表格的选项。
