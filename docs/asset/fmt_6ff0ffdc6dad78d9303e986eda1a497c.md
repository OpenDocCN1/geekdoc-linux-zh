
`button .button -text "Click Me" -background blue` 所示（见图 25.1）。

## 组件选项

所有 tk 组件都使用控制外观和功能的标准选项。大多数组件理解以下内容：

- `-background` color, `-bg`：组件的背景颜色。
- `-foreground` color, `-fg`：组件的前颜色。
- `-height`：组件的高度（像素）。
- `-width`：组件的宽度（像素）。
- `-borderwidth`, `-db`：边框宽度（像素）。
- `-padx`：组件在 x 方向所需的额外空间。
- `-pady`：组件在 y 方向所需的额外空间。
- `-relief`：组件的 3D 效果（平直、凸起、脊、凹陷）。
- `-text`：在组件中显示的字符串。
- `-font`：用于显示文本的字体。
- `-command`：使用组件时执行的 tk 命令。

除了这些选项外，`pack` 命令还理解以下自己的选项：

- `-side`：控制组件的放置顺序（左、右、上、下）。
- `-fill`：控制组件是否拉伸以填充窗口空间（无、x、y、both）。
- `-expand`：控制当窗口尺寸增大时组件是否扩大（0 或 1）。

## 一个 tcl/tk 组件编程示例

现在你已经了解了组件（widgets）和 `pack` 的选项，可以开始使用它们了。组件的有趣特性之一是它们的样式（reliefs），即组件的 3D 视觉效果。为了看到每个样式的效果，请使用以下代码创建一些标签：

```tcl
foreach i {raised sunken flat groove ridge} {
    label .i -relief $i text $i
    pack .i
}
```

此示例遍历了所有样式类型的集合，为每种类型创建一个标签，并将每个标签的文本设置为相应的样式类型。其布局看起来与图 25.2 类似。

图 25.2。具有不同样式的标签。

![](img/740d39911bdfa3e996ee27a7e4e7e4fa_545_0.png)

这里有两点需要注意。首先，标签的大小并不相同。其次，标签是堆叠在一起的。这是 `pack` 命令默认行为的一个示例；它会自动确定每个组件的大小，然后将每个组件放置在上一个放置好的组件下方。

让我们让所有标签的大小相同，并将它们并排排列，而不是一个接一个。有两种方法。第一种是重写循环：

```tcl
foreach i {raised sunken flat groove ridge} {
    label .i -relief $i text $i -height 10 -width 10
    pack .i -side left
}
```

第二种方法是使用 `configure` 选项配置标签，其语法如下：

```tcl
widget configure option
```

在这种情况下，你可以在标签创建后使用以下循环：

```tcl
foreach i {raised sunken flat groove ridge} {
    .i configure -height 10 -width 10
    pack $i -side left
}
```

那么，为什么要使用 `configure` 呢？

如果以交互模式运行 `wish`，并且只给了一个版本的循环，修改并再次运行它将产生以下错误：

`window name "raised" already exists in parent`

这是 `wish` 告诉程序员程序尝试创建一个已存在的组件（在本例中是名为 `raised` 的标签）的方法。因此，你需要使用 `configure`。事实上，当需要更改现有组件时，任何时候都需要使用 `configure`。

在这种情况下，使用新版本循环的办法是使用 `destroy` 命令销毁现有标签：

```tcl
foreach i {raised sunken flat groove ridge} {
    destroy $i
}
```

新的结果将类似于图 25.3。

**图 25.3.** 并排排列的具有不同样式的标签。

![](img/740d39911bdfa3e996ee27a74e7e4fa_546_0.png)

回到示例。在图 25.3 中，有两个地方看起来应该修复。首先，很难区分这些标签。其次，窗口的大部分是空白的。

你可以通过在 `pack` 时添加内边距（padding）并增加边宽（borderwidths）来让标签更容易区分。为了让标签占据所有可用空间，给 `pack` 设置针对 x 和 y 轴的 `fill` 选项，并将 `expand` 选项设置为 true：

```tcl
foreach i {raised sunken flat groove ridge} {
    label $i -relief $i -text $i
    $i configure -height 5 -width 5 -borderwidth 5
    pack $i -side left -padx 5 -pady 5 -fill both -expand 1
}
```

结果将类似于图 25.4。

图 25.4。不同样式的标签，版本 3。

![](img/740d39911bdfa3e996ee27a7e4e7e4fa_547_0.png)

通过将 `label` 替换为其他类型的组件，可以轻松更改此示例以使用任何组件类型。

## 一个 xsetroot 的 tcl/tk 接口

本节通过将它们应用于 X Window 程序 `xsetroot` 的 GUI 前端开发，介绍了 tk 工具包的其他功能。

大多数 X Window 用户都会熟悉 X Window 程序 `xsetroot`，它可以用于设置 X11 根窗口（root window）的背景颜色。实际命令是

```bash
xsetroot -solid color
```

其中 `color` 可以以 `#RRGGBB` 格式给出。前端将允许查看并应用颜色。

让我们开始吧。首先你需要一个存储颜色的变量。然后你需要创建两个基础框架（frames），一个用于应用程序的主区域，另一个用于放置消息。你还需要第三个框架用于控制控件。

框架是一个好用的工具，因为它们可以将特定类型/功能的条目打包在一起。此外，它们在将窗口划分成不改变的部分时非常有用。

全局创建颜色和框架：

```tcl
set color #000000
frame .main_frame
frame .message_frame
frame .control_frame
```

现在 `pack` 框架：

```tcl
pack .control_frame -in .main_frame -expand 1 -fill both
pack .main_frame -anchor c -expand 1
pack .message_frame -anchor s -padx 2 -pady 2 -fill s -expand 1
```

你还需要创建一个标签来处理消息。我将写为一个过程（procedure），这样易于修改和执行：

```tcl
proc make_message_label {} {
    label .message_label -relief sunken
    pack .message_label -anchor c -in .message_frame -padx 2 -pady 2 -fill both
}
```

将标签 `pack` 到 `.message_frame` 中，使其始终位于窗口底部。

现在制作滑块（scales）。你需要三个滑块，分别对应红色、蓝色和绿色，每个范围从 0 到 255。你还需要将滑块及其对应的标签 `pack` 在它们各自的框架中：

```tcl
proc make_scales {} {
    frame .scale_frame
    foreach i {red blue blue} {
        frame .scale_frame_$i -bg $i
        label .label_$i -text $i -bg $i -fg white
        scale .scale_$i -from 0 -to 255 -command setColor
        pack .label_$i -in .scale_frame_$i
    }
}
```
*(注：原文此处重复写了两次 blue，应为笔误，翻译时保持逻辑)* 修正后的逻辑：
```tcl
proc make_scales {} {
    frame .scale_frame
    foreach i {red blue blue} {
        frame .scale_frame_$i -bg $i
        label .label_$i -text $i -bg $i -fg white
