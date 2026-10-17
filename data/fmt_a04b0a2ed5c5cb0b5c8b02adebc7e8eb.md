
## 第 142 第 6 章：图形用户界面 (GUIs)

启动新应用程序时在命令行上的不同选项，这些值将覆盖您的 `.Xdefaults` 文件中的设置。

`.Xdefaults` 文件中的以下条目使所有 `xterm` 窗口以蓝色背景上的黄色字符显示启动：

```
XTerm@background: blue
XTerm@foreground: yellow
```

如果您省略了应用程序名称，则您列出的资源和值将被所有识别它们的应用程序使用。例如，以下条目会导致所有窗口具有蓝色背景，但 `xclock` 除外，它具有青色背景：

```
@background: blue
XClock@background: turquoise
```

星号 `*` 是一种模式，仅匹配应用程序或资源组件的全名。如 `XT*-background` 这样的规范将适用于名为 `XT` 的应用程序（如果存在的话），而不会对其他以字母 `XT` 开头的应用程序（如 `xterm`）产生影响。以下示例包含了一些实用的条目，以指导您设置自己的 `.Xdefaults` 文件。您可以通过在行开头使用感叹号 `!` 来在文件中包含注释。

```
+ * Resources for Xterm:
! 开启滚动条。
XTerm*scrollBar: True
! 使用大字体（10 像素宽，20 像素高）。
XTerm*Font: 10x20
! 保留更多可滚动行。
XTerm*saveLines: 150

+ ! Resources for the calculator
Xcalc*Background: slategray
Xcalc*Foreground: white
Xcalc*screen.LCD.Background: lightgray
Xcalc*screen.LCD.Foreground: black

+ ! 设置 Netscape 资源
Netscape@Foreground: White
Netscape@Background: #B2B2B2

+ ! 所有窗口（包括 XTerms）的一些默认设置
@highlight: black
@borderColor: black
@Foreground: black
@Background: bisque
```

## 自定义 fwm 窗口管理器 143

当应用程序启动时，它会检查主目录下的 `.Xdefaults` 以查找相关设置（如果该文件存在）。如果您在具有不同主目录的多个台计算机上拥有账户，您可以以每个主机为基础，为任何应用程序自定义资源。例如，如果您在 `sobel` 的 `.Xdefaults` 中设置了 `xterm*-background:blue`，而在 `kudos` 上设置了 `XTerm*-background:black`，那么您屏幕上 `xterm` 的背景颜色将取决于您是在 `sobel` 还是 `kudos` 上运行 `xterm`。如果您的主目录通过网络文件系统被许多台机器共享，您可以通过在主目录中创建多个 `.Xdefaults` 文件来实现相同的效果，其中包含识别该文件所在的主机名称。扩展上面的示例，命名为 `.Xdefaults-sobel` 和 `.Xdefaults-kudos` 的文件设置了针对在这些特定主机上启动的应用程序的资源。

您可以通过加载 X 服务器在多个主机上应用资源。在服务器中配置的资源优先于 `.Xdefaults` 文件中指定的资源。按照惯例，加载到服务器的资源通常存储在名为 `.Xresources` 的文件中。若要在启动 X 时加载这些资源，请在 `.xinitrc` 的开头添加以下行：

```
xrdb -load ~/.Xresources
```

在这种情况下，您不希望在后台运行该命令，因为这可能允许应用程序解析 `.Xresources` 中的选项。如果您在启动 X 窗口系统后更改了 `.Xresources` 文件，可以在 shell 提示符处输入上述命令来加载新规范。

如果您的系统配置为使用 `xdm` 管理 X 会话，则系统级 Xsession 脚本通常使用 `xrdb` 加载您的 `.Xresources` 文件，因此您不需要将该命令添加到 `.xsession` 文件中。

## 自定义 FWM 窗口管理器

您可以通过多种方式自定义 `fwm` 窗口管理器。您可以更改或添加用于与 `fwm` 交互的菜单，更改与按键和鼠标按钮绑定的操作，更改虚拟桌面的大小，以及更改界面的视觉效果。`fwm` 的默认配置指定在 `/usr/lib/X11/fwm/system default` 文件中，包括如何访问每个菜单、每个菜单中出现的项目名称，以及与每个项目关联的操作。为了根据您的需求自定义 `fwm` 的视觉效果，请将系统默认文件复制到您的主目录，并将其命名为 `.fwwmrc`。

您对 `.fwwmrc` 副本所所的更改不会影响其他用户。如果您在自定义 `fwm` 时遇到问题，可以随时通过将系统 `.fwwmrc` 文件复制到主目录来重新开始。

## .fwwmrc 文件

窗口管理器的行为由 `.fwwmrc` 文件决定。您可以修改此文件的内容，从而对 `fwm` 拥有巨大的控制权。在您可以配置的属性中：

- 窗口边界和菜单的颜色和字体
- 运行模式，例如点击聚焦以及图标放置的位置
- 用于模拟 Motif 窗口管理器部分的特殊功能
- 虚拟桌面的大小以及用于在桌面上移动的页器（pager）
- 查找添加 `fwm` 的任何特殊模块
- 与特定应用程序使用的特殊操作，例如标记那些应在桌面每个视图中显示的应用程序，以及当应用程序图标化时选择使用哪一个
- 使用哪些菜单以及在每个菜单中放入什么
- 按下鼠标按钮时使用的复杂函数以及操作与鼠标按钮的绑定
- 窗口标题栏中显示哪些按钮

> **警告**：实际上有两种格式用于配置 `.Xdefaults`，具体取决于版本。本节中使用的格式是版本 1。详情请参阅 `seewm` 手册。

## 设置主要模式

如果您想使用点击聚焦（click-to-focus）模式，请在 `.fwmrc` 中添加以下行：

```
ClickFocus
```

要使用跟随鼠标（focus-follows-mouse）模式，通过在开头添加井号 `#` 将其注释掉：

```
# ClickFocus
```

如果您希望在将鼠标指针停留短时间后自动升起窗口，请添加以下行：

```
AutoRaise 750
```

## 设置虚拟桌面

`fwm` 窗口管理器允许您指定比物理屏幕大得多的虚拟桌面。虚拟桌面的大小以物理尺寸为单位。例如，以下行创建了一个高三屏、宽四屏的虚拟桌面：

```
DeskTopSize 3x4
```

一个名为页器（Pager）的小窗口显示整个桌面。使用页器，您可以通过左鼠标键点击页器的相应部分，或通过右鼠标键拖动页器的选中部分来移动虚拟桌面。可以通过以下将页器放置在物理屏幕左上角：

```
Pager 5 5
```

为了让页器保持在所有窗口之上（使其不会被隐藏）并避免浪费标题栏空间，请添加：

```
StaysOnTop Fwm Pager
NoTitle Fwm Pager
```

您还可以通过鼠标指针碰撞物理显示边缘来移动虚拟桌面。要启用此功能，请添加以下行：

```
# 每次移动一个完整的物理屏幕 (100%)
EdgeScroll 100 100
# 在鼠标指针碰到边缘时设置轻微延迟，
# 以帮助避免物理显示的意外移动
EdgeResistance 250 50
```

## 自定义图标

若要在屏幕的固定位置（例如底部）放置图标，请使用一个或多个 `IconBox` 命令指定位置。以下指定了底部边缘的一个框：

```
IconBox -150 90 -5 -140
```

## GoodStuff

`GoodStuff` 模块提供了一个位于 `fwm` 根窗口上的按钮面板。这些按钮可以执行命令、提供信息（如显示时钟）或移动虚拟桌面。要运行 `GoodStuff`，请在您的 `.fwwm` 文件中放置 `Module GoodStuff` 行。有关如何设置 `GoodStuff` 以实现您的意愿的信息，请通过执行命令 `manStuff`（按所示使用大写）来查看帮助页。

# 146 第 6 章：图形用户界面 (GUIs)

## 特定应用程序的自定义

你可能希望窗口管理器特殊处理某些应用程序。例如，时钟等某些程序通常不需要标题栏。你可以通过以下几行去掉标题栏：

```
NoTitle clock
NoTitle sunclock
```

在移动虚拟桌面时，你可能希望某些窗口能够“固定”（留在物理屏幕的某个位置——就像粘在玻璃上一样）。使用以下几行：

- `Sticky clock`
- `Sticky sunclock`
- `Sticky xcb`
- `Sticky xbbiff`
- `Sticky xcalc`

如果你始终希望应用程序的窗口可见（显示在所有其他窗口之上），可以使用 `StaysOnTop`：

```
StaysOnTop sunclock
```

你也可以使用类似下行的代码为程序添加特殊的图标：

```
Icon "xcalc" /usr/include/X11/pixmaps/xcalc.ppm
```

## 为 fvwm 构建菜单

你使用 `Popup` 命令创建菜单。该命令的代码以 `.fvwm` 开头，以便向其他命令标识菜单；此名称不会显示在菜单上。`EndPopup` 行结束 `Popup` 命令。

`Popup` 和 `EndPopup` 之间的行是注释（以井号 `#` 开头的行）或菜单项。以下示例显示了一个可以让你启动实用工具菜单的菜单。左侧是代码，右侧（对应页）是该代码生成的弹出菜单。

```
Popup "Utilities"
# 设置菜单标题
Title "Utilities"
# 这些行运行一些实用的应用程序
Exec "Mail" exec /usr/local/bin/pine &
Exec "Man pages" exec /usr/local/bin/tkman & 
Exec "Calendar" exec /usr/local/bin/ical & 
Exec "Calculator" exec xcalc -rpn &
Exec "Rolodex" exec xrolo & 
Exec "Xgrab" exec xgrab &
# 在菜单中留空一行
Nop
  "
```

```
# 访问网络工具的子菜单
Popup "Networking" Network
```

## 启动 DOS 或 Macintosh 模拟器

```
Exec "Dos" exec xdos &
Exec "Macintosh" exec executor &
Nop
```

| 实用工具 |
| :--- |
| Mail (邮件) |
| Man pages (帮助页) |
| Calendar (日历) |
| Calculator (计算器) |
| Rolodex (通讯录) |
| Xgrab |
| Networking (网络) |
| Dos |
| Macintosh |
| Shells (终端) |
| Lock Screen (锁屏) |
| Toys (玩具) |
| Exit Fwm (退出 Fwm) |
| Refresh (刷新) |

# 访问不同 Shell 的终端模拟器子菜单

```
Popup "Shells" Shells
Nop
```

# 不同的屏幕锁和切换工具的子菜单

```
Popup "Lock Screen" Screenlock
Popup "Toys" Toys
Nop
```

# 退出或重启 Fwm 的子菜单

```
Popup "Exit Fwm" Quit-Verify
Nop
```

# 刷新屏幕以清理

```
Refresh "Refresh Screen"
EndPopup
```

以下行将标题 `Utilities`（实用工具）居中对齐并放置在弹出菜单的顶部。

```
# Title "Utilities"
```

你可以为菜单项指定一个名称；此名称恰好匹配弹出菜单的名称。

以 `Exec` 开头的行会插入在选中时运行程序的条目。`Exec` 后的第一个字段显示在菜单中，用于向用户标识命令。其余字段是选中时要运行的命令，包括任何参数。由于你通常希望在命令执行时继续使用窗口管理器，示例中的每个命令都以连接符 `&` 结尾，这会导致命令在后台运行。来自 `fwm` 的以下行代码会在菜单中显示一条水平分割（线）。这些行让你能够对菜单项进行分组。

```
Nop ""
```

你可以使用此行代码在菜单内部创建子菜单：

```
Popup "Networking" Network
```

如果用户选择了标记为 `Networking` 的项，`fwm` 将显示由 `Network Popup` 命令定义的菜单。

`Popup` 菜单代码中的最后一条条目添加了一个调用 `fwm` 内置命令 `Refresh` 的项目。

以下 `Mouse` 命令（来自 `.fwmrc` 文件）用于在根 (R) 窗口中按下鼠标键 1 时，将 `Utilities` 菜单绑定到该按钮。`A` 表示你可以结合任何修饰键（如 CONTROL 或 SHIFT）按下鼠标键。

```
Mouse R A Popup "Utilities"
```

通过本节中的命令，你可以为 `fwwm` 窗口管理器构建自定义界面。这让你能够轻松设计出符合你使用 X 窗口系统习惯的界面。参阅 `fwwm` 手页以了解更多如何自定义 `.fwwm` 文件的信息。

## 自定义 MOTIF 窗口管理器

通过 `fwwm`，你可以以多种方式配置 Motif 窗口管理器 (`mwm`)。除了使用资源属性自定义 Motif 的行为外，你还可以更改或添加用于与 Motif 交互的菜单，以及访问它们的方式。Motif 的默认配置由文件 `/usr/lib/X11/Xwm/system.mwmrc` 指定，包括如何访问每个菜单、每个菜单上显示的项目名称以及与每个项目关联的操作。

## 注意事项

如果你在自定义 Motif 时遇到问题，应该可以通过按下 `ALT-SHIFT-CONTROL-!` 将会话恢复到 `system.mwmrc` 中指定的默认值。Motif 会显示一个对话框要求你确认。

## 第 6 章：图形用户界面 (GUI)

请参阅系统提供的在线帮助手册页和其他文档。有关当前系统中不可用工具的更多信息，请访问支持 Linux 和 X 窗口系统的网站。这些网站还包含了其他你可能觉得有用的应用程序信息。第 7 章将更详细介绍如何使用你的 Linux 系统访问互联网。

如果你在 Linux 上使用 X，则有多种文字处理系统可供选择。商业系统包括许多 DOS 和 Windows 用户熟悉的流行的 WordPerfect 系统，以及 Applexware，这是一款包含文字处理器、电子表格程序和演示文管理器的办公套件。除了这些商业系统外，还有几个免费软件包也提供文字处理支持。这些包括 Andrew Toolkit 的一部分（第 128 页）中的 `ez editor`，以及 `Lyx`，后者为 LaTeX 文档格式化系统提供了一个强大的基于 GUI 的处理前端。

X 窗口系统的强大之处之处在于，应用程序独立于窗口管理器；窗口管理器（如 `fwm`）只是另一个应用程序。因此，你可以使用任何窗口管理器运行任何应用程序。应用程序不会继承窗口管理器的属性。例如，由 `xterm` 终端模拟器提供的 Athena 滚动条在所有窗口管理器下的显示和操作方式都是相同的；当你在运行 Motif 窗口管理器运行时调用 `xterm`，它不会变成 Motif 滚动条。

| 常见的 X 应用程序 | 功能 |
| :--- | :--- |
| `apres` | 列出适用于特定工具的资源值 |
| `bitmap` | 构建较小的黑白位图 |
| `color_xterm` | 具有颜色功能的修改版终端模拟器 |
| `executor` | 在 X 窗口中运行 Macintosh 模拟器 |
| `ez` | Andrew Toolkit 文字处理编辑器（第 128 页） |
| `ghostview` | 显示 PostScript 文件 |
| `messages` | 使用 Andrew Toolkit 收发邮件（第 128 页） |
| `pixmap` | 构建较小的彩色位图 (pixmaps) |
| `rxvt` | 一个比 `xterm` 更小的彩色终端模拟器 |
| `showrgb` | 显示 X 可用的所有颜色名称 |
| `sunclock` | 显示地地同步时钟 |
| `tkcvs` | CVS 版本控制的前端 |
| `tkdiff` | 查看两个文件之间的差异 |
| `tkinfo` | info 数据库的前端 |
| `tkispell` | ispell 拼写检查器的前端 |
| `tkmail` | 使用点点界面管理你的邮件 |

## 常见 X 应用程序

| 应用程序 | 功能 |
| :--- | :--- |
| `tkman` | 使用超文本链接访问手册页 |
| `vxp` | 用于开发 X 应用程序的可视 X 编程系统 |
| `wp` | WordPerfect 6.0（商业产品） |
| `xanim` | 显示动画序列 |
| `xcalc` | 模拟手持计算器 |
| `xcb` | 提供多个用于剪切和粘贴的缓冲区 |
| `xclipboard` | 存储并显示从其他应用程序复制的文本 |
| `xclock` | 显示运行中的每日时钟 |
| `xdos` | 在 X 窗口中运行 DOS 模拟器 |
| `xdpyinfo` | 列出有关 X 服务器的信息 |
| `xfig` | 绘制图表、图形和插图 |
| `xfontsel` | 显示可用字体和字体名称 |
| `xftp` | 在网络系统之间传输文件 |
| `x gdb` | gdb 调试器的前端 |
| `xgrab` | 将 X 显示的图像保存到文件 |
| `xhost` | 控制对 X 显示的访问 |
| `xload` | 显示系统忙碌程度的运行图 |
| `xlock` | 防止他人使用你的键盘和显示器 |
| `xfonts` | 列出可用字体的名称 |
| `xmag` | 显示屏幕部分的放大图像 |
| `xman` | 在线手册页的浏览器界面 |
| `xmodmap` | 重新映射鼠标按钮和键盘键 |
| `xpaint` | 在 X 显示上绘画 |
| `xpr` | 打印由 `xwd` 创建的图像 |
| `xrdb` | 将资源设置加载到活动数据库 |
| `xrolo` | 将 Rolodex 在线 |
| `xset` | 设置显示、键盘或鼠标偏好 |
