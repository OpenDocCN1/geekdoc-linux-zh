
此变量表示 `Icons` 变量中的图标位图（pixmaps）应覆盖任何客户端提供的位图。

### `FramePadding` pixels
此变量指定标题装饰（按钮和窗口）之间的距离。默认值为 2。

### `Grayscale` { colors }
此变量指定当屏幕具有 `Grayscale` 默认值时应执行的颜色分配列表。请参见 `colors` 的描述。

### `IconBackground` string
{{ win-list }}
此变量指定图标和图标窗口的背景颜色，只能指定 `Color`、`Grayscale` 或单色列表。可选的 `win-list` 是窗口列表，可以为每个窗口指定颜色。请参见 `BorderColor` 变量获取 `win-list` 的完整描述。默认值为黑色。

### `IconBorder` string
{{ win-list }}
此变量指定图标窗口边框颜色，只能指定 `Color`、`Grayscale` 或单色列表。可选的 `win-list` 是名称和颜色的列表，可以为每个窗口指定颜色。请参见 `BorderColor` 变量获取 `win-list` 的完整描述。默认值为黑色。

### `IconBorder` pixels
此变量指定图标窗口周围边框的像素宽度。默认值为 2。

### `IconDirectory` string
此变量指定如果在 `filepath` 路径中的任何目录中都找不到位图文件，则应搜索的目录。

### `IconFont` string
{{ win-list }}
此变量指定显示图标名称时使用的字体。默认由 `Color`、`Grayscale` 或单色列表指定。可选的 `win-list` 是窗口和颜色的列表，可以为每个窗口指定颜色。请参见 `BorderColor` 变量获取 `win-list` 的完整描述。默认值为黑色。

### `IconifyByUnmapping`
{{ win-list }}
此变量表示窗口在取消映射（unmapped）时应最小化为图标，而不尝试映射任何图标。用户可以通过图标管理器、`f.focus` 命令或 Twins 菜单移动窗口。如果提供了可选的 `win-list`，则对这些窗口指定取消映射。如果在用户的启动路径中设置了绑定到 Twins 菜单，则同时设置了此项和 `IconManagerDontShow` 设置的窗口可能无效。

### `IconBackgroundColor` string
{{ win-list }}
此变量指定图标管理器条目的背景颜色，只能指定 `Color`、`Grayscale` 或单色列表。可选的 `win-list` 是名称和颜色的列表，可以为每个窗口指定颜色。请参见 `BorderColor` 变量获取 `win-list` 的完整描述。默认值为白色。

### `IconManagerDontShow`
{{ win-list }}
此变量表示图标管理器不显示任何窗口。如果给了可选的 `win-list`，则不显示这些窗口。此变量用于防止极少调用的窗口（如时钟或 dock）占用图标管理器的空间。

*

# 第一部分：用户命令

### `IconManagerFont` string
此变量指定显示图标管理器条目时使用的字体。默认值为变量。

### `IconManagerForeground` string { win-list }
此变量指定显示图标管理器条目时使用的前景颜色，只能指定 `Color`、`Grayscale` 或单色列表。可选的 `win-list` 是窗口名称和颜色的列表，可以为每个窗口指定颜色。请参见 `BorderColor` 变量获取 `win-list` 的完整描述。默认值为黑色。

### `IconManagerGeometry` { columns }
此变量指定图标窗口的几何形状。字符串参数是标准几何形状，指示图标管理器的初始 own。图标窗口将被分成列，并根据图标管理器中的条目数量进行缩放。额外的条目将换行显示。默认列数为 1。

### `IconManagerHighlight` string { win-list }
此变量指定高亮当前图标管理器时使用的边框颜色，只能指定 `Color`、`Grayscale` 或单色列表。可选的 `win-list` 是窗口名称和颜色的列表，可以为每个窗口指定颜色。请参见 `BorderColor` 变量获取 `win-list` 的完整描述。默认值为黑色。

### `IconManagers` { iconmgr-list }
此变量指定图标管理器的列表。`iconmgr-list` 中的每个项目具有以下格式：
- `"winname"` `"iconname"`
- `"geometry"` columns
其中 `winname` 是应放入此图标管理器的窗口名称，`iconname` 是该图标管理器窗口的名称，`geometry` 是标准几何形状，`columns` 是该图标管理器的列数（参见 `IconManager-Geometry`）。例如：

```
IconManagers
{
  "Xterm" "300x5+0"
  "geometry" columns
}
```

### `IconManagerShow` { win-list }
此变量指定应放置标题栏的窗口列表。这用于在设置 `noTitle` 时请求标题。

### `IconManagerWidth` pixels
此变量指定图标窗口周围边框的像素宽度。默认值为 2。

### `IconManagerHeight` pixels
此变量指定图标窗口周围边框的像素高度。默认值为 2。

### `IconManagerPadding` pixels
此变量指定标题装饰（按钮和窗口）之间的距离。默认值为 2。

# 第一部分：用户命令

### `NoHighlight` {{ win-list }}
此变量表示不应高亮边框以跟踪指针的位置。如果提供了可选的 win-list，则仅对这些窗口禁用高亮。当边框被高亮时，它将使用当前的 `borderColor` 绘制。当边框未被高亮时，它将使用当前的 `BorderTitleForeground` 和 `BorderTitleback-gray` 颜色以灰色点状图案进行填充。

### `NoIconManagers`
此变量表示不应创建图标管理器。

### `NoMenuShadows`
此变量表示菜单不应在背后绘制投影阴影。这通常用于某些服务器，以牺牲菜单的可读性为代价节省菜单绘制开销。

### `NoRaiseDeiconify`
此变量表示窗口在取消激活时不应将其置于顶层。

### `NoRaiseOnMove`
此变量表示窗口在移动时不应应将其置于顶层。这通常用于允许窗口在彼此下方滑动。

### `NoRaiseOnResize`
此变量表示窗口在调整大小时不应将其置于顶层。这通常用于允许窗口在彼此下方调整大小。

### `NoRaiseOnWarp`
此变量表示当使用 `f.warp` 函数将窗口移动到某个位置时，不应将其置于顶层。如果设置了此选项，移动到一个被遮的窗口可能会导致窗口进入目标窗口内部，从而导致 `f.wrapping` 产生意外行为。

### `NoSaveUnder`
此变量表示窗口不应执行保存最小化（save-minimize），以避免重绘菜单选择。这通常用于重绘速度快于处理 save-under 能力的显示器。

### `NoStack` {{ win-list }}
此变量表示忽略更改堆栈顺序的客户端请求。如果提供了可选的 win-list，则仅忽略这些窗口的请求。这通常用于防止应用程序不断地跳到窗口堆栈的最顶端。

### `NoTitle` {{ win-list }}
此变量表示窗口没有标题栏。如果提供了可选的 win-list，则只有这些窗口没有标题。`MakeTitle` 可配合此选项用于强制在窗口上显示标题。

### `TitleFocus`
此变量表示在进入每个窗口时，不为该窗口设置键盘焦点。通常情况下，它们会设置焦点以便将每个事件分发给管理器。如果指针移动过快而响应缓慢，焦点将重定向到旧窗口而不是新窗口。这通常用于防止这种延迟，并解决某些焦点问题的旧应用程序。

### `OpaqueMove`
此变量表示 `f.move` 函数应仅在窗口轮廓范围内操作，以便用户能立即看到窗口在新位置的样式。此选项通常用于事实显示器（特别是当设置了 noResize 时）。

### `Pixmaps` {{ maps }}
此变量指定一个定义图像外观的 pixmap 列表。每一项都是将 pixmap 映射到一组字符串，该字符串为位图文件名。可以指定以下 pixmaps：
- `Pixmaps` { `TitleHighlight` "gray" }
`TitleHighlight` 的默认值是偶数样式图案。

### `Priority` priority
此变量设置窗口的优先级，这是一个无符号数字（例如， 999）。仅当服务器支持 SYN 事件时，此变量才生效。

### `RandomPlacement`
此变量表示未指定几何形状的窗口应放置在伪随机位置，而不是由用户拖拽。

## twm

## 551

### `ResizeFont` string
此变量指定在调整窗口大小时尺寸处使用的字体。默认是固定字体（fixed）。

### `RestartPreviousState`
此变量表示 `twm` 尝试使用客户端窗口上的 WM_STATE 属性来告知哪些窗口应该图标化，哪些窗口应该显示。这通常用于恢复到上一个窗口管理器关闭之前的状态。

### `SaveColor` { colors-list }
