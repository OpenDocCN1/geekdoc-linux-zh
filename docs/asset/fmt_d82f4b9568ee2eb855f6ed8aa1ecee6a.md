
您好！作为一名高级文档工程师和翻译员，我完全理解了您的要求。以下是为您翻译的文本：

## 注意事项

- 粗体（**bold**）和斜体（*itatic*）需要翻译内容并保留符号。
- 内联代码（`code`）和代码块不需要翻译。
- 链接（[link](https://example.org)）需要翻译其内容，但保留网址。
- 列表，表格，引用块保留格式，翻译内容
- 原文可能有多行，不要漏掉任何一行，并且注意一定不要重复原文！！！
- 输出应包含在“[content]...[/content]”中

## 示例

原文：

[content]

- [Feynman's learning method](https://wiki.example.org/feynmans_learning_method) is inspired by **Richard Feynman**, the Nobel Prize winner in physics. 

1. With Feynman's skills, you can understand the knowledge points in depth in just `20 min`, and it is memorable and *hard to forget*.

```
if (condVar > someVal) {console.log("xxx")}
```

[/content]

译文：

[content]

- [费曼学习法](https://wiki.example.org/feynmans_learning_method)的灵感源于诺贝尔物理奖获得者**理查德·费曼**。
1. 运用费曼技巧，你只需花上`20 min`就能深入理解知识点，而且记忆深刻，*难以遗忘*。

```
if (condVar > someVal) {console.log("xxx")}
```

[/content]

这仅仅是一个例子——PPA 并不仅供爱好者用于分发怀旧软件。某些 Ubuntu 开发者使用 PPA 来制作软件的最新版本，尽管是以非官方且未经测试的方式进行的。例如，当 OpenOffice.org 或 Firefox 发布新的大版本时，请关注 Ubuntu 论坛（http://www.ubuntuforums.org/），看看是否有人通过他们的 PPA 提供了最出的版本。

## 项目 6C：安装 Ubuntu 存储库中未提供的 DEB 包：Skype

如图 6-11所示，Skype 是一种网络电话（VoIP）软件，允许你通过互联网与其他 Skype 用户通话，其清晰度相当于普通电话线。最棒的部分是，它是免费的——即使你拨打海外用户。Skype 还提供如 SkypeOut 等服务，允许你从电脑拨打普通手机和座机电话，其费用仅为普通电话的一小部分。

![](img/58abec7ac6c22ade6357fd77ea421da3_126_0.png)

图 6-11: Skype

虽然 Ubuntu 中确实提供了如 Ekiga Softphone 这样的开源 VoIP 软件包，但它们与广为人知且更广泛使用的 Skype 并不兼容。由于你认识的大多数很可能在使用像 Skype 这样的 VoIP 软件包，因此使用你可以与他们轻松通信的 Skype 才有意义。

由于由于 Ubuntu 存储库中没有提供 Skype，你需要从 Skype 官方网站（http://www.skype.com/）获取。一旦点击“下载”（Download）按钮，它将自动带你进入 Skype Linux 版本的下载页面。在该页面，点击 Ubuntu 链接，并在弹出窗口中点击“保存文件”（Save File）按钮。

下载完成后，你将在硬盘上找到该 DEB 包，可能在你的“下载”（Downloads）文件夹中。双击该包以打开安装程序窗口（图 6-12）。点击“安装包”（Install Package），之后系统会提示你输入密码。安装完成后，点击弹出的窗口中的“关闭”（Close）按钮，再次在软件包安装程序窗口中点击关闭。

与所有的 APT 前端一样，你不能在另一个前端打开时使用软件包安装程序（Package Installer）。因此，在使用软件包安装程序之前，我们会关闭更新管理器（Update Manager）和 Ubuntu 软件中心（Ubuntu Software Center）。

一旦所有组件安装完毕，你可以通过选择“应用程序”（Applications）▸“互联网”（Internet）▸ Skype”来运行 Skype。如果你发现无法通话或声音工作不正常，请查看 https://help.ubuntu.com/community/Skype/ 获取故障排除提示。此外，既然提到声音，请记住使用耳机麦克风使用 Skype 是最好的，否则可能会导致反馈或回声，因为麦克风会拾取并传输来自扬声器的声音。

![](img/58abec7ac6c22ade6357fd77ea421da3_127_0.png)

图 6-12: 软件包安装程序窗口

## 7

## 整洁的嵌套

*Ubuntu 中的文件和光盘处理*

![](img/58abec7ac6c22ade6357fd77ea421da3_129_0.png)

无论你使用哪种操作系统，都必须处理文件。有些人非常有条理，在文件第一次保存时就会立即将其放在一个命名逻辑的文件夹中。还有像像我这样的人，会将所有内容都保存到桌面上，直到无法看清壁纸为止，只有在那个时候才开始认真整理（如果把所有这些文件放在一个名为“March17Cleanup”的单个文件夹里可以算整理的话）。

当然，存储在硬盘上的不仅是文件，它们还会在 CD、DVD、外部硬盘、优存盘和其他存储介质及设备之间复制。它们通常也被保存到归文件中，然后对归文件进行压缩以减小空间占用，使其更容易通过电子邮件发送或装入可移动存储介质中。

有了这些介绍，你可能已经猜到，在本章中，我将处理 Ubuntu 中的文件处理，特别是与 Nautilus（海牛）文件管理器有关，它是 GNOME 文件处理能力的核心。

## Nautilus：你的文件管理器

正如我提到的，在你的系统上创建文件查看和组织界面的程序称为 Nautilus，它是 GNOME 桌面环境的一部分。你以前可能没有将操作系统的文件管理器考虑过是一个程序，但事实上，它就是程序。（Windows 文件管理器被称为 Windows 资源管理器。）要查看 Nautilus，只需进入“位置”（Places）菜单并选择“主文件夹”（Home Folder）。

当 Nautilus 打开到你的主文件夹时（如图 7-1 所示），你会发现可以按主题存储文件：文档（Documents）、下载（Downloads）、音乐（Music）、图片（Pictures）、模板（Templates）和视频（Videos）。还有一个名为“桌面”（Desktop）的文件夹，如果双击它，将将显示你在桌面上存储的所有内容（在我的情况下很多；很可能你的也是如此）。另外还有一个名为“示例”（Examples）的文件夹，其中包含示例文件，让你了解 Ubuntu 为你准备了什么。

你可以随心所欲地创建额外的文件夹和文件，因为一旦你开始真正使用你的系统，这种预配置的状态肯定会改变。事实上，你将在第 8 章中进行一些更改，这会让一切看起来更具生活气息。

![](img/58abec7ac6c22ade6357fd77ea421da3_130_0.png)

图 7-1: 在 Nautilus 窗口中看到的主文件夹内容

## 侧边栏

Nautilus 有许多值得提及的有趣功能，其中最明显的是侧边栏（side pane），它出现在窗口的左侧。侧边栏允许你通过可选视图查看各种信息。你可以通过点击侧边栏顶部的下拉菜单来做出选择（图 7-2）。

![](img/58abec7ac6c22ade6357fd77ea421da3_131_0.png)

图 7-2: 为 Nautilus 侧边栏选择视图

Ubuntu“位置”（Places）中的默认视图是一种快速导航工具。在“位置”中，你会找到代表系统可用各种数据存储位置的图标，例如你的主文件夹、桌面、文件系统、你连接的任何网络共享（稍后会更详细介绍）以及你连接的任何可移动介质或设备。点击这些图标中的任何都会显示该位置的内容。当然，还有其他视图，例如“树”（Tree），它为你提供一个可扩展的文件系统视图；以及“历史”（History），它显示你最近访问过的地方，就像网络浏览器中的历史功能工作一样。还有其他视图供你选择，它们将在第 8 章中发挥作用。

### 眼见有，不见无

侧边栏是一个相当实用的功能，但有时你可能更喜欢有更多空间来查看窗口内容，并想去掉这个侧边栏。你可以通过点击侧边栏右上角的小关闭按钮，或者进入“视图”（View）菜单并取消勾选“侧边栏”（Side Pane）来轻松实现这一点。该选项旁边的勾标记将会消失，侧边栏也会之消失。要找回它，只需返回菜单并再次选择“侧边栏”。勾标记将再次出现，侧边栏也会随之出现。
