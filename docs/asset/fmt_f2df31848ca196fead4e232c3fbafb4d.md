
> 您的 Linux 发行版使用 KDE 桌面环境并不意味着它默认安装了 `kdialog` 软件包。您可能需要手动从发行版仓库中安装它。

### kdialog 小部件

与 `dialog` 命令类似，`kdialog` 命令使用命令行选项来指定要使用的窗口小部件类型。`kdialog` 命令的格式如下：

```bash
kdialog display-options window-options arguments
```

`display-options` 允许您自定义窗口小部件，例如添加标题或更改颜色。`window-options` 允许您指定要使用的窗口小部件类型。可用选项如表 18.3 所示。

#### 表 18.3 kdialog 窗口选项

| 选项 | 描述 |
| :--- | :--- |
| `--checklist title [tag item status]` | 复选框列表菜单，其中 status 指定项目是否已勾选 |
| `--error text` | 错误消息框 |
| `--inputbox text [init]` | 输入文本框，您可以使用 init 值指定默认值 |
| `--menu title [tag item]` | 菜单选择框标题以及由标签标识的项目列表 |
| `--msgbox text` | 带有指定文本的简单消息框 |
| `--password text` | 隐藏用户输入的密码输入文本框 |
| `--radiolist title [tag item status]` | 单选列表菜单，其中 status 指定项目是否已选中 |
| `--separate-output` | 针对复选框和单选列表菜单，逐行返回项目 |
| `--sorry text` | 抱歉消息框 |
| `--textbox file [width] [height]` | 显示文件内容的文本框，替代方式是通过宽度和高度指定 |
| `--title title` | 为 TitleBar 区域指定标题 |

### 使用 kdialog

你可以在 shell 脚本中使用 `kdialog` 窗口组件，方式类似于使用 `dialog` 组件。主要的区别在于，`kdialog` 窗口组件使用 `STDOUT` 而不是 `STDERR` 来输出值。下面是一个脚本，它将之前创建的系统管理菜单转换为一个 KDE 应用程序：

```bash
$ cat menu4
#!/bin/bash
# using kdialog to create a menu

temp=$(mktemp -t temp.XXXXXX)
temp2=$(mktemp -t temp2.XXXXXX)

function diskspace {
  df -k> $temp
  kdialog --textbox $temp 1000 10
}

function whoseon {
  who> $temp
  kdialog --textbox $temp 500 10
}

function memusage {
  cat /proc/meminfo> $temp
  kdialog --textbox $temp 300 500
}

while [ 1 ]
do
kdialog --menu "Sys Admin Menu" "1" "Display disk space" "2" "Display users" "3" "Display memory usage" "0" "Exit"> $temp2
if [ $? -eq 1 ]
then
  break
fi

selection=$(cat $temp2)

case $selection in
1)
  diskspace ;;
2)
  whoseon ;;
3) memusage ;;
0) break ;;
*)
    kdialog --msgbox "Sorry, invalid selection"
esac
done
$
```

使用 `kdialog` 命令的脚本与使用 `dialog` 命令的脚本没有太大区别。生成后的主菜单如图 18-10 所示。

![](img/a5025f22e05b92f409563a958cac7312_675_0.png)

**图 18-10** 使用 `kdialog` 的系统管理菜单脚本

现在，你简单的 shell 脚本看起来就像一个真正的 KDE 应用程序！现在你可以用交互式脚本做的事情没有上限。

### GNOME 环境

GNOME 图形环境支持两个可以生成标准窗口的流行软件包：

- `gdialog`
- `zenity`

迄今为止，`zenity` 是大多数 GNOME 桌面 Linux 发行版中最常见的软件包（在 Ubuntu 和 CentOS 中默认安装）。本节将描述 `zenity` 的功能，并演示如何在你的 shell 脚本中使用它。

#### zenity 组件

正如你所预期的那样，`zenity` 允许你通过使用命令行选项来创建不同的窗口组件。表 18.4 展示了 `zenity` 可以生成的各种组件。

**表 18.4** zenity 窗口组件

| 选项 | 描述 |
| :--- | :--- |
| `--calendar` | 显示完整的月份日历 |
| `--entry` | 显示文本输入对话框窗口 |
| `--error` | 显示错误消息对话框窗口 |
| `--file-selection` | 显示完整路径名和文件名对话框窗口 |
| `--info` | 显示信息对话框窗口 |
| `--list` | 显示检查列表或单选列表对话框窗口 |
| `--notification` | 显示通知图标 |
| `--progress` | 显示进度条对话框窗口 |
| `--question` | 显示是/否问题对话框窗口 |
| `--scale` | 显示带有滑动条以在范围内选择值的比例对话框窗口 |
| `--text-info` | 显示包含文本的文本框 |
| `--warning` | 显示警告对话框窗口 |

`zenity` 命令行程序的工作方式与 `kdialog` 和 `dialog` 程序略有不同。许多组件类型是通过在命令行上使用额外选项来定义的，而不是作为某个选项的参数包含在内。

`zenity` 命令确实提供了一些相当酷的高级对话框窗口。`--calendar` 选项会生成一个完整的月份日历，如图 18-11 所示。

![](img/a5025f22e05b92f409563a958cac7312_677_0.png)

**图 18-11** `zenity` 日历对话框窗口

当你从日历中选择一个日期时，`zenity` 命令将该值返回给 `STDOUT`，就像 `kdialog` 一样：

```bash
$ zenity --calendar
12/25/2011
$
```

![](img/a5025f22e05b92f409563a958cac7312_678_0.png)

**图 18-12** `zenity` 文件选择对话框窗口

`zenity` 中另一个相当酷的功能是文件选择选项，如图 18-12 所示。

你可以使用该对话框窗口浏览到系统上的任何目录位置（只要你拥有查看该目录的权限）并选择一个文件。当你选择一个文件时，`zenity` 命令返回完整的文件和路径名：

```bash
$ zenity --file-selection
/home/ubuntu/menu5
$
```

有了像这样的工具，你的 shell 脚本创作的可能性将无限广阔！

#### 在脚本中使用 zenity

正如你所预期的，`zenity` 在 shell 脚本中表现良好。不幸的是，`zenity` 的创建者选择不遵循 `dialog` 和 `kdialog` 中使用的选项约定，因此将任何现有的交互式脚本转换为 `zenity` 可能会具有挑战性。

在将系统管理菜单从 `kdialog` 转换为 `zenity` 时，我们需要对组件定义进行大量的操作：
