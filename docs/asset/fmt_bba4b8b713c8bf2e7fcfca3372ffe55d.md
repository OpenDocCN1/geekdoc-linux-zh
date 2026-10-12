
几个 Tk 组件，如 `label`、`text` 和 `canvas`，允许你指定用于显示文本的字体，通常通过 `font` 配置选项。与 Tk 中的许多事物一样，默认字体通常是不错的选择，但如果你确实想要进行修改，本节将描述几种方法。字体是几个高度平台相关的领域之一，因此如何指定它们很重要。

字体命令参考提供了关于指定字体以及其它字体相关操作的完整细节。

大多数显示文本的主题组件没有 `font` 配置选项，这与经典 Tk 组件不同。与其修改单个组件，在主题组件中正确的做法是指定样式中使用的字体，然后使用该样式为单个组件设置。这类似于在 HTML 页面中硬编码面向显示的标记（如字体标签）与使用 CSS 样式表将所有显示特定信息集中在一处之间的区别。

许多旧的 Tk 程序硬编码了大量字体，使用我们在下面看到的 `family size style` 格式、`X11` 字体名称或更旧且更晦涩的 X11 字体规范字符串。在许多情况下，随着平台的发展，这使得这些应用程序看起来过时了。此外，许多程序按单个组件指定字体，导致字体决策分散在整个程序中。使用命名字体以及 Tk 提供的标准字体是更好的解决方案。审查和更新现有应用程序中的字体使用是一个简单且重要的改动。

### 标准字体

特别是对于或多或少标准的用户界面元素，每个平台都定义了应使用的特定字体。Tk 将其中许多封装在一组始终可用的标准字体中，当然，标准组件使用这些字体。这有助于抽象平台差异。预定义的字体是：

| 字体名称 | 描述 |
|-----------------|-----------------------------------------------------------------------------|
| `TkDefaultFont` | 所有未特别指定的 GUI 项目的默认字体。 |
| `TkTextFont` | 用于 `entry` 组件、`listbox` 等。 |
| `TkFixedFont` | 标准固定宽度字体。 |
| `TkMenuFont` | 用于菜单项的字体。 |
| `TkHeadingFont` | 通常用于列表和表格列标题的字体。 |
| `TkCaptionFont` | 用于窗口和对话框标题栏的字体。 |
| `TkSmallCaptionFont` | 用于子窗口或工具对话框的较小标题字体 |
| `TkIconFont` | 用于图标说明的字体。 |
| `TkTooltipFont` | 用于工具提示的字体。 |

### 平台特定字体

还有一些可用的预定义字体，但具体集合取决于平台。显然，如果你使用这些字体，并且你的应用程序在不同平台之间可移植，你需要确保为每个平台单独定义适当的字体。

在 X11 上，可以使用任何有效的 X11 字体名称（参见例如 `xlsfonts` 命令）。但请记住，没有保证特定字体已在特定机器上安装。

在 Windows 上，可以使用以下映射到“显示”控制面板中可设置的字体的字体名称：`system, ansi, device, systemfixed, ansifixed, oemfixed`。

在 Mac OS X 上，可以使用以下字体（详情参见 Apple HIG）：`systemSystemFont, systemSmallSystemFont, systemApplicationFont, systemViewsFont, systemMenuItemFont, systemMenuItemCmdKeyFont, systemPushButtonFont, systemAlertHeaderFont, systemMiniSystemFont, systemDetailEmphasizedSystemFont, systemEmphasizedSystemFont, systemSmallEmphasizedSystemFont, systemLabelFont, systemMenuTitleFont, systemMenuItemMarkFont, systemWindowTitleFont, systemUtilityWindowTitleFont, systemToolbarFont, systemDetailSystemFont`。

### 命名字体

你还可以创建自己的字体，其用法与预定义字体完全相同。为此，你需要选择一个名称来引用该字体，然后指定定义字体外观的各种字体属性。通常，你会在不同平台上使用不同的字体属性；这样，你可以在程序中使用字体而无需担心细节，只需在字体实际定义的那个地方处理即可。

这是一个示例：

```python
from tkinter import font
appHighlightFont = font.Font(family='Helvetica', size=12, weight='bold')
ttk.Label(root, text='Attention!', font=appHighlightFont).grid()
```

### 字体描述

`family` 指定字体名称；`Courier`、`Times` 和 `Helvetica` 的名称保证受支持（并映射到合适的等宽、衬线或无衬线字体），但也可以使用系统中安装的其他字体（同样，务必注意确保该字体存在，否则系统将提供不同的字体，这可能并不一定是最佳匹配）。您可以使用以下命令获取所有可用字体的名称：

```python
font.families()
```

`size` 选项以磅（points）为单位指定字体大小。`weight` 选项可以是 `bold` 或 `normal`。您可以指定 `slant` 为 `roman` 或 `italic`。最后，布尔选项 `underline` 和 `overstrike` 也可用。

可以使用与更改小部件配置选项相同的机制来检查或更改这些选项的当前设置（例如 `configure`）。

另一种指定字体的方式是使用属性列表，以字体名称开头，然后可选地包含字号，以及可选的一个或多个样式选项。一些示例包括 `"Helvetica"`、`"Helvetica 12"`、`"Helvetica 12 bold"` 和 `"Helvetica 12 bold italic"`。这些字体描述随后用作 `font` 配置选项的值，而不是预定义或命名字体。

> 一般来说，建议从字体描述切换到命名字体，以便再次将字体差异隔离在程序中的一个位置。

### 颜色

与字体一样，有各种方式可以指定颜色。完整细节可以在颜色命令参考中找到。

一般来说，系统将为大多数内容提供正确的颜色。与字体类似，Mac 和 Windows 都指定了大量系统特定的颜色名称（参见参考手册），其实际颜色可能取决于系统设置（例如文本高亮颜色、默认背景）。

您也可以通过 RGB 指定颜色，就像在 HTML 中一样，例如 `"#3FF"` 或 `"#FF016A"`。最后，Tk 识别 X11 定义的一组颜色名称；通常这些名称不使用，除非是一些非常常见的名称，如 `"red"`、`"black"` 等。

对于主题化的 Tk 小部件，颜色通常用于定义应用于小部件的样式，而不是直接对应用颜色到小部件上。

可能不用说也明白，在颜色的使用上通常应当有所节制。

### 图像

我们已经看到过使用图像的基本方法，例如在标签或按钮中显示它们。我们创建图像对象，通常是从磁盘上的文件创建。

```python
imgobj = PhotoImage(file="myimage.gif")
label["image"] = imgobj
```

开箱即用，Tk 支持 GIF 和 PPM/PNM 图像。然而，有一个名为 `Img` 的 Tk 扩展库，它为许多其他格式添加了支持：BMP、XBM、XPM、PNG、JPEG、TIFF 等。虽然 `Img` 没有直接包含在 Tk 核心中，但它通常与其他打包分发版一起包含（例如 ActiveTcl）。

PYTHONTODO

Tk 的图像实际上非常强大且复杂，提供了多种检查和修改图像的方式。您可以从图像命令参考和照片命令参考中了解更多内容。

> *我们在这里看到的这种多色图像类型在 Tk 中被称为照片图像。Tk 还提供了另一种类型的图像，即双位位图图像，它们在 90 年代被广泛使用，当时大多数 Unix 工作站使用相当大的（与个人电脑相比）显示器，但它们的图像只有黑白。不用说，如今彩色是标配，因此强烈建议将图标等更新为全彩图像。*

### 画布

- 小部件概览
- 参考手册

**画布**（`canvas`）小部件管理一个 2D 图形对象集合——线条、圆形、图像、其他小部件等。Tk 的画布是一个极其强大且灵活的小部件，无疑是 Tk 的亮点之一。它适用于广泛的应用，包括绘图或制图、CAD 工具、显示或监控模拟或实际设备，以及用简单组件构建更复杂的小部件。画布小部件属于经典 Tk 小部件，而非主题化 Tk 小部件。

![](img/94378c1b05607c1dc5649c738af95c74_62_0.png)

画布小部件使用 `Canvas` 函数创建：

```python
canvas = Canvas(parent)
```
