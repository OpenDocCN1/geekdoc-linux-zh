
- `-error` `error_log_file` 指定一个写入错误信息的日志文件。
- `-resources` `resource_file` 指定用于指定认证组件配置参数的文件。
- `-server` `server_entry` 为 `DisplayManager.server` 指定一个值。
- `-udpPort` `port_number` 指定监控 XDMCP 请求的端口号。
- `-session` `session_program` 指定用户登录后运行的程序。
- `-xrm` `resource_specification` 允许像 X Toolkit 一样指定资源。

## xf86config

`xf86config` 生成用于 XFree86 服务器的 X86Config 文件。它是交互式的。

示例：交互式地生成 X86Config 文件：

```
xf86Config
```

### xinit [ [ client ] options ] [ -- server ] [ display ] options ]

`xinit` 程序用于启动 X window 服务器。（通常通过启动脚本调用）。在没有指定客户端的情况下，`xinit` 会在用户主目录查找 `.xinitrc` 文件以获取大部分配置信息。在缺少指定服务器的情况下，`xinit` 在用户主目录查找一个作为 shell 脚本运行的服务器文件。

示例：启动 X Window 服务器：

```
xinit
```

### xmseconfig [-sync] [-display display] [-geometry ]

该程序用于更改服务器的鼠标配置。更改不会保存到下次会话。

示例：配置鼠标：

```
xmseconfig
```

| `-sync` | 同步与服务器的所有 |
| :--- | :--- |
| `-display display` | 指定显示器 |
| `-geometry geometry` | 指定几何 |

## X Window System

## 外观与行为

- `-ah` 高亮文本光标。
+ `-ah` 禁用文本光标。
- `-ai` 禁用图标支持（如果编译进 xterm）。
+ `-ai` 启用图标支持（如果编译进 xterm）。
- `-aw` 允许自动换行。
+ `-aw` 不允许自动换行。
- `-b` 指定窗口与边缘之间的距离。
- `-bdc` 用加粗属性显示字符而不是颜色。
+ `-bdc` 不用加粗属性显示字符而不是颜色。
- `-cb` 将 `vt100` 资源设置为 FALSE。
+ `-cb` 将 `vt100` 资源设置为 TRUE。
- `-cc` 指定使用的字符范围。

## 命令

- `-cm` 禁用 ANSI 颜色序列识别。
+ `-cm` 启用 ANSI 颜色序列识别。
- `-cn` 在行模式下不切换行。
+ `-cn` 在行模式下切换行。
- `-cr` 指定用作为文本光标的颜色。
- `-cu` 使用 `more` 程序。
+ `-cu` 不使用 `more` 程序。
- `-dc` 禁用更改颜色的转义序列。
- `-e` `program [ arguments ]` 指定在 xterm 中运行的程序（以及可选的程序命令行参数）。
- `-fb` 指定用于显示加粗文本的字体。
- `-fi` 设置活动图标的字体，如果该功能已编译进 xterm。
- `-hc` 指定用于选中或或其他高亮文本背景的颜色。如果未指定，则使用反色模式。

## 命令

`343`

`-nul` 启用下划线显示。
`+nul` 禁用下划线显示。
`-pc` 启用 PC 风格粗体颜色。
`+pc` 禁用 PC 风格粗体颜色。
`-rightbar` 强制滚动条位于 VT100 屏幕右侧。
`-rw` 启用反换行。允许光标从当前行的最左列跳转到上一行的最右列。
# 启用反换行。
`+rw` 不允许。
`-s` 允许 xterm 异步滚动。也就是说，在滚动时，不强制 xterm 保持屏幕完全更新。
`+s` 强制 xterm 同步滚动。
`-sb` 开启滚动回。这意味着你最近查看过的行将保存在缓冲区中，可以通过屏幕上的滚动条访问。
`+sb` 不显示滚动条。
`-sf` 为功能键生成转义键转义码。
`+sf` 为功能键生成标准转义序列码。
`-si` 向窗口输出内容后，不自动将屏幕重新定位到滚动区域的底部。
`+si` 向窗口输出内容后，自动将屏幕重新定位到滚动区域的底部。
`-sk` 当按下按键并使用滚动条时，将窗口重新定位到滚动区域底部的正常位置。

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_372_0.png)

# 344

# X Window System

`+ -sk` 当按下按键并使用滚动条时，不重新定位窗口。
`+ -sl number` 指定要保存的屏幕顶部滚动行数（默认 = 64 行）。
`+ -sp` 假设使用 Sun/PC 键盘。
`+ -sp` 为数字键盘和功能键生成标准转义序列。
`+ -t` 以 Tektronix 模式启动 xterm 而非 VT102 模式。
`+ +t` 以 VT102 模式启动 xterm。
`+ -tm string` 指定一系列终端设置关键字，其后紧跟应绑定到这些功能上的字符。允许的关键字包括：intr, qit, erase, kill, eof, eol, switch, start, brk, susp, dusp, rmpnt, flush, weras, 和 inxt。控制字符可以指定为 ^char（例如 ^c 或 ^u），且 ^? 可用于指示删除。
`+ -tn name` 指定在环境变量中设置的终端类型名称。
`+ -ulc` 禁用将具有下划线属性的字符显示为颜色而非下划线。
`+ +ulc` 启用将具有下划线属性的字符显示为颜色而非下划线。
`+ -ut` 不向系统日志文件 `/etc/utmp` 写入记录。
`+ +ut` 将记录写入系统日志文件 `/etc/utmp`。
`+ -vb` 使用视觉铃声而非听觉铃声。
`+ +vb` 不使用视觉铃。
`+ -wf` 在启动子进程之前等待窗口被映射（mapped）。这确保了初始终端大小设置和环境变量是正确的。
`+ +wf` 不在启动应用前等待。

`345`

`-C` 表明 xterm 应该接收控制台输出。
`-Sccn` 指定在从机模式下使用的伪终端名称的最后两个字母。

以下标准 X Toolkit 命令行参数常与 xterm 配合使用：

`+ -bd color` 指定边界颜色。默认=黑色。
`+ -bg color` 指定背景颜色。默认=白色。
`+ -bw pixels` 指定窗口边界的宽度（像素为）。
`+ -display display` 指定要连接的 X 服务器。
`+ -fg color` 指定前景色（文本）颜色。默认=黑色。
`+ -fn font` 指定普通文本字体。默认=fixed。
`+ -geometry geometry` 指定 VT102 窗口的大小和位置。
`+ -iconic` 通知 xterm 请求窗口管理器以图标形式而非窗口形式启动。
`+ -name name` 指定获取资源的应用程序名称，而非默认可执行文件。
`+ -rv` 通过交换前景和背景颜色模拟反色。
`+ -title string` 指定窗口标题字符串。
`+ -xrm resourcestring` 指定要使用的资源字符串。

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_374_0.png)

# 346

X Window System

## 资源

程序理解所有的 X Toolkit 资源名称和类，以及：

| `iconGeometry` (class `iconGeometry`) | 指定图标化时的应用大小和位置。 |
| `iconName` (class `iconName`) | 指定图标名称。 |
| `sunFunctionKeys` (class `sunFunctionKeys`) | 生成 Sun 功能键转义码而非标准转义序列。 |
| `sunKeyboard` (class `sunKeyboard`) | 指定是否假设 Sun/PC 键盘布局而非 DEC VT220。 |
| `termName` (class `TermName`) | 指定环境变量 TERM 设置的终端类型。 |
| `title` (class `Title`) | 通知窗口管理器显示此应用时使用指定的字符串。 |
| `ttyModes` (class `TtyModes`) | 指定终端关键字字符串以及 |
| `useInsert` (class `UseInsert`) | 指定终端关键字字符串以及是否记录到 `/etc/utmp`。 |
| `utmpInhibit` (class `UtmpInhibit`) | 指定是否记录到 `/etc/utmp`。 |
| `waitForMap` (class `WaitMap`) | 指定在启动应用前是否等待。 |

# 

`+ -prev` 将 X 服务器切换到上一个模式。
`+ -next` 将 X 服务器切换到下一个模式。
`+ -unlock` 允许在 xvidtune 运行时通过热键切换视频模式。

## 命令

`at (at, atq, atm, batch)` 是一个用于在稍后执行命令的实用程序。一次可以调度多个命令执行。一组预定执行的命令被称为**队列 (queue)**。
