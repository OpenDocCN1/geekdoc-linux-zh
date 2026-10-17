
```
if {$x == "SJ" || ($x == "LA")} {
    put "You Live in California";
}
```

在下面的示例中，测试可以进行嵌套：

给 `if` 语句添加 `else` 子句的方法如下：

```
if {$x == 0} {
    set x 10;
} else {
    set x 0;
}
```

你还可以添加任意数量的 `elseif` 语句：

```
if {$x == 0} {
    set x 10;
} elseif {$x == 10} {
    incr x -1;
} elseif {$x == 100} {
    set x 50;
} else {
    set x 0;
}
```

在许多情况下，添加额外的 `elseif` 语句会变得繁琐且难以理解。为了提供一种更紧凑的方式表达相同的逻辑，`tcl` 实现了 `switch` 命令。`switch` 的工作原理是将值（字符串或数字）与一个块关联。将之前的 `if` 语句写成 `switch` 语句将变为：

```
switch $x {
0 {set x 10};
10 {incr x -1};
100 {set x 50};
}
```

默认情况下，只有与匹配值对应的块会被执行，但如果该块被指定为单个减号 (`-`)，`switch` 语句就可以实现“穿透”（fallthrough）。`switch` 语句

```
switch $x {
0 -
10 -
100 {incr x -1}
}
```

等同于以下 `if` 语句：

```
if { ($x == 0) || ($x == 10) || ($x == 100)} {
incr x -1;
}
```

# 循环

`tcl` 提供了三个循环命令：

- `for`
- `foreach`
- `while`

`tcl` 还提供了两个循环控制命令：

- `break`
- `continue`

`while` 循环在测试条件为真时执行其主体。该结构可以被认为是

```
while {condition} {block}
```

下面是一个计数到十的简单 `while` 循环：

```
set x 0;
while ($x < 10) { # 注意：原文为$x，tcl中通常用{}，此处保留原文逻辑或修正为符合tcl习惯的
incr x;
puts $x;
}
```

`foreach` 循环遍历一组参数并在每次运行时执行其主体。`foreach` 循环具有以下结构：

```
foreach variable {items} {block}
```

`variable` 是变量名，`items` 中的每个项将依次赋值给该变量。这是一个示例：

```
foreach element {o c n p li}{
  switch $element {
    o
    n {puts gas};
    c
    p
    li {puts solid;};
  }
}
```

在这种情况下，指定了要检查的项列表，也可以使用变量：

```
set elements 'o c n p li'
foreach element $elements {
  switch $element {
    o
    n {puts gas};
    c
    p
    li {puts solid;};
  }
}
```

如果给出的是变量而不是项列表，则不应使用大括号，因为大括号会被视为用于引号。

`for` 循环允许在循环时提供最大的控制。它可以被分解为：

```
for {initialization} {condition} {increment} {body}
```

一个计数到 10 的简单 `for` 循环示例是：

```
for {set i 0} {$i <= 10} {incr i} { puts $i; }
```

你已经见过简单的初始化语句，但 `for` 循环的初始化和增加部分可以根据需要变得复杂。

现在来看循环控制命令 `break` 和 `continue`。`break` 命令跳出循环并执行循环块之后的下一行代码；`continue` 命令跳到循环的下一次迭代。

`continue` 命令对于读取需要允许注释行的初始化文件非常方便。如果在读取文件的循环中包含以下语句，则所有以井号 (`#`) 开头的行都将被跳过。

```
if { [regexp "#" [string trim line]] {continue; }
```

# 文件 I/O 和文件信息

`tcl` 提供了一种简单有效的文件输入输出方法，类似于 C 标准 I/O 库中的方法。文件 I/O 第一步是打开文件并获取文件句柄或文件 ID。例如，命令

```
set f [open /etc/passwd r]
```

以 `r` 模式打开 `/etc/passwd` 文件并返回一个赋值给变量 `f` 的文件句柄。`tcl` 支持以下文件模式：

- `r`: 仅读打开；文件必须存在。
- `r+`: 读写打开；文件必须存在。
- `w`: 写入打开。如果文件不存在则将创建；否则将截断。
- `w+`: 与 `w` 相同，但文件是以读取模式打开的。
- `a`: 以追加模式打开文件；如果文件不存在则将创建。

```
set f [open /etc/passwd r]
```

以 `r` 模式打开 `/etc/passwd` 文件并返回一个赋值给变量 `f` 的文件句柄。`tcl` 支持以下文件模式：

- `r`: 仅读打开；文件必须存在。
- `r+`: 读写打开；文件必须存在。
- `w`: 写入打开。如果文件不存在则将创建；否则将截断。
- `w+`: 与 `w` 相同，但文件是以读取模式打开的。
- `a`: 以追加模式打开文件；如果文件不存在则将创建。

```
set f [open /etc/passwd r]
```

- `file`

以下选项返回真 (`1`) 或 假 (`0`) 的信息：

- `atime`: 返回自 1970 年 1 月 1 日以来最后访问的时间
- `mtime`: 返回自 1970 年 1 月 1 日以来最后修改的时间
- `size`: 返回文件大小
- `readlink`: 如果给定文件是符号链接，返回其指向的值
- `type`: 返回文件类型的字符串

# 过程

过程是 C 语言中函数的等价物。创建一个过程使用 `proc` 命令，其语法如下：

```
proc procedure_name {arguments} {body}
```

参数数量是变量，空参数列表由 `{}` 指定。`body` 可以包含任何有效的 `tcl` 语句并可以根据需要变长。一个简单的无参数过程如下：

```
proc test_proc { } puts "procedure test"; }
```

调用此过程，只需给出它的名称：

```
test_proc;
```

得到输出

```
procedure test
```

一个更真实的示例是文件输出过程，它接受文件名作为参数：

```
proc cat {filename} {
set f [open $filename r];
while { [ gets $f line ] >= 0 } {
puts $line;
}
close $f;
}
```

使用 `/etc/passwd` 作为参数调用此过程，使用：

```
cat /etc/passwd
```

这将打印 `/etc/passwd` 的内容。

在过程中三个重要的命令是 `return`、`global` 和 `catch`。`global` 命令用于让过程访问全局变量，`return` 命令用于从过程返回值。`catch` 命令用于检测错误并返回失败值。

你可以通过以下操作重写过程以使其更健壮：

```
proc cat {filename} {
set ret_code 0;
catch {
set f [open $filename r];
while { [ gets $f line ] >= 0 } {
puts $line;
}
}
}
```

```
}
close $f;
set ret_code 1;
}
return $ret_code;
}
```

这段代码演示了 `catch` 和 `return` 的用法。如果过程的任何部分失败，它将返回假（false），但如果 `catch` 执行成功，它将返回 1（真）。如果调用 `catch` 时传入一个要执行进程作为参数，此信息将非常有用。

## tk 工具包

`tk` 工具包允许使用 `tcl` 脚本语言编写 X Window 图形界面（GUI）。`tk` 工具包通过允许创建 GUI 组件（小部件）扩展了 `tcl` 语言。本节简要回顾了可用的 `tk` 小部件并展示了如何创建它们。

### 小部件简介

创建小部件的基本方法是：

```
widget_type path option
```

其中 `widget_type` 是下列表列出的部件类型之一，`path` 是窗口路径（通常以点开头，即根窗口名称），`option` 是小部件理解的任何选项。

`tk` 工具包定义了以下小部件类型：

- `canvas`: 允许绘制对象
- `entry`: 允许输入单行文本
- `frame`: 用于包含其他小部件
- `listbox`: 显示一组字符串并允许选择其中一个或多个
- `menu`: 显示菜单栏和菜单项
- `text`: 显示多行文本
- `label`: 显示单行静态文本
- `button`: 显示可点击按钮的小部件
- `checkbox`: 显示一个复选框
- `radiobutton`: 显示多个互斥的单选框
- `scale`: 类似于设置值的值的滑块

要创建和操作小部件，必须使用窗口窗口外壳 `wish`。要交互式地调用 `wish`，请在 UNIX 提示符处输入 `wish`。随后会出现以下 `wish` 提示符：%

与此同时，屏幕上弹出一个空窗口。该窗口是 `wish` 根窗口（称为 `.`），所有创建的小部件都将随它一起出现。

### 创建小部件

本节展示了如何创建并操作小部件。首先，创建一个按钮，如下所示：

```tcl
button .button;
```

那么这个操作做了什么？

由于小部件类型指定为 `button`，所以 `tk` 创建了一个按钮。路径是 `.button`，因此 `tk` 在根窗口（`.` 是根 `tk` 窗口）中创建了按钮并将其命名为 `button`。

那么，按钮在哪里在哪里？

按钮目前还没有显示；`tk` 只是创建了它。要显示按钮，你需要告诉 `tk` 如何显示该小部件。为此，请使用 `pack` 命令并提供你想要显示的小部件的路径：

```tcl
pack .button;
```

现在按钮显示了，但它是空的（见图 33.1）。这就是小部件选项派上用场的地方。

图 33.1

小部件起初是一个普通的按钮。

![](img/7675e31a0e104594fbf0bbbebdf7e922_831_0.png)

### 小部件选项

所有 `tk` 小部件都使用控制外观和功能的标准选项。大多数小部件都理解以下选项：

- 背景颜色 (`-bg` color):

小部件的背景颜色。有效值格式为 `#RRGGBB`、`#RRRGGBB` 或 `/usr/lib/X11/tk.txt` 中定义的名称之一。

- 前景颜色 (`-fg` color):

小部件的前景颜色。有效值格式为 `#RRGGBB`、`#RRRGGBB` 或 `/usr/lib/X11/tk.txt` 中定义的名称之一。

- 高度 (pixels):

小部件的像素高度。

- 宽度 (pixels):

小部件的像素宽度。

- 边框宽度 (pixels), `-db` pixels:

小部件在 x 方向上所需的额外空间。

- `padx` (pixels):

小部件在 y 方向上所需的额外空间。

- `pady` (pixels):

小部件在 y 方向上所需的额外空间。

- 样式 (type):

小部件的 3D 效果，其中 `type` 是以下字符串之一：flat（平）、raised（凸）、groove（槽）、ridge（脊）、sunken（凹）。

- `text` (string):

要在小部件中显示的字符串。

- 字体 (font):

小部件中显示的文本使用的字体；有效的字体定义由 `xfonts` 命令提供。

- `command`:

使用小部件时执行的 `tk` 命令；通常这里是过程名称或 `exec` 语句名。

除了这些选项外，`pack` 命令还理解它特有的以下选项：

- 方向 (type):

控制小部件放置的顺序。有效类型为 left、right、top、bottom。例如，`left` 表示新小部件应该放在现有小部件的左侧。

- 填充 (type):

控制小部件是否拉伸以填充窗口中的可用空间。有效值为 none、x、y 或 both。例如，`both` 表示小部件应该填充所有空间。

![](img/7675e31a0e104594fbf0bbbebdf7e922_832_0.png)

### 一个 tcl/tk 小部件编程示例

现在你已经知道了小部件和 `pack` 的选项，就可以开始使用它们了。小部件有趣的特性之一是它们的样式（relief），即小部件的 3D 外观。为了了解每样式样式，可以使用以下代码创建一些标签：

```tcl
foreach i {raised sunken flat groove ridge} {
    label $i -relief i -text $i;
    pack $i;
}
```

此示例遍历了样式集合，为每个样式创建一个标签并将其 `pack` 出来，同时设置了标签文本。布局将类似于 33.2。

图 33.2

不同样式的标签。

![](img/7675e31a0e104594fbf0bbbebdf7e922_833_0)

这里有两个点需要注意。首先，标签的大小不同。其次，标签是堆叠的。这是 `pack` 的默认行为；它决定每个小部件的大小并将其放置在上一个小部件下方。

现在让所有标签的大小相同，并将它们相邻放置而不是堆叠。有两种方法。第一种是重写循环：

```tcl
foreach i {raised sunken flat groove ridge} {
    label $i -relief i -text $i -height 10 -10;
}
```

第二种方法是使用 `configure` 选项配置标签：

```tcl
foreach i {raised sunken flat groove ridge} {
    $i configure -height 10 -width 10;
}
```

如果交互式地运行 `wish` 并给出循环版本，会产生以下错误：window name 'raised' already exists

这是 `wish` 告诉程序已尝试重新创建已的小部件（这次是标签）。所以你需要 `configure`；事实上，任何当需要更改现有小部件时都需要 `configure`。在这种情况下，使用新版本循环唯一的方法是使用 `destroy` 命令删除现有的标签：

```tcl
foreach i {raised sunken flat groove ridge} { destroy .i }
```

结果将类似于图 33.3。现在回到示例。33.3 中有两个点需要修复。首先，很难区分这些标签。其次，窗口是空的。

通过增加边框宽度，可以让标签易于区分。要让标签占据所有可用空间，请为 `pack` 提供 x 和 y 方向的选项，并将 `expand` 选项设置为真：

```tcl
foreach i {raised sunken flat groove ridge} {
    label $i -relief i -text $i;
    pack .i -side left -padx 5 -pady 5 -fill both -expand 1
}
```

结果将类似于图 33.4。

![](img/7675e31a0e104594fbf0bbbebdf7e922_834_0.png)

图 33.4

标签现在填充了空间。

### xsetroot 的 tcl/tk 接口

本节通过将其应用于 X Window 程序 `xsetroot` 的图形界面开发，介绍 `tk` 工具包的其他功能。

# tcl 和 tk 编程

第 33 章

大多数 X Window 用户都会熟悉 X Window 程序 `xsetroot`，在 X11 下它可以用于设置根窗口（root window）的背景颜色。实际的命令是：

```
xsetroot -solid color
```

其中颜色可以以 #ARRGBB 的形式给出。前端将允许查看并应用颜色。

你现在可以开始了。首先你需要一个用于存储颜色的变量。然后，你需要创建两个基础帧（frames），一个用于应用程序的主区域，另一个用于放置消息。你还需要第三个帧用于控制控件。

帧（Frames）非常方便，因为它们可以用来将特定类型或功能的项打包在一起。此外，它们在将窗口划分成不改变的区域时非常有用。

全局创建帧和颜色：

```
set color "#000000";
frame .main_frame;
frame .message_frame;
frame .control_frame;
# 打包（pack）帧:
pack .control_frame -in .main_frame -expand 1 -fill both;
pack .main_frame -anchor c -expand 1;
pack .message_frame -anchor s -padx 2 -pady 2 \
-fill x -expand 1;
```

你还需要创建一个标签（label）来处理消息。我将将其写为一个过程（procedure），这样方便修改和执行：

```
proc make_message_label {} {
    label .message_label -relief sunken;
    pack .message_label -anchor c \
    -in .message_frame -padx 2 \
    -pady 2 -fill both -expand 1;
}
```
