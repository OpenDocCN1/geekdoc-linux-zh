
`max@tiny:-s cat /etc/gdm/custom.conf`

```
[security]

disallowTCP=false
```

重启系统以重启 X 服务器和 `gdm` (`gdm-binary`) 使更改生效。有关更多信息，请参阅 `libgeometry.org/admin/gdm/2.28/configuration.html#daemonconfigconf`。

## xhost 授予显示器访问

在安装状态下，`xhost` 保护每个用户的 X 服务器。想要授予其 X 服务器访问的用户需要运行 `xhost`。假设 Max 已登录到名为 `tiny` 的系统，且 X 允许 `dog` 上的用户使用其显示器（X 服务器）。Max 运行此命令：

```
max@tiny:-s xhost +dog

being added to access control list

max@tiny:-s xhost +

access control enabled, only authorized clients can connect

INET-dog
```

在不带任何参数的情况下，`xhost` 会描述其状态。在前面的示例中，`INET` 表示 IPv4。如果 Max 想允许所有系统访问其显示器，他可以输入以下命令：

```
$ xhost +

access control disabled, clients can connect from any host
```

如果你经常通过网络与其他用户协作，你可能会发现将一行 `xhost` 命令添加到你的 `.bash_profile` 文件（第 293 页）中很方便——但请查看下一页关于使用 `xhost` 访问你的 X 显示器的安全提示；如果另一个系统有权访问你的显示器，你可能会发现工作经常被中断。

# 第 8 章 LINUX GUI：X 与 GNOME

## 安全与 xhost

使用 `xhost` 授予远程系统访问你的显示器意味着远程系统上的任何用户都可以看到你在终端仿真器中输入的所有内容，包括密码。因此，软件软件包（例如 T/Tk 开发系统 (`www.tcl.tk`)）在 `xhost` 允许远程访问 X 服务器时会限制其自身的功能。如果你担心安全或想充分利用 T/Tk 等系统，你应该使用更安全的方法为你的 X 会话授予远程访问。有关更安全的 `xhost` 替代品的信息，请使用 `auth maint map`。

## DISPLAY 变量

识别显示器的最常用方法是使用 `DISPLAY` 环境变量，这个本地唯一标识字符串在 X 服务器启动时会自动设置。`DISPLAY` 变量持有显示器的屏幕编号：

```
$ echo DISPLAY

:0.0
```

显示器的代码格式为：
`[hostname]:display-number.screen-number`
`hostname` 是运行 X 服务器的系统名称，`display-number` 是（物理）显示器的逻辑编号（如果你通过 `ssh` 运行 X，屏幕上可能连接了一个或多个图形终端），`screen-number` 是（如果你运行多个 X 实例）（虚拟）终端的逻辑编号。当你使用单个屏幕时，可以缩短该标识字符串。例如，你可以使用 `tiny:0` 或 `tiny:id` 来识别名为 `tiny` 系统上的物理显示器。当 X 服务器和客户端运行在同一系统上时，你可以进一步缩短此标识字符串为 `:0` 或 `-X`。一个示例是将 `DISPLAY` 设置为 `localhost:10.0`。你可能需要使用 `-X` 来设置此值。请参阅第 64 页的“X 转发”获取有关设置 `ssh` 以便转发到 X 的信息。

如果 `DISPLAY` 为空或未设置，你正在工作的屏幕并未运行。应用程序（X 客户端）使用 `DISPLAY` 变量的值来确定使用哪个显示器、键盘和鼠标（统称为 X 服务器）。要在本地系统上运行应用程序（例如 `gnome-calculator`），但让它在远程系统的 X 上，需要更改客户端系统上 `DISPLAY` 变量的值以识别远程服务器。

```
samod:$ export DISPLAY=tiny:0.0

samod:$ gnome-calculator-
```

前面的示例显示 Sam 在名为 `tiny` 的系统上运行默认 X 服务器并执行 `gnome-calculator`。在将 `DISPLAY` 变量设置为服务器的 ID 后，Sam 使用的所有程序（客户端）都将 `tiny` 作为它们的服务器（即输出出现在 `tiny` 的显示器上，输入来自 `tiny` 的键盘和鼠标）。尝试在 `gnome-calculator` 中运行 `term`，看看它接受哪个键盘输入。如果此示例产生错误，请参考前面的两个部分，它们解释了如何设置以允许远程系统连接。

### 当你更改 DISPLAY 值时

当你更改 `DISPLAY` 变量的值时，所有 X 程序都会将其输出发送到由 `DISPLAY` 指定显示器。

### -display 选项

对于单个命令，你通常可以指定由 `DISPLAY` 指定的显示器。

### 运行多个服务器

对于单个命令，你通常可以指定由 `DISPLAY` 指定的显示器。

### 停止 X 服务器

对于单个命令，你通常可以指定由 `DISPLAY` 指定的显示器。

### 重新映射鼠标按钮

对于单个命令，你通常可以指定由 `DISPLAY` 指定的显示器。

```bash

$ xmodmap -e 'pointer = 3 2 1 4 5 6 7 8 9'
```
