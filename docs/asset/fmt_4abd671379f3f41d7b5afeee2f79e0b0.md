
## wc

这是一个字数程序。`wc` 命令统计字符数、单词和行数。

## whoami

为了显示当前用户身份，`whoami` 命令会打印你当前的用户名。如果你以 root 操作员身份运行，它对于检查你的身份非常有用。

![](img/fbfff30e42d507bc7531108a281d6cf4_1196_0.png)

## xclock

这是一个 X11 钟客户端，可以以标准表盘或数字钟的形式运行。

## xcutsel

这是一个为复制粘贴操作提供缓冲的 X11 客户端。该程序对于不支持直接复制粘贴的程序之间的复制和粘贴信息非常有用。

## xdaliclock

一个 X11 数字钟客户端，具有熔化数字、透明背景以及丰富的自定义功能和键盘命令。

## xdm

此 X11 显示管理器提供了一个名为 `chooser` 的登录界面，当在系统中配置妥当时，它可以管理多个 X 显示。

## xfig

这是一个 X11 绘图程序。`xfig` 客户端是一个交互式绘图程序，使用对象而非像素图像来显示图形。你可以使用此程序绘制蓝图或其他技术图纸。

## xhost +

`xhost +` 命令允许在系统上显示 xterms。远程终端无法打开的最常见原因可能是没有运行 `xhost +` 命令。使用 `xhost -` 命令可以关闭允许 xterms 显示的权限。

## xjed

`xjed` 编辑器的 X11 版本。此版本的 `xjed` 编辑器运行在 X Window 系统下，并提供键盘菜单。

## xload

这是一个 X11 系统负载报告客户端，用于显示系统平均负载的图形，该负载是内存、CPU 和交换文件空间使用情况的组合。此程序像 X11 客户端一样，在后台启动：

```
# xload &
```

## ximage

这是一个 X11 客户端，可以加载、转换并显示由 `xwd` 客户端在你的显示器或桌面上创建的图像或窗口转储。你还可以使用 `ximage` 命令提供图形幻灯片。

## xlock

`xlock` 是一个 X11 终端锁定程序，提供密码保护和超过 50 种屏幕保护程序。

## xlsfonts

该 X11 客户端显示并搜索当前 X11 服务器识别的字体，对于查找特定字体或获取详细字体报告非常有用。

## xmessage

这是一个在你的显示器上显示消息的 X11 客户端。你还可以编写带有标签、按钮和其他信息的自定义消息。尽管此客户端经常与其他程序配合使用以提供预约提醒，但 `xmessage` 也可以作为便签贴提醒。

## xminicom

在 X11 终端窗口中运行 `minicom` 程序。这是在 X Window 系统下运行 `minicom` 通信程序的首选方式。

## xmkmmf

`xmkmmf` 命令（一个 shell 脚本）用于为 X 源码创建 Makefile。它实际上运行的是带有一组参数的 `imake` 命令。

## xmodmap

一个用于在 X 会话期间修改键盘或鼠标按钮的实用。你可以使用 `xmodmap` 重新映射键盘或重新排列鼠标按钮。

## xscreensaver

一个 X11 的屏幕保护程序，该客户端通常在后台运行，以便在预设时间后清空屏幕并运行屏幕保护程序。`xscreensaver` 客户端通常通过 `xscreensaver-command` 客户端控制。

## xscreensaver-command

此 X11 客户端用于控制 `xscreensaver` 程序以关闭屏幕保护并循环切换各种屏幕保护显示。

## xset

`xset` 命令设置 X Window 会话中的某些选项。你可以使用此选项设置你的蜂声（`xset b <volume> <frequency> <duration in milliseconds>`）、鼠标速度（`xset m <acceleration> <threshold>`）以及许多其他选项。

## xsetroot

一个 X11 客户端用于更改根窗口或显示器背景的外观，以及光标的外。你可以使用此客户端添加背景图案、颜色或图片，或者更改根窗口颜色。想要为 X11 桌面一个蓝色背景吗？尝试这个：

```
# xsetroot -solid blue
```

![](img/fbfff30e42d507bc7531108a281d6cf4_1198_0.png)

## xtop

类似于 `top` 命令，`xtop` 以图形方式显示最活跃系统资源密集型进程或程序。

## xv

你可以用 `xv` 在 X11 中显示图像。此 X11 客户端为捕获、更改、保存和打印图像提供了许多控制，并附有详尽文档。

## xwd

一个 X11 窗口转储客户端。你可以使用此客户端为窗口或整个显示器拍照。别忘记像这样指定输出文件：

```
# xwd >myscreendump.xwd
```

## xwininfo

该 X11 信息客户端收集有关窗口的可用信息并打印简短报告。你可以使用 `xwininfo` 实用工具确定窗口的大小和位置。

## xwud

一个 X11 图形实用工具客户端，用于显示由 `xwd` X11 客户端创建的窗口转储。

## zip

`zip` 命令列出、测试或将文件添加到压缩归档中。默认是将文件添加到归档。

## zsh

`z shell` 是 Linux 中最大的 shell，具有许多功能和大量的文档。该 shell 具有源自 `csh` 和 `tcsh` shell 的功能，并可以模拟 `ksh` (Korn) 和 `sh` (Bourne) shell。

## 总结（Summary）

如果你读了整个附录，你会注意到两点：第一，它包含了 200 多条命令；第二，你的时间实在太闲了——出去写些新的 Linux 驱动程序之类的吧！

我希望这个附录能帮助你了解一些可用的命令，无论你是用户、系统管理员，还是想学习更多关于 Red Hat Linux 的人。我鼓励你使用帮助页（`man pages`）来学习本附录未包含的许多细节。大多数命令都有可以传递给它们的参数，尽管本附录尝试指出其中一些，但要容纳帮助页中提供的细节需要一整本书。

## Linux 文档项目版权许可（The Linux Documentation Project Copyright License）

## 在本附录中（IN THIS APPENDIX）

- 版权许可 1166
- 发布 LDP 手册 1167

## 附录 C（APPENDIX C）

# 与其他系统协作

附录 D 1171

`DOSEMU` 可以从 Linux 控制台的命令行运行，也可以在 X 会话期间在自己的窗口中启动。主配置文件 `global.conf` 位于 `/var/lib/dosemu` 目录下。然而，要配置大多数系统级设置，你需要编辑 `/etc/dosemu.conf` 文件。你从中找到近 80 个不同的设置，通过这些设置可以配置 `DOSEMU` 的工作。

默认情况下，`DOSEMU` 可能仅允许 root 操作员启动。如果你首次尝试启动程序，你将看到此内容：

```
# dos
```

抱歉，bball。你未允许使用 `DOSEMU`。请联系系统管理员。

要允许其他用户启动并使用 `DOSEMU`，请使用你喜欢的文本编辑器（以 root 身份）编辑 `/etc/dosemu.users` 文件。查找以下内容：

```
# 如果你想允许所有用户使用受限制的 dosemu，请取消下行的注释

# all nosuidroot restricted # all other users have normal user restrictions
```

启用系统用户的一种方法是移除 `all` 单词前的符号 (`#`)：

```
all nosuidroot restricted all other users have normal user restrictions
```

保存文件。接下来，使用 `cp` 命令创建 `DOSEMU` 的副本：

```
# cp /usr/bin/dodos /usr/bin/dodos
```

最后，使用 `chmod` 命令移除程序的 SETUID 位：

```
# chmod 755 /usr/bin/dodos
```

你的用户可以启动 DOS 会话（对存储和硬件访问有限制）。要让你的用户在 X11 窗口中启动 DOS 会话，请为 `xdos` 命令制作一个副本并同时更改其权限。要在控制台或 X11 终端窗口内启动 DOS 会话，请输入新的 `DOSEMU` 命令名称：

```
# dodos
```
