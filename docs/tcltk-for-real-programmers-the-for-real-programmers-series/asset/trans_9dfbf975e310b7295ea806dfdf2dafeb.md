

## 第 9 章 canvas 小部件、图像与事件

### 9.4.5 字体与文本项

字体问题可能像书写语言 6000 年的努力所导致的那样复杂，也可以非常简单。我将只讨论一种与平台无关的字体处理方法。其他方法在在线文档的 `font` 章节中有描述。

Tk 8.0 之前的版本中字体使用 X Window 系统的命名规范：

```
-foundry-family-weight-slant-setwidth-addstyle-pixel-point-resx-resy-spacing-width-charset-encoding.
```

如果你需要使用早于 8.0 版本的 Tk，你可能运行在 Unix 系统上，并可以使用 XII 命令 `xfont -x xfonts` 来确定可用字体的正确名称。

随着 Tcl 和 Tk 8.0 版本的发布，情况变得简单了：字体通过属性列表进行命名：`family ?size? ?style?` 

如果 Tcl 解释器无法找到匹配请求的字体，它将找到最接近的匹配。可以保证，对于任何语法上正确的属性集，都能找到字体。

- family：字体的族名。在所有系统中都定义了 `helvetica` 和 `courier`。可以通过 `font families` 命令获取已定义字体的列表。
- size：字体的尺寸。如果这是一个正值，则是以磅（1/72 英寸）为单位的。显示器的缩放是在 Tk 初始化时定义的。如果这是一个负数，它将转换为正数，并以像素为单位定义字体大小。优先使用磅值定义字体，这可以确保应用程序在不同系统上看起来一致。
- style：字体的样式。可以是 `normal`（或 `roman`）、`bold`（粗体）、`italic`（斜体）、`underline`（下划线）或 `overstrike`（删除线）中的一个或多个。

可以通过 `font` 命令获取字体信息。按照惯，我只讨论一些常用的子命令。

### 9.4 Canvas 小部件子命令

语法：`font families ?-displayof windowName?`
`font families`

返回此系统的有效字体族列表。

- -displayof：如果存在此选项，它定义了返回此数据的窗口（frame、canvas、topwindow）。默认情况下，这是主图形窗口 "."。

`font measure` 命令在尝试以美观的方式在显示器安排文本时非常有用。

语法：`font measure font ?-display windowName? text`
`font measure`

`font measure` 命令返回字符串 `text` 在定义的字体中渲染时所需的水平像素数。

- font：字体的名称，如上所述。
- -displayof：如果存在此选项，它定义了返回此数据的窗口（frame、canvas、topwindow）。默认情况下，这是主图形窗口 "."。
- text：要待测量的文本。

如果 Tk 无法在你的系统上获取请求字体的精确匹配，它将找到最佳匹配。你可以通过 `font actual` 命令确定实际正在使用的是哪种字体。

语法：`font actual font ?-display windowName?`
`font actual`

返回请求字体时将实际使用的实际字体。

- font：请求的字体的名称。
- -displayof：如果存在此选项，它定义了返回此数据的窗口（frame、canvas、topwindow，等）。默认情况下，这是主图形窗口 "."。

### 第 9 章 canvas 小部件、图像与事件

随着 Tk 8.1 的发布，Tcl 和 Tk 开始支持 Unicode 字符字体。这些字体通过在四位 Unicode 值前加上 "\u" 来编码。你可以在 http://Unicode.org 获取 Unicode 字符集的信息。

Unicode 提供了一种处理美国 ASCII 字母以外的字母的标准方法。Unicode 字母表使用 16 位来描述 65,536 个字母。每个字母表都被分配了一个数字范围来表示其字符。通过 Unicode，你可以表示日语假名（katakana）、韩语（hangul）或其他任何主要字母。

以下示例演示了通用 Unix 系统上的可用字体，并显示了一些 ASCII 和 Unicode 示例文本。请注意，如果给字体不支持 Unicode，则会显示 Unicode 数字。此示例使用 Tcl/Tk 8.1a2 版本运行的。此修订版本中刚刚开始添加 Unicode 支持。当你读到这本书时，将会有更多的 Unicode 支持。

#### 示例 9.4.5-1

示例脚本

```tcl
canvas .c -height 950 -width 800
p .c ypos 15
pset families [font families]
foreach family $families {
  c create 4 $ypos -font [list times 18 bold] \
  -text "$family" -anchor nw
  c create 240 $ypos -font [list $family 18] \
  -text "text line -- UNICODE: \u30Ab \u042f \u3072" \
  -anchor nw
  c create 4 [expr $ypos+25] -font [list roman 14] \
  -text "[font actual [list family 18]]" -anchor nw
  c create line 4 [expr $ypos+45] 800 [expr $ypos+45]
 incr ypos 50
}
```

### 9.4 更多 Canvas 小部件子命令

#### 脚本结果

| fixed | test |
| :--- | :--- |
| -size 15 | helvetica |
| -size 16 | mincho |
| -size 15 | courier |
| -size 16 | lyricypewriter |
| -size 15 | lyricright |
| -size 16 | lucida |
| -size 15 | utopia |
| -size 16 | fixed |
| -size 15 | nil |
| -size 16 | clean |
| -size 15 | terminal |
| -size 16 | symbol |
| -size 15 | gothic |
| -size 16 | new century school |

### 9.4.6 使用比视图更大的 Canvas

当你使用 `canvas` 命令创建 canvas 时，可以提供 `-width xsize` 和 `-height ysize` 参数来定义显示的 canvas 尺寸。

如果你没有使用 `-scrollregion` 参数，那么 canvas 的尺寸将是 xsize 乘以 ysize。

`-scrollregion` 命令允许你声明实际 canvas 大于其可见部分。

例如，

```tcl
canvas .c -width 200 -height 150 -scrollregion {0 0 4500 2000}
```

创建一个高 150 像素、宽 200 像素的窗口，但实际上是一个 4500×2000 像素的 canvas。

如果你为此 canvas 附加滚动条，你可以在较大的空间内滚动这个 200x150 像素的窗口。

`-xscrollincrement` 和 `-yscrollincrement` 参数允许你设置每次滚动量。例如，如果你在 canvas 中显示大量文本，你会希望将 `-scrollincrement` 设置为行高。这将导致 canvas 显示完整的文本行，而不是在滚动文本时在 canvas 的顶部底部显示部分行。

下一个示例显示了一个棋盘格图案，每个方格都有标记以显示其在网格中的位置。因为 `-xscrollincrement` 设置为方格的大小，所以显示了每个方格的全宽。因为 `-yscrollincrement` 是方格高度的一半，所以可以显示半个方格的高度。

注意 `-scrollregion` 既可以包含负坐标也可以包含正坐标，但除非你设置的区域包含了你绘制的区域，否则你无法滚动到那里。

例如，如果你有一个复杂的图像要创建，在绘制之前不知道尺寸，你可以将图像绘制到 canvas 上，然后使用命令确定图像的边界框：

```tcl
set coords[canvasName bbox all]
```
.
