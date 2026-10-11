
```shell
menu

case $option in

  0)

    break ;;

  1)

    diskspace ;;

  2)

    whoseon ;;

  3)

    memusage ;;

  *)

    clear

    echo "Sorry, wrong selection";

esac

echo -en "\n\tHit any key to continue"

read -n 1

done
```

此菜单创建了三个函数，使用常用命令获取系统管理信息。它使用 `while` 循环循环菜单，直到客户选择选项 0，该选项使用 `break` 命令跳出 `while` 循环。你可以使用此模板创建任何 shell 菜单界面。它提供了一种与客户交互的简单方法。

### 整合

现在你已经了解了组成菜单的所有部分，让我们把它们整合在一起。这是一个示例：

```shell
$ smenu1

#!/bin/bash

# 在菜单中使用 select

function diskspace {

  clear

  df -k

}
```

```shell
function whoseon {

  clear

  who

}
```

```shell
function memessage {

  clear

  cat /proc/meminfo

}
```

```shell
PS3="Enter option: "

select option in "Display disk space" "Display logged on users"
"Display memory usage" "Exit program"
do
  case $option in
    "Exit program"
      break ;;
    "Display disk space"
      diskspace ;;
    "Display logged on users"
      whoseon ;;
    "Display memory usage"
      memessage ;;
    *)
      clear
      echo "Sorry, wrong selection";
  esac

  echo -en "\n\tHit any key to continue"

  read -n 1
done
```

```
done
clear
$
```

`select` 语句在代码文件中必须写在一行内。这通过列表中的续行符来指示。当你运行该程序时，它会自动生成以下菜单：

+   $ ./smenu1
1) 显示磁盘空间 3) 显示内存使用情况
2) 显示登录用户 4) 退出程序
输入选项：

当你使用 `select` 命令时，记住存储在变量中的结果值是整个文本字符串，而不是与菜单项相关的数字。在你的 `case` 语句中，你需要比较的是这些文本字符串值。

# 实现 Windows 界面

使用文本菜单是向正确方向的一步，但我们的交互式脚本中仍然缺少很多功能，特别是当我们尝试将其与图形化的 Windows 世界相比较时。幸运的是，开源世界中一些非常有资源的人帮了我们大忙。

`dialog` 软件包是一个精巧的小工具，最初由 Savio Lam 创建，目前由 Thomas E. Dickey 维护。该软件包使用 ANSI 转义控制代码在文本环境中重建了标准的 Windows 对话框。你可以轻松地将这些对话框整合到 shell 脚本中，以便与脚本用户交互。本节描述了 `dialog` 软件包并演示了如何在 shell 脚本中使用它。

## 注意

并不是所有的 Linux 发行版默认都安装了 `dialog`。如果默认没有安装，由于它的流行，几乎总是包含在软件仓库中。请检查你特定的 Linux 发行版文档查看如何加载 `dialog` 软件包。对于 Ubuntu Linux 发行版，以下是安装命令：

+   1. sudo apt-get install dialog

该软件包会安装 `dialog` 软件包以及系统所需的库。

# dialog 软件包

`dialog` 命令使用行参数来确定生成什么类型的 Windows 组件（widget）。组件是 `dialog` 中一类 Windows 元素的术语。`dialog` 软件包目前支持表 18.1 所示的类型组件。

表 18.1 dialog 组件

| 组件 | 说明 |
| --- | --- |
| calendar | 提供一个日历，从中可以选择日期 |
| checklist | 显示多个条目，每个条目都可以开启或关闭 |
| form | 允许你创建一个带有标签和待填文本字段的表单 |
| fselect | 提供文件选择以浏览文件 |
| gauge | 显示显示完成百分比的仪表 |
| infobox | 显示消息而无需等待 |
| textbox | 显示一个用于输入文本的单个文本框 |
| inputmenu | 提供一个可编辑的菜单 |
| menu | 显示一个供选择的列表 |
| msgbox | 显示一条消息并要求用户选择 OK 按钮 |
| pause | 显示显示指定暂停期间状态的仪表 |
| password | 显示一个隐藏输入文本的单个文本框 |
| passwordform | 显示一个带有标签和隐藏文本字段的表单 |
| radiolist | 提供一组菜单项，其中只能选择一个项 |
| tailbox | 使用 `tail` 命令在滚动窗口中显示文件文本 |
| textboxbg | 与 `tailbox` 相同，但在后台模式下运行 |
| textbox | 在滚动窗口中显示文件内容 |
| timebox | 提供一个用于选择小时、分钟和秒的窗口 |

# 提供带有“是”（Yes）和“否”（No）按钮的简单消息

如表 18.1 所示，你可以选择许多不同的组件。这让你花费很少精力就能让脚本看起来非常专业。

要在命令行上指定组件，你需要使用双横线格式：
`dialog --widget parameters`

其中 `widget` 是表 18.1 中的名称，`parameters` 定义了组件窗口的大小以及组件所需的任何文本。

每个 `dialog` 组件提供两种形式的输出：

-   使用 STDERR
-   使用退出码状态

`dialog` 的退出状态决定了用户选择的按钮。如果选择了 OK 或 Yes（是），`dialog` 命令返回退出状态 0。如果选了 Cancel（取消）或 No（否）按钮，`dialog` 命令返回退出状态 1。你可以使用标准的 `$` 变量来确定在 `dialog` 组件中选择了哪个按钮。

如果 `dialog` 返回任何数据（例如菜单选择），`dialog` 命令将使用 STDERR 发送数据。你可以使用标准的 bash 技术，将 STDERR 输出重定向到另一个文件或文件描述符：

```
dialog --inputbox "Enter your age:" 10 20 2age.txt
```

此命令将文本框中的文本重定向到 `age.txt` 文件。

接下来的章节将查看你在 shell 脚本中常用的某些 `dialog` 组件的示例。

# msgbox 组件

`msgbox` 是最常见的对话框类型。它在窗口中显示简单的消息，并等待用户点击 OK 按钮后才会消失。使用 `msgbox` 组件需要以下格式：

```
dialog --msgbox text height width
```

`text` 参数是你想想要放在窗口中的任何字符串。`dialog` 命令会根据 `height` 和 `width` 参数自动对文本换行以适应窗口大小。如果你想在窗口顶部放置一个标题，还可以使用 `--title` 参数以及标题文本。这里有一个使用 `msgbox` 组件的示例：

```
$ dialog --title Testing --msgbox "This is a test" 10 20
```

在输入此标题后，消息框将出现在你正在使用的终端模拟器会话屏幕上。图 18.2 显示了它的样子。

![](img/f4b40da3f699eed06c5e37a566e1b4a6_579_0)

如果你的终端模拟器支持鼠标，点击 OK 按钮关闭对话框。

# yesno 组件

`yesno` 组件比 `msgbox` 组件进了一步，允许用户回答窗口中显示的是/否问题。它在窗口底部有两个按钮——Yes（是）和 No（否）。你可以使用鼠标、Tab 键或键盘在按钮之间切换。

这是一个使用 `yesno` 组件的示例：

```
$ dialog -title "Please answer" -yesno "Is this thing on?" 10 20

echo $?
$
```
