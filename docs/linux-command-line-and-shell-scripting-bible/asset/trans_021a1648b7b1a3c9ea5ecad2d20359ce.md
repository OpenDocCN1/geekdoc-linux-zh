

当在 xterm 会话窗口中点击鼠标按键（右手鼠标的左键，或左手形鼠标的右键）时。图 2-4 显示了 xterm 主菜单的内容。

xterm 主菜单包含四个部分，将在后续章节介绍。

## X 事件命令

X 事件命令部分包含了允许你管理 xterm 与 X Window 显示器（display）交互的功能。

- **工具栏 (Toolbar):** 如果 xterm 安装支持工具栏，此选项将启用或禁用 xterm 窗口中工具栏的显示（与 `-tb` 命令行参数相同）。
- **安全键盘 (Secure Keyboard):** 将键盘按键限制在特定的 xterm 窗口中。这在输入密码时非常有用，可以确保密码不会被另一个窗口劫持。
- **允许发送事件 (Allow SendEvents):** 允许 xterm 窗口接受由其他 X Window 应用程序生成的 X 事件。
- **重绘窗口 (Redraw Window):** 指令 X Window 刷新 xterm 窗口。

## 图 2-4

xterm 主菜单

![](img/adcbcf1053b52dbf22f3aa187738232f_70_0.png)

# 第一部分 Linux 命令行

再次，所有这些功能都不可能由你特定的 xterm 实现支持。如果不支持，它们将在菜单中显示为灰色。

## 输出捕获

xterm 软件包允许你捕获窗口中显示的数据，并将其记录到文件中或发送到 X Windows 中定义的默认打印机。本节中出现的功能包括：

- 志记到文件 (Log to file): 将 xterm 窗口中显示的所有数据发送到文本文件。
- 打印窗口 (Print window): 将当前窗口中显示的所有数据发送到默认 X Window 打印机。
- 重定向到打印机 (Redirect to printer): 同样将 xterm 窗口中显示的所有数据发送到默认 X 打印机。必须关闭此功能才能停止打印数据。

如果你在显示区域使用图形或控制字符（例如彩色文本），捕捉功能可能会变得混乱。所有到显示器的字符（包括控制字符）都会存储在日志文件中或发送到打印机。

xterm 打印功能假设你已经在 X Window 系统中了默认打印机。如果你没有定义打印机，该功能将在菜单中显示为灰色。

## 键盘设置

键盘设置部分提供了允许自定义 xterm 如何向主机系统发送键盘字符的功能。

- **8 位控制 (8-bit controls):** 发送 8 位控制代码（用于 VT220 终端），而不是 7 位 ASCII 控制代码。
- **后退箭头键 (Backarrow key):** 在发送退格字符（backspace）或删除字符（delete）之间切换。
- **Alt/Numlock 修饰键 (Alt/Numlock Modifiers):** 控制 Alt 或 Numlock 键是否改变 PC 数字键盘的行为。
- **Alt 发送 Escape (Alt Sends Escape):** Alt 键连同其他按键一起发送退出控制代码。
- **Meta 发送 Escape (Meta sends Escape):** 控制功能键是否发送包含退出控制代码内的双字符控制代码。
- **Delete 为 DEL (Delete is DEL):** PC Delete 键发送删除字符而不是退格字符。
- **旧功能键 (Old Function keys):** PC 键模拟 DEC VT100 功能键。
- **HP 功能键 (HP Function keys):** PC 功能键模拟 HP 终端功能键。
- **Sun 功能键 (Sun Function keys):** PC 功能键模拟 Sun 工作站功能键。
- **VT220 键盘 (VT220 keyboard):** PC 功能键模拟 DEC VT220 功能键。

如你所见，设置键盘偏好通常取决于你所处的特定应用程序和环境。这也涉及到大量的个人偏好。这取决于哪种键盘设置对你来说最有效。

## VT 选项菜单

VT 选项菜单包含 xterm 在 VT102 仿真中使用的功能。你通过按住 Control 键并点击第二个鼠标键来访问 VT 选项菜单。通常情况下，第二个鼠标键是中间键。如果你使用的是双键鼠标，大多数 Linux X Window 配置会在你同时点击左键和右键时模拟中间键键。图 2-5 显示了 VT 选项菜单的内容。

从图 2-5 可以看到，许多可以从命令行参数设置的 VT 功能也可以从 VT 选项菜单进行设置。这产生了一个相当大的可用列表。VT 选项分为三组命令，将在后续章节中描述。

图 2-5

xterm 选项菜单

![](img/adcbcf1053b52dbf22f3aa187738232f_72_0.png)

## VT 功能

VT 功能命令更改 xterm 实现 VT102/220 仿真的方式。它们包括：

- 启用滚动条 (Enable Scrollbar)
- 启用跳转滚动条 (Enable Jump Scrollbar)
- 启用反显 (Enable Reverse Video)
- 启用自动换行 (Enable Auto Wraparound)
- 启用反向换行 (Enable Reverse Wraparound)
- 启用自动行 (Enable Auto Linefeed)
- 启用应用程序光键 (Enable Application Cursor Keys)
- 启用应用程序数字键盘 (Enable Application Keypad)
- 按键时滚动到底部 (Scroll to Bottom on Keypress)
- TTY 输出时滚动到底部 (Scroll to Bottom on TTY Output)
- 允许 80/132 列切换 (Allow 80/132 Column Switching)
- 选择到剪贴板 (Select to Clipboard)
- 启用视觉蜂铃 (Enable Visual Bell)
- 蜂铃时弹出 (Enable Pop on Bell)
- 启用边缘蜂铃 (Enable Margin Bell)
- 启用备用屏幕切换 (Enable Alternate Screen Switching)
- 启用活动图标 (Enable Active Icon)

你可以通过点击菜单中的功能来启用或禁用这些功能之一。启用的功能旁边会有一个勾标记。

## VT 命令

VT 命令部分向 xterm 仿真窗口发送特定的重置命令。它们包括：

- 执行软重置 (Do Soft Reset)
- 执行完全重置 (Do Full Reset)
- 重置并清除保存行 (Reset and Clear Saved Lines)

软重置发送一个控制代码来重置屏幕区域。如果程序错误设置了滚动区域，这将非常方便。完全重置会清除屏幕、重置任何制表符位置，并将会话期间设置的任何终端模式功能重置为初始状态。重置并清除保存行命令执行完全重置，还会清除滚动区域历史文件。

## 进入 Shell

## 当前屏幕命令

当前屏幕命令向 xterm 仿真器发送命令，影响哪个屏幕是当前活动屏幕。

- 显示 Tek 窗口 (Show Tek Window): 显示 Tektronix 窗口。
- 切换到 Tek 窗口 (Switch to Tek Window): 隐藏 VT100 窗口。
- 隐藏 VT 窗口 (Hide VT Window): 隐藏 Tektronix 窗口。
- 显示备用屏幕 (Show Alternate Screen): 显示备用区域。

xterm 仿真器提供了以 VT100 模式（默认）或 Tektronix 模式（使用命令行参数）启动的能力。启动其中一种模式后，你可以使用此菜单切换到另一种模式。

## VT 字体菜单

VT 字体菜单设置在 VT102/220 仿真中使用的字体。你可以通过按住 Control 键并点击鼠标键（右手鼠标的右键，或左手形鼠标的左键）来访问此菜单。图 2-6 显示了 VT 选项菜单的内容。

图 2-6

xterm 菜单

![](img/adcbcf1053b52dbf22f3aa187738232f_74_0.png)

# 第一部分 Linux 命令行

VT 字体菜单在后续章节介绍，包含三组选择。

## 设置字体

这些菜单选项设置 xterm 窗口中使用的字体大小。可用大小有：

- 默认 (Default)
- 不可读 (Unreadable)
- 极小 (Tiny)
- 小 (Small)
- 中等 (Medium)
- 大 (Large)
- 巨大 (Huge)
- 转义序列 (Escape Sequence)
- 选择 (Selection)

默认字体是用于在当前 X 窗口中显示文本的标准字体。不可读字体正如其名，它将 xterm 窗口缩小到实际上无法使用的尺寸。然而，当你想要在桌面上最小化窗口而不完全最小化时，这非常有用。巨大字体选项为视觉障碍用户提供了巨大的字体。

转义序列选项将字体设置为 VT100 设置字体控制代码设置的字体。选择选项允许你使用特殊的字体名称保存当前字体。

## 显示字体

此部分的选项定义了创建文本的字符类型。有两个可用选项：

- 绘线字符 (Line Drawing Characters): 指令 Linux 系统产生 ANSI 图形线条，而不是使用所选字体中的线条。
- 双倍字符 (Doubledized characters): 指令 Linux 系统将设置的字体缩放到正常大小的两倍。
