
window并使用命令 `python tk_listbox.py` 运行此程序

选择一个选项并点击按钮以确认您的选择

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_249_0.png)

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_249_1.png)

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_249_2.png)

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_249_3.png)

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_250_0.png)

如果 `selectmode` 被设置为 `MULTIPLE`，`curselection()` 方法将返回一个包含被选中索引的元组。

## 轮询单选按钮

`Radiobutton` 组件为应用程序提供了一个用户可以选择的单项。当多个单选按钮组合在一起时，用户只能选择组中的任意一项。在 tkinter 中，当单选按钮对象指定同一个控制变量对象以在选择时赋值时，它们会被分组。为了此目的，可以使用 `StringVar()` 构造函数创建一个空字符串变量对象，或使用 `IntVar()` 构造函数创建一个空整数变量对象。

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_251_0.png)

你不能使用普通变量来存储从单选按钮选择赋值的值——它必须是一个对象。

通过为 `Radiobutton()` 构造函数指定四个参数创建一个单选按钮对象：

- 父容器的名称，例如 frame 名称。
- 显示标签的文本，指定为 `text=text` 键对。
- 控制变量对象，指定为 `variable=variable` 键对。
- 要赋值的值，指定为 `value=value` 键对。

每个单选按钮对象都有 `select()` 方法，可以在程序启动时用于指定单选按钮组中的默认选择。通过选择单选按钮赋值的字符串值可以通过 `get()` 方法从字符串变量中检索。

- 通过让 GUI 功能和 messagebox 功能作为短别名可用，启动一个一个新的 Python 程序

```python
from tkinter import *
import tkinter.message as box
```

### tk_radio.py

- 现在，创建一个 frame 来包含这些组件

```python
frame = Frame(window)
```

- 然后，构造一个字符串变量对象来存储选择

```python
book = StringVar()
```

- 接下来，创建三个单选按钮组件，它们的值在选择时将被赋值给字符串变量对象

```python
radio_1 = Radiobutton(frame, text='HTML5', \
variable = book, value='HTML5 in easy steps')
radio_2 = Radiobutton(frame, text='CSS3', \
variable = book, value='CSS3 in easy steps')
radio_3 = Radiobutton(frame, text='JS', \
variable = book, value='JavaScript in easy steps')
```

- 现在，添加一条语句来指定程序启动时默认选择哪个单选按钮

```python
radio_1.select()
```

- 然后，添加一个函数来显示单选按钮以及一个调用该函数的按钮

```python
def showinfo('Selection', \
'Your Choice: ' + book.get())
btn = Button(frame, text='Choose', command=dialog)
```

- 将推按钮和单选按钮添加到 frame

```python
btn.pack(side=RIGHT, padx=5)
radio_1.pack(side=LEFT)
radio_2.pack(side=LEFT)
radio_3.pack(side=LEFT)
frame.pack(padx=30, pady=30)
```

- 最后，添加循环来捕获此窗口的事件

```python
window.mainloop()
```

将文件保存在你的脚本目录下，然后打开命令提示符窗口并使用命令 `python tk_radio.py` 运行此程序——选择一个选项并点击按钮以确认您的选择

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_253_0.png)

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_253_1.png)

`Radiobutton` 对象有一个 `deselect()` 方法，可以用于通过程序取消选择。

## 勾选框

`Checkbutton` 组件为应用程序提供了一个用户可以选择的单项。当多个复选框一起出现时，用户可以选择一个或多个项目。复选框对象指定单独的控制变量。可以使用 `StringVar()` 构造函数创建一个空字符串变量对象，或使用 `IntVar()` 构造函数创建一个空整数变量对象来实现此目的。通过为 `Checkbutton()` 构造函数指定五个参数：

- 父容器的名称，例如 frame 名称。
- 显示标签的文本，指定为 `text=text` 键对。
- 控制变量对象，指定为 `variable=variable` 键对。
- 要赋值的值，指定为 `value=value` 键对。
- 要赋值的值，指定为 `value=value` 键对。

通过选择单选按钮赋值的字符串可以通过 `get()` 方法从字符串变量中检索。

- 通过让 GUI 功能和 messagebox 功能作为短别名可用，启动一个一个新的 Python 程序

```python
from tkinter import *
import tkinter.message as box
```

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_254_0.png)

- 现在，创建一个 window 对象并指定标题

```python
window = Tk()
window.title('Checkboxes')
```

创建一个 frame 来包含这些组件

- 构造一个字符串变量对象来存储选择

```python
frame = Frame(window)
```

创建三个单选按钮组件，它们的值在选择时将被赋值给字符串变量对象

```python
radio_1 = Checkbutton(frame, text='HTML5', \
variable = book, value='HTML5 in easy steps')
radio_2 = Checkbutton(frame, text='CSS3', \
variable = book, value='CSS3 in easy steps')
radio_3 = Checkbutton(frame, text='JS', \
variable = book, value='JavaScript in easy steps')
```

- 现在，添加一条语句来指定程序启动时默认选择哪个单选按钮

```python
radio_1.select()
```

- 添加一个函数来显示单选按钮以及一个调用该函数的按钮

```python
def showinfo('Selection', \
'Your Choice: ' + book.get())
btn = Button(frame, text='Choose', command=dialog)
```

- 将推按钮和单选按钮添加到 frame

```python
btn.pack(side=RIGHT, padx=5)
radio_1.pack(side=LEFT)
radio_2.pack(side=LEFT)
radio_3.pack(side=LEFT)
frame.pack(padx=30, pady=30)
```

- 最后，添加循环来捕获此窗口的事件

```python
window.mainloop()
```

将文件保存在你的脚本目录下，然后打开命令提示符窗口并使用命令 `python tk_check.py` 运行此程序——勾选一些框并点击按钮以确认您的选择

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_256_0.png)

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_256_1.png)

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_256_2.png)

`Checkbutton` 对象有 `select()` 和 `deselect()` 方法，可以用于通过程序开启或关闭状态。任何 `Checkbutton` 对象的状态都可以通过 `toggle()` 方法反转。

## 添加图像

使用 tkinter 模块，GIF 或 PGM/PPM 格式的图像可以使用 `ImageTk()` 构造函数显示在 Label、Button、Text 和 Canvas 组件上。这只需要一个文件参数来指定图像。有趣的是，它还有一个 `subsample()` 方法，可以通过指定 `x=` 和 `y=` 参数采样值来缩小图像。例如，`x=2, y=2` 每隔一个像素采样一次——因此图像对象是原始大小一半。

一旦创建了图像对象，可以通过 `image=` 将其添加到 Label 或 Button 构造语句中。

`Text` 对象有一个 `image_create()` 方法，用于将图像嵌入文本字段。这需要两个参数来指定位置和图像。例如，‘1.0’指定第一行第一个字符。

`Canvas` 对象有一个 `create_image()` 方法，它需要两个参数来指定位置和图像。在这里，位置设置了画布上绘制图像的 x,y 坐标。

- 通过让 GUI 方法和属性可用，创建一个新的 window 对象并指定标题

```python
from tkinter import *
window = Tk()
window.title('Image Example')
```

现在，从本地图像文件创建一个图像对象

```python
img = PhotoImage(file = 'python.gif')
```

然后，创建一个标签对象，在彩色背景上显示该图像

```python
label = Label(window, image = img, bg = 'yellow')
```

从第一个图像对象创建一个半大小的图像对象

```python
small_img = PhotoImage.subsample(img, x = 2, y = 2)
```

现在，创建一个按钮来显示这个小图像

```python
btn = Button(window, image = small_img )
```

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_258_0.png)

`PhotoImage` 类还有一个 `zoom()` 方法，该方法可以使用相同的 `x=2,y=2` 值将图像放大一倍。

创建一个文本字段并嵌入小图像，然后在后面插入一些文本

```python
txt = Text(window, width = 25, height = 7)
txt.image_create('1.0', image = small_img)
txt.insert('1.1', 'Python Fun!')
```

创建画布并在彩色背景上绘制小图像，然后在其上方绘制一条对角线

```python
can = Canvas(window, width = 100, height = 100, bg = 'cyan')
can.create_image( 50, 50, image = small_img)
can.create_line( 0, 0, 100, 100, width = 25, fill = 'yellow' )
```

然后，将组件添加到窗口

```python
label.pack(side = TOP )
btn.pack(side = LEFT, padx = 10 )
txt.pack(side = LEFT)
can.pack(side = LEFT, padx = 10 )
```

最后，添加循环来捕捉此窗口的事件

```python
window.mainloop()
```

将文件保存到你的脚本目录中，然后在那里打开命令提示窗口并运行命令 `python tk_image.py` – 以查看图像。

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_259_0.png)

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_259_1.png)

注意，Text 的方法是 `image_create()` 而 Canvas 的方法是 `create_image()` – 相似又不同。

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_259_2.png)

`Text` 和 `Canvas` 组件都非常强大且灵活 – 在 `docs.python.org/3.7/library/tkinter.html` 发现更多信息。

## 总结

- `tkinter` 模块可以导入到 Python 程序中，为窗口应用程序提供属性和方法。
- 每个 tkinter 程序都必须通过调用 `Tk()` 来创建一个窗口，并调用其 `mainloop()` 方法来捕捉事件。
- 窗口对象的标题通过其 `title()` 方法指定。
- 通过向 `Label()` 构造函数指定其父容器名称和文本作为参数来创建标签组件。
- 可以使用 `pack()`、`grid()` 或 `place()` 几何管理器将组件添加到应用程序中。
- 通过向 `Button()` 构造函数指定其父容器名称、文本以及用户按下时调用的函数名称作为参数来创建按钮。
- `tkinter.messagebox` 模块可以导入到 Python 程序中，为消息框提供属性和方法。
- 要求用户做出选择的消息框会向程序返回一个值，用于条件分支。
- `Frame()` 构造函数创建一个容器，在其中多个组件可以组合在一起以便更好的定位。
- `Entry()` 构造函数创建一个单行文本字段，可以通过其 `get()` 方法检索当前内容。
- 通过 `insert()` 方法将项添加到 `Listbox` 对象中，并通过指定索引到 `get()` 方法进行检索。
- `Radiobutton` 对象通过其 `variable` 属性在 `StringVar` 或 `IntVar` 中存储值。
- `PhotoImage()` 构造函数创建一个图像对象，该对象有一个 `subsample()` 方法，可以缩小图像。
- 图像可以添加到 Button 和 Label 对象中，嵌入到 Text 对象中，并在 Canvas 对象上绘制。

# 10 开发应用程序

本章整合了之前章节的元素，以构建一个完整的应用程序。

- 生成随机数
- 规划程序
- 设计界面
- 分配静态属性
- 初始化动态属性
- 测试程序
- 总结

## 生成随机数

在本书的后续页面开发的图形应用程序将在特定范围内生成六个随机数。最初，它的功能可以开发为控制台应用程序，稍后说明它可以如何应用于图形组件。Python 标准库中有一个 `random` 模块，它提供了生成伪随机数的方法。系统默认在每次初始化时使用当前系统时间作为随机生成器的“种子” – 因此它不会重复选择。通过调用 `random` 模块中的 `random()` 方法可以生成一个 0.0 到 1.0 之间的伪随机浮点数。可以使用 *乘法运算符* 修改生成数字的范围以指定最大值，并使用内置 `int()` 函数将其舍整为整数。例如，生成一个零到九范围内的整数：

```python
random.random() * 10
```

或者生成一个一到 10 范围内的整数：

```python
int(random.random() * 10) + 1
```

此语句可以在循环中使用，在给定范围内生成多个随机整数，但输出中任何数字都可能重复 – 它没有唯一性。相反，可以通过 `random` 模块中的 `sample()` 方法生成给定范围内的唯一随机整数。这需要两个参数来指定范围和返回的唯一整数数量。使用内置的 `range()` 函数来指定最大值非常方便。例如，生成零到九范围内的六个唯一数字：

```python
random.sample(range(10), 6)
```

或者生成一到十范围内的六个唯一数字：

```python
random.sample(range(1, 11), 6)
```

这种技术可以代表彩票投注，例如选择从 1 到 59 之间的六个唯一数字。

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_264_0.png)

通过内置 `int()` 函数从 `float` 数据类型转换为 `int` 数据类型的浮点数会在小数点处被截断。

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_264_1.png)

`range` 函数可以指定起始和结束值。如果没有提供起始值，则默认为零。

- 启动纯文本编辑器，通过导入“random”模块开始一个 Python 程序

```python
from random import random, sample
```

![](img/4d3471d9d7885aa6ac413c9170a3fa2e_264_2.png)

`sample.py`

- 下一步，将随机浮点数赋值给变量，然后显示其值

```python
num = random()
print('Random Float 0.0-1.0 : ', num)
```

- 现在，将浮点数乘以并转换为整数

```python
num = int(num * 10)
print('Random Integer 0 - 9 : ', num)
```

- 添加循环将多个随机整数添加到列表
