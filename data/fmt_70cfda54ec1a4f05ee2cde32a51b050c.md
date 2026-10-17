
Combobox 组件将输入框（`entry`）与一组选项列表相结合。这使得用户既可以从您提供的一组值中进行选择（例如，典型设置），也可以输入自己的值（例如用于不常见的情况）。

![](img/44299b92074ede1d1ea1f48186743151_113_0.png)

下拉框组件。

```
countryvar = StringVar()
country = ttk.Combobox(
textvariable=countryvar)
```

与 `entry` 类似，`textvariable` 选项将您程序中的变量与下拉框的当前值关联起来。与其他组件一样，您应该在自己的代码中初始化关联的变量。

下拉框会生成一个 `<<>>` 虚拟事件，您可以在其值变化时对其进行绑定。（您也可以像我们在前面几个章节中看到的那样，跟踪 `trace` 的变化。绑定到事件更加直接，因此通常是我们的首选方案。）

```
country.bind('<<>>');
```

### 预定义值

您可以使用 `values` 配置选项为用户提供一组可以选择的值列表：

```
country['values'] = ('USA', 'Canada', 'Australia')
```

如果设置了 `readonly` 状态标志，将限制用户只能从预定义值列表中进行选择，而不能输入自己的值（尽管如果下拉框的当前值不在列表中，它也不会被更改）。

```
country.state(["readonly"]);
```

如果您在只读模式下使用下拉框，我建议在值变化时（即触发 `<<>>` 事件时），调用 `selection_clear` 方法。如果不这样做，视觉上看起来会有点奇怪。

您还可以使用 `get` 方法获取当前值，并使用 `set` 方法更改当前值（该方法接受一个参数，即新值）。

为了补充 `get` 和 `set` 方法，您还可以使用 `current` 方法来确定预定义值列表中选择了哪一项。不带参数调用 `current`；它将返回列表的从0开始的索引，如果当前值不在列表中则返回 -1。您可以通过带一个从0开始的索引参数调用 `current` 来选择列表中的某项。

想为列表中的每项关联某些其他值，以便您的程序在内部使用一个值，但在下拉框中显示为其他内容？当我们在几个章节后讨论 `listbox` 时，将需要查看标题为“保留额外项目数据”的章节。

## 7. 网格几何管理器 (The Grid Geometry Manager)

我们将暂时停止讨论不同的组件（在屏幕上放置什么），转而关注几何管理（将这些组件放置在什么位置）。我们在“`Tk` 概念”章节中引入了几何管理的通用概念。在这里，我们关注一个特定的几何管理器：

正如我们所看到的，`grid` 允许您以列和行来布局组件。如果您熟悉使用 HTML 表格进行布局，在这里您会感到自如。本章将说明调整 `grid` 的各种方式，以让您获得对用户界面所需的所有控制。

`grid` 是 `Tk` 中提供的几种几何管理器之一，它的强大、灵活性和易用性的结合使其成为通用的最佳选择。它的约束模型与当今依赖组件对齐的布局天然契合。`Tk` 中还有其他几何管理器：`pack` 也非常强大但更难使用和理解，而 `place` 则让您对每个元素的定位具有完全控制权。即使是面板窗口（paneled windows）、笔记本（notebooks）、画布（canvas）和文本（text）等我们将探索的组件也充当几何管理器。

值得注意的是，`grid` 在 1996 年引入 `Tk`，这在 `Tk` 流行几年后才被人们接受。在此之前，开发者一直使用 `pack` 进行基于约束的管理。当 `grid` 出现时，许多开发者继续使用，您仍然会在很多 `Tk` 程序和文档中发现它。`grid` 算法本身没有问题，但修改现有布局可能会困难。在用户界面的不同部分对齐组件更加复杂。`grid` 具有 `pack` 的所有功能，产生更好的布局（水平和垂直方向对齐组件），并且更容易学习和使用。正因如此，大多数时候，`grid` 是正确的选择。使用 `grid` 编写新程序，并在修改现有用户界面时切换到 `grid`。`grid` 的参考文档提供了关于 `grid`、其行为以及所有选项的详尽描述。

```
https://tkdocs.com/man/grid
```

### 7.1. 列与行

在 `grid` 中，组件被分配一个列号和一个行号。这些编号指示组件相对于其他组件的位置。同一列的组件位于上下。同一行的组件位于左或或右。

列号和行号必须是正整数（例如 0, 1, 2, ...）。您不必从 0 开始，可以在列和行号上留空隙（例如 1, 2, 10, 11, 12, 20）。如果您计划以后在用户界面中间添加更多组件，这非常有用。每列的宽度取决于其中包含的所有组件。每行也是如此。这意味着当您规划用户界面并将其划分为行列时，不需要担心每列宽度相等。

### 7.2. 跨单元格

组件在 `grid` 中可以占据多个单元格；为了实现这一点，我们在网格组件时使用 `colspan` 和 `rowspan` 选项。这些类似于 HTML 表格的 "colspan" 和 "rowspan" 属性。

这是一个带有多个组件的用户界面示例，其中某些组件占据了超过一个单元格。

![](img/44299b92074ede1d1ea1f48186743151_119_0.png)

布局多个组件。

```
from tkinter import *

from tkinter import ttk
```

```
root = Tk()
```

```
content = ttk.Frame(root)

frame = ttk.Frame(content, borderWidth=5, relief="ridge", width=200, height=100)

amelbl = ttk.Label(content, text="Name")

name = ttk.Entry(content)
```

```
onevar = BooleanVar(value=True)

twovar = BooleanVar(value=False)
```

```
threevar = BooleanVar(value=True)
```

```
one = ttk.Checkbutton(content, text="One", variable=onevar,

onvalue=True)

two = ttk.Checkbutton(content, text="Two", variable=twovar,

onvalue=True)

three = ttk.Checkbutton(content, text="Three", variable=threevar,

onvalue=True)

ok = ttk.Button(content, text="Ok")

cancel = ttk.Button(content, text="Cancel")
```

```
content.grid(column=0, row=0)

frame.grid(column=0, row=0, columnspan=3, rowspan=2)

namelbl.grid(column=3, row=0, columnspan=2)

name.grid(column=3, row=1, columnspan=2)

one.grid(column=0, row=3)

two.grid(column=1, row=3)

three.grid(column=2, row=3)

ok.grid(column=3, row=3)

cancel.grid(column=4, row=3)
```

```
root.mainloop()
```

`https://tkdocs.com/code/gridexample1.py`

### 7.3. 单元格内的布局

列的宽度（行的高度）取决于其中的所有组件。这意味着某些组件可能比它们所处的单元格小。如果是这样，它们应该放在单元格的的确切位置？

默认情况下，如果单元格大于其中包含的组件，组件将在单元格内水平和垂直方向上居中。容器的背景颜色将显示在组件周围的空白区域中。在下面的图中，右上角的组件比分配给它的单元格小。容器的（白色）背景填充了单元格的其余部分。

![](img/44299b92074ede1d1ea1f48186743151_121_0.png)

单元格内的布局和 'sticky' 选项。

`sticky` 选项可以改变这种默认行为。它的值是由一个或多个指南方向组成的字符串，指定单元格组件的哪些边缘应该“粘”在上面。例如，`n`（北）的值会将组件推向顶部，底部留出任何额外的垂直空间；组件仍将水平居中。`nw`（西北）的值意味着组件将粘附在左上角，在底部和右侧留出额外空间。

在 `Tkinter` 中，你也可以将其指定为包含 `west` 和 `east` 的列表。
这是一种风格上的选择，我们在书中会倾向于使用列表格式。

指定两个相对的边缘，例如我们使用的 `(west, east)`，意味着组件将被拉伸。在这种情况下，它将紧贴在单元格的左边缘和右边缘。因此，组件的宽度将大于它的“理想”尺寸。

如果你想让组件扩展以填充整个单元格，请在使用 `grid` 时将 `sticky` 值设置为 `nsew`（北、南、东、西），这意味着它将紧贴在每一侧。这在上方图中左下角的组件中所示。

大多数组件都有可以在其大于需要所需的尺寸时控制其显示方式的选项。例如，`label` 组件有一个 `anchor` 选项，用于控制标签文本在组件边界内的位置。上图中左下角的标签使用了默认的 `anchor`，即：左侧、垂直居中。

如果你在尝试让各个元素按照你意图的方式对齐时遇到困难，请先确保你知道组件有多大。正如上一章讨论 `label` 组件时所说，更改组件的背景或边框会有所帮助。

### 7.4. 处理调整大小

如果你尝试过调整示例的大小，你会发现没有任何东西完全没有移动，如下所示。

| | Name | | | |
|---|---|---|---|
| | | | |
| [x] One [ ] Two [x] Three | Okay | Cancel |

*调整窗口大小*

即使你看了下文并为我们的示例添加了额外的 `sticky` 选项，你仍然会看到同样的结果。看起来 `sticky` 只是告诉 `Tk` 如果单元格的行或列调整大小时该如何反应，但它并没有真正告诉 `Tk` 当有任何额外空间可用时，行或列是否应该调整大小。让我们来修复这个问题。

网格中的每一列和每一行都有一个与其关联的 `weight` 选项。此网格决定了当主窗口中有额外空间可填充时，列或行应该增长多少。默认情况下，每列或每行的 `weight` 为 0，这意味着它不会扩展以填充任何额外空间。

为了让用户界面能够调整大小，我们需要为想要扩展的列和行指定一个正 `weight`。你必须为至少一列和一行提供 `weight`。这是通过 `grid` 的 `columnconfigure` 和 `rowconfigure` 方法实现的。这个 `weight` 是相对的。如果两个列具有相同的 `weight`，它们将相同的速率扩展。在我们的示例中，我们将最左侧的三列（包含复选框）的 `weight` 设置为 3，最右侧的两列的 `weight` 设置为 1。右列每增长一个像素，左列就会增长三个像素。因此，随着窗口变大，大部分额外空间将分配到左侧。

`columnconfigure` 和 `rowconfigure` 还接受 `minsize` 网格选项，它指定了你不希望列或行收缩小于某个最小尺寸。

### 7.5. 填充（Padding）

通常情况下，每列或每行都将直接相邻，以便组件彼此相邻。这有时是你所需要的（例如 `listbox` 和滚动条），但通常你希望在组件之间留有一些空间。在 `Tk` 中，这被称为 `padding`（填充），你有几种可以选择的方法来添加它。我们已经看到了一种方法，即使用组件自身的选项在其周围添加额外空间。并不是所有组件都有此选项，但 `frame` 有；这是很有用的，因为 `frame` 通常用作 `grid` 组件的主容器。`frame` 的 `padding` 选项允许你指定框架内部的填充，无论是四个面相同，还是每个面都不同。第二种方法是在添加组件时使用 `padx` 和 `pady` 选项。如你预期的，`padx` 在左右两侧添加一些额外空间，而 `pady` 在顶部和底部添加额外空间。单个值会在左右（或顶部和底部）设置相同的填充，而双值列表则允许你在左右（或顶部和底部）设置不同的值。请注意，这种填充是在包含组件的网格单元格内部的。如果你想在整行或整列周围添加填充，`columnconfigure` 和 `rowconfigure` 方法接受 `padding` 选项，它们将为你完成此操作。让我们为我们的示例添加 `sticky`、调整大小和填充行为（已加粗**）。

```
from tkinter import *

from tkinter import ttk

root = Tk()

content = ttk.Frame(root, padding=(3,3,12,12))

frame = ttk.Frame(content, borderwidth=5, relief="ridge", width=200, height=100)

amelbl = ttk.Label(content, text="Name")

name = ttk.Entry(content)

onevar = BooleanVar()

twovar = BooleanVar()

threevar = BooleanVar()

onevar.set(True)

twovar.set(False)

threevar.set(True)

one = ttk.Checkbutton(content, text="One", variable=onevar, value=True)

two = ttk.Checkbutton(content, text="Two", variable=twovar, value=True)

three = ttk.Checkbutton(content, text="Three", variable=threevar, value=True)

ok = ttk.Button(content, text="Okay")

cancel = ttk.Button(content, text="Cancel")
```

```
content.grid(column=0, row=0, sticky=(N, S, E, W))

frame.grid(column=0, row=0, colspan=3, rowspan=2, sticky=(N, S, E, W))

amelbl.grid(column=3, row=0, colspan=2, sticky=(N, S, E, W))

name.grid(column=3, row=1, colspan=2, sticky=(N, W), pady=5, padx=5)

one.grid(column=0, row=3)

two.grid(column=1, row=3)

three.grid(column=2, row=3)

ok.grid(column=3, row=3)

cancel.grid(column=4, row=3)

root.columnconfigure(0, weight=1) root.rowconfigure(0, weight=1)

content.columnconfigure(0, weight=3) content.columnconfigure(1, weight=3) content.columnconfigure(2, weight=3)

content.columnconfigure(3, weight=1) content.columnconfigure(4, weight=1) content.rowconfigure(1, weight=1)

root.mainloop()
```

这看起来更有前景。操作示例以获得调整大小的感觉。

Grid 示例，处理单元格布局和调整。

### 7.6. 其他网格功能

如果你查看 `grid` 的参考文档，你会看到使用 `grid` 可以做的许多其他事情。这里是其中一些有用的。

`https://tkdocs.com/man/grid`

#### 查询和更改网格选项

就像组件本身一样，检查各种网格选项或更改它们非常简单。在第一次 `grid` 组件时设置选项确实方便，但你可以根据需要随时更改。

`slaves` 方法会告诉你所有在主容器内网格化的组件，或者可选返回特定列或行内的组件。`info` 方法将返回组件的所有网格选项及其取值的列表。最后，`configure` 方法允许你更改组件的一个或多个网格选项。这些在下面的交互会话中所示：

```
>>> content.grid_slaves()

[object .frame.button2, object .frame.button,

object .frame.checkbox3, object .frame.checkbox2,

object .frame.checkbutton, object .frame.entry,

object .frame.label, object .frame]

>>> content.grid_slaves(row=3)

[object .frame.button2, object .frame.button,

object .frame.checkbox3, object .frame.checkbox2,

object .frame.checkbutton, object .frame.entry,

object .frame.label]

>>> content.grid_slaves(column=3)

[object .frame.label, object .frame.entry]

>>> content.grid_slaves(row=3, column=3)

[]
```
