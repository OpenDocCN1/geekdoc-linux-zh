

```
breaksw
endsw
```

```
# umask 022 means most files will be created world-readable by default.
umask 022
```

在很大程度上，此示例与上一节中的示例 .bashrc 相似。提示符有些复杂，因为我们正在检查是否拥有交互式 shell，如果是，则是否使用 tcsh 或 csh。交互式与非交互式之间的区别对于 tcsh 和 csh 非常重要，因为在非交互式 shell 中定义别名和终端修改可能会导致错误并带来性能损失。

## PROBLEM 111

- **症状：** .cshrc 中的交互式 shell 命令在非交互式 shell 启动时意外运行。

- **问题：** .cshrc 没有检查 shell 是否为交互式，或在交互式检查之前设置了提示符。

- **修复：** 确保提示符变量检查 shell 是否为交互式（请与上面 .cshrc 示例中的 `$?prompt` 进行比较）。如果这样做了而交互式命令仍然意外运行，请检查是否在该检查之前意外设置了提示符（确保它不在任何 .login 文件中）。

与 bash 中的 .profile 类似，tcsh 如果认为 shell 是登录 shell 就会读取 .login 文件。尽量避免使用 .login 文件，因为它们在使用窗口系统时会使情况变得混乱。

## 9.5 几个 X Window 启动文件

除了 shell 启动文件外，与 X Window System 相关的某些文件在用户登录时往往会引起额外问题：.xinitrc、.xsession 和 .Xdefaults。在本节中，我们将介绍这些文件，并讨论用于控制台登录的 X 显示管理器（xdm）。我们不会讨论如何设置窗口管理器。如果你想要这方面的建议，这里是：让它尽可能简单朴素，因为如果你添加装饰，人们会怀疑你的品味。说真的，添加大量晦涩的选项只会惹恼用户。此外，每当窗口管理器发布新版本时，你都会发现维护配置很令人沮丧，很可能破坏你所有的自定义选项。

### X 启动：.xinitrc 和 .xsession

.xinitrc 和 .xsession 之间的区别在于你如何启动 X Window System。如果你运行 xinit 或 startx 从控制台启动服务器，你需要一个 .xinitrc 文件；基于 xdm 的系统使用 .xsession 文件。

使用 startx 或 xinit 启动 X 是一种相当迂回的方法：首先你必须登录到控制台，然后使用另一个命令启动 X 服务器和客户端（例如窗口管理器）。不幸的是，由于 PC 图形硬件的诸多困难，Linux 安装通常将 X 服务器配置推迟到以后，这意味着它们以控制台模式启动，并期望用户自行处理。因此，系统管理员从未配置 xdm，并习惯于使用 xinit 或 startx 启动 X 服务器。

另一方面，xdm 在启动时启动 X 服务器并向用户呈现登录窗口。由于启动 X 服务器通常是开始会话中最耗系统资源的部分，xdm 节省了大量时间（有关如何配置 xdm，请参阅下面的 X 启动：xdm 部分）。

### .xinitrc 和 .xsession 文件

.xinitrc 和 .xsession 文件之间实际上并没有太大区别——它们都启动窗口管理器和一些客户端。这些差异仅在 X 终端方面才重要（例如控制台消息去向等问题）。为此，你可以在启动文件中检查 X 终端，但它们正变得越来越过时。

下面是一个示例 .xsession 或 .xinitrc 文件：

```sh
#!/bin/sh

# The background color and foreground colors (dark blue/white)
BG='#003'
FG=white

# Start up a terminal.
xterm -geometry 80x24+50+50 &

# Mail notification program.
xbiff -geometry -100+0 -foreground $FG -background $BG &

# Clock.
xclock -geometry -0+0 -foreground $FG -background $BG -hands $FG &

# Set the background color to a dark blue.
xsetroot -solid $BG

# Start the window manager.
twm
```

