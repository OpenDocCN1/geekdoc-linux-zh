
![](img/6e977c6eee8c1535039c864d41da5ccf_158_0.png)

![](img/6e977c6eee8c1535039c864d41da5ccf_158_1.png)

## 创建线性渐变 (CREATE A LINEAR GRADIENT)

- 7 声明一个矩形对象。
- 注意：参见“Graphics Object”部分以“创建 Rectangle”。
- 9 在参数中，矩形名称、起始颜色、结束颜色和旋转角度之间用逗号分隔。
- 11 按 `F5` 运行项目。
- 如果必要，画笔将绘制到填充区域内。
- 8 输入 `Dim gradient As Drawing2.LinearGradientBrush`，将 `LinearGradient` 替换为渐变名称。
- 10 输入使用画笔的代码。

## 创建画笔 (CREATE A PEN)

你使用画笔（Pen）来告诉 VB.NET 绘制各种基元图形的线条样式、颜色和粗细。例如，各种轮廓基元使用了 `Pen`、矩形、椭圆和曲线。`Pen` 指定了让 VB.NET 知道如何绘制这些内容的细节。使用画笔填充或勾勒 `Pen` 实例。关于 `Brush` 对象的更多信息，请参见“创建画笔”。

要根据画笔创建 `Pen` 对象，请创建 `Pen` 类的新实例并将画笔作为第一个参数。要指定画笔的宽度，请使用接受 `Brush` 和 `Single` 类型线宽的备构造函数。

创建 `Pen` 实例后，有许多属性允许编辑外观。`StartCap` 和 `EndCap` 属性接受来自 `LineCap` 枚举的常量。这些属性指定了画笔末端的类型，`LineJoin` 属性指定了线条如何连接。使用画笔填充或勾勒 `Pen` 实例。关于 `Brush` 对象的更多信息，请参见“创建画笔”。

### 创建画笔步骤

- 1 创建新画笔或打开一个现有画笔。
- 2 点击类列表并选择（基类）事件或要绘制的控件。
- 3 点击方法名称列表并选择 `Point` 事件。
- 4 输入 `Dim redPen As New Drawing.Pen(Color.Red)`，将 `redbrush` 替换为 `redPen`，将 `Red` 替换为颜色。
- 5 输入 `Dim myPen As New Drawing.Pen(myBrush)`，将 `myBrush` 替换为画笔名称。
- 6 在括号中，输入要遵循的阴影图案，后面跟着前景和背景颜色，用逗号分隔。
- 7 声明一个矩形对象。
- 注意：参见“Graphics Object”部分以“创建 Rectangle”。
- 8 在参数中，矩形名称、起始颜色、结束颜色和旋转角度之间用逗号分隔。
- 9 按 `F5` 运行项目。
- 如果必要，画笔将绘制到填充区域内。
- 10 输入 `Dim myPen As New Drawing.Pen(myBrush, 5)`，将 `myBrush` 替换为画笔名称。
- 11 输入使用画笔的代码。

## 额外 (Extra)

如果你需要简单的实色画笔，可能会发现不断创建自定义画笔非常耗时。但是，你可以使用一个预创建的画笔来避免创建 `SolidBrush` 类新实例的麻烦。`System.Drawing.Brushes` 类为颜色列表中的每种颜色提供了一组画笔。你可以通过“使用 Graphics 对象”查看许多颜色选择。

在 Windows 中，用户在桌面偏好设置各种颜色，所有 Windows 应用程序都会以这种方式做出响应。你可能想在表单上绘制，但你需要遵循其他人使用的 Windows 颜色。你可以使用 `SystemBrushes` 类填充特定系统的区域。`SystemBrushes` 类是 `System.Drawing` 命名空间的一部分。例如，`System.Desktop` 返回用户控件颜色的画笔，使用 `SystemClasses` 获取每个画笔依赖的单个颜色值。你可以在帮助中输入 `Systemmembers` 来搜索可用颜色的完整列表。

示例：

```
Dim myPlum As Drawing.SolidBrush =
Drawing.Brushes.Plum
```

示例：

```
Dim myControlColor As
Drawing.SolidBrush =
Drawing.SystemBrushes.Control
```
