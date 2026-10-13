
尽管 KSpread 包含相当数量的基础财务函数，可用于计算名义利率之类的内容，但其对回归测试等统计函数的支持非常有限。希望 KOffice 的人员未来能解决这个问题，但目前 KSpread 基本上仅限于基础的数值计算。如果需要更全面的功能集，您可能希望从 Sun 获取 StarOffice，它包含可与 Microsoft Office 文件互操作的电子表格应用程序。然而，该程序是商业软件，直到其开源版本（OpenOffice）完全移植到 FreeBSD，您可能无法免费获得它。个人认为它物有所值。

## KPresenter

KPresenter 是一个类似 PowerPoint 的程序，可用于创建幻灯片演示。图 20.5 显示了 KPresenter 编辑幻灯片的情况。

图 20.5
*KPresenter 幻灯片程序。*

![](img/ba0161b65b37e94cffc801ecbacaba5e_345_0.png)

![](img/ba0161b65b37e94cffc801ecbacaba5e_345_1.png)

> 在撰写本文时，KPresenter 极不稳定，通常无法正确显示幻灯片演示。因此，我建议目前不要将 KPresenter 用于任何实际演示。OpenOffice 在可用时将提供功能齐全的演示应用程序，可作为 KPresenter 的替代方案。

## KIllustrator

KIllustrator 是一个用于创建插图的基本绘图程序。图 20.6 显示了 KIllustrator 程序。

图 20.6
编辑图形的 KIllustrator 程序。

![](img/ba0161b65b37e94cffc801ecbacaba5e_346_0.png)

再次，熟悉绘图程序的读者应该能够比较轻松地适应 KIllustrator。

## StarOffice

StarOffice 来自 Sun Microsystems，是一款功能齐全的桌面生产力套件，其与 Microsoft Office 的集成程度优于任何 KOffice 应用程序。然而，正如前面讨论的那样，StarOffice 是商业软件，您必须通过光盘订购、现成购买或从 Sun 的网站（www.sun.com/staroffice）下载。下载文件非常大，您可能会认为支付全额费用（约 40 美元）通过邮件获取光盘物有所值。

StarOffice 不仅包含功能齐全的文字处理和电子表格应用程序，拥有几乎所有 Microsoft Office 的核心功能（以及双向文件兼容性），还包括桌面浏览器、电子邮件客户端、Web 浏览器和其他工具。它拥有文档模板、剪贴画以及家庭或商业环境中可能需要的多数工具。

StarOffice 在技术上并非适用于 FreeBSD；它实际上是 Linux 原生的软件套件，通过其 Linux 兼容层在 FreeBSD 下运行。下载 StarOffice 文件（so-6.0-ga-bin-linux-en.bin）后，将其移至 /usr/ports/distfiles，然后使用 cd 进入 /usr/ports/editors/staroffice60。完成此操作后，您可以输入 make 和 make install，将 StarOffice 连同必要的 FreeBSD 补丁一起安装到系统。端口中的安装程序会询问您一些问题，例如是否要进行“网络安装”或“本地安装”；您可能希望进行网络安装，以便将 StarOffice 二进制文件放置在所有用户都可以访问的位置。

完成此过程后，运行 StarOffice 只需在命令行输入 soffice。您将被启动到 StarOffice 桌面，如图 20.7 所示。

**图 20.7**
*StarOffice 桌面。各种图标代表可运行的任务，例如创建各种类型的文档。*

![](img/ba0161b65b37e94cffc801ecbacaba5e_347_0.png)

关于如何充分利用 StarOffice 的完整教程，可在 Sams Teach Yourself StarOffice 5 for Linux in 24 Hours 或最近出版的众多 StarOffice 书籍中找到。这些文本将涵盖如何使用 StarOffice 完成您习惯使用 Microsoft Office 的每项任务，以及更多内容。

## Image Editing

FreeBSD 有一个非常强大的图像编辑程序可用，名为 The GIMP——即 Gnu Image Manipulation Program（GNU 图像处理程序）的缩写。GIMP 的功能足以应对除最复杂的图像编辑任务之外的所有任务，其功能可与 Adobe Photoshop 相媲美。此外，与本小时讨论的所有其他应用程序一样，GIMP 也是免费提供的。

## Installing and Starting GIMP

GIMP 可在 FreeBSD ports 树的 Graphics 目录中找到。有关从 FreeBSD ports 集合安装软件的详细信息，请参阅第 6 小时“添加和删除第三方软件”。

安装 GIMP 后，您可以从 KDE 中启动它，方法是单击 K 按钮、运行命令，并在打开的框中输入 gimp。首次运行 GIMP 时，它会询问一些设置问题。一般来说，您可以接受它提供的默认答案。设置完成后，GIMP 控制面板将显示（见图 20.8），以及其他对话框和窗口，您现在可以关闭它们。

图 20.8
GIMP 中的
主控制面板。

![](img/ba0161b65b37e94cffc801ecbacaba5e_348_0.png)

要在 GIMP 中打开图像进行编辑，请单击文件、打开。这将弹出如图 20.9 所示的对话框。

打开文件对话框的左侧是目录列表，右侧是所选目录中的文件列表。另请注意，内置了一个原始文件管理器。您可以删除和重命名文件，以及创建新目录。

将图像加载到 GIMP 后，它将出现在如图 20.10 所示的新窗口中。

如前所述，GIMP 的用户界面不符合您可能使用的大多数软件的规范。使用 GIMP 时最重要的是要记住，大多数图像处理功能都不会在可见的窗口菜单中找到，而是通过右键单击图像窗口，然后从弹出菜单中选择其中一个选项来访问。如果牢记这一点，您应该能够相对快速地适应 GIMP。

## 图 20.9

在 GIMP 中打开图像进行编辑。

![](img/ba0161b65b37e94cffc801ecbacaba5e_349_0.png)

## 图 20.10

GIMP 中已将图像加载到窗口中进行编辑。

![](img/ba0161b65b37e94cffc801ecbacaba5e_349_1.png)

例如，要在 GIMP 中保存文件，您需要右键单击要保存的图像（在其显示窗口中），然后从弹出菜单中选择文件、保存。

图像编辑功能的工作方式类似。右键单击图像，然后选择编辑以获取可用编辑命令列表。从右键菜单中选择图像可提供诸如更改图像模式、亮度、对比度以及适用于整个图像的其他功能等选项。使用对话框子菜单访问构成 GIMP 用户界面的各种浮动窗口，包括工具箱（包含二十五种可选图像编辑工具）和 GIMP 控制中心窗口，您可使用它打开新图像并控制 GIMP 的设置。

## Internet Applications

KDE 桌面附带了一些功能相当齐全的 Internet 应用程序。大多数人感兴趣的主要是 Konqueror 内置 Web 浏览器和 KMail 内置电子邮件程序。

## Konqueror Web Browser

Konqueror 是 KDE 的内置 Web 浏览器。它的行为与 Microsoft Internet Explorer 或 Netscape Navigator 非常相似。图 20.11 显示了 Konqueror Web 浏览器。

图 20.11
Konqueror Web 浏览器。

![](img/ba0161b65b37e94cffc801ecbacaba5e_350_0.png)

菜单栏中唯一非标准的菜单项是位置。然而，它实际上与您在 Internet Explorer 和 Netscape 中习惯的文件菜单功能相同。从位置菜单中，您可以打开新的网站、将网页保存到文件等等。
