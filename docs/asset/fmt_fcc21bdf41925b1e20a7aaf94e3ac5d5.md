
DrawRectangles 使用单个 Pen 绘制一系列矩形。将 `Pen` 作为第一个参数，`Rectangle` 对象数组作为第二个参数传递。

DrawPolygon 根据一组点绘制多边形。它会自动连接第一个点和最后一个点。参数传递 `Pen` 和 `Point` 对象数组。

![](img/d6f772854306e15fb6df39b861a7b541_163_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_163_1.png)

1. 创建或打开一个 Windows 应用程序项目，然后双击您要绘制的窗体。
2. 单击类列表，然后选择（基类事件）或要绘制的控件。
3. 单击方法名称列表，然后选择 Paint 事件。
4. 声明 `Pen` 类的一个新实例。
5. 键入 `e.Graphics.DrawEllipse`，并将 `DrawEllipse` 替换为要绘制的方法名。

注意：要声明 `Pen`，请参阅“创建 Pen”一节。

### 扩展

您可以使用 `Graphics` 对象创建填充区域，其中包含一组用于绘制填充图元的方法。您可以像使用 `DrawLine` 和 `DrawEllipse` 等绘图命令一样使用这些命令创建图元，不同之处在于这些命令填充区域而不是绘制轮廓。这些方法中的每一个都接受与其对应的轮廓绘制方法相同的参数，只是将 `Pen` 参数替换为 `Brush`。要创建 `Brush`，请参阅“创建 Brush”一节。`FillRectangle` 使用提供的 `Brush` 填充矩形空间。`FillEllipse` 填充椭圆区域。`FillRectangles` 填充一系列矩形。`FillPolygon` 根据一组点填充多边形区域。如果要绘制带边框的填充区域，可以组合使用这两个命令。先绘制填充图元，然后将同样的大小和参数传递给轮廓图元。以相反的顺序调用这些方法会导致填充覆盖 `Pen`。

示例：

```vb
Dim rect As New Drawing.Rectangle(50, 50, 200, 100)
Dim redBrush As Drawing.SolidBrush = _
System.Drawing.Brushes.Red
e.Graphics.FillEllipse(redBrush, rect)
```

![](img/d6f772854306e15fb6df39b861a7b541_164_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_164_1.png)

6. 在括号内输入适当的参数。
7. 按 `F5` 运行您的项目。

窗体绘制该图元。

## 绘制曲线

VB.NET 提供了一组用于绘制曲线的函数，这些复杂的线条形式使用高级算法，仅凭几个参考点即可绘制。您可以使用简单的图形图元命令来创建各种曲线和形状。

`DrawArc` 方法是最简单的曲线命令，因为它绘制椭圆的一部分。您需要将 `Pen` 作为第一个参数传给该方法。对于接下来的参数，您可以传递一个包含整个椭圆尺寸的 `Rectangle`，或者四个表示椭圆尺寸的整数或 `Single`。在这些参数之后，您需要指定开始角度，然后是扫描角度，两者均以度为单位。角度从 x 轴开始顺时针测量。`DrawPie` 和 `FillPie` 方法绘制类似弧线的饼形楔形，不同之处在于有两条线绘制到椭圆的中心。由于 `FillPie` 创建填充区域，因此第一个参数传递 `Brush` 而不是 `Pen`。

`DrawCurve` 方法通过指定的点数组绘制曲线。`DrawCurve` 构造函数的第一个参数是用于绘制曲线的 `Pen`。第二个参数是 `Point` 类的数组，它指定绘制曲线所经过的点。另一个构造函数采用相同的两个参数，并加上张力（tension）作为第三个参数。张力为零时会创建一条直线。

`DrawClosedCurve` 绘制一条曲线，并用一条线连接曲线中的第一个点和最后一个点。基本构造函数只需要 `Pen` 和 `Point()`，例如 `DrawCurve`。另一个构造函数采用这两个参数，加上张力作为第三个参数，以及来自 `FillMode` 枚举的常量作为第四个参数。`FillMode` 决定曲线的哪一部分包围该区域。`FillClosedCurve` 填充曲线的封闭空间。您需要传入 `Brush` 作为第一个参数，而不是 `Pen`。

![](img/d6f772854306e15fb6df39b861a7b541_165_0.png)

1. 创建新的 Windows 应用程序项目，或打开现有项目。
2. 打开需要绘制曲线的 Paint 事件。
3. 声明一个 `Pen` 来绘制曲线。
4. 要绘制弧线或饼图，键入 `e.Graphics.DrawPie(myPen,` 并将 `DrawPie` 替换为 `DrawPie` 或 `DrawArc`，将 `myPen` 替换为 `Pen` 对象的名称。
5. 键入一个表示尺寸的 `Rectangle` 对象。
6. 键入逗号，然后跟随开始角度和扫描角度。

要使用填充例程，您也可以声明一个 `Brush`。注意：要创建 `Pen`，请参阅“创建 Pen”一节。要创建 `Brush`，请参阅“创建 Brush”一节。

### Extra

你可以使用 `FillMode` 枚举为具有复杂形状的对象创建不同的填充模式，例如曲线。你有两种 `FillMode` 选项：`Winding`，以及默认的 `Alternate`。`Alternate` 穿过曲线，并在遇到曲线线条时在填充和不填充之间交替。`Winding` 使用曲线的方向来确定是否填充它。通常，默认的 `Alternate` 能有效完成工作，但在 `Alternate` 未给出适当结果时，你可以尝试 `Winding`。

你可以使用 `Bezier` 曲线，一种更高级的三次曲线，来指定曲率的更精确坐标。大多数专业绘图应用程序使用 `Bezier` 曲线而不是 `DrawCurve` 使用的更简单的 cardinal spline 曲线。要绘制 `Bezier` 曲线，你使用 `DrawBezier` 方法，该方法仅绘制由四个点定义的单一曲线。该方法需要一个 `Pen` 对象，其后跟四个 `Point` 对象作为参数。第一个和最后一个 `Point` 对象构成曲线的端点。两个中间的 `Point` 对象构成创建所需曲率的两个控制点。绘制曲线时，它会将曲线拉向控制点。

```
Example:
e.Graphics.DrawBezier(Drawing.Pens.Red, _
    New Point(100, 100), New Point(150, 150), _
    New Point(150, 200), New Point(100, 250))
```

![](img/d6f772854306e15fb6df39b861a7b541_166_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_166_1.png)

7 要绘制曲线，请声明一个曲线经过的 `Point` 对象数组。
8 输入 `e.Graphics.DrawCurve(myPen, pts)`，将 `DrawCurve` 替换为 `DrawCurve` 或 `DrawClosedCurve`，将 `myPen` 替换为 `Pen` 对象的名称，将 `pts` 替换为 `Point` 数组的名称。
9 按 `F5` 运行你的项目。

曲线绘制到图形容器上。

# DRAW TEXT

大多数应用程序使用文本来为窗体上的标题、标签和解释功能。在某些情况下，`Label` 控件可以提供必要的外观。对于高级文本渲染，你可以使用 VB .NET 在 `Graphics` 对象中包含的文本绘制例程。有关 `Label` 控件的更多信息，请参阅第 3 章。使用 `Graphics` 系统，你可以将 `Brush` 应用于文本，以创建填充有渐变、位图纹理或斜线图案的文本。

使用 `Graphics` 对象渲染文本的标准方法是 `DrawString` 方法。在每个可用的重载方法调用中，第一个参数包含要打印的 `String`。`DrawString` 期望第二个参数为 `Font` 对象，第三个参数为 `Brush` 对象。对于第四个参数，你传递一个 `Point` 对象，指定绘制文本的左上角点。最简单的构造函数需要这四个参数。可选地，对于第五个参数，你可以传递一个 `StringFormat` 对象来指定文本样式。

第 4 章包含有关 `String` 变量类型的更详细信息。

要提供要传递给 `DrawString` 的字体，请创建 `System.Drawing.Font` 类的新实例。根据要提供给 `Font` 构造函数的數據，你可以传递 `FontFamily` 对象，或一个 `String` 来选择字体系列，例如 Arial 或 Times New Roman。第二个参数是字体大小，以磅为单位。可选地，对于第三个参数，使用 `FontStyle` 枚举指定字体样式。

`Graphics` 对象公开了一个名为 `MeasureString` 的方法。使用此方法确定要绘制的字符串的宽度和高度。将 `String` 和 `Font` 作为两个参数传递给该方法。`MeasureString` 返回一个包含在 `System.Drawing` 命名空间中的 `SizeF` 结构。`SizeF` 的 `Width` 和 `Height` 属性包含适当的值。

# DRAW TEXT

![](img/d6f772854306e15fb6df39b861a7b541_167_0.png)
