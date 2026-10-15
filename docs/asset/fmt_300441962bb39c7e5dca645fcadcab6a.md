
```vb
' define a point that represents
' the (100, 100) position.
Dim pt As New Drawing.Point(100, 100)
```

### Size 对象

`Size` 对象表示特定对象的大小。要创建 `Size` 对象的实例，请将宽度和高度传递给构造函数。属性 `Width` 和 `Height` 存储您指定的值。

示例：

```vb
' define a size of 200 pixels across
' and 100 pixels in height.
Dim sz As New Size(200, 100)
```

### Rectangle 对象

`Rectangle` 对象指定一组四个坐标来定义矩形的大小。本章中的许多图形原语都使用 `Rectangle` 对象。要创建 `Rectangle` 对象的新的实例，请传递左坐标 x、上坐标 y，以及宽度和高度。属性 `Left`、`Top`、`Width` 和 `Height` 存储您指定的每个值。

示例：

```vb
' define a rectangle that starts at
' position (100, 100), is 200 pixels
' across, and 50 high.
Dim rect As New Drawing.Rectangle(100, 100, 200, 50)
```

### 颜色

`Graphics` 对象以 ARGB 格式处理颜色。0-255 的值表示透明度（alpha 混合），以及每个红色、绿色和蓝色值的 0-255 范围组合起来创建完整的 32 位颜色集。要创建自定义颜色，请调用 `Color.FromArgb` 方法或指定组合的 ARGB 整数或用逗号分隔四个值。该函数使用给定的颜色或生成适当的组合数字并返回一个 `Color` 对象。

VB 通过 `Drawing.Color` 对象按名称为您提供大量颜色。颜色范围从 `AliceBlue` 到 `YellowGreen`。下面是 `Color` 对象中可用颜色的部分列表。要获取完整列表，请在 VB.NET 帮助中搜索，输入 `Color members`。

### Sample System.Drawing.Color Members

| Color | Color | Color | Color |

|---|---|---|---|

| AliceBlue | AntiqueWhite | Aqua | Beige |

| Black | Blue | BlueViolet | Brown |

| CadetBlue | Chartreuse | Chocolate | Coral |

| CornflowerBlue | Crimson | Cyan | ForestGreen |

| Fuchsia | GhostWhite | Gold | Goldenrod |

| Gray | Green | GreenYellow | Honeydew |

| Indigo | Ivory | Khaki | Lavender |

| Lime | LimeGreen | Linen | Magenta |

| Maroon | MidnightBlue | Navy | OldLace |

| Olive | Orange | OrangeRed | Orchid |

| Peru | Pink | Plum | PowderBlue |

| Purple | Red | RoyalBlue | Salmon |

| SandyBrown | SeaGreen | Sienna | Silver |

| SkyBlue | SlateBlue | SlateGray | Snow |

| SpringGreen | SteelBlue | Tan | Teal |

| Thistle | Transparent | Turquoise | Violet |

| White | WhiteSmoke | Yellow | YellowGreen |

## 创建画刷

您使用 `Brush` 类来告诉 VB.NET 如何填充区域。每个填充的基元（例如填充矩形）都需要使用 `Brush` 来指定如何填充区域。要生成一个可在 VB.NET 中使用的 `Brush`，请使用 `New` 运算符创建 `Brush` 类型的实例。VB 根据您需要的样式提供了许多 `Brush` 类。每个画刷都有特定的大小。如果要填充的形状大于画刷，画刷会平铺以填充整个空间。

`System.Drawing` 命名空间包含 `SolidBrush` 和 `TextureBrush` 类。`SolidBrush` 以单一颜色绘制区域。将画刷的颜色作为唯一参数传入。由于这些画刷是纯色的，因此画刷的大小仅为 1 x 1。

`System.Drawing.Drawing2D` 命名空间包含许多更复杂的画刷。`HatchBrush` 基于图案创建画刷。Windows 提供了一组 2 位阴影图案。VB.NET 在 `HatchStyle` 枚举中为这些图案提供了常量，范围从 `BackwardDiagonal` 到 `ZigZag`。要创建画刷，请声明一个 `HatchBrush` 类的实例，并将要使用的图案传递给构造函数，前景色作为第二个参数，背景色作为第三个参数。

`LinearGradientBrush` 以任意角度从一个颜色到另一个颜色进行平滑过渡。对于构造函数，传递一个 `Rectangle` 类的实例，其中包含要创建的渐变画刷的大小。下一个参数指定开始颜色，第三个参数指定结束颜色。请参阅“了解 Graphics 对象”一节来指定颜色。最后一个参数是渐变的度数角度。0 度创建水平渐变，90 度创建垂直渐变。

## 创建纯色画刷

- 1. 创建一个新项目或打开现有项目。
- 2. 单击类列表并选择（基类事件）或要绘制的控件。
- 3. 单击方法名称列表并选择 `Paint` 事件。
- 4. 键入 `Dim redBrush As New Drawing.SolidBrush(Color.Red)`，将 `redBrush` 替换为画刷的名称，将 `Color.Red` 替换为颜色。

## 创建阴影画刷

- 5. 键入 `Dim confettiBrush As New Drawing2D.HatchBrush()`，将 `confettiBrush` 替换为画刷的名称。
- 6. 在括号内，键入要使用的阴影图案，后跟前景色和背景色，全部用逗号分隔。

![](img/d6f772854306e15fb6df39b861a7b541_157_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_157_1.png)

## 补充

如果您需要简单的纯色画刷，可能会觉得不断创建自定义画刷对象很耗时。但是，您可以使用预先创建好的画刷来省去创建 `SolidBrush` 类新实例的麻烦。`System.Drawing.Brushes` 类为标准颜色列表中的每种颜色提供了一组画刷。有关常见颜色选择的列表，请参阅“使用 Graphics 对象”一节。

在 Windows 中，用户会在桌面首选项中设置各种颜色，所有 Windows 应用程序都以相同的方式响应。您可能想要在窗体上绘制，但需要遵循用户选择的 Windows 颜色。您可以使用 `SystemBrushes` 类以特定系统颜色填充区域。`SystemBrushes` 类是 `System.Drawing` 命名空间的一部分。例如，`SystemBrushes.Desktop` 返回当前用户桌面颜色的画刷。您还可以使用 `SystemColors` 类检索每个画刷所依赖的单个颜色值。您可以在“帮助”中键入“`SystemBrushes members`”来搜索可用系统颜色的完整列表。

```
Example:
Dim myPlum As Drawing.SolidBrush =
    Drawing.Brushes.Plum
```

```
Example:
Dim myControlColor As
    Drawing.SolidBrush =
    Drawing.SystemBrushes.Control
```

![](img/d6f772854306e15fb6df39b861a7b541_158_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_158_1.png)

## 创建线性渐变画刷

- 7 声明一个 `Rectangle` 对象。
- 注意：请参阅“使用您的 Graphics 对象”一节来创建 `Rectangle`。
- 8 键入 `Dim gradient As New Drawing2D.LinearGradientBrush`，将 `LinearGradient` 替换为画刷的名称。
- 9 在括号内，键入 `Rectangle` 名称、开始和结束颜色，以及旋转角度，用逗号分隔。
- 10 键入使用画刷的代码。
- 11 按 `F5` 运行项目。

画刷绘制到要填充的区域，如有必要会进行平铺。

## 创建画笔
