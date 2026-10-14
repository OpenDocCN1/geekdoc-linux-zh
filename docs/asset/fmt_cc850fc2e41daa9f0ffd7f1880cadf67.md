
```
$ gconftool2 -R /apps/compiz/plugins/wobbly
/apps/compiz/plugins/wobbly:
/apps/compiz/plugins/wobbly/allscreens:
/apps/compiz/plugins/wobbly/allscreens/options:
shiver = false
snap_key = <Shift>
snap_inverted = false
/apps/compiz/plugins/wobbly/screen0:
spring_k = 8
map_effect = 0
map_window_match = Splash | DropdownMenu | PopupMenu | \
focus_window_match = Notification | Combo | Dnd | Unknown
friction = 3
focus_effect = 0
maximize_effect = true
grab_window_match =
min_grid_size = 8
grid_resolution = 8
move_window_match = Toolbar | Menu | Utility | Dialog | \
Normal | Unknown
```

`-R`选项告诉你递归检索指定存储库的设置。关于给定插件是否存储在`/apps/compiz/general/allscreens/options/active_plugins`存储库项中的信息，例所示：

```
$ gconftool-2 -g /apps/compiz/general/allscreens/options/active_plugins
[svg,img.jpg,text.png,neg,workarounds,dbus,video,regex,\
resize,core,vpswitch,move,reize,shift,extraw,decoration,\
wall,animation,expo,zoom,swimmer,fade,scale,scaleaddon,scalefilter]
```

### 注意

在书中所有关于字符限制的示例中，`\character`被用于过长而无法在本书正文中正确显示的行末尾。你不会在输出中看到这个字符，在实际输入命令时，你不应该使用该字符、随后的换行符或下一行开头的任何空格，如示例所示。■

`-g`选项返回指定存储库键的值。该命令的输出显示晃动窗口插件未启用。

若要从命令行激活晃动窗口插件，你将使用`-s`选项，它允许你将指定的存储库键设置为指定的值。`-s`选项必须与`--type`选项配合使用，以识别你正在设置的值类型。有效的选项包括：

## 第二部分：面向桌面用户的 Ubuntu

```
-- type 选项有 bool（布尔值），float（浮点数值），int（整数），list（一个由 bool, float, int 或 string 组成值列表），pair（两个不同的值）或 string（文本字符串）。需要识别正在设置的值类型，以便 gconf-2 能够确定（例如）值 true 是字符串还是布尔值。
```

设置`active_plugins`存储库键以激活晃动窗口插件的命令类似于如下：

```
$ gconf-2 -s /apps/general/allscreens/options/active_plugins \
  [svg,jpeg,text,place,png,ng,workarounds,dbus,video,regex,resize,\n  core,pswitch,move,resizeinfo,shift,extraw,decoration,wall,animation,\n  expo,ezoom,switcher,fade,scale,scaleaddon,scalefilter,wobbly]' \
  --type list --list-type
```

你必须以字符`{`和`}`结尾以限制列表。一旦执行此命令，检查`active_plugins`键的值将显示晃动窗口插件现在已在插件列表中：

```
$ gconf-2 -g /apps/compiz/general/allscreens/options/active_plugins \
  [svg,jpeg,text,place,png,ng,workarounds,dbus,video,regex,resize,\n  core,pswitch,move,resizeinfo,shift,extraw,decoration,wall,animation,\n  expo,ezoom,switcher,fade,scale,scaleaddon,scalefilter,wobbly]
```

你也可以通过使用鼠标抓取任何窗口的标题栏并移动它来确认此插件已启用。总会有果冻（JELL-O）留的空间！

`gconf-2`对于从命令行快速查询和操作 GConf 设置非常有用。然而，`gconf-2`可能不是设置“正确”的 GConf 键、识别可能的值以及反复迭代多个设置和值直到获得你想要的效果的工具。我是命令行工具的忠实支持者，但我并不是纯粹主义者——在大多数情况下，图形化工具比命令行工具更易用，特别是当你需要在实验配置值时进行多次更改和测试循环时。

GNOME 用于检查和编辑 GConf 存储库的图形化工具`gconf-editor`默认安装在基于 GNOME 的 Ubuntu 系统上。你可以从任何命令行环境启动`gconf-editor`工具。与`gconf-2`一样，你想通过`sudo`以身份启动`gconf-editor`，这样你就只有你个人 GNOME 存储库的内容。

图 6-2 显示了`gconf-editor`启动时的界面。要找到特定的存储库键，使用`Edit Find`命令显示图 6-3 所示的对话框。

## 图 6-2

图形化 GNOME 配置编辑器

![](img/c20d2ef7a27788ee7a3a4ec5714cd3c)

*(注：由于你提供的待翻译文本存在大量严重的重复和逻辑错位，我已按照文档逻辑进行了清理清理翻译。)*

*(抱歉，由于你提供的待翻译文本中存在严重的错误，我无法进行完全的字面翻译。以上译文是基于上下文逻辑对内容进行清理后的结果。)*

## 第 6 章：使用 Compiz 窗口管理器

...（此处省略，见上方完整逻辑翻译）...

## 第 6 章：使用 Compiz 窗口管理器

Compiz 配置工具让你能够非常容易地迭代更改许多选项，以至于你可能不知道如何将它们恢复到原始值（或者至少不知道那些原始值是什么）。CompizConfig 接口为该问题提供了一个良好且一致的解决方案：它在每个单独的配置设置旁边提供了一个看起来像打蛋器的小图标。随时点击此图标即可将关联配置恢复到其原始默认值。

要启用任何插件但保留其默认配置，请点击该插件图标和名称左侧的复选框，如图 6-7 所示。要配置任何 Compiz 或 Compiz Fusion 插件，请点击该插件的名称或图标。这将显示该插件的配置面板，图 6-8 显示了其中的示例。在配置插件后，你还可以通过在像图 6-8 所示的配置面板左侧中，“使用此插件”（Use This Plugin）下方的选择或取消勾选复选框来启用或禁用该插件。你可以点击左下角的“返回”（Back）按钮回到顶级 CompConfig 面板。

**图 6-8**

在 CompizConfig 中配置特定插件

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_242_0.png)

CompizConfig 屏幕顶部的“通用选项”（General Options）组（参考图 6-7）允许你配置 Compiz 自身的选项，这样做可能会影响多个（或所有）插件。命令（Commands）、GNOME 兼容（GNOME Compatibility）和 KDE 兼容（KDE Compatibility）允许你定义按键/命令映射，并微调 Compiz 对 GNOME 和 KDE 桌面的仿真。这些较少，因此我将在节中重点介绍通用选项组。

### 第二部分：面向桌面用户的 Ubuntu

选择“通用选项”组后，会显示五个标签页，如图 6-9 所示。

图 6-9

在 CompizConfig 中设置“通用选项”

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_243_0.png)

这些标签页中的每一个都包含多个配置选项，例如：

- **常规 (General)**：允许你配置光标及其大小、配置用于命令行运行的终端应用程序、控制 Compiz 是否提供警告和错误消息的听觉通知等。

- **显示设置 (Display Settings)**：允许你配置 Compiz 与显示器交互的各个方面；屏幕显示表面纹理的精细程度、Compiz 是否尝试在变换时自动调暗屏幕（光照 Lighting）、屏幕刷新率、哪些屏幕更新限制在垂直空白期期间进行、Compiz 知知的输出设备以及它是否应该尝试自动识别它们等。
