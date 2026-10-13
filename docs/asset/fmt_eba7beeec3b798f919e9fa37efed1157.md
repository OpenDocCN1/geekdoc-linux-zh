
```
# xset s on
```

10 秒后，X 显示空白屏幕。如果您想看到图形和背景图案，可以对 `xset s` 命令行选项使用 `noblank` 选项，例如：

```
# xset s noblank
```

如您所见，屏幕上显示了一个大 X。要关闭屏幕保护，请使用 `s off` 命令行选项（如果您使用 `xset`，请不要忘记将屏幕保护间隔更改为更合理的值，例如 `600` 代表 10 分钟）。如果这不是您心目中的屏幕保护程序，您可以尝试 `xscreensaver` 客户端。

由 Jamie Zawinski 编写的 `xscreensaver` 和 `xscreensaver-command` 客户端位于 `/usr/X11R6/bin` 目录下。`xscreensaver` 客户端有 16 个命令行选项。虽然本章不涵盖所有选项，但使用此屏幕保护程序的基本方法是首先在后台运行 `xscreensaver` 客户端，如下所示：

```
# xscreensaver -timeout 5 &
```

此命令将屏幕保护程序设置为在五分钟无键盘或鼠标活动后运行。您可以使用 `xscreensaver` 命令客户端控制此客户端以打开或关闭 `xscreensaver` 或立即激活它。虽然 `xscreensaver` 客户端具有 `-lock` 选项可对显示进行密码保护，但您必须重新编译程序才能启用此功能。

`xscreensaver` 客户端附带近二十四种不同的屏幕保护程序，它们也可以作为独立程序运行。例如，您可以在窗口中按如下方式运行分形绘图程序 `hopalong`：

```
# hopalong
```

按下 Enter 后，分形图像会出现在窗口中（如图 7.9 所示），以便您可以看到它的外观。

### 图 7.9

`hopalong` 客户端是 X11 屏幕保护程序的一部分。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_192_0.png)

要获取与 `xscreensaver` 客户端配合使用的屏幕保护程序列表，请阅读 `/usr/X11R6/lib/X11/app-defaults` 目录中的文件 `XScreenSaver`。您可以在该文件中找到其他设置，该文件是此客户端的 X11 资源文件。

您可能也会对 `xlock` 客户端感兴趣。虽然它不是屏幕保护程序，但 `xlock` 是一款功能强大的终端锁定程序，具有近 50 个命令行选项和 50 多种内置显示。`xlock` 客户端在您想通过密码保护显示以防止他人在您离开时使用计算机时很有帮助。

默认情况下，在您启动 `xlock` 程序后，必须在再次使用显示之前输入密码。您可以在不使用密码保护的情况下将其用作简单的屏幕保护程序来显示各种动画，例如：

```
# xlock -duration 10 -nolock -mode random
```

此命令行告诉 `xlock` 程序显示其动画的随机选择，每个动画运行 10 秒。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_193_0.png)

> 如果您使用 `-inroot` 命令行选项，`xlock` 客户端也可以使您的桌面成为动画显示。这不会保护您的系统，但您可能会觉得视觉效果很刺激！

## 探索 X11 程序

本小时没有足够空间讨论 CD-ROM 上的所有 X11 客户端。您可以在本书其余部分找到有关不同客户端的讨论，但本节向您展示了一些有用的程序，它们可以提供有关系统的更多信息以及使用它们的技巧。

### 使用 `xlsfonts` 列出 X11 字体

如果您想要一份系统上 X11 识别的所有字体的列表，可以使用 `xlsfonts` 客户端。如果不带任何选项调用客户端，请使用 `less` 或 `more` 等分页器（在第 4 小时“阅读和导航命令”中讨论）。您还可以使用通配符或模式匹配字体名称。这在查找系统上的特定字体时非常方便，例如：

```
# xlsfonts -fn "*italic*"
lucidasans-bolditalic-10
lucidasans-bolditalic-10
lucidasans-bolditalic-12
lucidasans-bolditalic-12
lucidasans-bolditalic-14
lucidasans-bolditalic-14
lucidasans-bolditalic-18
lucidasans-bolditalic-18
lucidasans-bolditalic-24
lucidasans-bolditalic-24
lucidasans-bolditalic-8
lucidasans-bolditalic-8
lucidasans-italic-10
lucidasans-italic-12
```

```
lucidasans-italic-12
lucidasans-italic-14
lucidasans-italic-16
lucidasans-italic-18
lucidasans-italic-18
lucidasans-italic-24
lucidasans-italic-24
lucidasans-italic-8
lucidasans-italic-8
```

正如您所见，这列出了 X11 服务器上已安装或识别的所有斜体字体。您可以使用 `xlsfonts` 客户端来排查字体是否被识别或已安装，或在启动客户端时查找字体名称以作为 X Toolkit 选项。

## 使用 `xwininfo` 客户端获取窗口信息

您可以使用 `xwininfo` 客户端，或窗口信息实用程序，来获取有关窗口的有用信息。使用此命令时，您可以点击另一个窗口以获取详细的信息列表，例如：

```
# xwininfo
xwininfo: Please select the window about which you
would like information by clicking the
mouse in that window.
```

点击所需窗口后，您会看到信息列表，例如以下内容：

```
xwininfo: Window id: 0xc00002 "rxvt"

Absolute upper-left X: 8
Absolute upper-left Y: 397
Relative upper-left X: 0
Relative upper-left Y: 0
Width: 574
Height: 158
Depth: 8
Visual Class: PseudoColor
Border width: 0
Class: InputOutput
Colormap: 0x21 (installed)
Bit Gravity State: ForgetGravity
Window Gravity State: NorthWestGravity
Backing Store State: NotUseful
Save Under State: no
Map State: IsViewable
Override Redirect State: no
Corners: +8+397 -218+397 -218+45
-geometry 80x11+3+40
```

此信息很有帮助，例如，如果您想获取下次运行程序时窗口几何设置的相关规范，或者如果您想通过编辑其资源文件来更改窗口的默认行为。

## 使用 `xmessage` 客户端制作便签日历

`xmessage` 客户端由 Chris Peterson 和 Stephen Gildea 创建，是在工作时创建快速笔记作为提醒的一种便捷方式。这个看似简单的客户端易于使用。例如，如果您想快速记录一个电话号码，可以使用以下命令：

```
# xmessage "George called at 10:15; call him back at 555-1212" &
```

此命令行会显示带有您消息文本的 `xmessage` 客户端窗口。虽然这是一个简单的示例，但您也可以使用 `xmessage` 客户端来显示程序搜索的输出，或在个人日程中使用它，在工作时自动发送提醒。有关详细信息，请参阅第 18 小时“个人生产力工具”或第 24 小时“使用调度自动化系统管理”。

您还可以使用 `xmessage` 作为便捷的日历显示程序，如果您需要在屏幕上保留当前日历的副本，或在启动 X 会话时希望桌面上显示日历。您找不到 `cal` 日历程序的简单 X11 版本，但这里有一个可用版本：

```
# cal | xmessage -file "-" &
```

这会在正方形的 `xmessage` 客户端窗口中显示 `cal` 日历程序的输出。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_195_0.png)

> 您可以在 `/usr/X11R6/bin` 目录下找到 `ical` X11 客户端，但这是一个具有更大日历显示的个人调度实用程序。有关详细信息，请参阅第 18 小时。

## 使用 X11 时钟保持时间

如果您是习惯看钟的人，使用 X11 时您很幸运，因为可以找到多个时钟。您一定能找到喜欢的一个。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_196_0.png)
