
## 使用 SSH 进行安全显示转发

由于 X 窗口系统的以下特性，产生了一系列安全问题：

- 它被分为服务器和客户端组件。

- 它跨网络进行通信。

- 客户端应用程序很容易与 X 服务器建立连接。

为了避免安全问题，多种机制提供了防止未经授权访问的保护（见 `man Xsecurity`）。

其中之一是 SSH，通过安全 shell 进行网络访问。

通过安全 shell，可以在可能不安全的网络上进行主机之间的加密通信。

每个主机都有一个私有主机密钥和一个公主机密钥。主机之间的验证通过一个主机使用另一个主机的公钥加密其请求并发送给该主机来实现。

只有另一个主机才能用其私钥解密该请求。

### 130 第 4 使用 YaST 管理工具

主机之间的整个会话通过会话密钥进行额外的保护，出于安全考虑，该密钥仅位于计算机的主内存中并定期重新生成。

例如，如果用户想通过 SSH 登录 `da10` 机器，他必须输入：

```
tux@da5:~ ssh da10
```

显示如下内容：

```
无法建立主机 'da10 (10.0.0.10)' 的真实性。
RSA密钥指纹为 ea:79:90:9a:d4:bf:b6:a2:40:ee:72:56:f8:d9:e5:76。

你确定要继续连接吗 (yes/no)? yes
警告: 已将 'da10,10.0.0.10' (RSA) 永久添加到已知主机列表。
password:
```

```
tux@da10:~
```

用户 tux 可以使用选项 `-l` 来指定用户名：

```
tux@da5:~ -l geeko da10
```

要将主机 `da10` 上的 X 输入输出重定向到主机 `da5`（自动重定向），用户 tux 可以输入：

```
tux@da5:~ -X da10
```

X 协议通过安全隧道转发（X11 转发）。

> 使用 SSH，这种 X 隧道是默认建立的。使用 OpenSSH 时，你必须指定 `-X` 来实现此功能。

SSH 的先驱是 r-tools。

由于各种安全问题，如网络上的明文密码或仅基于 IP 地址的身份验证，它们不应再使用。

SSH 和 SCP 通过加密手段增加了安全性，提供了相同的功能。

r-tools 如下：

- rlogin (远程登录)。允许你登录到计算机，类似于 telnet。根据远程机器上 `/etc/hosts.equiv` 或 `~/.hosts` 文件中的条目，可能完全不需要密码。

- rsh (远程 shell壳)。在远程计算机上启动程序。如果没有向 rsh 传递命令，将启动一个使用 rlogin 的交互式会话。

## 配置 X 窗口系统

- rcp (远程复制)。用于从一台机器复制文件到另一台机器。语法与 scp 类似。如果 `/etc/hosts.equiv` 和 `~/.hosts` 中存在合适的条目，则不需要密码。

## 了解 X 服务器配置文件

X 服务器的配置文件是 `/etc/X11/XF86Config`。该文件包含了鼠标设置、键盘、分辨率和频率等规范。该文件分为几个部分：

- "Files" 部分：文件名。

- "Module" 部分：动态模块加载。

- "ServerFlags" 部分：服务器标志位。

- "Input Device" 部分：输入设备描述。

- "Device" 部分：图形设备描述。

- "VideoAdaptor" 部分：X 视频适配器描述器描述。

- "Monitor" 部分：显示器描述。

- "Modes" 部分：视频模式描述。

- "Screen" 部分：屏幕配置。

- "ServerLayout" 部分：整体布局。

- "DRI" 部分：特定于 DRI 的配置（直接渲染基础设施）。

- "Vendor" 部分：特定于厂商的配置。

该配置文件的示例为 `usr/X11R6/lib/X11/XF86Config`。

> 注意：有关配置文件 XF86Config 的信息，请参阅手册页。输入 `man XF86Config`。

## 了解配置 X 服务器的工具

有多种工具可配置 X 服务器 (XFree86 4.x)：

- SaX2。SaX2（SuSE 高级 X 配置）支持 X 服务器并可配合鼠标（包 `sax2`）。

### 第 4 部分 使用 YaST 管理工具

- `/usr/X11R6/bin/xf8config`。与 SaX2 相，这是一个用于配置 X 服务器的文本程序。

- `/usr/X11R6/bin/xvidtune`。此程序可用于配置屏幕尺寸（宽度、高度）。

定义屏幕尺寸的模型包含在 `/etc/X11/XF86Config` 文件的 "Modes" 部分。

你可以使用 `XF86Setup` 配置版本为 3.3.x 的 X 服务器。

某些 X 应用程序的默认定义在 `~/.Xdefaults` 文件中，必要可以在此处进行修改。还有一个名为 `~/.Xresources` 的文件。然而，这仅仅是指向 `~/.Xdefaults` 的链接。这两个文件在 SLES 9 上默认不存在。如果修改了这些文件，请重启 X 服务器或进入 `xterm` 以重新读取 `~/.Xdefaults` 文件。可以通过输入 `xrdb --help` 查看选项。KDE 和 GNOME 使用不同的配置文件。

## 练习 4-6 可选：探索 X 窗口系统的组件

X Server 是一个独立的程序，各种窗口管理器也是。此练习的目的是向你演示这些独立的组件。

- 1. 从图形环境中退出并切换到文本控制台 `Ctrl + Alt + F1`。使用密码 `novel` 登录 root。

- 2. 输入 `init 3` 切换到运行级别 3（运行级别将在课程后面详细解释）。

- 3. 输入 `X &` 启动 X 服务器。会出现一个带有灰色图案和鼠标光标的图形界面。

- 4. 切回文本控制台 `Ctrl + Alt + F1`。尝试输入 `xterm &` 启动 xterm。你会得到一个错误信息：“Can't open display”。

- 5. 再次启动 xterm，设置显示变量：`DISPLAY=:0 xterm &`。

- 6. 使用 `Alt + F7` 切换到图形屏幕。

- 7. 将鼠标光标移动到 xterm 窗口上方并输入 `fwm &`。

- 8. 如果喜欢，探索 fwm 的。点击左键从菜单中选择。

- 9. 按 `Ctrl + Alt + Backspace` 杀死 X 服务器。

- 10. 在文本控制台输入 `init 5` 切换回运行级别 5。当图形登录界面出现时，使用密码 `novel` 登录。

## 章节总结

- SLES 的主配置工具是 YaST。你可以在命令行终端中使用基于菜单的 YaST 界面，也可以在桌面环境中使用它。

- 你可以使用 Software 部分在 SLES 系统上安装和管理软件包。YaST 可以从各种来源安装并检查依赖项。

- 系统中的每个用户账户都有唯一的用户 ID (UID)。同样，每个组通过唯一的组 ID (GID) 识别。root 用户和 root 组的 UID 和 GID 均为 0。你可以使用 YaST 创建、编辑或删除用户和组。

- 虽然在安装期间通常会配置打印机，但你可以使用 Printer 模块为你的系统添加或更改打印机。

### 核心术语

- `/usr/X11R6/bin/xf86config` — 一个带有 XFree86 4 版本的基于文本的 X 服务器配置工具。

- `~` 指向当前用户主目录的特殊字符。

- `internet command`（互联网命令）— 通常用于拨号你的调制解调器以建立互联网连接。它也可以用于关闭互联网连接。

- `dependencies`（依赖关系）— 软件包所需的先决软件。

- `DISPLAY` — 存储你的系统默认显示名称的变量。

- `display name`（显示名称）— XWindow 系统用于确定要使用的 X 服务器位置的名称。

- `gdm` — 一个用于显示 GNOME 风格图形登录界面的程序。

- `Group ID (GID)` — Linux 操作系统用于识别用户的数字。根 组（root group）的 GID 始终为 0。

- `home directory`（主目录）— 你硬盘上你拥有完全权限默认放置的目录。它通常是 `/home/username`。

- `init command`（init 命令）— 用于更改系统状态。

- `kdm` — 用于显示 KDE 风格图形登录界面的程序。它是 SLES 中的默认登录管理器。

- `Internet`（互联网）— 一个用于拨号你的调制解调器以建立互联网连接的图形实用工具。它也可以用于关闭互联网连接。

- `login manager`（登录管理器）— 为用户提供图形化登录的程序。成功登录后，登录管理器会启动 X 服务器、窗口管理器和桌面环境。

- `login shell`（登录 shell）— 提供命令提示符并执行用户命令的程序。SLES 的默认 shell 是 Bourne Shell (`/bin/bash`)。

- `ncurses` — 在命令行终端内运行的基于菜单的程序所使用的标准。

- `package`（包）— 在 SLES 系统上提供某些功能的软件程序组。

- `private host key`（私有主机密钥）— 一段用于解密使用公主机密钥加密信息的字符字符串。

- `public host key`（公有主机密钥）— 一段用于加密信息的字符字符串。

- `Qt` — 在桌面环境中创建 GUI 程序的标准工具包。

- `rc command`（rc 命令）— 用于跨网络将文件从一台远程 Linux 或 UNIX 计算机复制到另一台。

- `login command`（login 命令）— 用于从网络上的远程 Linux 或 UNIX 计算机获取命令行接口。

- `rsh command`（rsh 命令）— 用于在远程 Linux 或 UNIX 计算机上运行程序。

- `r-tools` — 一系列通常用于访问远程 UNIX 计算机、向其复制文件以及运行程序的实用工具。最常用的 r-tools 是 rlogin、rsh 和 rcp。

- `runlevel 3`（运行级别 3）— 一种允许你登录 tty1 到 tty6 的系统状态，但在 tty7 上不包含图形登录界面。

- `runlevel 5`（运行级别 5）— 一种允许你登录 tty1 到 tty7 的系统状态。它是 SLES 中的默认系统状态。

- SaX2 — SLES 中的主要 X 服务器配置工具。

- SSH — 一种实用工具，可以通过加密发送到网络上的任何数据，以安全的方式访问远程计算机。SSH 代表 Secure Shell（安全外壳）。

- `startcommand`（启动命令）— 用于从命令行终端启动 X 服务器和默认桌面环境。

- `User ID (UID)` — Linux 操作系统用于唯一标识账户的数字。根用户的 UID 始终为 0。

- `users`（用户）— SLES 系统中所有新用户被放置的默认组。

- `xdm` — 用于显示图形登录界面的程序。

- `XF86Setup` — 在旧版本 XFree86 中使用的 X 服务器配置工具。

- YaST — SUSE Linux 中的主要系统配置工具。

## 4 使用 YaST 管理实用工具

### 复习题

1. 在基于菜单的 (ncurses) YaST 界面中，你可以使用哪些键在选择之间进行导航？（选择两个。）

a. Tab

b. 空格键

c. Alt

d. Alt+Tab

2. 你可以在命令提示符执行哪条命令来启动用户管理模块？

a. `yast users`

b. `yast /users`

c. `yast sw`

d. `yast -u`

3. 你可以使用 `yast` 命令的哪个选项来显示 YaST 模块列表？

4. 你想从安装介质使用 YaST 安装另一个软件包。你能验证你的系统是否具有相应的软件包吗？

a. 使用 dependencies 选项启动 YaST 程序。

b. 点击 YaST 内部的 Check 按钮。

c. 查看 YaST 内的选项卡。

d. 在 YaST 中右键点击软件包并选择 Verify。

5. 你如何在 YaST 中更改软件包的默认位置？

6. 根账户使用哪个 UID？

7. 使用 YaST 创建新用户时，使用的默认 Shell 是什么？

a. `/bin/shell`

b. `/bin/bash`

c. `/home/tux`

d. `/home/users`

8. 当你使用 YaST 创建新用户时，新用户分配的默认组是什么？

a. users

b. root

c. system

d. home

9. 使用 YaST 添加新用户时，修改了哪些文件？

10. 当使用 YaST 添加新组时，修改了哪个文件？

11. 你可以使用 YaST 在你的系统上配置以下哪些类型的打印机？（选择所有适用项）

a. USB

b. IrDA

c. 并口 (Parallel)

12. 你可以使用 YaST 配置哪种设备来连接调制解调器？

13. 在使用 YaST 访问调制解调器时，哪些状态是允许的？（选择所有适用）

a. runlevel 3

b. runlevel 5

14. 使用 YaST 创建新用户时，默认 Shell 是什么？

a. `/bin/shell`

b. `/bin/bash`

c. `/home/tux`

d. `/home/users`

15. 使用 YaST 创建新用户时，分配的默认组是什么？

a. users

b. root

c. system

d. home

16. 使用 YaST 添加新用户时，修改了哪些文件？

17. 使用 YaST 添加新组时，修改了哪个文件？

18. 你可以使用 YaST 在你的系统上配置以下哪些类型的打印机？（选择所有适用项）

a. USB

b. IrDA

c. 并口 (Parallel)

19. 根账户使用哪个 UID？

20. 哪些实用工具可以安全地访问远程计算机？（选择所有适用）

a. rlogin

b. rsh

c. rcp

d. SSH

21. 哪些命令可以用于在远程 Linux 或 UNIX 计算机上运行程序？（选择所有适用）

a. rlogin

b. rsh

c. rcp

d. SSH

22. 哪些命令可以用于从网络上的远程 Linux 或 UNIX 计算机获取命令行接口？（选择所有适用）

a. rlogin

b. rsh

c. rcp

d. SSH

23. 哪些实用工具通常用于访问远程 UNIX 计算机、向其复制文件以及运行程序？（选择所有适用）

a. rlogin

b. rsh

c. rcp

d. SSH

24. 哪些程序是为用户提供图形化登录的？（选择所有适用）

a. gdm

b. kdm

c. xdm

d. SSH

25. 哪些程序是 SLES 中的默认登录管理器？（选择所有适用）

a. gdm

b. kdm

c. xdm

d. SSH

26. 哪些程序是用于显示图形登录界面的？（选择所有适用）

a. gdm

b. kdm

c. xdm

d. SSH

27. 哪些实用工具是旧版本 XFree86 中使用的？（选择所有适用）

a. XF86Setup

b. SaX2

c. YaST

d. SSH

28. 哪些实用工具是 SUSE Linux 中的主要系统配置工具？（选择所有适用）

a. XF86Setup

b. SaX2

c. YaST

d. SSH

29. 哪些工具包用于在桌面环境中创建 GUI 程序？（选择所有适用）

a. Qt

b. ncurses

c. YaST

d. SSH

30. 哪些标准是在命令行终端内运行的基于菜单的程序所使用的？（选择所有适用）

a. Qt

b. ncurses

c. YaST

d. SSH

### 探索练习

### 探索 YaST

1. 在基于菜单的 (ncurses) YaST 界面中，你可以使用哪些键在选择之间进行导航？（选择两个。）

a. Tab

b. 空格键

c. Alt

d. Alt+Tab

2. 你可以在命令提示符执行哪条命令来启动用户管理模块？

a. `yast users`

b. `yast /users`

c. `yast sw`

d. `yast -u`

3. 你可以使用 `yast` 命令的哪个选项来显示 YaST 模块列表？

4. 你想从安装介质使用 YaST 安装另一个软件包。你能验证你的系统是否具有相应的软件包吗？

a. 使用 dependencies 选项启动 YaST 程序。

b. 点击 YaST 内部的 Check 按钮。

c. 查看 YaST 内的选项卡。

d. 在 YaST 中右键点击软件包并选择 Verify。

5. 你如何在 YaST 中更改软件包的默认位置？

6. 根账户使用哪个 UID？

7. 使用 YaST 创建新用户时，使用的默认 Shell 是什么？

a. `/bin/shell`

b. `/bin/bash`

c. `/home/tux`

d. `/home/users`

8. 当你使用 YaST 创建新用户时，新用户分配的默认组是什么？

a. users

b. root

c. system

d. home

9. 使用 YaST 添加新用户时，修改了哪些文件？

10. 当使用 YaST 添加新组时，修改了哪个文件？

11. 你可以使用 YaST 在你的系统上配置以下哪些类型的打印机？（选择所有适用项）

a. USB

b. IrDA

c. 并口 (Parallel)

12. 你可以使用 YaST 配置哪种设备来连接调制解调器？

13. 使用 YaST 访问调制解调器时，哪些状态是允许的？（选择所有适用）

a. runlevel 3

b. runlevel 5

14. 使用 YaST 创建新用户时，默认 Shell 是什么？

a. `/bin/shell`

b. `/bin/bash`

c. `/home/tux`

d. `/home/users`

15. 使用 YaST 创建新用户时，分配的默认组是什么？

a. users

b. root

c. system

d. home
