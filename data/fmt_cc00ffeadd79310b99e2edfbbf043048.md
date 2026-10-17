
然后填写空处。

## 使用 x86config

`x86config` 程序是一个较旧的非 GUI 的程序。它会询问你许多关于显卡、显示器及更多信息。`xf86config` 是面向文本的，并且比 `XConfigurator` 技术性强得多。

该程序会在你的当前目录下生成一个 `XF86config` 文件。在尝试新配置之前，你需要将此文件复制到 `/etc/XF86config`。

![](img/d86aa78922e215fd387e0c1556445cac_336_0.png)

记住，如果你使用新配置文件启动 X Window 系统，如果配置无效，请立即中止。（如果情况运行不符合预期，你的屏幕会变得错乱——这就是你知道该立即中止进程的方法。）

## 手动编辑配置文件

如果你有特殊的硬件，配置程序可能无法生成配置文件。在这种情况下，你可以尝试“手动”编辑 `XF86Config` 文件。

![](img/d86aa78922e215fd387e0c1556445cac_336_1.png)

注意，编辑这个文件不是给胆子小的人准备的。它是晦涩的，充满了奇怪的数字，而且通常非常令人头疼。之所以有两个专门设计为你生成它的程序，是有充分原因的。

两个文本文件可能对你有所帮助。第一个是所有已知显卡及其配置的列表。它位于 `/usr/lib/X11/doc/`。

第二个文件包含显示器信息。该文件位于 `/usr/lib/X11/doc/Monitors`。

## 在 XF86Config 中生成数字

除非你是一个熟悉视频显示器和显示卡内部原理的电气工程师——并且可以使用专门的测试设备——否则不要尝试从零开始生成 `XF86Config`。

只有那些知道自己在做什么并且有大量时间的人才具备生成此类文件的诀窍和能力。如果你到为止还没有被吓跑，可以查看 XFree86 文档-`/usr/doc/FAQ` 获取更多信息。

有一个名为“视频模式漫游者指南”（The Hitchhiker's Guide to Video Modes）的非常好的教程可以帮助你。你可以在以下地址找到教程：

```
http://www.xfree86.org/3.1.2/VideoModes.html
http://www.ccil.org/~esr/faqs/video-modes.html
http://tsikova.tiac.net/video-modes.html
```

## 使用 xvidtune 进行调优

在你使配置基本工作后，可以使用 X Window 实用程序 `xvidtune` 对其进行调优。通过此工具，你可以对屏幕的位置和大小进行微调。图 16-1 显示了该程序提供的控制面板。

| Hdisplay: 1200 | Vdisplay: 1024 |
| HSyncStart: 1320 | VSyncStart: 1026 |
| HSyncEnd: 1512 | VSyncEnd: 1026 |
| Hdisplay: 1200 | Vdisplay: 1024 |
| HSyncStart: 1320 | VSyncStart: 1026 |
| HSyncEnd: 1512 | VSyncEnd: 1026 |
（注：OCR 中的表格是重复的，根据视觉结构修正）

![](img/d86aa78922e215fd387e0c1556445cac_341_0.png)

图 16-3 fwm2 窗口管理器

![](img/d86aa78922e215fd387e0c1556445cac_341_1.png)

图 16-4 twm 窗口管理器

![](img/d86aa78922e215fd387e0c1556445cac_342_0.png)

## 执行常见的 X Window 配置任务

本节介绍了如何执行常见的 X Window 配置任务，例如重映射键盘和自定义窗口管理器。

## 将 Control 键置回原位

当 IBM 设计 PC 时，它为这台机器设计了一个全新的、不同的键盘。他们之所以这样做是一个谜团，因为新键盘非常奇异、难以使用，并且通常被认为布局不当。IBM 因忽略了当时标准的文字处理键盘而受到严厉批评，那是 IBM 最初发明的 IBM Selectric 打字机所使用的键盘。

多年来，键盘变得越来越合理。尽管如此，一个问题经常存在：制造商将 Caps Lock（大写锁定）键放在了 Ctrl 键的位置。

你可以通过在你的 `$HOME/.Xmodmap` 文件中放入以下行来交换这两个键：

```
remove Lock = Caps_Lock
remove Control = Control_L
keysym Control_L = Caps_Lock
keysym Caps_Lock = Control_L
add Lock = Caps_Lock
add Control = Control_L
```

注意：Linux 还有其他工具允许你在 X Window 系统之外修改键盘映射。请参阅 `loadkeys` 和 `dumpkeys` 的 man 页面。

## 将你的窗口管理器更改 fwm2

默认情况下，Linux 选择 `fwm95-2` 作为你的窗口管理器。当你使用控制面板工具创建账户时，它通过在你的家目录中创建一个 `.Xclients` 文件来实现此操作。
`.Xclients` 文件包含以下行：

```
#!/bin/bash
rm -f /tmp/Xrootenv.0
rm -f /tmp/fwmrc*
if [ -f $HOME/.fwm2rc.m4 ]; then
  RCFILE=$HOME/.fwm2rc.m4
else
  RCFILE=/etc/X11/TheNextLevel/.fwm2rc.m4
fi
if [ ! -z $(type -path fwm95-2) ]; then
  env > /tmp/Xrootenv.0
  exec fwm95 2 -f "FwmM4 -debug $RCFILE" -display :0 \
  > $HOME/.FWM95-errors 2>&1
fi
```
