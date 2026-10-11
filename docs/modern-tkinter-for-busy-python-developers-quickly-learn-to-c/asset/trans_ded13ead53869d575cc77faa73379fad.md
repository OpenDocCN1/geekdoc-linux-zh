

实际上我们已经见过一种方法，即使用控件自身的选项来添加其周围额外的空间。并非所有控件都支持此功能，但框架（frame）就是一个支持的例子；这非常有用，因为框架通常用作主容器来网格化其他控件。框架的 "padding" 选项允许你指定框架内部的额外内边距，无论是四边相同的量，还是每边不同的量。

第二种方法是在添加控件时，使用 "padx" 和 "pady" 网格选项。正如你所料，"padx" 会在控件的左右两侧添加一点额外空间，而 "pady" 则在上下两侧添加额外空间。如果该选项设为单个值，则左右（或上下）会使用相同的内边距；而如果是两个值的列表，则允许你在左右（或上下）设置不同的量。请注意，这种额外的内边距位于包含该控件的网格单元格内部。

如果你想为整行或整列添加内边距，"columnconfigure" 和 "rowconfigure" 方法接受一个 "pad" 选项，它可以帮你完成这项工作。

让我们在我们的示例中添加额外的粘性、调整大小和内边距行为（新增内容以粗体显示）。

```python
from tkinter import *
from tkinter import ttk

root = Tk()

content = ttk.Frame(root, padding=(3,3,12,12))
frame = tk.Frame(content, borderwidth=5, relief="sunken", width=200, height=100)
namelbl = tk.Label(content, text="Name")
name = tk.Entry(content)

onevar = BooleanVar()
twovar = BooleanVar()
threvar = BooleanVar()

onevar.set(True)
twovar.set(False)
threvar.set(True)

one = tk.Checkbutton(content, text="One", variable=onevar, onvalue=True)
two = tk.Checkbutton(content, text="Two", variable=twovar, onvalue=True)
three = tk.Checkbutton(content, text="Three", variable=threvar, onvalue=True)
ok = tk.Button(content, text="Okay")
cancel = tk.Button(content, text="Cancel")

content.grid(column=0, row=0, sticky=(N, S, E, W))
frame.grid(column=0, row=0, columnspan=3, rowspan=2, sticky=(N, S, E, W))
namelbl.grid(column=3, row=0, columnspan=2, sticky=(N, W), padx=5)
name.grid(column=3, row=1, columnspan=2, sticky=(N, E, W), pady=5, padx=5)
one.grid(column=0, row=3)
two.grid(column=1, row=3)
three.grid(column=2, row=3)
ok.grid(column=3, row=3)
cancel.grid(column=4, row=3)

root.columnconfigure(0, weight=1)
root.rowconfigure(0, weight=1)
content.columnconfigure(0, weight=3)
content.columnconfigure(1, weight=3)
content.columnconfigure(2, weight=3)
content.columnconfigure(3, weight=1)
content.columnconfigure(4, weight=1)
content.rowconfigure(1, weight=1)

root.mainloop()
```

这样看起来更有希望。你可以多玩玩这个示例，感受一下调整大小的行为。

![](img/94378c1b05607c1dc5649c738af95c74_33_0.png)

> *你会注意到窗口右下角有一个小的调整大小控件；虽然我们只是走了捷径，通过额外的内边距来避开它，但稍后我们会看到如何更好地使用 "sizergrip" 控件来考虑这一点。*

## 更多网格功能

正如你在网格参考中看到的那样，网格还有很多其他功能。以下是一些更实用的功能。

### 查询和修改网格选项

就像控件本身一样，内省各种网格选项以及修改它们都很简单；在最初网格化控件时设置选项只是一种便利，你完全可以随时更改它们。

"slaves" 方法会告诉你所有在主容器内部网格化的控件，或者（可选地）仅位于特定列或行内的控件。"info" 方法会给你一个控件的所有网格选项及其值的列表。最后，"configure" 方法允许你更改控件上的一个或多个网格选项。

这些在一个交互式会话中演示：

```python
>>> **content.grid_slaves()**
<map object at 0x00C3F470>
>>> for w in **content.grid_slaves()**: print(w)
...
.14597008.14622128
.14597008.14622096
.14597008.14622064
.14597008.14622032
.14597008.14622000
.14597008.14621872
.14597008.14621840
.14597008.14621808
>>> for w in **content.grid_slaves(row=3)**: print(w)
...
.14597008.14622128
.14597008.14622096
.14597008.14622064
.14597008.14622032
.14597008.14622000
>>> for w in **content.grid_slaves(column=0)**: print(w)
...
.14597008.14622000
.14597008.14621808
>>> namelbl.grid_info()
{'rowspan': '1', 'column': '3', 'sticky': 'nw', 'ipady': '0', 'ipadx': '0', 'columnspan': '2', 'in': '<tkinter.ttk.Frame object at 0x00DEBB90>', 'padx': '0', 'padx': '5', 'row': '0'}
>>> namelbl.grid_configure(sticky=(E,W))
>>> namelbl.grid_info()
{'rowspan': '1', 'column': '3', 'sticky': 'ew', 'ipady': '0', 'ipadx': '0', 'columnspan': '2', 'in': '<tkinter.ttk.Frame object at 0x00DEBB90>', 'padx': '0', 'padx': '5', 'row': '0'}
```

### 内部填充

你看到了 "padx" 和 "pady" 网格选项如何在控件外部添加额外空间。还有一种较少使用的填充类型称为 "内部填充"，由网格选项 "ipadx" 和 "ipady" 控制。

区别可能很细微。假设你有一个 20x20 的框架，并为每一侧指定 5 像素的常规（外部）填充。该框架会请求 20x20 的矩形（其自然大小）给布局管理器。通常，这就是它获得的，所以它会获得一个 20x20 的框架矩形，周围环绕着 5 像素的边框。

使用内部填充时，布局管理器在确定控件的自然大小时，实际上会将额外的填充加到控件上，就好像控件请求了 30x30 的矩形一样。如果框架居中，或附着在单侧或角落（使用 "sticky"），你将得到一个 20x20 的框架，周围有额外空间。然而，如果框架设置为拉伸（即 "sticky" 值为 "we"、"ns" 或 "nwes"），它将填满额外空间，结果是 30x30 的框架，没有边框。

### Forget 和 Remove

网格的 "forget" 方法，接受一个包含一个或多个从属控件的列表作为参数，可用于将从属控件从它们当前所在的网格中移除。这并不会彻底销毁控件，只是将其从屏幕上移除，就好像它一开始就没有被网格化一样。你可以稍后再次网格化它，尽管你最初分配的网格选项将会丢失。

网格的 "remove" 方法工作方式相同，但网格选项会被记住。

### 嵌套布局

随着你的用户界面变得复杂起来，你用来组织所有控件的网格也会变得越来越复杂，粒度也越来越细。这使得修改和维护你的程序变得非常困难。

幸运的是，你不必用单个网格来管理整个用户界面。如果你的用户界面中有一个区域相对独立于其他区域，创建一个新框架来容纳该区域，并在该框架内部网格化属于该区域的控件。如果你有一个某种图形程序，具有多个调色板、工具栏等，其中每个区域都可能是放入其自身框架的候选者。

从理论上讲，这些具有各自网格的框架可以任意深度嵌套，但在实践中，通常不会超过几层。这对于模块化你的程序可能会有很大帮助。例如，如果你有一个绘图工具调色板，你可以在一个单独的例程中创建整个东西，包括创建所有组件控件、将它们一起网格化、设置事件绑定等。从你的主程序的角度来看，它只需要看到包含所有这些的单个框架控件。

我们的示例仅展示了这一点的一小部分，其中内容框架被网格化到主窗口中，然后其他所有控件被网格化到内容框架中。

# 更多控件

本章继续介绍几个更多的控件：listbox、scrollbar、text、progressbar、scale 和 spinbox。其中一些开始比之前我们看到的基本控件更强大一些。在这里，我们还将看到使用经典 Tk 控件的几个实例，在那些没有（或不需要）主题化对应物的情况下。

