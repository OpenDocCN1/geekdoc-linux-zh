

# 对话框选项描述

| 对话框 | 选项 | 描述 |
| :--- | :--- | :--- |
| 消息框 | --msgbox | 显示文本消息并等待用户响应。 |
| 密码框 | --password | 与输入框类似，但会隐藏用户的输入。 |
| 暂停 | --pause | 显示文本消息和倒计时器。当计时结束或用户按下“确定”或“取消”按钮时，对话框将终止。 |
| 程序框 | --programbox | 显示管道命令的输出。当命令完成后，对话框等待用户点击“确定”按钮。 |
| 进度框 | --progressbar | 与程序框类似，不同之处在于管道命令完成后对话框会自动终止，而不是等待用户点击确定。 |
| 单选列表框 | --radiolist | 显示选项列表并允许用户选择单项。任何之前选中的项目将变为取消选中。 |
| 范围框 | --rangebox | 允许用户使用基于键盘的滑块在指定范围内选择数值。 |
| 尾部框 | --tailbox | 显示实时更新的文本文件。工作类似于命令 `tail -f`。 |
| 文本框 | --textbox | 简单的文本文件查看器。支持许多与 `less` 相同的键盘命令。 |
| 时间框 | --timebox | 用于输入当天时间的对话框。 |
| 树形视图 | --treeview | 以树形层次结构显示项目列表。 |
| 是/否框 | --yesno | 显示消息并给予用户用“是”或“否”响应的机会。 |

支持的对话框

以下是一些示例：

![](img/9aafc495f4afbc0a97de2b31a0d13f46_88_0.png)
yesno 对话框截图

![](img/9aafc495f4afbc0a97de2b31a0d13f46_88_1.png)
radiolist 对话框截图

dialog 79

# 可用性

dialog 在大多数发行版的仓库中通过包“dialog”提供。除了程序本身，dialog 包还包含一个相当详尽的 man 和大量的示例程序，演示了它可以显示的各种对话框。在基于 Debian 的系统上安装后，这些示例程序可以在 //share/doc/dialog/examples 目录中找到。其他发行版也类似。

顺便说，使用 Midnight Commander 浏览示例目录是运行示例程序和学习脚本本身的极佳方法：

| 左侧文件命令选项 | 右侧 ...share/doc/dialog/examples -<c> |
| :--- | :--- |
| 'n 名称 大 修改时间 | ../ 名称 大 修改时间 |
| -checklist1 815 Jan 13 2018 | -calendar 229 Jan 13 2018 |
| -editbox 103 Jan 13 2018 | -calendar-stout 215 Jan 13 2010 |
| -editbox-utf8 665 Jan 13 2018 | -calendar-2-stout 207 Jan 13 2010 |
| -formi 1428 Oct 4 2011 | -Checklist 1084 Jan 13 2018 |
| -form 119 Jan 13 2018 | -Checklist1 815 Jan 13 2018 |
| -fselect-stout 199 Jan 13 2018 | -editbox 1039 Jan 13 2018 |
| -fselect 322 Jan 13 2018 | -editbox-utf8 665 Jan 13 2018 |
| -fselect-stout 312 Jan 13 2018 | -formi 1428 Oct 4 2011 |
| -fselect2 194 Jan 13 2018 | -form 119 Jan 13 2018 |
| -fselect2-stout 212 Jan 13 2018 | -fselect 239 Jan 13 2018 |
| -gauge 336 Jan 13 2018 | -fselect 234 Jan 13 2018 |
| -gauge-input-fd 466 Jan 13 2018 | -fselect-stout 199 Jan 13 2018 |
| -gauge2 | | -calendar-stout |

使用 Midnight Commander 浏览示例

# 工作原理

从表面上看，dialog 看起来非常简单。我们启动 dialog，随后跟上一个或多个通用选项（无论所需的对话框如何都适用），然后是框选项及其关联参数。使用 dialog 的难点在于如何从从中提取数据。

dialog 接收的数据（例如输入输入框中的字符串）通常返回在标准错误输出中。这是因为 dialog 使用标准错误来显示内容。让我们来看看它们。

## 方法 1：将结果存储在临时文件中

脚本的第一部分定义了 dialog 使用的一些常量。我们使用临时文件来处理这些。

```bash
#!/bin/bash

# inputbox - 演示输入框

# 定义 dialog 的退出状态
DIALOG_OK=0
DIALOG_CANCEL=1
DIALOG_HELP=2
DIALOG_EXTRA=3
DIALOG_ITEM_HELP=4
DIALOG_ESC=255

# 使用 tempfile 命令创建一个名为 tmp_file 的临时文件
tmp_file=$(mktemp)

# 设置 trap（信号捕获）以确保在程序退出时删除临时文件
trap "rm -f $tmp_file" EXIT

# 进入 dialog 命令本身。我们首先为输入框设置标题，并指定 --clear 选项，告诉 dialog 擦除屏幕上之前的任何对话框。接下来，我们指明我们想要的对话框类型及其所需的参数。这些参数包括显示在输入字段上方的标题，以及框所需的高度和宽度。虽然[截断] 尽管我们也可以将这两个值都指定零，dialog 将尝试自动确定大小。

# 由于 dialog 通常将其结果输出到标准错误，我们将它的文件描述符重定向到我们的临时文件进行存储。
dialog \
  --title "INPUT BOX \
  --clear \
  --inputbox "" 10 40 2>"$tmp_file"
```
*(注：由于原始文本在此处截断，后续的 Method 2 及完整代码未包含翻译)*

