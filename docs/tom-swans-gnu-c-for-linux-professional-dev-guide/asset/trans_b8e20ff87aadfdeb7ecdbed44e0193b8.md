

## XLSFONTS

如需查看 X 系统上已安装字体的完整列表（虽然可能会让你眼花缭乱），可以运行该程序。它有助于查找特定字体，而且因为列表已排序，还可以定位某类已安装字体，例如 Courier 的所有样式。（第 27 章“控制 Xlib 输入与输出”列出了类似程序 xfont.cpp 的源代码。）

## XPROP

这是每个开发系统上都有的工具之一，它显示海量信息，其中有些有用，有些则只有原作者才知道其用途。不过，你或许会想摆弄一下这个程序。它似乎需要一个命令行参数，所以不要只输入它的名字。若要按名称查看特定窗口的属性（名称可以从程序的窗口标题栏获得），可使用 `-name` 选项输入命令，例如：

```
$ xprop -name nxterm
```

这会显示名为“nxterm”的窗口的各种属性。若要查看根窗口的信息，请输入命令：

```
$ xprop -root
CUT_BUFFER0(STRING) = "\n"
```

除其他信息外，此命令还会显示“剪切”缓冲区的当前内容，也就是我们常说的剪贴板。根窗口拥有这些信息是合理的，这些信息由原子 CUT_BUFFER0 标识。（在我的系统上，可能其他系统也是如此，共有八个剪切缓冲区，分别由原子 CUT_BUFFER0 到 CUT_BUFFER7 命名。）要了解更多关于 xprop 的信息，可以使用如下 `-help` 选项：

```
$ xprop -help
```

## XSYSINFO

这是一个小巧可爱的程序，显示一些关于内存使用和 CPU 负载的信息。它可能有助于找出内存大户和 CPU 消耗大户，不过如果调整窗口堆叠顺序使其保持在其它窗口之上，它的实用性会更强。

此实用程序可能已自动安装，也可能没有。如果你找不到它，请查找类似 xsysinfo.rpm 的软件包文件（文件名中可能包含版本信息）。有关使用 Red Hat 包管理器（RPM）安装软件包的信息，请参阅第 3 章“安装 GNU C++”。

## XWININFO

xwininfo 是最实用的工具之一，你可以点击任意窗口，然后查看其参数、位置、大小、重力（调整大小或移动时子窗口相对于父窗口的关系）以及其他有用信息的列表。如果你在让窗口按预期方式显示时遇到问题，可以使用此工具检查 X 服务器掌握的关于该窗口的信息。以下是在我的系统上运行某个程序的示例输出：

```
$ xwininfo
xwininfo: Window id: 0x30000d6 "spider"
Absolute upper-left X: 21
Absolute upper-left Y: 124
Relative upper-left X: 0
Relative upper-left Y: 0
Width: 910
Height: 449
Depth: 24
Visual Class: TrueColor
Border width: 0
Class: InputOutput
Colormap: 0x23 (installed)
Bit Gravity State: NorthWestGravity
Window Gravity State: NorthWestGravity
Backing Store State: NotUseful
Save Under State: no
Map State: IsViewable
Override Redirect State: no
Corners: +21+124 -93+124 -93+195 +21+195
-geometry 910x449+16+101
```

## 使用输出语句调试

跟踪 X 客户端的事件可能是调查 bug 成因最有用的技术之一。如果从一开始就把这种逻辑构建到程序中，就可以生成客户端从 X 服务器接收到的完整事件历史记录。通常，导致问题的是事件的顺序（例如，响应 Expose 事件的多次绘制可能导致窗口出现严重的抖动问题）。

要跟踪事件，可以使用 `#ifdef` 和 `#ifndef` 指令，并配合像 `DEBUG` 这样的符号，在客户端的事件循环中启用输出语句。例如，使用 xwelcome.cpp（参见清单 26.3），下面是修改后的 switch 语句的一部分，其中输出语句由 `DEBUG` 符号启用：

```cpp
bool done = false;
XEvent event;
while (!done) {
    XNextEvent(display, &event);
    switch (event.type) {
    case Expose:
#ifdef DEBUG
        cout << "Expose event received" << endl;
#endif
        break;
    ...
    }
}
```

使用选项 `-DDEBUG` 编译程序以启用输出语句。不带该选项编译则会忽略输出语句。在随附光盘的 `c26/xwelcome` 目录中

