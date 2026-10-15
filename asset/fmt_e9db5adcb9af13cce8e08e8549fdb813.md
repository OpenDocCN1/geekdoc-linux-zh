
TTimer 组件随 Kylix 一起发布并出现在组件面板（Component Palette）上。然而，该组件是手动创建对象实例的：你完全不需要使用可视化工具。以下是使用 `TTimer` 组件需要了解的一些基本事实：

- 当你想启动计时器时，将 `TTimer.Enabled` 属性设置为 `True`。
- 要停止计时器，将 `Enabled` 设置为 `False`。
- `OnTimer` 事件会在指定的间隔内调用你程序中的方法。
- `TTimer.Interval` 属性定义了计时器调用之间的时间长度，单位为毫秒。

创建计时器的典型方式如下：

```pascal
FTimer := TTimer(Self); // 自动销毁
FTimer.OnTimer := OnTimer;
FTimer.Interval := 250;
FTimer.Enabled := True;
```

赋值给 `Interval` 属性的值 `250` 表示计时器每 250 毫秒被调用一次，或者每四分之一秒一次。

计时器事件通过 `OnTimer` 事件发送到你的窗口：

```pascal
procedure TfClock.OnTimer(Sender: TObject);
```

对此的响应是一个简单的过程，它调用 `TextOut` 并从 `LCode` 单元中名为 `GetTimeString` 的函数获取时间：

```pascal
procedure TfClock.OnTimer(Sender: TObject);
var
  S: string;
  X, y, TextWidth, TextHeight : Integer;
  SaveColor: TColor;
begin
  S := GetTimeString;
  TextWidth := Canvas.Width(S);
  TextHeight := Canvas.Height(S);
  x := (Canvas.Width / 2) - (TextWidth / 2);
  y := (Canvas.Height / 2) - (TextHeight / 2);
  SaveColor := Canvas.Pen.Color;
  Canvas.Pen.Color := Canvas.Brush.Color;
  Canvas.Rectangle(x, y, x + TextWidth, y + TextHeight);
```

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_526_0.png)

## CLX

# 第二部分

```pascal
Canvas.Pen.Color := SaveColor;
Canvas.TextOut(x, y, S);
end;
```

注意我使用了 `QGraphics` 单元中 `TCanvas` 对象的 `TextWidth` 和 `Height` 函数来计算文本在水平和垂直方向延伸的距离。我的目标是确保文本字符串的中心尽可能靠近控件的。

启用和禁用计时器的调用主要通过名为 `Running` 的属性管理：

```pascal
property Running: Boolean read FRunning SetRunning;
```

写入机制是一个名为 `SetRunning` 的过程，这是一个非常直接的过程：

```pascal
procedure TFClock.SetRunning(Run: Boolean);
begin
  if Run then begin
    FTimer.Enabled := True;
    FRunning := True;
  end else begin
    FRunning := False;
    FTimer.Enabled := False;
  end;
end;
```

如果用户将 `Running` 属性设置为 `True`，则执行此过程并将 `FTimer.Enabled` 设置为 `True`。如果用户将 `Running` 设置为 `False`，则 `FTimer.Enabled` 被设置为 `False`，时钟立即停止运行。

## 时钟 Paint 方法

在结束对 `TFClock` 对象的描述之前，我应该简要提到一下 `Paint` 方法：

```pascal
procedure TFClock.Paint;
begin
  Canvas.Ellipse(0, 0, Width, Height);
end;
```

每当定义时钟周边的圆需要重绘时，就会调用此过程。你永远不需要检查这种情况，也不需要直接调用 `Paint`。Kylix 依赖底层系统来监控 `TFClock` 窗口。如果它需要绘制，Kylix 会自动发送 `OnPaint` 事件，从而调用此处显示的 `Paint` 方法。

## 高级组件设计

## 第 10 章

### 注意

在编写组件时，有时直接进入底层 Qt 或 Xlib 层级，或者尽可能接近该层级，是最简单的。前两章展示的过滤器（Filter）技术可以帮助你实现这一点。

### 时钟 Paint 方法

在编写组件时，有时直接进入底层 Qt 或 Xlib 层级，或者尽可能接近该层级，是最简单的。前两章展示的过滤器技术可以帮助你实现这一点。

*(注：此处原文存在大量重复段落，已根据要求保留格式并完成翻译)*

### 时钟 Paint 方法

在结束对 `TFClock` 对象的描述之前，我应该简要提到一下 `Paint` 方法：

```pascal
procedure TFClock.Paint;
begin
  Canvas.Ellipse(0, 0, Width, Height);
end;
```

每当定义时钟周边的圆需要重绘时，就会调用此过程。你永远不需要检查这种情况，也不需要直接调用 `Paint`。Kylix 依赖底层系统来监控 `TFClock` 窗口。如果它需要绘制，Kylix 会自动发送 `OnPaint` 事件，从而调用此处显示的 `Paint` 方法。

# 高级组件设计

第 10 章

注意，我也暴露了 `TControl` 的 `Color` 属性：

```pascal
property Color;
```

回到 `TControl` 的源码（位于 `Controls.pas`）中，你可以在类声明的 `protected` 部分找到该属性的原始声明。我在这里所做的仅仅是将该属性暴露在 `Published` 部分，使其显示在对象检查器（Object Inspector）中。

`Color` 属性定义了表单的背景颜色，而 `FaceColor` 则定义了钟面的颜色。如果你想让钟面看起来是直接绘制在父控件的表面上，只需让 `Color` 保持默认值或设置为父控件的颜色即可。

# 创建华丽的时钟

华丽的时钟通过为用户提供字体选择使钟面更具吸引力。该对象还添加了边框和斜角，并允许用户将面绘制为矩形或圆形：

```pascal
TClockStyle = (csEllipse, csRectangle);
TelfFancyClock = class(TelfColorClock)
private
  FClockStyle: TClockStyle;
  FBevelWidth: Integer;
  FBorderWidth: Integer;
  // 此省略代码
published
  property BevelWidth: Integer read FBevelWidth write SetBevelWidth;
  property BorderWidth: Integer read FBorderWidth write SetBorderWidth;
  property ClockStyle: TClockStyle read FClockStyle write FClockStyle;
  property Font;
end;
```

这一切看起来似乎是一个复杂的过程，但如果你利用了 CLX 中的代码，实现起来其实相当简单。

例如，考虑到字体的种类众多，添加字体支持将是一项非常困难的操作。然而，CLX 允许你通过在程序中添加两个单词来让用户对字体拥有完全控制权：

```pascal
property Font;
```

将此内容添加到对象的 `published` 部分，会暴露在对象祖类中声明的 `Font` 属性。它还会自动引入字体编辑器。字体编辑器作为对象检查器的一部分出现，如图 10.2 所示。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_530_0.png)

# CLX

第二部分

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_531_0.png)

# 图 10.2

属性编辑器的字体默认用于所有声明为 `TFont` 类型的属性。

除了新的 `TFont` 属性外，`T1FancyClock` 组件为用户提供了两种不同的钟外观：一个是圆形，另一个矩形，如前面的图 10.1 所示。`TClockStyle` 枚举类型为用户提供了追踪选择的方法：
