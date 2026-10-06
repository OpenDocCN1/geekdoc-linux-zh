

# 高级 Shell 脚本

```bash
selection=`cat $temp2`

case $selection in
1)
diskspace ::
2)
whoseon ::
3)
memusage ::
0)
break ::
**) dialog --msgbox "Sorry, invalid selection" 10 30
esac
done
rm -f $temp2 > /dev/null
$
```

该脚本使用带有常量真值的 `while` 循环来创建一个无限循环，显示菜单对话框。这意味着在执行完每个函数后，脚本都会返回显示菜单。图 15-8 显示了对话菜单的样子。

# 图 15-8

使用 `dialog` 命令的脚本菜单

![](img/adcbcf1053b52dbf22f3aa187738232f_439_0.png)

菜单对话框包含一个取消取消按钮，因此脚本会检查 `dialog` 命令的退出状态，以防用户按下取消按钮退出。由于它位于 `while` 循环中，退出只需使用 `break` 命令跳出循环即可。

脚本使用 `mktemp` 创建两个临时文件，用于存储 `dialog` 命令的数据。第一个文件 `$temp` 用于存储 `df` 命令的输出，该输出可以在文本对话框中显示。第二个临时文件 `$temp2` 用于存储来自主菜单对话框的选择值。

# 获取图形界面

如果你正在为你的交互式脚本寻找更多图形界面，可以更进一步。但 KDE 和 GNOME 桌面环境（见第 1 章）已经扩展了 `dialog` 命令的概念，并包含了为它们各自的环境生成 X Windows 图形小组件的命令。

本节描述了 `kialog` 和 `zenity` 包，它们分别为 KDE 和 GNOME 桌面提供图形窗口小组件。

# KDE 环境

KDE 图形环境默认包含 `kialog` 包。`kialog` 包使用 `kialog` 命令在你的 KDE 桌面内生成标准窗口，类似于 `dialog` 风格的小组件。这允许你直接从 Shell 脚本生成 Windows 级的用户界面！

# kialog 组件

与 `dialog` 命令一样，`kialog` 命令使用命令行选项来指定要使用的窗口小组件类型。`kialog` 命令的格式为：

```
kialog display-options window-options arguments
```

`window-options` 选项允许你指定使用的窗口小组件类型。可用选项如表 15-5 所示。

从表 15-5 可以看出所有的标准的对话框类型都被包含了。然而，当你使用 `kialog` 窗口小组件时，它会作为 KDE 桌面上的独立窗口出现，而不是在终端模拟器会话内部！

checklist（复选列表）和 radiolist（单选列表）小组件允许你定义列表中的单个项目，以及它们默认是否被选中：

```bash
$ kialog --checklist "Items I need" 1 "Toothbrush" on 2 "Toothpaste" off 3 "Hair brush" on 4 "Deodorant" off 5 "Slippers" off
```

# 第三部分 高级 Shell 脚本

# 表 15-5

| 选项 | 说明 |
| --- | --- |
| --checklist title [tag item status] | 复选列表菜单，状态指定项目是否被勾选。 |
| --error text | 错误消息框。 |
| --input text [init] | 输入文本框。你可以使用 *init* 值指定默认值。 |
| --menu title [tag item] | 菜单选择框和一组由标签标识的项列表。 |
| --msgbox text | 带有指定文本简单消息框。 |
| --password text | 隐藏用户输入的密码输入文本框。 |
| --radiolist title [tag item status] | 单选列表菜单，状态指定项目是否被选中。 |
| --separate-output | 为复选列表和单选列表菜单分行返回项目。 |
| --sorry text | 抱歉消息框。 |
| --textbox file [width] [height] | 显示 *file* 内容的文本框，也可以通过宽度和高度指定。 |
| --title text | 为对话框的标题栏区域指定标题。 |
| --warningyes text | 带有“是”和“否”按钮的警告消息框。 |
| --warningcontinuecancel text | 带有“继续”和“取消”按钮的警告消息框。 |
| --warningyesnocancel text | 带有“是”、“否”和“取消”按钮的警告消息框。 |
| --yesno text | 带有“是”和“否”按钮的问题框。 |
| --yesocancel text | 带有“是”、“否”和“取消”按钮的问题框。 |

生成的复选列表窗口如图 15-9 所示。要在复选列表中选择或取消选择某项，只需点击它即可。如果你选择 OK 按钮，`kdialog` 将标签值发送到 STDOUT。

```bash
$ kdialog --checklist "Items I need" 1 "Toothbrush" on 2 "Toothpaste" off 3 "Hair brush" on 4 "Deodorant" off 5 "Slippers" off "1" "3" "5"
```

# 为脚本添加颜色

# 图 15-9

一个 kdialog 复选列表窗口

![](img/adcbcf1053b52dbf22f3aa187738232f_442_0.png)

当你按下 Enter 回车键时，对话框就会出现。当你点击 OK 或 Cancel 按钮时，`kdialog` 将每个标签作为字符串返回到 STDOUT（这些你在示例中看到的 "1"、"3" 和 "5" 值）。你的脚本必须能够解析结果并将它们与原始值匹配。

# 使用 kdialog

你可以像使用 `dialog` 组件一样在 Shell 脚本中使用 `kdialog` 窗口小组件。主要的区别是 `kdialog` 窗口小组件使用 STDOUT 而不是 STDERR 输出值。这里有一个将之前系统管理员创建的脚本转换为 KDE ：

```bash
#!/bin/bash
# 使用 kdialog 创建菜单
temp=`mktemp -t temp`
temp2=`mktemp -t temp2`
```

```bash
function diskspace {
  df > $temp
  kdialog --textbox $temp 1000 10
}
```

```bash
function whoseon {
  who > $temp
  kdialog --textbox $temp 500 10
}
```

```bash
function memusage {
  cat /proc/meminfo > $temp
  kdialog --textbox $temp 300 500
}
```

```bash
while [ 1 ]
do
  kdialog --menu "Sys Admin Menu" "1" "Display disk space" "2" "Display users" "3" "Display memory usage" "0" "Exit" > $temp2
if [ $? -eq 1 ]
then
    break
fi
```

```bash
selection=$cat $temp2
case $selection in
1)
  diskspace ::
2)
  whoseon ::
3)
  memusage ::
0)
  break
*)
  dialog --msgbox "Sorry, invalid selection"
esac
done
```

使用 `kdialog` 命令和 `dialog` 命令之间没有太大区别。生成的菜单如图 15-10 所示。现在看起来像一个真正的应用程序了！你的交互式脚本可以做的事情是没有限制的。

# GNOME 环境

GNOME 图形环境支持两个可以生成标准窗口的流行包：

- dialog
- zenity

# 图 15-10

使用 kdialog 的系统管理员菜单脚本

![](img/adcbcf1053b52dbf22f3aa187738232f_444_0.png)

Zenity 是 GNOME 桌面发行版（如 Ubuntu 和 Fedora）中常见的包。本节描述了 zenity 的功能并演示了如何在 Shell 脚本中使用它。

# zenity 组件

正如你所预期的，zenity 允许你使用命令行选项创建不同的窗口小组件。表 15-6 显示了 zenity 可以产生的不同组件。zenity 程序的工作方式与 `kdialog` 和 `dialog` 不同。许多组件类型是通过额外的选项定义的，而不是作为选项的参数。

zenity 程序提供了一些很酷的基础对话框。calendar 生成一个完整的日历，如图 15-11 所示。当你从日历中选择日期时，zenity 将值返回到 STDOUT，就像 `kdialog` 一样：

```bash
$ zenity --calendar
11/25/2008
```

zenity 的另一个很酷的窗口是文件选择选项，如图 15-12 所示。

# 第三部分 高级 Shell 脚本

# 表 15-6

| 选项 | 说明 |
| --- | --- |
| --calendar | 显示完整的日历。 |
| --entry | 显示文本输入对话框。 |
| --error | 显示错误消息对话框。 |
| --file-selection | 显示完整路径和文件名对话框。 |
| --info | 显示信息提示对话框。 |
| --list | 显示复选列表或单选列表对话框。 |
| --notification | 显示通知图标。 |
| --progress | 显示进度条对话框。 |
| --question | 显示是/否问题对话框。 |
| --scale | 显示比例尺对话框。 |
| --text-info | 显示包含文本的文本框。 |
| --warning | 显示警告对话框。 |

# 图 15-11

zenity 日历对话框

![](img/adcbcf1053b52dbf22f3aa187738232f_445_0.png)

