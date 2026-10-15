
| `calendar` | 提供一个可以从中选择日期的日历 |
| `checklist` | 显示多个条目，每个条目都可以开启或关闭 |
| `form` | 允许构建带有标签和待填充文本字段的表单 |
| `fselect` | 提供文件选择以浏览文件 |
| `gauge` | 显示显示完成百分比的仪表表 |
| `infobox` | 显示消息而不等待响应 |
| `inputbox` | 显示一个用于文本录入单文本框 |
| `inputmenu` | 提供一个可编辑的菜单 |
| `menu` | 显示一个选择列表，从中进行选择 |

# 第 18 章：为图形桌面编写脚本

| | |
|---|---|
| `msgbox` | 显示一条消息并要求用户选择 OK 按钮 |
| `pause` | 显示显示指定暂停期间状态的仪表表 |
| `passwordbox` | 显示一个隐藏输入文本的单文本框 |
| `passwordform` | 显示一个带有标签和隐藏文本字段的表单 |
| `radiolist` | 提供一组菜单项，其中只能选择一个项 |
| `tailbox` | 使用 `tail` 命令在滚动窗口中显示文件文本 |
| `tailboxbg` | 与 `tailbox` 相同，但在后台模式下运行 |
| `textbox` | 在滚动窗口中显示文件内容 |
| `timebox` | 提供一个选择小时、分钟和秒的窗口 |
| `yesno` | 提供一个带有 Yes 和 No 按钮的简单消息 |

如表 18-1 所示，你可以从许多不同的控件中进行选择。这可以让你付出极少努力就让你的脚本看起来更专业。

要在命令行上指定控件，你需要使用双破折线格式：

```
dialog --widget parameters
```

其中 `widget` 是表 18-1 所示的名称，`parameters` 定义了控件窗口的大小以及该控件所需的任何文本。

每个控件都提供两种形式的输出：

字体 使用 STDERR

- 使用退出码状态

`dialog` 命令的退出码状态取决于用户选择按钮。如果选择了 OK 或 Yes，`dialog` 命令返回 0 退出状态。如果选择了 Cancel 或 No 按钮，`dialog` 命令返回 1 退出状态。你可以使用标准 `$` 变量来确定在 `dialog` 控件中选择了哪个按钮。

如果控件返回任何数据（例如菜单选择），`dialog` 命令会将数据发送到 STDERR。你可以使用 bash shell 技术将 STDERR 输出重定向到另一个文件或文件描述符：

```
dialog --inputbox "Enter your age:" 10 20 2>age.txt
```

此命令将输入框中输入的文本重定向到 `age.txt` 文件。

接下来的章节将查看你在 shell 脚本中使用的一些常用 `dialog` 控件的示例。

# 第三部分：高级 Shell 脚本编写

## `msgbox` 控件

`msgbox` 控件是最常见的对话框类型。它在窗口中显示简单的消息，并等待用户点击 OK 后才消失。使用 `msgbox` 控件需要以下格式：

```
dialog --msgbox text height width
```

`text` 参数是你想要放在窗口中的任何字符串。`dialog` 命令会根据使用的 `height` 和 `width` 参数自动对文本换行，以适应你创建的窗口大小。如果你想在窗口顶部放置标题，可以使用 `--title` 参数以及标题文本。这里有一个使用 `msgbox` 控件的示例：

```
$ dialog --title Testing --msgbox "This is a test" 10 20
```

输入此命令后，消息框出现在你正在使用的终端模拟器会屏幕上。18-2 显示了它的样子。

### 18-2

在 `dialog` 命令中使用 `msgbox` 控件

![](img/3d824df0fbf2e68950f7ddee680ca359_521_0.png)

如果你的终端模拟器支持鼠标，你可以点击 OK 按钮关闭对话框。你也可以使用键盘命令模拟点击——只需按 Enter 键即可。

## `yesno` 控件

`yesno` 控件是向用户提问题的简单方法。它显示一条带有两个按钮的消息。使用 `yesno` 控件需要以下格式：

```
dialog --yesno "question text" height width
```

`text` 参数是你想要问的问题。`dialog` 命令会自动对文本换行以适应窗口大小。如果你想在窗口顶部放置标题，可以使用 `--title` 参数以及标题文本。这里有一个使用 `yesno` 控件的示例：

```
$ dialog --title Confirm --yesno "Are you sure?" 10 20
```

输入此命令后，消息框出现在你正在使用的终端模拟器屏幕上。18-3 显示了它的样子。

### 18-3

在 `dialog` 命令中使用 `yesno` 控件

![](img/3d824df0fbf2e68950f7ddee680ca359_522_0.png)

如果你的终端模拟器支持鼠标，你可以点击 OK 按钮关闭对话框。你也可以使用键盘命令模拟点击。

## `inputbox` 控件

`inputbox` 控件允许用户输入单行文本。它显示一个带有 OK 按钮的窗口。使用 `inputbox` 控件需要以下格式：

```
dialog --inputbox text height width
```

`text` 参数是给用户的提示信息。`dialog` 命令会自动对文本换行以适应窗口大小。如果你想在窗口顶部放置标题，可以使用 `--title` 参数以及标题文本。这里有一个使用 `inputbox` 控件的示例：

```
$ dialog --title Input --inputbox "What is your name?" 10 40
```

输入此命令后，消息框出现在你正在使用的终端模拟器屏幕上。18-4 显示了它的样子。

### 18-4

在 `dialog` 命令中使用 `inputbox` 控件

![](img/3d824df0fbf2e68950f7ddee680ca359_523_0.png)

如果你的终端模拟器支持鼠标，你可以点击 OK 按钮关闭对话框。你也可以使用键盘命令模拟点击。

## `textbox` 控件

`textbox` 控件用于显示文件内容。它提供一个包含文件的滚动窗口。使用 `textbox` 控件需要以下格式：

```
dialog --textbox filename height width
```

`filename` 参数是你想要显示的文件的路径。`height` 和 `width` 参数定义窗口的大小。如果你想在窗口顶部放置标题，可以使用 `--title` 参数以及标题文本。这里有一个使用 `textbox` 控件的示例：

```
$ dialog --title "File Content" --textbox /etc/passwd 15 50
```

输入此命令后，消息框出现在你正在使用的终端模拟器屏幕上。18-5 显示了它的样子。

### 18-5

`textbox` 控件

![](img/3d824df0fbf2e68950f7ddee680ca359_524_0.png)

如果你的终端模拟器支持鼠标，你可以使用滚动条浏览文件。你也可以使用键盘命令滚动文件。

## `menu` 控件

`menu` 控件允许用户从列表中选择项。它显示一个包含菜单项的滚动窗口。使用 `menu` 控件需要以下格式：

```
dialog --menu title height width limit tag1 "label1" tag2 "label2" ...
```

`title` 参数定义菜单窗口的标题。`height` 和 `width` 参数定义窗口的大小。`limit` 参数定义一次性显示的项目数量。每个菜单项由一个 `tag` 和一个 `label` 组成。`tag` 用于识别被选中的项，而 `label` 是显示给用户的内容。这里有一个使用 `menu` 控件的示例：

```
$ dialog --menu "Selection" 15 40 5 1 "Disk space" 2 "Users" 3 "Memory usage" 4 "Exit"
```

输入此命令后，菜单出现在你正在使用的终端模拟器屏幕上。18-6 显示了它的样子。

### 18-6

在 `dialog` 命令中使用 `menu` 控件

![](img/3d824df0fbf2e68950f7ddee680ca359_525_0.png)

# 第三部分：高级 Shell 脚本

图 18-6

带有菜单-Virtual-Platform: ~ 的菜单组件

![](img/3d824df0fbf2e68950f7ddee680ca359_525_0.png)

如果用户通过按下对应标签的键来选择菜单项，该菜单项会被高亮但不会被选中。只有使用鼠标或 Enter 键选择 OK 按钮后才会完成选择。`dialog` 命令会将选中的菜单项文本发送到 stderr，你可以根据需要对其进行重定向。
