
## 第三部分：高级 Shell 脚本编程

### 图 18.5
*textbox*（文本框）组件。

![](img/0798d50a0e5dbf1265fbda3832b3e015_467_0.png)

您可以使用箭头键在文本文件中左右滚动，也可以上下滚动。窗口底部的行显示当前查看位置在文件中的百分比。*textbox*（文本框）组件仅包含一个 Exit（退出）按钮，选择该按钮即可退出组件。

## *menu*（菜单）组件

*menu*（菜单）组件允许您创建本章前面提到的文本菜单的窗口版本。您只需提供每个项目的选择标签和文本即可：

```bash
$ dialog --menu "Sys Admin Menu" 20 30 10 1 "Display disk space" \
  2 "Display users" 3 "Display memory usage" 4 "Exit" 2> test.txt
```

第一个参数定义菜单的标题。接下来的两个参数定义菜单窗口的高度和宽度，第三个参数定义窗口中一次显示的菜单项目数量。如果菜单项目更多，您可以使用箭头键滚动查看。

在这些参数之后，必须添加菜单项目对。第一个元素是用于选择菜单项目的标签。每个菜单项目的标签都应是唯一的，并且可以通过按下键盘上相应的键来选择。第二个元素是菜单中使用的文本。图 18.6 展示了该示例命令生成的菜单。

如果用户通过按下标签对应的适当按键来选择菜单项目，该菜单项目会被高亮显示但未被选中。只有在使用鼠标或 Enter 键选中 OK（确定）按钮时，才会做出选择。`dialog` 命令将选中的菜单项目文本发送到 STDERR，您可以按需重定向它。

## 第 18 章：为图形桌面编写脚本

### 图 18.6
带有菜单项目的菜单组件。

![](img/0798d50a0e5dbf1265fbda3832b3e015_468_0.png)

## fselect 组件

dialog 命令提供了几个功能强大的内置组件。fselect 组件在处理文件名时极其方便。您不必强制用户输入文件名，而是可以允许他们使用 fselect 组件浏览到文件位置并选择文件，如图 18.7 所示。

### 图 18.7
fselect 组件。

![](img/0798d50a0e5dbf1265fbda3832b3e015_468_1.png)

`fselect` 组件的格式如下：

```bash
$ dialog --title "Select a file" --fselect $HOME/ 10 50 2>file.txt
```

`fselect` 选项后的第一个参数是窗口中使用的起始文件夹位置。`fselect` 组件窗口左侧是目录列表，右侧是显示所选目录中所有文件的文件列表，还有一个包含当前选定文件或目录的简单文本框。您可以在文本框中手动输入文件名，也可以使用目录和文件列表选择一个（使用空格键选择要添加到文本框中的文件）。

## dialog 选项

除了标准组件外，您还可以在 `dialog` 命令中自定义许多不同的选项。您已经见过 `--title` 参数的作用。该参数允许您设置组件的标题，该标题显示在窗口的顶部。

许多其他选项允许您完全自定义窗口的外观和行为。表 18.2 显示了 `dialog` 命令可用的选项。

### 表 18.2 dialog 命令选项

| 选项 | 描述 |
| :--- | :--- |
| `--add-widget` | 除非按下 Esc 键或点击 Cancel 按钮，否则继续下一个对话框 |
| `--aspect-ratio` | 指定窗口的宽/高长宽比 |
| `--backtitle title` | 指定显示在屏幕顶部背景上的标题 |
| `--begin x y` | 指定窗口左上角的起始位置 |
| `--cancel-label label` | 为 Cancel 按钮指定替代标签 |
| `--clear` | 使用默认对话框背景色清除显示 |
| `--colors` | 在对话框文本中嵌入 ANSI 颜色代码 |
| `--cr-wrap` | 允许对话框文本中包含换行符并强制换行 |
| `--create-rc file` | 将示例配置文件转储到指定文件 |
| `--defaultno` | 将 yes/no 对话框的默认值设为 No |
| `--default-item string` | 设置清单、表单或菜单对话框中的默认项目 |
| `--exit-label label` | 为 Exit 按钮指定替代标签 |
| `--extra-button` | 在 OK 和 Cancel 按钮之间显示一个额外按钮 |
| `--extra-label label` | 为 Extra 按钮指定替代标签 |
| `--help` | 显示 `dialog` 命令的帮助信息 |
| `--help-button` | 在 OK 和 Cancel 按钮后显示一个 Help 按钮 |
| `--help-label label` | 为 Help 按钮指定替代标签 |
| `--help-status` | 如果点击了 Help 按钮，在帮助信息后写入清单、单选列表或表单信息 |
| `--ignore` | 忽略 dialog 不识别的选项 |
| `--input-fd fd` | 指定除 STDIN 以外的文件描述符 |
| `--insecure` | 将密码组件更改为输入时显示星号 |
| `--item-help` | 为清单、单选列表或菜单中的每个标签项在屏幕底部添加一个帮助列 |
| `--keep-window` | 不清除屏幕上的旧组件 |
| `--max-input size` | 指定输入的最大字符串大小；默认值为 2048 |
| `--nocancel` | 抑制 Cancel 按钮 |
| `--no-collapse` | 不将对话框文本中的制表符转换为空格 |
| `--no-kill` | 将 tailboxbg 对话框置于后台并禁用该进程的 SIGHUP |
| `--no-label label` | 为 No 按钮指定替代标签 |
| `--no-shadow` | 不显示对话框窗口的阴影 |
| `--ok-label label` | 为 OK 按钮指定替代标签 |
| `--output-fd fd` | 指定除 STDERR 以外的输出文件描述符 |
| `--print-maxsize` | 将允许的对话框窗口最大尺寸打印到输出 |
| `--print-size` | 将每个对话框窗口的尺寸打印到输出 |
| `--print-version` | 将 dialog 版本打印到输出 |
| `--separate-output` | 逐行输出清单组件的结果，不加引号 |
| `--separator string` | 指定分隔每个组件输出的字符串 |
| `--separate-widget string` | 指定分隔每个组件输出的字符串 |
| `--shadow` | 在每个窗口的右侧和底部绘制阴影 |
| `--single-quoted` | 如果清单输出需要，则使用单引号 |
| `--sleep sec` | 在处理完对话框窗口后延迟指定秒数 |
| `--stderr` | 将输出发送到 STDERR——默认行为 |
| `--stdout` | 将输出发送到 STDOUT |
| `--tab-correct` | 将制表符转换为空格 |
| `--tab-len n` | 指定制表符使用的空格数量；默认值为 8 |
| `--timeout sec` | 如果无用户输入，指定在退出并返回错误代码之前的秒数 |
| `--title title` | 指定对话框窗口的标题 |
| `--trim` | 删除对话框文本中的前导空格和换行符 |
| `--visit-items` | 修改对话框窗口中的制表位以包含项目列表 |
| `--yes-label label` | 为 Yes 按钮指定替代标签 |

`--backtitle` 选项是通过脚本为菜单创建通用标题的便捷方式。如果您为每个对话框窗口指定它，它将在您的应用程序中持续存在，为您的脚本创造专业的视觉效果。

如您从表 18.2 中可以看出，您可以覆盖对话框窗口中任何按钮的标签。此功能允许您创建几乎任何您需要的窗口情况。

### 在脚本中使用 dialog 命令

在脚本中使用 dialog 命令非常简单。只需记住两件事：

- 如果可用 Cancel 或 No 按钮，请检查 dialog 命令的退出状态。
- 重定向 STDERR 以获取输出值。

如果您遵循这两个规则，很快就能拥有一个外观专业的交互式脚本。以下是一个使用 dialog 组件重现本章前面创建的系统管理员菜单的示例：

```bash
$ cat menu3
#!/bin/bash
# using dialog to create a menu

temp=$(mktemp -t test.XXXXXX)
temp2=$(mktemp -t test2.XXXXXX)

function dipkspace {
df -k > $temp
dialog --textbox $temp 20 60
}

function whoseon {
who > $temp
dialog --textbox $temp 20 50
}
```

