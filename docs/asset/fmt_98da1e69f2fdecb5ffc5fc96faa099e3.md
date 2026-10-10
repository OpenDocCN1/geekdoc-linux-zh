
## 使用 xvidtune 进行调优

在你使配置基本工作后，可以使用 X Window 实用程序 `xvidtune` 对其进行调优。通过此工具，你可以对屏幕的位置和大小进行微调。图 16-1 显示了该程序提供的控制面板。

| Hdisplay: 1200 | Vdisplay: 1024 |
| HSyncStart: 1320 | VSyncStart: 1026 |
| HSyncEnd: 1512 | VSyncEnd: 1026 |

使用 6 位宽查找表（或在 6 位模式下）
第二段视频：Hercules
芯片组：标准版

随后，你可以找到关于 `XFree86` 配置程序的信息，例如 `XConfigurator`、`XF86Setup` 或 `xf86config`。这些程序均可用于配置 `XFree86`。其中一些易于使用，另一些更为完整。接下来的几节将讨论每个程序的特性。

## 使用 XConfigurator

我们已在第 3 章中介绍过 `XConfigurator` 程序。它是最简单、最易使用的程序，但它并没有涵盖所有情况。你可能需要使用技术上更复杂的工具。

## 使用 XF86Setup

如果 `XConfigurator` 不起作用，你可以尝试 `XF86Setup`。`XF86Setup` 是一个基于 GUI 的程序，它使用基本的 VGA 服务器来显示其图形。该程序对写入配置文件的内容提供了大量的控制。要使用此程序，请使用以下命令运行它：

```
[root@pc root]$ XF86Setup
```
