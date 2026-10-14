
- Animations（动画）：在执行窗口操作（如最小化和最大化应用程序、启动和终止应用程序等）时提供图形效果

- Desktop Wall（桌面壁纸）：提供平滑的虚拟桌面/视口切换应用程序

- Expo：在屏幕上显示您所有窗口的缩小版图像，以便您可以快速选择特定窗口

- Move Window（移动窗口）：为移动窗口提供鼠标和键盘快捷键，如果标题栏不易于选择，那么这会非常有用

- Resize Info（缩放尺寸信息）：在缩放窗口时提供共享预览，并在移动鼠标时显示关于窗口当前大小的数字信息

- Snapping Windows（窗口吸附）：允许您通过将窗口拖动到屏幕边缘将其移动到其他桌面，并允许您配置此发生的速度以防止意外将窗口移动到其他桌面

- Static Application Switcher（静态应用程序切换器）：为切换打开的应用程序提供更具吸引力的 Alt+Tab 界面、高级图像加载和文本渲染效果

- Window Decorations（窗口装饰）：额外的窗口装饰功能，例如阴影（某些窗口装饰器如 Emerald 需要）

Normal 设置还激活了其他插件，这些插件可能执行内部功能或默认未绑定到特定键。

* Extra（额外）：选择此选项将激活与 Normal 外观偏好设置相关的插件并激活其他插件，其中最有趣的是：

- Shift Switch（Shift 切换）：应用程序切换器的增强版，此插件显示最小化预览。

- Wobbly Windows（摇晃窗口）：Compiz 最著名的效果之一，此插件会导致窗口在您移动时产生抖动。

# 提示

所述，选择“None”将禁用 Compiz 和 Compiz Fusion 插件。■

## 第二部分：桌面用户的 Ubuntu

Compiz 和 Compiz Fusion 插件列表在不断扩展，因此在这里给出一个完整列表是不可能的。侧边栏“These Are a Few of Favorite Things（这些是一些喜爱的事物）”在本章的后面列出了一些我发现有用且认为您可能也喜欢的其他插件。

### 详细的 Compiz 配置

两节中讨论的配置机制允许您激活、自定义和禁用 Compiz 及 Compiz Fusion 插件，让您可以访问当前系统上安装的插件完整列表。

在 Ubuntu 系统上，您可以使用标准的 GNOME 配置工具或使用 CompizConfig Settings Manager 来配置 Compiz、Compiz 插件和 Compiz Fusion 插件。其他配置工具也可用，GConf 和 Compiz 是两个大头。在这两种配置机制中，我建议安装并使用 CompizConfig Settings Manager，但如果您不熟悉命令行或已经非常熟悉图形配置编辑器，标准的 GNOME 工具也可以运行得很好。

## 使用 GNOME 配置工具配置 Compiz

在 Ubuntu 系统上，可以使用标准的 GNOME 配置工具配置 Compiz、Compiz 插件和 Compiz Fusion 插件，而无需安装任何特殊工具。GNOME 系统提供了两个操作 GConf 存储的主要配置工具：`gconftool-2`（一个命令行工具）和 `gconf-editor`（一个图形应用程序）。您应该以自己的身份运行它们，不要使用 `sudo`，因为它们可以操作存储在每个用户个人 GConf 存储中的 GNOME 配置信息。如果您通过 `sudo` 运行它们，将编辑 root 用户的 GConf 存储。

# 提示

下一节讨论的 CompizConfig Settings Manager 配置 Compiz 要容易得多。大多数人（包括我在内）总是使用 CompizConfig Settings Manager。■

## 第 6 章：使用 Compiz 窗口管理器

命令行。例如，以下命令检查了 Compiz 晃动窗口（Wobbly Windows）插件的设置：

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

`-R` 选项告诉你递归检索指定存储库的设置。关于给定插件是否存储在 `/apps/compiz/general/allscreens/options/active_plugins` 存储库项中的信息，例所示：

```
$ gconftool-2 -g /apps/compiz/general/allscreens/options/active_plugins
[svg,img.jpg,text.png,neg,workarounds,dbus,video,regex,\
resize,core,vpswitch,move,reize,shift,extraw,decoration,\
wall,animation,expo,zoom,swimmer,fade,scale,scaleaddon,scalefilter]
```

### 注意

在书中所有关于字符限制的示例中，`\character` 被用于过长而无法在本书正文中正确显示的行末尾。你不会在输出中看到这个字符，在实际输入命令时，你不应该使用该字符、随后的换行符或下一行开头的任何空格，如示例所示。■

`-g` 选项返回指定存储库键的值。该命令的输出显示晃动窗口插件未启用。

若要从命令行激活晃动窗口插件，你将使用 `-s` 选项，它允许你将指定的存储库键设置为指定的值。`-s` 选项必须与 `--type` 选项配合使用，以识别你正在设置的值类型。有效的选项包括：

### 第二部分：面向桌面用户的 Ubuntu

```
-- type 选项有 bool（布尔值），float（浮点数值），int（整数），list（一个由 bool, float, int 或 string 组成的值列表），pair（两个不同的值）或 string（文本字符串）。需要识别正在设置的值类型，以便 gconf-2 能够确定（例如）值 true 是字符串还是布尔值。
```

设置 `active_plugins` 存储库键以激活晃动窗口插件的命令类似于如下：

```
$ gconf-2 -s /apps/general/allscreens/options/active_plugins \
  [svg,jpeg,text,place,png,ng,workarounds,dbus,video,regex,resize,\n  core,pswitch,move,resizeinfo,shift,extraw,decoration,wall,animation,\n  expo,ezoom,switcher,fade,scale,scaleaddon,scalefilter,wobbly]' \
  --type list --list-type
```

你必须以字符 `{` 和 `}` 结尾以限制列表。一旦执行此命令，检查 `active_plugins` 键的值将显示晃动窗口插件现在已在插件列表中：

```
$ gconf-2 -g /apps/compiz/general/allscreens/options/active_plugins \
  [svg,jpeg,text,place,png,ng,workarounds,dbus,video,regex,resize,\n  core,pswitch,move,resizeinfo,shift,extraw,decoration,wall,animation,\n  expo,ezoom,switcher,fade,scale,scaleaddon,scalefilter,wobbly]
```

你也可以通过使用鼠标抓取任何窗口的标题栏并移动它来确认此插件已启用。总会有果冻（JELL-O）留的空间！
