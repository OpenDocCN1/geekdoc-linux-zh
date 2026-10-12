
`-inversescreen` 开关反转控制台的色彩。如果你使用两次，`-inversescreen` 可以使显示器闪烁，以提醒用户重要事件。例如，要闪烁屏幕一秒，请执行以下操作：

```bash
$ setterm -inversescreen on
$ sleep 1
$ setterm -inversescreen off
```

其他有用的开关包括：

- `-cursor`—显示或隐藏输入光标
- `-repeat`—打开或关闭控制台键盘重复
- `-appcrskeys`—打开或关闭光标键应用模式
- `-linewrap`—打开或关闭控制台自动换行

这些功能可以打开或关闭。例如，要隐藏输入光标，请输入以下内容：

```bash
$ setterm -cursor off
```

还有其他属性用于控制如电源节省和 Tab 使用等功能。请参阅本章末尾的参考部分以获取完整的开关列表。

## `tput`

你可以使用 `setterm` 命令适用于任何终端显示，但尝试使用控制台特有的功能会被忽略。相反，有一个旧命令叫 `tput`（`terminal put`），它的工作方式与 `setterm` 非常相似，但适用于所有纯文本显示。

`tput` 有一个参数；一个基于 `terminfo` 终端数据库的屏幕属性代码。这些代码与 `setterm` 开关不同。你可以在 `terminfo` 手册页（`$ man 5 terminfo`）上找到完整列表。

```bash
$ tput cols # width of display
80
$ tput clear # clear the screen
```

## `select` 菜单

内置的 `select` 命令创建简单的菜单。`select` 是一个特殊的循环。该命令后跟一个参数列表，并将它们显示为编号选项。当用户通过输入该数字选择一项时，参数会被赋值给 `select` 变量，并且执行 `select` 语句内部的命令。参见列表 13.1。

**列表 13.1 `select_demo.sh`**

```bash
#!/bin/bash
# # select_demo.sh: a simple select menu
#
shopt -s -o nounset

declare -i
SCRIPT=${0##*/}

printf "\$\n" "Select a document type:"
select ITEM in "orders" "purchase orders" "packing slips" ; do
    if [ -z "$ITEM" ] ; then
        printf "Please choose 1, 2 or 3...\n"
    else
        printf "Processing $ITEM documents...\n"
    fi
done
printf "Done\n"
```

当选择的项目不在列表中时，变量会被赋值为空字符串。循环持续直到读取到 EOF（通常是 Control-D）。

```text
Select a document type:
1) orders
2) purchase orders
3) packing slips
#? 1
Processing orders documents...
#? 4
Please choose 1, 2 or 3...
#?
1) orders
2) purchase orders
3) packing slips
#?
```

旧版本的 Bash 每次遇到 `select` 语句时都会显示菜单。新版本仅在 `REPLY` 变量为空时显示列表，例如当用户在 `select` 提示符处按下 `Return` 键时。

提示符位于变量 `PS3` 中。如果未定义 `PS3`，Bash 使用 `#?` 作为提示符。若要更改提示符，请更改 `PS3` 的值。用户的响应也保存在变量 `REPLY` 中。如果缺少 `in` 部分，Bash 将从脚本参数中选择。

与其他循环类似，`select` 命令可以使用 `break` 和 `continue`。

## 自定义菜单

虽然 `select` 命令可以用很少的工作创建简单的菜单，但它不提供任何用于复杂用户交互的功能。为了提供外观更友好的通信并支持更复杂的屏幕，Linux `dialog` 命令创建弹出文本屏幕对话框。

该命令适用于任何纯文本显示。有几种类型的对话框：

- 背景文本框（`-textbox`）—在处理其他内容时监控命令
- 日历框（`-calendar`）—选择日期
- 复选列表（`-checklist`）—可选择项目的列表
- 文件选择（`-fileselect`）—选择文件
- 进度条（`-gauge`）—温度计图表
- 信息框（`-infobox`）—状态消息
- 输入框（`-inputbox`）—请求用户输入文本
- 菜单（`-menu`）—列出替代选择
- 消息框（`-msgbox`）—带有“确定”按钮的信息框
- 密码框（`-passwordbox`）—请求用户输入文本但隐藏输入
- 单选列表（`-radiolist`）—替代项目列表
- 尾部框（`-tailbox`）—监控命令
- 时间框（`-timebox`）—选择时间值
- 是/否框（`-yesno`）—询问是/否问题
- 文本框
- 是否框

使用 `-yesno` 开关创建是否框。对话框包含带有“是”和“否”按钮的消息。该开关接受三个参数：文本、高度和宽度。所有对话框都有这三个参数。`-defaultno` 开关使“否”按钮成为默认按钮。

例如，要创建一个消息为“你确定吗？”、宽 70 个字符、高 7 个字符并在屏幕居中显示的对话框，你输入以下内容。

```bash
$ dialog -yesno "Are you sure?" 7 70
```

`dialog` 返回的状态码指示选择了哪个按钮：0 是“是”（或其他对话框中的“确定”），1 是“否”（或其他对话框中的“取消”）。状态码为 -1 表示错误或用户通过按下 Escape 键中止了对话框。图 13.1 显示了一个典型的是/否对话框。

你可以通过在消息中嵌入换行代码（`\n`）将长文本分成单独的行。

```bash
$ dialog -title Testbox -yesno "Delete files:\nAre you sure?" 7 70
```

`-checklist` 开关创建一个复选框列表。基本参数是文本标题、列表的高度和宽度。在这些之后，每个检查列表项使用其名称、项目文本以及指示其当前是否被选中（on）或未选中（off）的信息来描述。选中的项会打印到标准错误。

```bash
$ dialog -checklist "Printer type:" 20 70 14 p1 "p 1" on p2 \
"printer 2" off fax "Fax" off
```

在这种情况下，打印机 1 和传真机被选中。

![](img/7da864b222941ec315ee1c456ff472dd_261_0.png)

**图 13.1** 一个是否对话框。

可以将结果捕获到变量中。由于标准输出用于绘制屏幕，而结果写入标准错误，因此需将标准错误重定向到文件。

```bash
$ declare CHOICE_FILE="/tmp/choice.$$"
$ declare CHOICE
$ dialog --checklist "Printer type:" 20 70 14 p1 "printer 1" on p2 \
"printer 2" off fax "Fax" off 2> "$CHOICE"
$ CHOICE="cat "$CHOICE_FILE""
```

文件选择对话框（见图 13.2）使用 `-fselect` 开关创建。此对话框需要起始目录，以及高度和宽度。

```bash
$ dialog -fselect "$HOME" 10 50
```

![](img/7da864b222941ec315ee1c456ff472dd_261_1.png)

**图 13.2** 一个文件选择对话框。

仪表是一个显示百分比进度的温度计条形图。新的百分比值会逐个从标准输入读取，直到到达文件末尾为止。`-gauge` 开关需要提供一个文本消息、高度、宽度以及一个可选的起始百分比（参见列表 13.2）。百分比可以通过命名管道发送给仪表，这将在第 11 章“文本文件基础”中讨论。

假设你希望显示一个显示打印发票系列文件进度的温度计图形，这些发票文件存储在一个名为 `invoices` 的目录中。下面的演示在发票被发送给另一个名为 `print_invoice` 的脚本时显示发票。

## 列表 13.2 `gauge_demo.sh`
