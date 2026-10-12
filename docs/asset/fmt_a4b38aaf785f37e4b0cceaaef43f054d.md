
在本章示例和程序中的许多长行代码在脚本中都被拆分为两或多行，尽管它们被 `Tk` 解释为单行。任何以 `\` 结尾的行都是单行代码的一部分，该代码在下一行脚本中继续。

## 1 分钟自测

- `Tk` 有哪些几何布局管理器？
- 你用于调用 `Tk` 的命令是什么？

### 提问专家

**问题：** 几何布局命令之间有什么区别？

**答案：** `pack` 几何布局命令简单地将组件（widgets）排列在一起，仅占据框架或窗口中足够容纳表单的空间。如果需要，你可以添加内边距（padding）来增大它们之间的间距。`place` 几何布局命令允许你将组件放置在框架的特定位置。`grid` 几何布局命令允许你设置一个类似单元格的网格，并在其中放置组件。

**问题：** 我什么时候该使用 `grid`？

**答案：** `grid` 有助于以特定的格式（如表单）排列组件。例如，如果你想设置一个包含输入框和按钮的表单，你可以使用 `grid` 将组件放置在表单的不同部分。要引用网格中的某个特定单元格，你需要指定它的行和列。

**问题：** 你如何使用 `place` 命令？

**答案：** 当你想要将组件放置在窗口或框架上远离其他组件的特定点时，`place` 几何布局命令非常有用。虽然 `pack` 和 `grid` 命令是将组件相邻放置，但你可以通过指定 `x` 和 `y` 坐标使用 `place` 将组件放在任何地方。例如，你可以将一个 OK 按钮组件放置在远离屏幕中间出现的文本组件的角落。

- `pack`, `place`, and `grid`
- `wish`

### 284 Linux 编程：入门指南

![](img/3cfc28f62e3fe98d5a49b453e25d689c_307_0.png)

图 8-1 `mydir1` 的 `Tk` 列表框和滚动条

![](img/3cfc28f62e3fe98d5a49b453e25d689c_307_1.png)

## 项目 8-1：显示目录

以下 `mydir` 程序是一个简单的 Tcl/Tk 程序，它在带有滚动条的 `Tk` 列表对象中显示文件和目录名称列表。图 8-1 显示了这个列表框。列表框对象允许你显示项目列表，可以使用鼠标轻松地滚动和选择。你可以附加滚动条，以适应数量多于指定列表框大小的项目。

## 逐步详解

1. 使用 `scrollbar` 命令定义滚动条：将其命名为 `.scroll` 并将其与命令 `.list yview` 绑定。这指示滚动条在 y 轴上垂直附加到列表框上。

2. 使用 `listbox` 命令定义列表框，将其命名为 `.list`，并通过 `.scroll` 的宽度（width）提供 y 轴滚动能力。列表框将以“凹陷”（sunken）的形式出现，具有指定的宽度和高度。

```
scrollbar .scroll -command ".list yview"
```

```
listbox .list -yscroll ".scroll set" -relief sunken -width 15 -setgrid
```

3. 使用 `pack` 命令创建这两个对象（滚动条和列表框），并将它们放置在窗口中。滚动条和列表框放置在窗口的左侧，并将扩展填充窗口。它们的锚点在窗口的西侧，如随后的代码中的 `w` 所示。首先放置列表框 `.list`，然后是滚动条 `.scroll`。

```
pack .list .scroll -side left -fill both expand -yes -anchor w
```

### 模块 8：Tk 285

4. 运行一个 Tcl `if` 来判断用户在调用程序时是否输入了参数。`if` 测试检查 `argv` 列表（存储任何参数）是否包含第一个元素。如果没有检测到参数，则使用当前目录（用 `.` 表示）。所选目录被赋值给变量 `dir`。

5. 使用 Tcl `foreach` 操作填充列表框。使用通过 `exec` 命令执行的 shell `ls` 命令获取文件和目录列表。

6. 使用 `Tk` `insert` 操作为 `.list` 对象将文件和目录列表放入列表框。`insert` 命令接受一个位置和一个值。这里的值是存储在 `$i` 中的文件名，它被放在列表末尾：

```
.list insert end $i
```

7. 将 CTRL-C 字符绑定到 `exit` 命令，允许用户轻松地关闭窗口。

`mydir1` 脚本所示：

```bash
#!/usr/bin/wish -f

## 创建滚动条和列表框

scrollbar .scroll -command "list view" -relief sunken -width 15 -height 15 -setgrid

pack list -yscroll .scroll set -side left -fill both -expand -anchor w

# 如果用户输入了目录参数则使用它，否则使用当前目录

if {$llength $argv > 0} then

    set dir [lindex $argv 0]

else

    set dir ""

}

# 使用从 ls 获取的文件目录列表填充列表框 (.list)

cd $dir

foreach i [exec ls -a] {

    if [file is $i] {

        .list insert end $i

    }

}

# 为文件管理器设置绑定。Control-c 关闭窗口。

bind all <Control-c> {destroy . }
```

## 事件与绑定

`Tk` 程序是事件驱动的，这意味着它在运行时会等待事件（例如鼠标事件或键盘事件）来执行动作。鼠标事件可以是鼠标点击。鼠标事件可以是鼠标点击或键盘事件。虽然 `pack` 和 `grid` 命令是将组件相邻放置，但你可以通过指定 `x` 和 `y` 坐标使用 `place` 将组件放在任何地方。例如，你可以将一个 OK 按钮组件放置在远离屏幕中间出现的文本组件的角落。

- `pack`, `place`, and `grid`
- `wish`

### 288 Linux 编程：入门指南

| 事件模式序列 | 描述 |
|--- |--- |
| Triple（三击） | 三次重复的事件，例如三次点击鼠标 |
| 事件类型 | | |
| `ButtonPress` | 按下鼠标按钮；`Button` 修饰符的默认类型 |
| `ButtonRelease` | 释放鼠标按钮 |
| `Destroy` | 销毁组件 |
| `Enter` | 进入组件内部 |
| `KeyPress`, `Key` | 按下键 |
| `KeyRelease` | 释放键 |
| `Leave` | 离开组件 |
| `Motion` | 鼠标移动到组件上 |
| Event Details（事件详情） | 按钮的编号；如果没有提供数字，则匹配所有按钮 |
| 如果省略了类型，则使用 `ButtonPress` 的默认类型 |
| `Button-1` 等于 `Button-Button-Press-1` |
| 键盘字符的键符号——例如，`A`、`COMMA`（逗号）、`SHIFT-R` |

### 表 8-4 用于 `bind` 命令的事件模式（续）

当按下时，程序会执行绑定到该事件的动作。这些动作可以是任何 Tcl/Tk 命令或一系列命令。通常，这些命令会调用可以执行复杂操作的函数。执行完这些操作后，程序将继续扫描其他事件。这种扫描将一直持续，直到被 `exit` 或 `destroy` 命令强制中断，就像对 CTRL-C 绑定所做的那样。

图 8-2 显示的 `myriad2` 程序了函数和对象的绑定。在这里，`mydir1` 程序被增强了显示两个列表框的能力：一个用于目录，另一个用于文件。每个列表框都有自己的滚动条。目录列表命名为 `listdir`，其滚动条命名为 `.scrolldir`。每个列表框和滚动条都经过定义后创建，首先创建 `.listdir` 和 `.scrolldir`，这样它们就会出现在窗口的左侧。

定义了 `Tk` 函数 `listdirsunc` 来填充两个列表框。该函数接受一个目录作为参数。`cd` 命令将切换到该目录，提供了列出不同目录的能力。然后通过 `isdirectory` 测试检查是否为目录，将其放入 `listdir` 列表框中。

```
proc listdirfsunc dir {

    .listdir delete 0 end

    .list delete 0 end

    cd $dir

    foreach i [exec -a] {

        if [file isdirectory $i]

            .listdir insert end $i

        } else

            .list insert end $i

    }

}
```

在该函数的定义之后是一个函数调用。需要调用一次 `listdirfsunc` 函数来用当前目录的内容填充列表框。

```bash
## 第一次显示目录和文件
```
