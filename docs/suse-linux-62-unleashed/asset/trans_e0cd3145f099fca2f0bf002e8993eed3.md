

# 常用 Linux 命令与工具
附录 C

# umount

umount 命令用于从你的 SuSE 文件系统中卸载文件系统（你必须是 root 用户，除非你编辑了文件系统表 /etc/fstab 来授予权限）。命令的语法为：

```
umount <filesystem>
```

# unalias

unalias 是取消别名（alias）的命令。要取消别名，只需输入 unalias <别名> 即可。

# unzip

unzip 命令用于列出、测试或从压缩包中提取文件。默认操作是从压缩包中提取文件。基本语法为 unzip <filename>。

# updatedb

此命令在 /var/lib 目录下构建 `locate` 命令的数据库，名为 `locatedb`。

# uptime

你可以显示系统已运行了多久（如果你想向你的 NT 朋友炫耀的话）。uptime 命令显示你的 Linux 系统已运行了多久、当前登录的用户是谁，以及过去 5、10 和 15 分钟的平均系统负载。Linux 系统的运行时间通常以年为单位（几乎总是由于硬件故障导致的）。

# vdir

使用 vdir 列出目录内容。此命令相当于使用 `ls` 命令配合 `-l` 选项获取详细的目录列表。

# vi

在 SuSE Linux 下通常被称为 vi（视觉）编辑器，vi 是指向 vim 编辑器的符号链接。在此模式下，vim 编辑器紧密模拟了最初随伯克利软件发行版（BSD UNIX）提供的经典 vi 编辑器。

![](img/cbac72550c7126a22162e94d91a0c360_1058_0.png)

# view

指向 vim 编辑器的符号链接。

# vim

vim 代表 Visual editor iMproved（改进的视觉编辑器）。该编辑器是 vi 编辑器的改进，还可以模拟 ex 行编辑器。该编辑器的 X11 版本被称为 gvim。

# vmstat

vmstat 打印虚拟内存统计数据。此命令显示系统使用了多少磁盘空间，通常在交换文件分区上。

# W

使用 w 命令显示谁正在登录，它不仅显示当前登录你系统的人，还显示了与 uptime 命令相同的信息。

# wall

wall 在所有当前登录用户的所有终端上显示标准输入的内容。基本上，该命令写入所有终端；因此得名如此。它也可以显示文件的内容。超级用户或 root 可以向那些选择拒绝消息或正在使用自动拒绝消息程序的终端写入内容。

# wc

这是一个字数程序。wc 统计文件中的字符数、单词数和行数，并在显示器上打印一份简短报告。默认显示所有三项，但你可以通过 -c、-w 或 -l 选项来限制报告。

# whatis

此命令在 whatis 数据库（位于 /usr/man 目录下）中搜索命令名，并打印每个命令功能的单行摘要。使用 whatis 命令，后跟另一个命令的名字：

```
# whatis emacs
```

# 常用 Linux 命令与工具
附录 C

# whereis

使用 whereis 查找命令、命令源和手册页（manual pages）。该程序通过搜索内置目录列表来查找并打印你指定的命令名称的匹配项。

# who

who 命令要么调用了一只猫头鹰（实际上它并没有），要么打印每个当前登录用户的登录名、终端类型、登录时间和远程主机名。以下是 who 命令的示例：

$ who

```
root tty0 Jul 27 11:44 (www01.mk.net)
dpitts tty2 Jul 27 19:32 (d12.dialup.seane)
ehooban tty3 Jul 27 11:47 (205.177.146.78)
dpitts tty4 Jul 27 19:34 (d12.dialup.seane)
```

# whoami

要显示你当前的用户身份，whoami 命令会打印你当前使用的用户名。它对于检查你是否以 root 操作员的身份运行非常有用。

# XF86Setup

XF86Setup 命令启动 XF86_VGA16 XFree86 X 服务器，尝试为 SuSE Linux 配置或重新配置 X11。此命令将生成一个 XF86Config，供指定的 X11 服务器在 X 会话使用。

# xclock

X11 时钟客户端可以以标准表面或数字钟的形式运行。

# xcutsel

X11 客户端为复制和粘贴操作提供缓冲区。该程序对于在可能不支持直接复制和粘贴的程序之间复制和粘贴信息非常有用。

# xdaliclock

一个 X11 数字钟客户端，具有融化数字、透明背景以及广泛的自定义功能和键盘命令。

# xdm

此 X11 显示管理器（Display Manager）提供了一个名为“chooser”的登录界面，当在系统上正确配置后，它可以管理多个 X 显示器。

# xf86config

xf86config 命令包含在 XFree86 中，用于为 SuSE Linux 配置一个工作的 XF86config。该命令可以在控制台或 X11 终端的命令行中使用，以在 Linux 上配置或重新配置 X11。

# xfig

一个 X11 绘图程序。xfig 客户端是一个交互式绘图程序，它使用对象而非像素图像来显示图形。你可以使用此程序开发蓝图或其他技术图纸。

# xhost +

xhost + 命令允许任何其他 X11 客户端在系统中显示，或来自指定主机的连接。使用这种形式的命令可能不是个主意，但在没有互联网连接的局域网中是完全可以的。你可以允许来自主机的连接：

```
# xhost +presario.home.org
```

要关闭此功能，请使用 xhost 命令。

# xjed

这是 jed 编辑器的 X11 版本。此版本的 jed 编辑器运行在 X Window 系统下并提供键盘菜单。

# xload

这是 X11 系统负载报告客户端。此 X11 命令用于显示系统平均负载的图形，它是内存、CPU 和交换文件空间使用情况的结合。该程序像许多 X11 客户端一样在后台启动：

```
# xload &
```

# xli

这是一个 X11 客户端，可以加载、翻译并显示由 x 客户端在你的显示器或桌面创建的图形图像或窗口转储（window dumps）。你可以使用 xli 在显示器上显示图形。

# xv

你可以在 X11 中运行标准时钟或数字钟。

# xlock

xlock 是一个 X11 锁定程序，提供密码保护和超过 50 种屏幕保护程序。

# xlsfonts

此 X11 客户端显示并搜索当前 X11 服务器识别的字体。

# xmessage

一个 X11 客户端，在你的显示器上显示消息。你可以使用带有标签、按钮和其他信息的自定义消息。尽管该客户端通常与其他程序配合使用作为提醒，但 xmessage 也可以提供快速日历：

```
# cal | xmessage -title 'Calendar' &
```

# xminicom

在 X11 窗口中运行 minicom 程序。这是在 X Window 系统下运行通信程序的首选方式。

# xmkmmf

xmkmmf 命令（一个脚本）用于为 X 源码创建 Makefile。它实际上是带有参数运行 imake 命令。

# xmodmap

一个在 X 会话期间修改键盘或鼠标按钮的工具。你可以使用 xmodmap 重新映射键盘或调整鼠标按钮。

# xscreensaver

X11 的屏幕保护程序，该客户端通常在后台运行，在预选时间后使屏幕变空。xscreensaver 通常由 xscreensaver-command 控制。

# xscreensaver-command

此 X11 客户端用于控制 xscreensaver 程序开启或关闭屏幕保护，或切换各种显示。

# xset

xset 命令设置 X Window 会话中的某些选项。你可以使用此选项设置铃声（xset b <音量> <毫秒>）、鼠标速度（xset m <加速度> <阈值>）、屏幕保护超时（xset s <秒>）以及许多其他设置。

# xsetroot

X11 根窗口或显示背景外观以及光标样式。你可以使用此客户端添加背景图案、颜色或图片，或者更改根窗口光标。想要 X11 桌面显示蓝色背景？尝试以下：

```
# xsetroot -solid blue
```

# xv

你可以用 xv 在 X11 显示图像。此 X11 客户端提供了许多捕捉、更改、保存和打印图像的功能，并附有详细文档。

# xwd

X11 窗口导出客户端。你可以使用该客户端拍摄窗口或整个屏幕。不要忘记指定输出文件：

```
# xwd > myscreendump.xwd
```

# xwininfo

此 X11 信息客户端收集窗口的可用信息并打印一份简短报告。你可以使用 xwininfo 工具确定窗口的大小和位置。

