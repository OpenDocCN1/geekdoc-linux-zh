

# 为脚本添加颜色

图 15-12

zenity 文件选择对话框

![](img/adcbcf1053b52dbf22f3aa187738232f_446_0.png)

你可以使用该对话框浏览系统上的任何目录位置（只要你有查看该目录的权限）并选择一个文件。当你选择一个文件时，zenity 会返回完整的文件和路径：

```bash
$ zenity --file-selection
/home/ubuntu/menu5
```

这在 shell 脚本世界中已经是尽可能专业的视觉了！

# 在脚本中使用 zenity

正如你所预期的，zenity 在 shell 脚本中表现良好。遗憾的是，zenity 选择不遵循 `dialog` 和 `kdialog` 使用的选项，因此将现有的交互式脚本转换为 zenity 可能会面临挑战。

在将系统管理员菜单从 `kdialog` 转换为 `zenity` 时，我发现我必须对组件定义进行大量的操作：

```bash
$ cat menu5
#!/bin/bash
```

# 高级 Shell 脚本编程

```bash
# 使用 zenity 创建菜单

temp=`mkktemp -t temp.XXXXXX`
temp2=`mkktemp -t temp2.XXXXXX`
```

```bash
function diskspace {
  df -k $temp
  zenity --text-info --title "Disk space" --filename=$temp
  --width 750 --height 10
}
```

```bash
function whose {
  who > $temp
  zenity --text-info --title "Logged in users" --filename=$temp
  --width 500 --height 10
}
```

```bash
function memusage {
  cat /proc/meminfo > $temp
  zenity --text-info --title "Memory usage" --filename=$temp
  --width 300 --height 500
}
```

```bash
while [ 1 ]

  zenity --list --radiolist --title "Sys Admin Menu" --column "Select" \
  --column "Menu Item" FALSE "Display disk space" FALSE "Display users" \
  FALSE "Display memory usage" FALSE "Exit" > $temp2
  if [ $? -eq 1 ]
    then
      break
```

```bash
selection=`cat $temp2`
case $selection in
  "Display disk space")
    diskspace ;;
  "Display users")
    whose ;;
  "Display memory usage")
    memusage ;;
  "Exit")
    break ;;
  *)
    zenity --info "Sorry, invalid selection" ;;
esac
done
```

# 图 15-13

使用 zenity 的系统管理员菜单

![](img/adcbcf1053b52dbf22f3aa187738232f_448_0.png)

由于 zenity 不支持 `dialog` 对话框，我在主菜单使用了 `radiolist`，如图 15-13 所示。`radiolist` 使用两列，每列都有标题。第一列用于选择的单选按钮，第二列是项目。`radiolist` 也没有为项目使用标签。当你选择一个项目时，该项目的完整文本将返回到 STDOUT。这让 `case` 命令变得变得有趣得多。如果文本中有任何空格，`zenity` 包可以为你的 shell 脚本增添活力。

# 总结

交互式 shell 脚本被认为是枯燥无味的。你可以通过使用 Linux 系统提供的不同技术和工具来改变这一点。首先，你可以使用 `case` 命令为交互式脚本创建菜单，并使用 `read` 命令读取用户的响应。然后，`case` 命令根据输入的值选择合适的 shell 函数。

你可以使用 ANSI 控制代码来活跃文本菜单，设置如闪烁和粗体等颜色。通常，更改菜单的颜色有助于让脚本体验更加愉快。`dialog` 程序提供了几个预构建的组件，用于创建文本对象。你可以使用 `dialog` 程序创建用于显示文本、选择文件和日期的对话框。这为你的 shell 脚本注入了更多活力。

如果你在图形环境中运行 shell 脚本，你可以在交互式脚本中使用更多工具。对于 KDE 桌面，有一个 `kdialog` 程序，它为所有功能提供了组件。对于 GNOME 桌面，有 `dialog` 和 `zenity` 程序。这些程序提供的组件可以像真正的应用程序一样完美融入桌面。

下一章将深入探讨编辑和操作文本文件的主题。通常，shell 脚本最大的用途是围绕解析和显示文本文件（如日志文件）中的数据。Linux 环境包含了两个非常有用的工具 `sed` 和 `awk` 用于在 shell 脚本中处理文本数据。下一章将向你介绍这些工具并展示它们的基本用法。

# 第 16 章：介绍 sed 和 awk

- 本章内容
- 处理文本文件
- 发现 sed
- 探索 awk

## 文本操作

第 7 章展示了如何使用 Linux 环境中不同的编辑器程序来编辑文本文件。这些编辑器允许你通过简单的命令或鼠标点击来轻松操作文本文件中包含的文本。

但有时你会发现自己想要即时操作文件中的文本，而无需调出一个完整的交互式编辑器。在这些情况下，拥有一个简单的命令行编辑器，可以自动格式化、插入、修改或删除文本元素将是非常用的。

Linux 系统提供了两个常用的工具来实现这一目标。本节描述了 Linux 世界中使用的两种流行的命令行编辑器：`sed` 和 `awk`。

# sed 编辑器

`sed` 编辑器被称为流编辑器，与普通的交互式文本编辑器不同。在像 `vim` 这样的交互式文本编辑器中，你交互式地使用键盘命令在数据中插入、删除或替换文本。流编辑器根据你预先提供的一组规则在编辑器处理数据之前对数据流进行编辑。

`sed` 编辑器可以根据你在命令行输入的命令或存储在命令文件中的命令来操作数据流中的数据。它每次从输入中读取一行数据，与提供的命令进行匹配，然后将流中的新数据输出到 STDOUT。当流编辑器对行数据匹配所有命令后，它读取下一行数据并重复该过程。当流编辑器处理完流中的所有数据行后就会终止。

由于命令是按行顺序应用的，`sed` 编辑器只需要对数据流通过一次即可完成编辑。这使得 `sed` 编辑器比交互式编辑器快得多，允许你快速地对数据文件进行更改。

使用 `sed` 命令的格式为：

```bash
sed options script file
```

`options` 参数允许你自定义 `sed` 命令的行为，包括表 16-1 所示的选项。

### 表 16-1
sed 命令选项
| 选项 | 描述 |
| :--- | :--- |
| -e script | 将脚本中指定的命令添加到处理输入时运行的命令中。 |
| -f file | 将文件中指定的命令添加到处理输入时运行的命令中。 |
| -n | 不为每个命令产生输出，而是等待打印 命令。 |

