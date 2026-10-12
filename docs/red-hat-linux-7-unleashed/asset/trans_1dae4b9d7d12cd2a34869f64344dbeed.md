
## 更改窗口操作

在控制中心的模块菜单下，点击外观与感觉、窗口行为、操作菜单项。该对话框（如图 5.21 所示）用于设置窗口的布局以及确定焦点策略。

### 图 5.20
左利手鼠标用户可以受益于 KDE 灵活的鼠标配置！

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_170_0.png)

### 图 5.21
使用窗口对话框更改 KDE 会话期间窗口的行为。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_170_1.png)

焦点策略部分告诉 KDE 如何使窗口处于活动状态。默认操作是，你必须点击窗口以激活它或使其能够接收键盘输入；其他策略则会在鼠标指针悬停在窗口上方时激活该窗口。

## 使用键盘控制光标

KDE 的一项新功能是可访问性对话框（如图 5.22 所示）。此功能允许你使用计算机键盘通过数字键盘（笔记本电脑用户可能会觉得这有点不便，但它是有效的）来移动鼠标。选择模块菜单中的个性化菜单，然后点击可访问性菜单项。接下来，在对话框中点击鼠标选项卡，并勾选通过键盘移动鼠标（使用数字键盘）复选框。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_171_0.png)

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_171_1.png)

其他可访问性选项包括可视铃声，以及粘滞键、慢速键和防抖键（用于帮助人们在需要同时按下两个或更多按键时单手输入按键）。

## 控制 KDE 桌面边框

通过控制中心的模块菜单，然后选择外观与感觉、桌面和边框菜单项访问的边框对话框，用于控制虚拟桌面之间的光标移动。默认情况下，你必须点击桌面板上的虚拟桌面按钮才能在桌面之间移动。如果你在边框对话框（如图 5.23 所示）中点击启用活动桌面边框项，然后点击应用按钮，你就可以通过将鼠标光标移动到当前桌面边缘来切换到不同的桌面。

**注意**
不想点击面板上的桌面按钮或将鼠标拖动到边缘来移动桌面吗？改用键盘！按 `Ctrl+Tab` 遍历桌面（会出现一个弹出窗口）。按 `Alt+Tab` 遍历（激活）当前桌面中的窗口。

你还可以拖动不同的滑块来设置桌面切换的时间延迟以及每个桌面敏感边缘的宽度。

### 图 5.23
边框对话框用于告诉 KDE 是否使用鼠标在桌面之间移动，切换速度有多快，以及何时进行切换。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_172_0.png)

## fvwm2 窗口管理器

fvwm2 窗口管理器（如图 5.24 所示）具有可配置的任务栏、3D 窗口边框、按钮、滚动条以及广泛的自定义能力。该窗口管理器的自定义配置是红帽 Linux 在早期红帽发行版中提供的几个复杂且流行的 X 桌面（如 TheNextStep 和 AnotherLevel!）的基础。

该窗口管理器的默认启动文件位于 /etc/X11/fvwm2 目录下，名为 system.fvwm2rc。将此文件复制到你的主目录并重命名为 .fvwm2rc，然后进行修改以自定义你的 X 会话。要使用 fvwm2，请在你的 .xinitrc 文件中插入其名称，并使用 startx 命令启动你的 X 会话。

### 图 5.24
fvwm2 窗口管理器具有基本的窗口管理器功能，例如其虚拟桌面的分页器。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_173_0.png)

fvwm2 的启动文件包含用于自定义窗口颜色和样式、菜单、键盘操作以及虚拟桌面数量的部分。查找桌面部分，其内容如下：

```
DeskTopSize 2x2
```

fvwm2 的默认启动文件定义了四个不同的虚拟桌面。通过更改 DeskTopSize 值，你可以减少或增加虚拟桌面的数量。例如，使用类似以下的设置可以另外添加两个桌面：

```
DeskTopSize 2x3
```

当你重启 fvwm2 时，你会看到 fvwm2 分页器窗口中额外增加了两个桌面。你可以通过在桌面分页器窗口中相应的方块上按下鼠标左键来移动到不同的桌面。然而，你可以做的另一个修改可能会成为救命稻草，特别是当你的计算机鼠标损坏或者你想仅使用键盘移动指针时，即插入定义以启用方向键切换到不同的桌面或移动指针！

滚动你的 .fvwm2rc 文件，直到找到默认的 Key 定义：

```
# some simple default key bindings:
Key Next A SCM Next [ ] Focus
Key Prior A SCM Prev [ ] Focus
```

添加以下光标键定义：

```
# Shift + Ctrl moves 1 page in direction
Key Left A CS Scroll -100 +0
Key Right A CS Scroll +100 +0
Key Up A CS Scroll +0 -100
Key Down A CS Scroll +0 +100
```

这些定义指定了 `Shift+Ctrl+方向键X`，它会将你的桌面切换到 X 方向上下一个可用的桌面。这意味着你可以在不使用鼠标的情况下在桌面之间移动！接下来，插入以下定义：

```
# Alt + Shift move 1/10 page in direction
Key Left A MS Scroll -10 +0
Key Right A MS Scroll +10 +0
Key Up A MS Scroll +0 -10
Key Down A MS Scroll +0 +10
```

这些定义指定了 `Alt+Shift+方向键X`，它会将当前桌面沿指定的 X 方向移动 1/10 页。这意味着你可以通过移动屏幕来处理窗口超出当前桌面边框的客户端！最后，添加可能最有用的定义：

```
# Alt + Ctrl move cursor 1/100 page in direction
Key Left A CM CursorMove -1 +0
Key Right A CM CursorMove +1 +0
Key Up A CM CursorMove +0 -1
Key Down A CM CursorMove +0 +1
```

这些定义指定了 `Alt+Ctrl+方向键X`，它会将你的鼠标指针沿指定方向移动当前页面宽度的 1/100。这种分辨率足以处理几乎每个桌面。完成更改后，使用 fvwm2 的根菜单（在桌面的空白区域点击鼠标左键）来重启窗口管理器。这将立即使你的更改生效。

你可能还希望定义额外的按键（如 F 键）与 `Alt` 或 `Ctrl` 结合使用，以模拟鼠标按键按下或根菜单操作。这是创建无指针 X11 环境的一种便捷方式！有关创建自定义定义的提示可以在 fvwm2 的手册页中找到。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_174_0.png)

## twm 窗口管理器

twm，即标签窗口管理器（如图 5.25 所示），随 XFree86 X Window 发行版一起提供。安装在 /usr/X11R6/bin 目录下，此窗口管理器提供 X 窗口管理的基本功能：

- 自定义键盘命令
- 自定义鼠标命令
- 图标停靠区
- 图标
- 可调整大小的窗口
- 窗口标题

### 图 5.25
twm 为你的 X 会话提供基本的窗口操作。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_175_0.png)

你可以在 /etc/X11/twm 目录下找到 twm 的系统范围配置文件 system.twmrc。该文件包含你可以修改和使用的默认定义。将 system.twmrc 复制到你主目录中的 .twmrc 以进行修改。你可以通过在 .xinitrc 文件中插入 twm 命令来使用 twm。

twm 的默认启动文件，定义了 twm 的根菜单（通过按压在桌面空白处的鼠标左键访问），现在包含一个终端的菜单项定义。你肯定希望自定义此菜单以添加其他客户端。在使用 twm 之前，打开你最喜欢的文本编辑器（如 pico，其中 `-w` 选项禁用了自动换行）中的 `.twmrc` 副本：

```
# pico -w .twmrc
```

查找定义根菜单的部分：

```
menu "defops" {
  "Twm" f.title
  "Iconify" f.iconify
  "Resize" f.resize
  "Move" f.move
  "Raise" f.raise
  "Lower" f.lower
  "---------" f.nop
  "Focus" f.focus
  "Unfocus" f.unfocus
  "Show Iconmgr" f.showiconmgr
  "Hide Iconmgr" f.hideiconmgr
  "------" f.nop
  "Xterm" f.exec "exec xterm &"
  "-----" f.nop
  "Kill" f.destroy
  "Delete" f.delete
  "--------" f.nop
  "Restart" f.restart
  "Exit" f.quit
}
```

`.twmrc` 的这一部分包含根菜单标签，随后是适用于 twm 窗口管理器的相应命令。例如，要“杀死”一个窗口，你在桌面上按下鼠标左键，向下拖动以选择“杀死”菜单项，然后在目标窗口上方按下鼠标按钮——twm 随后会移除选定的窗口。

现在插入一个菜单定义，以创建并显示当前月份的日历，如下所示：

```
menu "defops" {
  "Twm" f.title
  "Iconify" f.iconify
  "Resize" f.resize
  "Move" f.move
  "Raise" f.raise
  "Lower" f.lower
  "---------" f.nop
  "Focus" f.focus
  "Unfocus" f.unfocus
  "Show Iconmgr" f.showiconmgr
  "Hide Iconmgr" f.hideiconmgr
```

