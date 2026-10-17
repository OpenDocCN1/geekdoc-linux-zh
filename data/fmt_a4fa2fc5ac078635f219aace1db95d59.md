
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

Wait that's example. Need actual text.

Let's produce proper output.

[content]
### 7. 收集您的电子邮件
选择您发送的消息并选择所有的 iCalendar 账户。

### 8. 保存附件
选择 `文件 -> 保存附件 -> 所有附件`。

### 9. 确认保存
在“保存所有附件”对话框中，点击确定。

### 10. 选择保存位置
选择一个文件夹用于保存附件。找到您的 iPod，然后找到它的“日历”文件夹并点击确定。

您现在已在 iPod 上存储了单一日历事件。当您断开 iPod 时，进入日历，您将在指定的日期看到您的事件。

# 第2章 — 不仅仅是音乐

## 剪贴板到笔记
`Clipboard to Note`。这是一种非常简单、快速的为你的 iPod 添加笔记的方法。要使用它，请选择文本并复制，然后切换到 iTunes 并运行此脚本。复制的内容将进入笔记并传输到 iPod。如果你复制的文本超过了 iPod 笔记的 4K 限制，别担心：脚本会自动将你的文本复制到链接的笔记中。

## 清除所有笔记
`Clear All Notes`。使用此脚本可以快速清除所有的笔记。脚本还提供删除所有子文件夹的选项。

## 列出笔记
`List Notes`。当你想查看所有笔记列表时，运行此脚本。你可以选择一个并点击“打开”，在文本编辑 `TextEdit` 应用程序中显示文本。如果你有很多笔记，这可能需要一些时间。图 2-12 显示了工作原理的示例。

![](img/8c2b1397c975afc8f1f77ad5fa49fc6c_57_0.png)

图 2-12：列表显示其结果。

## MacCentral
此脚本使用 Safari 打开 MacCentral 网站，并将第一篇文章作为 iPod 笔记。因为你可以获得脚本的源代码列表，你也可以将其修改以适用于其他网站。

## 打印友好
`Printer Friendly`。这是一个非常用但有点奇怪的功能。它获取 Safari 前台窗口的文本并将其制作笔记。它被称为“打印友好”，是因为它可以处理带有图形或链接的页面，你也可以将其用于指向的任何页面。

# 第一部分 — 破解 iPod

## 脚本实现的成功

如果你对学习更多关于 AppleScript 如何帮助你用 iPod 做酷的事情感兴趣，请一定要访问 `www.malcolmadams.com/itunes` 查看 Doug 的 iTunes AppleScripts，并且不要错过第 6 章对 Doug 某些脚本的探索。

## 在 iPod 上使用 WinAmp

此破解方法仅适用于 Windows 电脑。

![](img/8c2b1397c975afc8f1f77ad5fa49fc6c_58_0.png)

你可能知道 iTunes 并不是唯一的音乐播放器。其他程序，如 MusicMatch Jukebox 和 WinAmp，存在于数百万快乐用户的硬盘中。当 iPod 首次出现时，还没有 Windows 版 iTunes。相反，Apple 与 MusicMatch 合作，使 MusicMatch Jukebox 成为 Windows 的官方 iPod 软件。尽管这种身份在 2003 年 10 月 Apple 推出 Windows 版 iTunes 时结束了，但你仍然可以自由在 iPod 上使用 MusicMatch。

然而，数百万 WinAmp 用户并没有那么幸运。WinAmp 是最早的数字音乐应用之一，它包含了游戏和可换皮肤等精妙功能。然而，WinAmp 并没有提供 iPod 支持。但在 2004 年 2 月，Christophe Thibault 发布了适用于 WinAmp 的 iPod Plug-in。这段小代码允许 WinAmp 用户连接他们的 iPod 并传输音乐到其中。当你安装 iPod Plug-in 时，你的 iPod 就会出现在 WinAmp 的设备列表中，如图 2-13 所示。

iPod Plug-in 提供了基本功能，例如将音乐复制到 iPod 以及在 WinAmp 中播放存储在 iPod 上的音乐。但插件缺少功能，最显著的是不支持 iTunes 管理的播放列表。尽管如此，WinAmp 的忠实粉丝现在可以继续使用他们喜欢的数字音乐程序并管理他们的 iPod。

要下载 WinAmp，请访问 `www.winamp.com/player/`。WinAmp 的基础版本是免费的——$15 可以获得更多功能，包括 MP 提取和快速 CD 刻录。iPod Plug-in 在 `www.winamp.com/plugins/details.php?id=13888` 免费获取。

## 将 iPod 连接到 Mac 和 Windows PC

如果你同时有 Mac 和 PC，你可能会发现很难在两台电脑上都使用你的 iPod。有一个简单的方法。首先，确保 iPod 上没有你需要的内容，因为你将重新格式化它。要这样做，运行 Windows 版的 `iPod Updater` 并点击“恢复”`恢复`。这会使用 FAT32 系统格式化 iPod。

![](img/8c2b1397c975afc8f1f77ad5fa49fc6c_59_0.png)

图 2-13：安装 iPod Plug-in 时 WinAmp 中的 iPod 播放器。

![](img/8c2b1397c975afc8f1f77ad5fa49fc6c_59_1.png)

图 2-14：`iPod Updater` 正在为 Windows 格式化 iPod。

系统是 Windows 的原生系统，但也受 Mac OS X 支持。然后，你可以在任何一个操作系统上通过 iTunes 与 iPod 通信，也可以通过 Mac OS X 访达 `Finder` 以及 Windows 资源管理器。

如果你以后决定想让你的 iPod 专为 Mac 格式化，可以通过运行 Mac 版的 `iPod Updater` 来反转过程。再次，在用 `iPod Updater` 抹除磁盘内容之前，确保 iPod 上没有你想要保留的内容。

> 你可以通过选择 `设置 ↻ 关于` 并一直滚动到底来判断 iPod 是否是为 Windows 格式化的。

![](img/8c2b1397c975afc8f1f77ad5fa49fc6c_60.png)

## 下载音频书

音乐并不是唯一的资源。

iPod 的另一个酷功能是标记。你可以使用标记跳转到书的不同部分。

数字音频书、广播、播客，在《纽约时报》处可以找到。

关于音频书的更多信息，请查看时间线。

![](img/8c2b1397c975afc8f1f77ad5fa49fc6c_60.png)

![](img/8c2b1397c975afc8f1f77ad5fa49fc6c_61.png)

| 商店 | 什么是 Audible | 为什么选择 Audible | 如何工作 | 我需要 | 购买方式 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 登录 | 收听《纽约时报》或畅销书。 | 亮点 | 新 iPhone/iPad 支持 | 新免费收听 | |
| 密码 | 随时随地收听音频书、广播、播客。 | 新音频书 | 每日播客 | 新超值 | |
| 加入 | 加入时获得免费入门礼品。 | 期刊与广播 | 《经济学人》 | 收听列表 | |
| 记住我 | 首月会员费五折 | 一种智能、灵活的纸质书籍替代品。 | 无字、无界 | | |
| 演示 | | Apple® iPod 捆装优惠 $10 | iPod MP3 播放器 | | |
| 搜索 | | | | 输入标题或关键词 | |
| 浏览内容 | | | | | |
| 自我提升 | 艺术与娱乐 | 新闻 | 传记与记忆 | 科幻与幻想 | 报纸 | 杂志 | 广播与电视 |

图 2-15：Audible.com 首页。

由 Audible 提供。

## 从 OmniOutliner 查看大纲

此破解方法仅适用于 Mac 计算机。

来自 Omni Development, Inc. 的 OmniOutliner 是处理任何类型层次结构的超级工具，例如脑力风暴、大纲、目录和组织结构图。Mac 预装了 OmniOutliner。如果你还没有，你可以在 `www.omnigroup.com/applications/omnioutliner` 下载免费体验版或购买。
