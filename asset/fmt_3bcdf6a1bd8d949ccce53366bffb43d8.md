
当 `lizardx` 的第一个屏幕出现时（如图 5-14 所示），缓慢移动鼠标以对其进行自动配置。然后选择 `Next`（下一步）进入另一个屏幕，在那个屏幕上你可以选择键盘型号和布局。大多数用户可以接受默认设置并简单地选择 `Next` 继续。

![](img/0de795a4f3f708f3baad48fd57def247_194_0.png)

图 5-14 `lizardx` 鼠标配置屏幕

下一个屏幕是 `lizardx` 向导功能显而易见的地方。在 `Select Video Card`（选择显卡）屏幕中，你会发现显卡已经自动检测并出现在屏幕顶部的下拉列表中（见图 5-15）。要完成显卡的配置，选择 `Probe`（探测）按钮；然后在在弹出的对话框中选择 `OK` 以确认开始探测。屏幕变黑，片刻后返回并显示消息“Probing is complete and apparently successful”（探测完成且似乎成功）。选择 `Next` 按钮继续。

![](img/0de795a4f3f708f3baad48fd57def247_195_0.png)

图 5-15 `lizardx` 的 `Select Video Card` 屏幕

下一个屏幕是 `lizardx` 向导功能显而易见的地方。在 `Select Video Card` 屏幕中，你会发现显卡已经自动检测并出现在屏幕顶部的下拉列表中（见图 5-15）。要完成显卡的配置，选择 `Probe`（探测）按钮；然后在在弹出的对话框中选择 `OK` 以确认开始探测。屏幕变黑，片刻后返回并显示消息“Probing is complete and apparently success”（探测完成且似乎成功）。选择 `Next` 按钮继续。

![](img/0de795a4f3f708f3baad48fd57def247_195_0.png)

图 5-15 `lizardx` 的 `Select Video Card` 屏幕

下一个屏幕是 `lizardx` 向导功能显而易见的地方。在 `Select Select Video Card` 屏幕中，你会发现显卡已经自动检测并出现在屏幕顶部的下拉列表中（见图 5-15）。要完成显卡的配置，选择 `Probe`（探测）按钮；然后在在弹出的对话框中选择 `OK` 以确认开始探测。屏幕变黑，片刻后返回并显示消息“Probing is complete and apparently success”（探测完成且似乎成功）。选择 `Next` 按钮继续。

![](img/0de795a4f3f708f3baad48fd57def247_196_0.png)

图 5-16 `lizardx` 的 `Select Mode` 屏幕

要使用 `XF86Setup` 完成配置，请选择 `Mode`（模式）标签并选择屏幕分辨率。最常用的分辨率是 `1024 × 768`。除非你从其他来源获得特殊指令（如你的显卡制造商），否则你不需要设置 `Other`（其他）标签页上的任何选项，尽管你可以根据需要探索它们。

当你点击 `Done`（完成）按钮并确认已准备好启动 `XF86Setup` 时，该实用程序将为你创建一个临时 `XF86Config` 文件并启动 X 服务器以测试配置。如果服务器启动成功，你将看到 `xvidtune` 程序的图形界面。你可以使用程序中的选项调整图片在显示器上的位置，但这通常不是必要的。（你通常使用位于显示器正面的控件来控制屏幕位置。）图 5-13 显示了 `xvidtune` 程序的视图。当你探索完程序中的选项后，选择 `Save and Exit`（保存并退出）退出 X 服务器并保存新的 `XF86Config` 文件。

![](img/0de795a4f3f708f3baad48fd57def247_193_0.png)

图 5-13 `xvidtune` 程序

偶尔 `XF86Setup` 程序看起来运行正常（也就是说，在过程结束时的测试屏幕显示正确），但按照在本章稍后描述的方法启动 X 时，窗口管理器或桌面环境并没有如预期那样出现。在这种情况下，你可以退出 X 并重启 `XF86Setup` 程序以尝试不同的配置选项。

## 运行 X 窗口系统

## 使用 lizardx

配置 X 最简单的方法是使用来自 Caldera Systems 的 `lizardx` 程序。该程序像 `XF86Setup` 一样提供了一个图形界面，通过你可以选择几个简单的选项。但 `lizardx`（Linux installation wizard for X 的 Linux 安装向导缩写）不需要你了解关于显卡的任何知识。它的自动探测功能是 Linux 上最出色的。

`Lizardx` 取自于 Caldera Systems 的 OpenLinux 产品的安装程序。但 `lizardx` 是一个独立的程序，你可以在任何 Linux 发行版的命令行中执行它（前提是你已经从 Caldera Systems 的 FTP `ftp.calderasys.com` 下载了 `lizardx` 程序）。使用此命令启动程序：

```
lizardx
```
