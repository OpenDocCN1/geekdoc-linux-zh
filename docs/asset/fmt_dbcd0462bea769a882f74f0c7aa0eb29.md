
你可以通过多种方式进入 Laddie CLI。你可以以用户 `cli` 身份无密码 `telnet` 到 192.188.1.11。你也可以以 `root` 身份 `telnet` 到 Laddie，然后在 `bash` 提示符中使用命令 `cli` 启动 Laddie 的 CLI。

# Laddie 命令摘要

以下是所有的 Laddie CLI 命令及其语法和要描述。

- `clear [all|1-5]` - 清除报警
- `test [1-5]` - 手动设置报警
- `view` - 查看系统状态
- `view [all|1-5]` - 查看区域状态
- `view logs` - 列出最后 20 条日志消息
- `set zone [1-5] enabled [yes|no]` - 启用或禁用某个区域
- `set zone [1-5] latching [yes|no]` - 设置区域是否锁存报警
- `set zone [1-5] name "zone name"` - 给区域命名
- `set zone [1-5] contact [no|nc]` - 设置为常开或常闭
- `set logs [yes|no]` - 将日志流式传输到此 CLI 会话
- `help` - 查看关于 Laddie 的帮助
- `dump` - 以 CLI 命令的形式查看配置
- `(comments)` - 注释行
- `quit` - 退出命令行界面

你已经熟悉了 Laddie 日志记录器的配置，因此我们将对每个命令进行详细解释。不过，有几个命令值得特别提及。

# set logs on

Laddie 日志记录器的少数功能之一是，你可以对其建立一个 `telnet` 连接，并通过该连接将日志消息发送给你。

设计命令行界面 141

`set logs` 命令打开（或关闭）与日志记录器的连接以接收这些消息。一个示例会话可能会使其更清晰。

```
> > set logs on
> test 2
> 2006-06-21 14:40:29 User set alarm on zone 2, Back Door
> 2006-06-21 14:40:29 Alarm system status: alarm
> set logs off
> clear all
```

注意，执行 `clear all` 命令后没有显示日志消息，因为我们通过 `set logs off` 命令关闭了与日志记录器的连接。

系统会在日志发生时打印它们，日志消息的输出出现在正在输入的命令中间。这可能会很困扰，因此你可能建议用户使用两个窗口并在每个启动一个 CLI，一个用于日志消息，另一个用于交互式命令。

在 CLI 会话中出现日志消息对设备来说是一个加分项。你的客户可以使用 CLI 将日志消息从设备发送到他们的网络管理系统。此外，在 CLI 中显示日志对任何尝试远程管理设备的人都有很大帮助。

# dump

`dump` 命令将 Laddie 的配置显示为可以回传 CLI 的命令列表。输出的第一行是注释，用于标识显示的内容，更重要的是显示显示的时间。虽然我们没有在顶行包含 CLI 版本号，但这样做会有帮助。

```
> dump
# Laddie Alarm System Configuration as of 2008-06-21 15:01:02
set enabled 1 yes
set name 1 "Front Door"
set contact 1 no
set latch 1 no
set enabled 2 yes
set name 2 "Back Door"
set contact 2 nc
set latch 2 yes
set enabled 3 yes
set name 3 "Garage"
set contact 3 no
set latch 3 no
set enabled 4 no
set name 4 "Motion Detector"
set contact 4 nc
set latch 4 no
```

```
set enabled 5 yes
set name 5 "Smoke description"
set contact 5 no
set latching 5 no
```

一些 Linux 命令（例如 `seterial`）也有一个选项，可以可以回传到命令的形式打印配置信息。

# help

Laddie CLI 提供了 `help` 命令，让用户能够快速查看哪些可用命令。在不带任何参数的情况下，`help` 提供其他帮助命令的建议。

- 可用的帮助主题：
- `help intro` - Laddie 报警系统简介
- `help commands` - 可用 CLI 命令列表
- `help howto` - “如何操作”帮助主题列表
- `help whatif` - “如果怎样”帮助主题列表

`test` 命令的语法由以下几行定义。

```
%token ZONE_ID
%token TEST
```

```
test_command :
    TEST ZONE_ID      { test_zone(Zone); }
;
```

`ZONE_ID` 和 `TEST` 的标记定义被转换为 `#define` 语句并传递到 lex 的文件 `token.l` 中。`test` 命令的语法定义需要一个 `TEST` 后面紧跟一个 `ZONE_ID`。如果命令行有一个有效的 `test` 命令，将调用 C 子程序 `test_zone()` 并将区域 ID 作为参数传递。

# C 代码

`commands.c` 中的 C 子程序 `test_zone()` 是执行实际测试工作的地方；它将 `Zone` 表格中的 `alarm` 字段设置为 1。以下是 `test_zone()` 程序的完整完整代码。

```
void test_zone(int zone) {
    char cmd[100];   /* 用于构建 SQL 命令的地方 */
    sprintf(cmd, "UPDATE Zone SET alarm = 1 WHERE id = %d", zone);
    update(cmd);
}
```

`update(cmd)` 子程序是一个实用程序，它向 `ladd` 守护进程发送一个 PostgreSQL 更新命令。该程序的代码与第 5 章中的 SQL 更新代码几乎相同，因此我们在此处不再展示该程序的代码。

# 代码审查笔记

根据我们的计算，添加 `test` 命令的增量成本大约为 15 行代码。显然，`yacc`、`lex` 和 `RTA` 可以让构建 CLI 变得简单。。事实上，危险可能源于添加大量 CLI 命令的倾向。不要忘记，每个新命令都会给你的用户带来学习该命令的更大负担，从而减慢你的 CLI 的采用速度。

# 总结

在本章中，我们查看了在应用程序中包含 CLI 的原因以及你可以使用的各种 CLI 类型。我们展示了 Laddie 的 CLI，并对 `test` 命令进行了极简的代码审查。

考虑到你可能不会希望直接原样使用 Laddie CLI，我们 CLI 的程序员特别仔细地对源代码进行了文档说明，以便你修改。此外，帮助系统也经过构建，可以方便地移植到你的设备中。

在下一章中，我们将继续对 UI 的讨论，介绍如何将按钮、发光二极管（LED）和简单的文本液晶显示器（LCD）整合到你的设备中的技术。虽然下一章不会称其为 CLI，但我们认为 LCD 接口是一个带有字符界面的菜单系统。

# 10

# 构建面板接口

![](img/ab18faa434b6e1e10df0a92984bf70fc_170_0.png)

按钮、发光二极管（LED）和小型字母数字显示是非常常见的，以至于我们几乎注意它们。打印机、微波炉、手机以及 DVD 和 CD 播放器都使用按钮、LED 和 LCD 作为用户界面的一部分——你可能也希望在你的设备面板上拥有按钮和 LED。

在本章中，我们将描述如何构建面板 UI。首先，我们将讨论前面板上使用的硬件，然后通过审查 Laddie 面板 UI 的需求和设计，向你展示如何为面板设计 UI 和菜单系统。

我们将面板接口的范围分为以下几个部分：

- 按钮、LED 和 LCD
- 设计面板 UI
- Laddie 面板
- 改进我们的设计

我们将从查看面板硬件的细节开始。（如果你对硬件或接线图不熟悉，可以随心所快速略过这一章。）

## 按钮、LED 和 LCD

本节介绍了你在应用程序面板上会看到的硬件类型，包括按钮、LED 和 LCD。

## 按钮

你的量产规模可能决定你在设计中使用的硬件类型，特别是在按钮方面。当你的设备作为大批量生产的一部分进行生产时，按钮将直接构建在打印电路板上。另一方面，小规模生产或原型通常使用预制开关或单立开关。

从电气角度来说，按钮仅仅是开关，在大多数情况下是**常开**的。每个按钮通常需要一条可以由你的处理器读取的数字输入行。（第 5 章解释了你如何使用输入行来读取单个开关的状态。）

## 键盘
