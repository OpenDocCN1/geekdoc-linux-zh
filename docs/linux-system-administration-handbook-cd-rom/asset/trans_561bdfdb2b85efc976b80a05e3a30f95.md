
注意，你可以输入一个几何尺寸（geometry）或一个偏移量（offset），但你不能只输入 XOFF 或宽度。几何尺寸和偏移量必须成对输入。也就是说，你不能输入：

```
> xterm -geometry 80
```

或者

```
> xterm -geometry +0
```

但以下命令是有效的：

```
> xterm -geometry 80x25
```

或者

```
> xterm -geometry +0+0
```

还有另一种方法可以为 X 程序指定默认设置，那就是通过 `.Xdefaults` 文件。在启动程序时，可以通过命令行设置的任何内容都可以存储在 `.Xdefaults` 文件中，你不需要提供所有选项。这些选项被称为资源（resources）。

## 16.6 X RESOURCES

一个 X 资源可以由四种类型的项目组成：

`program.widget[..].resource: value`

其中：

- program: 程序名称
- widget: 一或多个层级的组件（widget），它们是窗口的子部分。组件可以是按钮、菜单、滚动条、选项列表等。
- resource: 组件的“最小公约数”。该资源可被多个程序使用。例如，“geometry”被所有 X 程序使用，是一个资源。
- value: 资源被设置的值。可以是数字、布尔值（true 或 false）、颜色或其他值。这取决于资源。

从 `!` 到行尾的任何文本都是注释。

# 第 16 章 • X 窗口系统

为了从最具体的组件（程序）到最不具体的组件（资源），必须对组件进行组合。这些组合可以通过点 `.` 或星号 `*` 来指定。点表示紧密绑定（tight binding），星号（asterisk）表示松散绑定（loose binding）。

在松散绑定中，两个组件之间的链接不需要是直接，它的作用几乎类似于 Gray 中的正则表达式。也就是说，你可以有一个如下条：

```
*geometry: 80x25
```

这意味着所有的 geometry 设置都为 80x25。虽然对于基于文本的程序这很好，但对于一个设置为 80x25 像素的图形应用程序来说确实非常小。如果你有一个特定的程序，可以变得更具体。例如，如果你想让所有使用 `vt100` 组件的程序几何尺寸都为 80x25，你可以这样设置：

```
*vt100.geometry: 80x25
```

你还可以设置得更具体。假设你想让你的终端模拟器大小为 80x25，而你想让你的 Seyon² 模拟器大小为 80x40。那么你会有两个设置：

```
xterm.vt100.geometry: 80x25
Seyon.vt100.geometry: 80x40
```

这里是紧密绑定。Seyon 程序使用 `vt100` 组件，然后设置几何尺寸。对 Seyon 使用松散绑定：

```
Seyon*geometry: 80x40
```

这将导致 Seyon 创建的所有窗口都变为 80x40。由于 Seyon 创建了几个基于图形的窗口，这将产生 80 像素乘以 40 像素的图形窗口。

注意，你可以将紧密绑定替换为松散绑定。以下两个条目具有相同的效果：

```
Seyon.vt100.geometry: 80x40
Seyon*vt100.geometry: 80x40
```

以下是几个适用于 xterm 的示例条目：

```
xterm*scrollBar: true    开启左侧的滚动条
```

> ² Seyon 是一个终端模拟器。

## 16.7 APPLICATIONS

除了 xterm 和 Seyon，还有许多其他你可以运行的客户端程序。几乎所有的 X 程序都使用 `-display`、`-geometry`、`-background` 命令以及一些额外的选项。注意，虽然这些选项会覆盖 `Xdefaults` 中的设置，但设置的制定实际上取决于窗口管理器（window manager）。这些选项（以及 `Xdefaults` 中的设置）实际上是对窗口管理器的建议。窗口管理器通常允许这些请求，但可能存在窗口管理器执行自己一套的情况。

- `-fg <color>` 或 `-foreground <color>`—前景
- `-font <font>` 或 `-font <font>`—默认字体
- `-iconic`—以图标形式启动程序
- `-title <text>`—为窗口指定标题

- 可用的 X 应用程序：

- mxh—电子邮件处理器
- bitmap—位图编辑器
- xman—连接到 man 程序的 X 界面
- clock—数字或模拟时
- xcal—计算器
- skill—杀死窗口
- xwd—将窗口图像转储到文件

还有其他不属于 X 项目但有时随 Linux 安装的 X 应用程序：

- seyon—通信程序程序
- xsysinfo—系统信息（CPU 空闲、空闲内存等.）
- xpaint—绘画程序
- ghostview—查看 PostScript 文件

随着 Linux 的普及，“非服务器”应用程序的数量也随之增加。这些程序从无聊的消遣品到通常与 Windows 或 Macintosh 桌面相关的所谓个人生产力应用不等。

我们到为止讨论的大多数应用程序都是面向服务器的或编程语言的。少数几个例外是办公套件、文字处理器和电子表格。

在这里，我们想谈谈某些应用程序。
