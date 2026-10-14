
当然，所有这些选择的问题在于你的菜单栏可能会变得非常杂乱，这就是为什么 Ubuntu 随附每个任务一个应用程序——你得到一个网页浏览器、一个文本编辑器、一个电子表格，等等。如果你尝试了这些应用并发现它们不适合你，就该跳出 Ubuntu 沙盒，看看免费软件世界的其他部分能为你提供什么：是时候安装一些新软件了！在开始之前最后说一句：在 Linux 上，软件被打包成我们所说的“包”——即软件本身，加上任何配置文件、文档等。这些包传统上由包管理器管理，其优点是所有程序都来自一个中心位置，这意味着它们可以轻松安装，也能轻松更新，可以以与安装相同的方式移除，并且有保证能正常工作。

使用包管理器意味着你可以用一个简单的程序安装 Ubuntu 所提供几乎所有内容。

## 菜单上有什么？

转到 Applications > Add/Remove 以打开 Add/Remove Applications 对话框。它分为四个主要部分：顶部可以搜索应用程序；左侧是用于过滤的类别列表；顶部中间是与过滤条件匹配的应用程序列表，而底部中间是对当前所选包的描述。

你会注意到每个应用程序左侧都有一个复选框，右侧有一个星级评分：如果它当前已安装，复选框会被勾选，星级评分显示有多少人安装了该特定程序。你会发现 Ubuntu 默认安装的所有包（例如 Gimp 图像编辑器）的人气都为五星，但也有不少其他软件也有五星——这些是值得研究的！

从窗口的顶部栏开始，首先确保“Show”选项设置为“Supported applications”。可以设置的选项共有五种：

- 1 All available applications Shows everything.
- 2 All open source applications Shows everything that is free software (as opposed to proprietary software).
- 3 Supported applications Programs that the team behind Ubuntu provide official support for.
- 4 Third party applications Programs from anyone outside of the free software community.
- 5 Installed applications The programs you have installed currently; generally used when you want to uninstall something.

正如你所见，‘Supported Applications’类别对新用户来说是最好的，因为该类别中的所有应用程序都由 Ubuntu 团队提供官方支持——这意味着当它们可用时，他们会为你发布补丁和升级。如果你想稍微拓宽视野，可以尝试将此选项更改为‘All Open Source applications’。请注意，此选项包含大量未得到 Ubuntu 官方支持的应用程序，但这只意味着你不能保证会发布更新——你几乎肯定会获得补丁和更新，因为这是免费软件的特性，但你不能保证。

![](img/afd38ba98c33e56aa8435c9f1db6bed0_99_0.png)

类别

都是由 Ubuntu 团队官方支持的——这意味着他们会在可用时为你发布补丁和升级。如果你想稍微拓宽视野，可以尝试将此选项更改为‘All Open Source applications’。请注意，此选项包含大量未得到 Ubuntu 官方支持的应用程序，但这只意味着你不能保证会发布更新——你几乎肯定会获得补丁和更新，因为这是免费软件的特性，但你不能保证。

现在，让我们开始安装软件的实际操作。假设你决定 OpenOffice.org 对你的需求来说太慢了，想要一个快一点的。你通常会使用搜索框查找诸如“文字处理器”等术语，但在这里我只是给你一个提示：列表中的第一项 AbiWord 是一个速度极快且功能丰富的文字处理器，与 Gnumeric 电子表格一起，是 OpenOffice.org 的绝佳替代品。因此，选择 AbiWord 左侧的复选框，然后点击窗口底部的 Apply Changes 按钮。

你现在会被提示确认要进行的更改列表——这是因为你可以一次添加和删除大量程序，而且有时安装一个程序需要移除另一个程序，因为它们会冲突。阅读将要进行的更改列表（在本例中，AbiWord 将被添加），然后点击 Apply。AbiWord 包将在几分钟内下载并安装，完成后你会看到已安装的新程序列表。由于 AbiWord 是一个办公程序，它将出现在 Applications > Office

![](img/afd38ba98c33e56aa8435c9f1db6bed0_100_0.png)

![](img/afd38ba98c33e56aa8435c9f1db6bed0_100_1.png)

1 选择你想要的内容并点击 Apply Changes 后，Ubuntu 会要求你在进行更改前确认更改。

![](img/afd38ba98c33e56aa8435c9f1db6bed0_100_2.png)

2 Ubuntu 从互联网下载软件，因此下载和安装你选择的包需要几秒钟。

![](img/afd38ba98c33e56aa8435c9f1db6bed0_100_3.png)

3 Ubuntu 会显示所有已安装程序的列表。双击其中任何一个即可运行它们。

![](img/afd38ba98c33e56aa8435c9f1db6bed0_100_4.png)

如果你正在寻找 OpenOffice.org Writer 的替代文字处理器，AbiWord 是一个极佳的选择。

## 提交统计信息

Add/Remove Applications 对话框的人气信息来自一个名为 Popcon 的程序，Popcon 是‘popularity contest’的缩写。该程序扫描你的系统以查看你安装了哪些包，然后将其上传到中央 Ubuntu 服务器，以便他们弄清楚人们使用哪些包以及不使用哪些包，并据此指导他们决定人们真正希望看到支持的软件是什么。默认情况下，Popcon 已安装但未启用，这意味着你选择的包不会对所有 Ubuntu 包的整体人气产生任何影响，但如果你想参与，只需进入 Software Sources 窗口，选择最后一个标签页（Statistics），并勾选标记为‘Submit Statistical Information’的框即可。

## 获取更多软件

菜单中，但你只需双击“已安装新应用程序”框中的 AbiWord 即可立即启动它。如果你想卸载某个程序，只需反向操作：取消勾选，然后点击“应用”。

使用“添加/删除应用程序”系统是开始管理计算机软件的好方法，但更有经验的用户更喜欢一个名为 Synaptic 的程序。它没那么美观，没那么简洁，但功能更丰富——功能丰富对高级用户来说是好事，因为这意味着我们可以精确获得所需，而不必费力寻找晦涩的选项。你可以在“系统 > 管理 > Synaptic 软件包管理器”菜单项下找到 Synaptic。乍一看，你会注意到它与“添加/删除应用程序”窗口并非完全不同——确实图标少一些，但它保留了应用程序的分类筛选器，以及描述窗格，点击程序时会显示更多信息。

### 高级软件包选择

既然你已踏入高级用户领域，现在是时候了解一下你可用的海量软件了。前往“设置 > 软件源”，那里保存着所有软件来源的列表。Ubuntu 将软件包选择划分为多个软件源，以便人们可以选择他们想要的软件类型——就像“添加/删除应用程序”窗口一样，这些选择包括你是否想要 Ubuntu 支持的软件包、第三方软件包等。

目前，我们将启用全部选项，因此请确保出现的“软件源”窗口中前四个复选框已勾选。即“Canonical 支持”、“社区维护”、“专有驱动程序”和“受版权限制的软件”。选中这些后，点击“关闭”，Synaptic 会警告你软件源选择已更改，这意味着你需要点击“刷新”按钮来下载该软件源中所有可用的软件。

软件选择信息下载完成后，你会看到左侧有许多分类。如果你愿意，可以使用它们，但我们通常发现，使用

> Synaptic 能让你对软件包安装有更多控制，但学习起来需要稍长时间。

![](img/afd38ba98c33e56aa8435c9f1db6bed0_101_0.png)

Ubuntu 的更新管理器会自动选择所有可用更新，因此你只需点击标有“安装更新”的按钮即可保持最新状态。

Synaptic 搜索对您来说是更快、更简单的选项——按 Ctrl+F，确保“搜索范围”改为“描述和名称”，然后输入你想安装的内容，例如“3D 游戏”。启用所有软件源后，搜索可能需要几秒钟，但完成后，你可以滚动浏览结果列表，找到要安装的软件。

### 依赖关系
