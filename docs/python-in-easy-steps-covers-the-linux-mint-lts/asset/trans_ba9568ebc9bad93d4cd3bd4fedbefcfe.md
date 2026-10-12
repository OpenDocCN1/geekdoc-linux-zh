

现在，从一个本地图像文件创建图像对象
`img = PhotoImage( file = 'python.gif' )`

然后，创建一个标签对象以在彩色背景上显示上述图像
`label = Label( window , image = img , bg = 'yellow' )`

从第一个图像对象创建一个半尺寸图像对象
`small_img = PhotoImage.subsample( img, x = 2, y = 2 )`

现在，创建一个按钮以显示小图像
`btn = Button( window , image = small_img )`

![](img/d06b1f1cf83677f6647237f0c7827141_258_0.png)

PhotoImage 类还有一个 zoom() 方法，在 x=2 和 y=2 的值相同的情况下，它会将图像尺寸加倍。

创建一个文本框并嵌入小图像，然后在其后插入一些文本
`txt = Text( window , width = 25, height = 7 )`
`txt.image_create( '1.0' , image = small_img )`
`txt.insert( '1.1', 'Python Fun!' )`

创建一个画布，在彩色背景上绘制小图像，然后在其上方绘制一条对角线
`can = Canvas( window , width = 100 , height = 100 , bg = 'cyan' )`
`can.create_image( ( 50 , 50 ), image = small_img )`
`can.create_line( 0 , 0 , 100 , 100, width = 25 , fill = 'yellow' )`

然后，将小部件添加到窗口
`label.pack( side = TOP )`
`btn.pack( side = LEFT , padx = 10 )`
`txt.pack( side = LEFT )`
`can.pack( side = LEFT , padx = 10 )`

最后，添加循环以捕获此窗口的事件
`window.mainloop()`

将文件保存在你的脚本目录中，然后在那里打开一个命令提示符窗口，并使用命令 `python tk_image.py` 运行此程序 – 以查看图像

![](img/d06b1f1cf83677f6647237f0c7827141_259_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_259_1.png)

请注意，Text 方法为 `image_create()`，但 Canvas 方法为 `create_image()` – 相似但不同。

![](img/d06b1f1cf83677f6647237f0c7827141_259_2.png)

Text 和 Canvas 小部件都很强大且灵活 – 请在 docs.python.org/3.7/library/tkinter.html 上发现更多内容

## 摘要

- **tkinter** 模块可以导入 Python 程序中，为窗口化应用程序提供属性和方法。
- 每个 **tkinter** 程序都必须通过调用 `Tk()` 来创建窗口并调用其 `mainloop()` 方法来捕获事件。
- 窗口对象的标题由其 `title()` 方法指定。
- **Label** 小部件通过将其父容器的名称及其文本作为 **Label()** 构造函数的参数来创建。
- 可以使用 `pack()`、`grid()` 或 `place()` 布局管理器将小部件添加到应用程序中。
- 按钮小部件通过将其父容器的名称、其文本以及当用户按下时调用的函数名称作为 **Button()** 构造函数的参数来创建。
- **tkinter.messagebox** 模块可以导入 Python 程序中，为消息框提供属性和方法。
- 要求用户做出选择的消息框会向程序返回一个值，用于条件分支。
- **Frame()** 构造函数创建一个容器，其中可以组合多个小部件以获得更好的定位。
- **Entry()** 构造函数创建一个单行文本框，其当前内容可以通过其 `get()` 方法检索。
- 项通过 **Listbox** 对象的 `insert()` 方法添加，并通过指定其索引号给其 `get()` 方法检索。
- **Radiobutton** 和 **Checkbutton** 对象在由其 `variable` 属性指定的 **StringVar** 或 **IntVar** 对象中存储值。
- **PhotoImage()** 构造函数创建具有 `subsample()` 方法的图像对象，该方法可以缩小图像。
- 图像可以添加到 Button 和 Label 对象中，嵌入在 Text 对象中，并在 Canvas 对象上绘制。

## 10

### 开发应用程序

*本章将前面章节中的元素整合起来，以构建一个完整的 Python 应用程序。*

- 生成随机数
- 规划程序
- 设计界面
- 分配静态属性
- 初始化动态属性
- 添加运行时功能
- 测试程序
- 安装冻结工具
- 冻结程序
- 摘要

## 生成随机数

本书后续页面中开发的图形应用程序将在特定范围内生成六个随机数。最初，其功能可以作为控制台应用程序开发，然后再进行转换，以说明如何将其应用于图形小部件组件。

标准 Python 库有一个 random 模块，提供生成伪随机数的方法。默认情况下，每当随机生成器初始化时，使用当前系统时间来“播种”随机生成器 – 因此它不会重复其选择。

可以通过调用 random 模块的 random() 方法来生成 0.0 到 1.0 之间的伪随机浮点数。使用 * 乘法运算符指定最大值可以修改生成数的范围，并使用内置的 int() 函数将其向下取整为整数值。例如，要在零到九的范围内生成一个整数：

```python
int(random.random() * 10)
```

或者要在 1 到 10 的范围内生成一个整数：

```python
int(random.random() * 10) + 1
```

此语句可以在循环中使用，以在给定范围内生成多个随机整数，但输出中可能会重复任何数字 – 没有保证唯一性。相反，可以通过 random 模块的 sample() 方法在给定范围内生成多个唯一的随机整数。这需要两个参数来指定范围和要返回的唯一整数数量。使用内置的 range() 函数指定最大值很方便。例如，要在零到九的范围内生成六个唯一数字：

```python
random.sample(range(10), 6)
```

或者要在 1 到 10 的范围内生成六个唯一数字：

```python
random.sample(range(1, 11), 6)
```

此技术可以通过选择例如在 1 到 59 之间的六个唯一数字来表示随机彩票号码。

![](img/d06b1f1cf83677f6647237f0c7827141_264_0.png)

由内置 **int()** 函数从 **float** 数据类型转换为 **int** 数据类型的浮点数在小数点处被截断。

![](img/d06b1f1cf83677f6647237f0c7827141_264_1.png)

**range()** 函数可以指定开始和结束值。如果没有提供起始值，则默认为零。

1. 启动一个纯文本编辑器，然后通过从 “random” 模块导入两个函数开始 Python 程序
   `from random import random , sample`

   ![](img/d06b1f1cf83677f6647237f0c7827141_264_2.png)

   sample.py

2. 接下来，将一个随机浮点数赋值给一个变量，然后显示其值
   `num = random()`
   `print('Random Float 0.0-1.0 :', num)`

3. 现在，将浮点数相乘并将其转换为整数，然后显示其值
   `num = int( num * 10 )`
   `print('Random Integer 0 - 9 :', num)`

4. 添加一个循环，将多个随机整数分配给列表，然后显示列表项
   `nums = [] ; i = 0`

   ```python
   while i < 6:
       nums.append(int(random() * 10) + 1)
       i += 1
   print('Random Multiple Integers 1-10:', nums)
   ```

5. 最后，将多个唯一的随机整数分配给列表，然后显示列表项

   ```python
   nums = sample(range(1, 59), 6)
   print('Random Integer Sample 1 - 59:', nums)
   ```

6. 保存文件，然后多次执行程序 – 以查看生成的随机数

   ![](img/d06b1f1cf83677f6647237f0c7827141_265_0.png)

   ![](img/d06b1f1cf83677f6647237f0c7827141_265_1.png)

**random.sample()** 函数返回一个列表，但实际上不会替换指定范围内的任何元素。

## 规划程序

在创建新的图形应用程序时，首先花一些时间规划其设计是有用的。明确定义程序的精确目的，决定需要哪些应用程序功能，然后决定需要哪些界面小部件。

一个简单的应用程序计划，用于为彩票号码选择数字，可能看起来像这样：

![](img/d06b1f1cf83677f6647237f0c7827141_266_0.png)

### 程序目的

- 该程序将生成 1-59 范围内的一系列六个唯一的随机数，并具有重置功能。

### 所需功能

- 一个生成并显示六个唯一随机数的函数。
- 一个清除显示的最近六个随机数的函数。

### 所需的界面小部件

- 一个不可调整大小的窗口，包含所有其他小部件并显示应用程序标题。
- 一个 Label 小部件，显示静态的应用程序徽标图像 – 仅用于增强界面外观。
- 六个 Label 小部件，动态显示生成的唯一随机数序列 – 每个 Label 显示一个数字。
- 一个 Button 小部件，当此 Button 被点击时生成并在 Label 小部件中显示数字。当...

