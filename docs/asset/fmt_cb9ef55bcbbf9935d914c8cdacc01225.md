
```
Style ** Icon unknown.xpm, color white/gray, BorderWidth 4
Style "xtern" Icon.xpm, color red/blue, BorderWidth 2
Style "xclock" NoTitle, WindowlistSkip, NoHandles, BorderWidth 2
```

第一行规定所有应用程序（通配符字符）在最小化时应使用 `unknown.xpm` 图标。未焦点的标题栏和装饰应显示为灰色背景上的白色，边框应为四像素宽。第二行表示该样式的例外是 `xtern` 应用程序，它在最小化时应使用文件 `xtern.xpm` 作为其图标，未聚焦时应显示为蓝色背景上的红色，且边框宽度仅为两像素。第三行表示 `xclock` 应用程序不应被赋予标题栏或边框句柄，边框宽度应为两像素，且不应出现在窗口列表中。

# fwwm 2 基础

`fwwm 1` 是如此灵活的，以至于配置它往往会变成一整天的工作，然而 `fwwm 2` 至少是 `fwm` 窗口管理器的四倍，引入了令人眼花缭的功能和关键字，并从根本上重构了配置文件的格式。遗憾的是，开发 `fwm 2` 远超本文的范围；它的复杂性是无法简化，而且通常更像是一种编程语言而不是配置文件。

`Style` 关键字仅仅提供了一种方便的机制，通过该机制可以同时配置单个窗口或一类窗口，并且具有极大的灵活性。例如，考虑以下配置文件的段落：

```
Style ** Icon unknown.xpm, color white/gray, BorderWidth 4
Style "xtern" Icon.xpm, color red/blue, BorderWidth 2
Style "xclock" NoTitle, WindowlistSkip, NoHandles, BorderWidth 2
```

第一行规定所有应用程序（通配符字符）在最小化时应使用 `unknown.xpm` 图标。未焦点的标题栏和装饰应显示为灰色背景上的白色，边框应为四像素宽。第二行表示该样式的例外是 `xtern` 应用程序，它在最小化时应使用文件 `xtern.xpm` 作为其图标，未聚焦时应显示为蓝色背景上的红色，且边框宽度仅为两像素。第三行表示 `xclock` 应用程序不应被赋予标题栏或边框句柄，边框宽度应为两像素，且不应出现在窗口列表中。

使用这种样式，可以微配置桌面的外观，甚至是单个窗口顶部出现的功能按钮——这在其他操作系统中，甚至在使用许多窗口管理器时都是无法实现的。

# 菜单样式

`fwwm 2` 菜单的颜色不再由简单的关键字和颜色对控制；`fwwm 2` 实现了一套改进巨大且灵活得多的菜单样式系统，其中按命名的菜单样式 `MenuStyle` 函数是其核心。

## fwwm 窗口管理器

`MenuStyle` 函数的语法非常简单：

`MenuStyle stylename option, [option, ...]`

格式简单，但 `MenuStyle` 函数支持的选项列表很大。这些选项中最基础的如表 9.13 所示。

### 表 9.13 基础 MenuStyle 选项

| 选项 | 说明 |
| :--- | :--- |
| `FWWM` | 以传统的 `fwwm` 样式绘制菜单，具有三维效果，子菜单会重叠父菜单，并有延迟弹出。 |
| `MWM` | 以 `MWM` 窗口器的样式绘制菜单，具有三维效果，子菜单不会重叠父菜单，并即时弹出。 |
| `WIN` | 以 `Windows` 样式绘制菜单，具有平面的实色效果，子菜单不会重叠父菜单，并即时弹出。 |
| `Foreground color` | 使用该颜色作为菜单中的文本颜色。 |
| `Background color` | 使用该颜色作为此菜单的背景色。 |
| `Font XLFD` | 使用指定的字体作为菜单条目的字体。 |
| `MenuFace style` | 使用华丽的糖果像素图（pixmaps）或渐变色作为此菜单的背景。该样式是本文后续其他样式支持的选项之一。还可以使用另外两种渐变样式 `DGradient` 和 `BGradient`（均为对角）。 |

例如，考虑以下菜单样式定义：

`MenuStyle NormalMenus WIN, Foreground, Background white`

此样式定义了一个名为 `NormalMenus` 的样式，它将产生蓝色背景白字的 `Windows` 风格菜单。要使用像 `NormalMenus` 这样的样式，必须使用 `ChangeMenuStyle` 函数。`ChangeMenuStyle` 函数的语法简单，如下：

`ChangeMenuStyle menename [menuname ...]`

例如，为名为 `MainMenu`、`ExitStuff` 和 `OpsStuff` 的菜单分配我们创建的样式，函数如下：

`ChangeMenuStyle NormalMenus MainMenu ExitStuff OpsStuff`

与 `fwwm 2` 中的其他所有内容一样，由于 `MenuStyle` 和 `ChangeMenuStyle` 是函数，它们可以绑定到键盘或鼠标点击上，或者从菜单内部调用以在运行时触发菜单。

# 第 9 章 运行时环境配置

## fwwm 2 函数

`fwwm 2` 中创建函数的新机制与创建菜单的新机制类似。所涉及的函数是 `AddToFunc`，其用法如下：

```
AddToFunc FunctionName "trigger" Function
+ "trigger" Function
+ "trigger" Function
```

再次，不需要 `EndFunction` 关键字；`fwwm 2` 在遇到第一个空行时将停止向命名函数添加内容。

`fwwm 2` 中的事件触发器与 `fwwm` 中的触发器名称不同。`fwwm 2` 中的触发器仅由 `fwwm` 原触发器名的首字母表示：`Immediate` 变为 `I`，`Motion` 变为 `M`，以此此类推。作为 `fwwm` 示例的 `MoveRaiseLowerMaximize` 函数在 `fwwm 2` 中定义如下：

```
AddToFunc MoveRaiseLowerMaximize "M" Raise
+ "M" Move
+ "C" RaiseLower
+ "D" Maximize 80 80
```

`AddToFunc` 也是 `fwwm 2` 中的一个函数，与 `fwwm` 中的 `Function` 关键字不同。这意味着 `fwwm 2` 函数可以根据用户交互在运行时动态构建，这是一个强大的功能，需要一些练习才能使用。

注意，两个特殊函数 `InitFunction` 和 `RestartFunction` 在 `fwwm 2` 中也存在，并可以以相同的方式使用，尽管它们必须使用新的 `AddToFunc` 函数而不是 `fwwm` 函数关键字来定义。

## fwwm 2 外观与样式处理

除了一套大量更新的函数以及在运行时动态重新构建或编辑菜单和函数的能力外，`fwwm 2` 还提供了一套新的、强大的样式处理函数，允许各种样式应用于各种类型的窗口管理器对象。由于这些是 `fwwm 2` 中定义窗口、网格、装饰外观的主要方法，因此稍微了解它们非常重要。遗憾的是，它们和实用性一样复杂；掌握它们需要练习。

基础的 `fwwm 2` 样式范式规定，窗口管理器中的每个对象（从按钮到标题栏到窗口）都有可以配置的属性。配置通过样式函数指定，并可以使用 `AddStyle` 函数更新任意次。配置也可以通过 `UseStyle` 选项应用于对象之间，以便装饰可以共享外观。样式函数在后的段落中概述；其基本格式为：

```
StyleFunction [btn] [state] [style] [!] ...
```

`Style` 函数是表 9.14 列出的函数之一。以 `Add` 开头的函数在现有样式基础上实现新样式。不以 `Add` 开头的函数则替换现有样式。对于影响标题栏按钮的样式函数，需要按照表 9.15 指定按钮；否则，不指定按钮。

### 表 9.14 fwwm 2 样式函数

| Function | Description |
| :--- | :--- |
| `ButtonStyle` | 实现新的标题栏按钮样式。 |
| `AddButtonStyle` | 向现有的标题栏样式中添加新元素。 |
| `TitleStyle` | 实现新的标题栏样式。 |
| `AddTitleStyle` | 向现有的标题栏样式中添加新元素。 |
| `BorderStyle` | 实现新的窗口边界样式。 |
| `AddBorderStyle` | 向现有的窗口边界样式中添加新元素。 |

### 表 9.15 fwwm 2 样式的按钮规格

| Specifier | Button |
| :--- | :--- |
