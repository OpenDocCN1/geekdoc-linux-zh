

尽管也可以使用其他图形应用程序来完成此操作，但 GIMP 支持极其广泛的文件格式，甚至允许你将图像文件保存为压缩的 tarball，这使其成为真正的格式转换之王。

要执行文件转换，只需在 GIMP 中打开的图像上右键单击，然后在弹出菜单中选择 File ▸ Save As。你也可以从 File 菜单中进行同样的选择。无论哪种方式，Save Image 窗口随后会出现。在该窗口中，你可以通过在该窗口顶部 Name 框中用你想要转换到的格式的扩展名替换原始文件扩展名来指定新的文件格式。如果你不确定有哪些格式可用，请单击 Select File Type (By Extension) 左侧的小箭头，然后从下方出现的窗格中的选项中进行选择。要保存进行中的作品，请使用 GIMP 原生的 XCF 格式，以便以后可以继续处理该图像。

## Learning More

通过随意玩弄 GIMP 来学习使用它非常有趣。为了让你入门，大多数有趣的功能都位于任何图像窗口的 Filters 菜单中。当然，在修改文件之前，你应该先备份任何计划进行实验的文件。

如果你更喜欢通过手册和教程学习，而不是仅仅通过瞎搞来学习，你可以通过在 Ubuntu Software Center 中搜索 gimp-help-en，然后安装 Documentation for the GIMP (English) 来下载并安装 GIMP 用户手册。安装后，你可以从 GIMP 内的 Help 菜单访问手册。你也可以在线查看手册，网址为 http://docs.gimp.org/en/，并且可以在 http://www.gimp.org/tutorials/ 找到一系列教程。

## Phatch Photo Batch Processor

虽然 GIMP 和 F-Spot 在处理绝大多数照片整理和编辑任务方面都相当强大，但它们缺乏一种易于使用的批量文件转换方法，无法让你同时对一组文件应用各种转换。例如，假设你想将 100 张照片转换为看起来像带白边黑白快照的照片，比原图小 50%，具有相似的主题文件名，并且以 .tiff 而非 .jpg 格式保存。逐一应用所有这些更改将是极其痛苦的——幸运的是，Phatch 来救援了！（参见 Figure 13-9。）

你可以通过在 Ubuntu Software Center 中搜索 phatch 来下载并安装 Phatch。安装后，你可以通过选择 Applications ▸ Graphics ▸ Phatch PHoto bATCH Processor 来运行它。

![](img/f7cef0df22f9dba5a41777808c98eece_290_0.png)

Figure 13-9: Batch photo file conversions with Phatch

## Using Phatch

使用 Phatch 很简单，而且实际上非常有趣。然而，其界面对于初次使用者可能并不明显。考虑到这一点，以下是使用 Phatch 的简要说明：

- 1. 单击主 Phatch 窗口中的 + 按钮，Phatch actions 窗口将会出现。
- 2. 在该窗口中，选择你想要应用于照片的操作（转换），然后单击 Add。对你想要应用的任何其他操作重复此过程。
- 3. 添加完所有想要的操作后，单击主 Action List 中的每个操作，并为每个操作输入适当的参数（大小、文件格式、边框大小、输出位置等）。
- 4. 如果操作未按你想要的顺序排列，请单击你想要移动的操作，然后使用上下箭头按钮更改其位置。
- 5. 一切准备就绪后，使用有意义的名称保存你的 Action List，以便在需要时再次使用，然后选择 Tools ▸ Execute。

- 6. 在出现的窗口中，单击 **Browse Folder** 按钮找到你想要转换的照片，然后单击 **Batch** 按钮。

- 7. 随后会打开另一个窗口，显示将要处理哪些文件。在该窗口中单击 **Continue**。

Phatch 将会按照 Action List 中列出的顺序执行转换。它会显示其工作进度，然后会出现一个小窗口告知已完成。你可以在选择的<|message|>
