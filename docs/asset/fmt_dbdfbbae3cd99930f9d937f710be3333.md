
如果命令行上没有指定特定的程序，`xinit` 将在用户主目录下查找 `.xserverrc` 文件并作为 shell 脚本运行客户端程序。如果不存在此类文件，`xinit` 将使用以下作为默认值：

注意服务器。然而，用户随后选择了菜单项来关闭 X。

`xrdb -load HOME/.Resources xsetroot -solid gray &`

# 第一部分：用户命令

```
xclock -g 8x50-50+ -bw 0 &\
xload -g 8x50-50+ -bw 0 &\
xterm -g 80x24+24-0 &\
xterm -g 80x24+24-0 &\
ntwm
```

想要创建通用启动环境的站点可以创建一个默认的 `xinitrc`，该文件引用一个站点级的启动文件：

```sh
#!/bin/sh
/usr/local/lib/site.xinitrc
```

另一种方法是编写一个脚本，使用特定的 shell 脚本启动 `xinit`。此类脚本通常命名为 `xist`、`xstart` 或 `startx`，是为用户提供简单界的方便方式：

```sh
#!/bin/sh
xinit /usr/local/lib/site.xinitrc -- /usr/X11R6/bin/X bc
```

# 环境变量

`DISPLAY`

`XINITRC`

此变量被设置为客户端连接的显示名称。

此变量指定包含启动初始窗口命令的初始化文件。默认情况下，将使用主目录下的 `xinitrc`。

# 文件

`.xintrc`

`xterm`

`.xerverrc`

`X`

| 说明 | 状态 |
| :--- | :--- |
| 默认客户端脚本 | 运行 `.xintrc` 的客户端不存在 |
| 默认服务器脚本 | 运行 `.xerverrc` 的服务器不存在 |

# 另请

`X(1)`, `startx(1)`, `Xserver(1)`, `xterm(1)`

## 作者

Bob Scheifer (MIT 计算机科学实验室)

X 版本 11 发布 6

# xkill

`xkill`—通过其 X 资源杀死客户端

## 概览

`xkill [-display displayname] [-id resource] [-button number] [-frame] [-all]`

## 描述

`xkill` 是一个用于强制 X 服务器关闭与客户端连接的实用。该程序非常危险，但对于终止在用户屏幕上显示了非预期窗口的程序非常有用。如果没有通过 `-id` 提供资源标识，`xkill` 将显示一个特殊的光标作为提示，让用户选择要杀死的窗口。如果在一个非根窗口上按下指针按钮，服务器将关闭创建该窗口的客户端的连接。

## 选项

`-display displayname`

`-id resource`

`-button number`

`-all`

`-frame`

此选项指定要联系的 X 服务器的名称。

此选项指定要终止的资源创建者的 X 标识。如果没有指定资源，`xkill` 将显示一个特殊光标，您应该通过它选择一个要杀死的窗口。

此选项指定在选择窗口时应使用的指针按钮数。如果指定了单词 `"any"`，则可以使用指针映射上的任何按钮。使用指针映射中的第一个按钮（通常是最左侧的按钮）。

此选项指示屏幕上所有具有顶层窗口的客户端都应该被杀死。`xkill` 将要求您使用当前定义的每个按钮来选择窗口，以给您提供多次终止的机会。强烈不建议使用此选项。

此选项指示 `xkill` 将忽略查找顶层客户端窗口的标准惯例（这些窗口通常嵌套在窗口管理器窗口内），并简单地认为你想杀死根的直接子节点。

# XDEFAULTS

`Button`

在选择窗口时指定使用特定的指针按钮编号或单词 `"any"`。

# 另请

`X(1)`, `xwininfo(1)`, 程序员手册中的 `XClient` 和 `XGetPointerMapping`，X 规范中的 `KillClient`

## 作者

Jim Fulton (MIT X 委员会) 和 Dana Chee (Bellmore)

X 版本 11 发布 6

# xlogo

`xlogo`—X窗口系统标志

## 概览

```
xlogo [-toolkitoption ...]
```

## 描述

`xlogo` 程序显示 X窗口系统标志。

## 选项

`xlogo` 接受所有标准的 X Toolkit 命令行选项，以及以下选项：

`-shape`

此选项指示标志窗口应该是形状化的而不是矩形的。

# 第一部分：用户命令

# 资源

默认宽度和默认高度均为 100 像素。此程序使用 Athena 组件集中的 Logo 组件。它还理解所有的 Simple 组件资源名称和类名：

`-foreground (class Foreground)`

指定标志的颜色。默认值取决于是否指定了 `reverseVideo`。如果指定了 `reverseVideo`，默认值为 `xtDefaultForeground`，否则默认值为 `xtDefaultBackground`。

`shapeWindow (class ShapeWindow)`

指定窗口被形状化为 X 标志。默认为 False。

# 组件

为了指定资源，了解组成 `xlogo` 的组件的层级结构很有用。在表示法中，缩进表示层级结构。首先给出组件类名，然后是组件实例名。

`Xlogo xlogo`

`Logo xlogo`

- `DISPLAY` 获取默认的主机和显示器编号。

获取资源文件的名称，该文件覆盖存储在 `RESOURCE_MANAGER` 属性中的全局资源。

## 环境

# 文件

`<XRoot>/lib/X11/app-defaults/Xlogo` 指定所需的资源

# 另请

`X(l)`, `xrdb(1)`

## 作者

Apollo Computer 的 Ollie Jones 和 MIT X 委员会的 Jim Fulton 根据 Apollo Computer 的 Danny Chong 和 Ross Chapman 的设计编写了标志图形例程。

> X 版本 11 发布

# xlsatoms

`xlsatoms`—列出在服务器上定义的内部原子（interned atoms）

## 概览

`xlsatoms [-options ...]`

## 描述

`xlsatoms` 列出内部原子。默认情况下，将列出从 1（协议定义的最低原子值）开始的所有原子，直到找到未知的原子。如果给出了显式范围，`xlsatoms` 将尝试范围内的所有原子，无论其中是否有未定义的原子。

# xlclients

66

## 选项

`-display dpy`
