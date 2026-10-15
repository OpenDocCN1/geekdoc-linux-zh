
| 0–9 | 样式按此顺序作用于标题栏。 |

| All | 作用于所有。 |

| Left | 仅作用于标题栏的左侧（奇数）。 |

| Right | 仅作用于标题栏的右侧（偶数）。 |

样式函数提供的状态是表 9.16 中的单词之一。如果提供状态，则样式将适用于所有。样式函数提供的样式是表 9.17 中列出的指令之一。在指定状态和/或样式之后，用户可以两个破折号并跟随一系列标志（如有必要）。

### State

| State | Description |

| :--- | :--- |

| Active | 窗口拥有焦点时。此状态仅用于边界。 |

| ActiveUp | 窗口拥有焦点（活动）且控件未处于点击事件（上升）中间。 |

| ActiveDown | 窗口拥有焦点（活动）且控件正处于点击事件（按下）中间。 |

| Inactive | 窗口没有焦点时。 |

### Style

| Style | Description |

| :--- | :--- |

| Default | 指定此装饰使用编译进 `fwwm 2` 的默认样式。 |

| Pixmap file | 使用命名图像作为此装饰的单个像素图。 |

| TiledPixmap file | 使用命名图像作为此装饰的壁纸式像素铺。 |

| Solid color | 使用实色填充装饰。 |

| Vector n pt ... | 之前讨论的 `fwwm` 中 `ButtonStyle` 关键字的等物。点的数由 `n` 决定，每个 `pt` 是有效的点和线条颜色。仅用于按钮样式函数。 |

| Gradient n c1 c2 | 使用从 `c1` 到 `c2` 的 `n` 垂直渐变绘制装饰。注意，另一种更强大的渐变样式在此未被涵盖。 |

| Hgradient n c1 c2 | 使用从 `c1` 到 `c2` 的 `n` 水平渐变绘制装饰。注意，另一种更强大的渐变样式在此未被涵盖。 |

| MiniIcon | 在指定的按钮绘制应用程序的 MiniIcon。MiniIcon 概念将在下一节“`fwwm 2` 装饰与窗口样式”中讨论。仅用于按钮样式函数。 |

## 表 9.18 常用样式标志

| 标志 | 描述 |

| --- | --- |

| UseTitleStyle | 尝试从当前标题样式中获取按钮样式。 |

| UseBorderStyle | 尝试从当前边框样式中获取按钮样式。 |

| Raised | 使装饰呈现出三维的凸效果。 |

| Sunk | 使装饰呈现出三维的凹陷效果。 |

| Flat | 使装饰不带任何三维边缘。 |

| HiddenHandles | 不在边框的角上绘制句柄。仅用于边框样式函数。 |

| NoInset | 不在边框周围绘制内凹斜角，而是保持边框与窗口对齐。仅用于边框样式函数。 |

| Left | 在装饰的左侧开始平铺或显示位图。 |

| Right | 在装饰的右侧开始平铺或显示位图。 |

| Top | 在装饰的顶部开始平铺或显示位图。 |

| Bottom | 在装饰的底部开始平铺或显示位图。 |

尽管新界面具有一致性，但它确实比原始 `fwwm` 中简单的键值对行要复杂得多。然而，获得的灵活性是巨大的。考虑以下示例：

```
TitleInactive Gradient Red Blue -- Flat
TitleActiveTiledPixmap focused.xpm -- Top Left
TitleActiveSolid Red
BorderStyle All -- NoInset HiddenHandles
ButtonStyle All -- UseTitleStyle
AddButtonStyle1 Vector 4 50x201 20x201 80x201
AddButtonStyle2 1 Pixmap bottom-2.xpm
```

前三行定义了未焦点的窗口标题具有从红色到蓝色的水平渐变作为背景颜色。在未聚焦时，标题将以扁平方式绘制，没有三维效果。当窗口获得焦点时，将使用位图 `focused.xpm` 从标题栏的左上角开始平铺作为背景。当标题栏被点击或拖动时，它将变为实红色。

第四行规定窗口边框在内部不应有三维凹斜角，角处不带缩放句柄。

最后三行指定所有按钮都应该从当前标题栏样式获取其初始样式提示。然后，按钮 1（最左侧的按钮）更新为新的矢量图案，按钮 2（最右侧的按钮）更新为新的位图。

# 第 9 章 运行时环境配置

## fwwm 2 装饰与窗口样式

`fwwm 2` 包含的样式处理函数显然强大且灵活，但最好的还在后面。除了刚刚讨论的样式函数外，`fwwm 2` 提供了创建装饰的能力，装饰是可以基于窗口应用的的样式集合。装饰使用 `AddToDecor` 函数构建，如下：

```
AddToDecor decorname
+ StyleFunction [btn] [state] [style] -- [!]flag
+ StyleFunction [btn] [state] [style] -- [!]flag
...
```

再次，可以在任何时间动态地添加装饰，并在遇到文件中的空行时完成添加。一个使用我们上一节样式的示例装饰可能看起来所示：

```
AddToDecor StDecor
+ StyleInactive Red Blue -- Flat
+ StyleActiveUp Tiledmap focused.xpm -- Top Left
+ StyleActiveDown Solid Red
+ BorderStyle All -- NoInset HiddenHandles
+ ButtonStyle All -- UseFontStyle
+ AddButtonStyle 1 Vector 4x5080 20x201 80x201 50x800
+ AddButtonStyle 2 Pixmap button-2.xpm
```

在定义了名为 `StDecor` 的装饰后，用户可以决定窗口样式将其分配给特定窗口。单个窗口的 Basic Style 关键字在 `fwwm 2` 中仍然存在，但在 `fwwm 2` 中它是一个函数。`fwwm 1` 中 `Style` 关键字支持的所有选项仍然适用，表9.19 中的新选项现在也适用。

## 表 9.19 一些 fwwm 2 窗口样式选项

| 样式 | 描述 |

| --- | --- |

| UseStyle | 使用由另一个 Style 函数已定义的样式作为此样式的基础。 |

| UseDecor decor | 在装饰此样式中命名的窗口时使用该名称。 |

| MiniIcon | 使用文件图标作为窗口的微图标，请求时可以绘制在标题按钮中。 |

| IconBox geometry | 指定此窗口的最小化图标应放入指定的图标框中。与 `fwwm 1` 中的 `IconBox` 关键字类似，它仅适用于应用样式的窗口，几何由 `Xt/Athena` 风格的几何字符串给出，如 `100x100-1`。 |

| IconGrid x y | 在指定的图标框中形成一个虚拟网格，每个网格单元宽 `x` 像素，高 `y` 像素；尝试仅在空网格单元中放置图标。 |

# fwm 窗口管理器 227

## 样式

| 样式 | 描述 |

| --- | --- |

| IconFill pos1 pos2 | 在图标框中建立填充重力。`pos` 参数之一必须是顶或底，另一个必须是左或右。例如，`pos1` 设置为左，`pos2` 设置为底部的重力将从左到右、从下到上填充图标框。 |

| MWMBorder/FwmBorder | 分别按照 MWM 样式或 `fwm` 样式绘制窗口边框。 |

| SmartPlacement | 智能地放置此窗口。 |

| DumbPlacement | 不要尝试智能地放置此窗口。 |

| RandomPlacement | 以随机方式放置此窗口。 |

| ActivePlacement | 允许用户手动放置此窗口。 |

| DecorateTransient | 装饰弹出对话框窗口。 |

| NakedTransient | 不装饰弹出对话框窗口。 |

| SkipMapping | 允许窗口出现在视觉桌面区域之外并进行放置。 |

| ShowMapping | 始终按照窗口出现和放置的位置显示窗口。 |

| ClickToFocus | 要求点击此窗口以接收焦点。 |

| SloppyFocus | 允许此窗口在鼠标指针进入时随时接受焦点；如果鼠标指针再次离开并仅进入根窗口，则保持焦点。 |

| MouseFocus | 允许此窗口在鼠标指针进入时随时接受焦点；一旦鼠标指针丢失，立即失去焦点。 |

有关其余其他新样式选项的信息，请参阅 `fwm2` 手册。请注意 `Ustyle` 和 `UseDecor` 选项都存在。通过这两个样式选项，可以逐个窗口地为所有窗口分配给定的焦点、颜色和字体样式（作为装饰和标题样式）。以下配置段说明了了：
