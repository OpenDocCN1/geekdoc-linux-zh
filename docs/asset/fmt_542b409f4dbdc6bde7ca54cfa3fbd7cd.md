
```pas
enum Type (
  None = 0,
  Timer = 1,
  MousePress = 2,
  MouseRelease = 3,
  DoubleClick = 4,
  MouseMove = 5,
  KeyPress = 6,
  KeyRelease = 7,
  FocusIn = 8,
  FocusOut = 9,
  Enter = 10,
  Leave = 11,
  Paint = 12,
  Move = 13,
  Resize = 14,
  Create = 15,
  Destroy = 16,
  Show = 17,
  Hide = 18,
  Quit = 19,
  Repaint = 20,
  ShowMinimized = 21,
  ShowNormal = 22,
  WindowActivate = 23,
  WindowDeactivate = 24,
  ShowToParent = 25,
  ShowMaxized = 26,
  Wheel = 28,
  Wheel = 30,
  Activate = 31,
  Change = 32,
  Change = 33,
  ParentFont = 34,
  ApplicationFont = 35,
  ParentPalette = 36,
  ApplicationPalette = 37,
  Clipboard = 38,
  Speed = 39,
  SockAct = 40,
  AccelOverride = 41,
  DragEnter = 42,
  DragMove = 43,
  DragLeave = 44,
  Drop = 45,
  DragResponse = 46,
  ChildInserted = 47,
  ChildRemoved = 48,
  LayoutHint = 49,
  ShowWindowRequest = 50,
  ActivateControl = 51,
  DeactivateControl = 52,
  User = 53
)
```

显然，这种枚举类型与 Pascal 的 `QEventType` 之间存在联系。进一步查阅 TrollTech 页面显示了 `QEvent_type` 函数访问的方法：

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_380_0.png)

# CLX

## 第二部分

```cpp
QEvent::QEvent ( Type type )
创建一个带有指定类型的事件对象。
QEvent::~QEvent () [virtual]
析构事件。如果事件已发布（posted），它将从事件列表中移除。
QEvent::Type QEvent::type() const
返回事件类型。
```

此对象包含一个构造函数、一个析构函数和一个返回事件类型的方法。这些类型实际上是枚举类型，而之前讨论的那个神秘的 `case` 语句就是围绕这个枚举类型构建的。

如果你进一步深入研究 Qt 文档，你会发现大多数事件都有相关文档：

- `MouseMove`: 鼠标移动，`QMouseEvent`

- `KeyPress`: 按键按下（包括例如 shift 键），`QKeyEvent`

- `KeyRelease`: 按键释放（此处应为Release），`QKeyEvent`

- `FocusIn` - 控件获得键盘焦点，`QFocusEvent`

- `FocusOut` - 控件失去键盘焦点，`QFocusEvent`

- `Enter` - 鼠标进入控件区域

- `Leave` - 鼠标离开控件区域

在这里你可以获得一些很有启发性的信息，例如 `MouseMove` 事件在鼠标移动时发生，而 `KeyPress` 事件在按下按键时发生。好吧，也许这些信息并不十分具有启示性。但不要急于评价 TrollTech 的文档；某些信息其实更有用。特别是，你可以看到 `Enter` 和 `Leave` 事件记录了鼠标进入或离开控件时发生的情况。

这一切又回到了我们开始这个事件章节的起点。正如你记得的，你看到了两个 CLX 事件：

```pascal
procedure MouseEnter(AControl: TControl); override;
procedure MouseLeave(AControl: TControl); override;
```

当我引入这些方法时，我说它们回到了鼠标进入和离开控件“空间”的时刻。

到目前为止，这些令人叹叹的方法神秘感应该已经消失了。你已经了解了 CLX 是如何获取这些事件的以及 Qt 本身是如何处理它们的。此外，如果你想深入研究 Qt 源码并查看 Kylix 程序中发生了什么，你已经很清楚该从哪里开始查找了。

毋得说，编写 Kylix 程序可能并不需要深挖 Qt 源码。事实上，你通常甚至不应该查看 `FilterEvents` 方法。相反，你只需要找到标准的 CLX 方法（如 `MouseEnter` 和 `MouseLeave`），重写它们，并利用它们的力量。

# CLX 架构与视觉开发

## 第七章

然而，理解你所使用的工具是非常有意义的。事实上，作为一个对知识有着无限渴求的程序员，你的工作就是理解你的工具是如何组合的。利用这些知识，你可以发现程序的各种和局限性。所以，如果你有此意，请深入研究 CLX——甚至可能破解 Qt 的代码。如果你有探索的欲望，那么愿源码与你同在！

## 注意

关于事件还有更多可以说的。请参第 9 章，并特别关注“在组件中使用 `FilterEvents`”部分。

# 7

## 架构

### CLX

#### 使用样式

在第 4 章中，你在“所有者绘制列表框”部分遇到了所有者绘制列表框。事实证明还有另一种改变表单项外观的方法。第二种技术涉及更改你所用组件的样式。

你可以通过一行代码更改应用程序的样式。以下是该代码的两种示例：

```pascal
Application.Style.DefaultStyle := dsWindows;
```

```pascal
Application.Style.DefaultStyle := dsMotif;
```

第一个示例使你的应用程序样式类似于 Windows 程序，如图 7.3 所示。第二个示例使你的代码呈现 motif 风格，如图 7.4 所示。

以下常量可以以与 CLX 文件 `Styles.pas` 中声明的 `dsWindows` 和 `dsMotif` 相同的方式更改代码：

```pascal
TDefaultStyle = (dsWindows,
dsMotif,
dsMotifPlus,
dsCOE,
dsQtSI,
dsPlatinum,
dsSystemDefault);
```

# CLX

## 第二部分

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_385_0.png)

### 图 7.3

按钮边缘可以看到 Windows 风格。

### 图 7.4

按钮边缘可以 motif motif 风格。

你可以通过一行代码让程序呈现 motif 风格：

```pascal
Application.Style.DefaultStyle := dsMotif;
```

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_385_1.png)

# CLX 架构与视觉开发

## 第七章

### 使用样式

```pascal
procedure TForm.DrawRadio(Sender: T; Canvas: TCanvas);
var
  Rect: TRect;
begin
  Rect := Rect(10, 10, 50, 50);
  if Checked then
    Canvas.FillRect(Rect, clBlue)
  else
    Canvas.FillRect(Rect, clWhite);
end;
```

按钮边缘可以看到 Windows 风格。

按钮边缘可以看到 motif 风格。

# CLX 架构与视觉开发

## 第7 章

你可以从 Wine 项目获取 `wrc`，这是一个可以从网上免费提供的开源 Windows 仿真项目。安装 Wine 后，默认情况下，`wrc` 将放置在 `/usr/bin` 目录。

要运行 `wrc`，输入以下命令：

```
wrc -r MyResource.rc
```

`MyResource.rc` 可能看起来如下所示：

```
Sammy BITMAP "Background.bmp",
```

在运行时加载文件，请编写如下代码：

```
Bitmap := TBitmap.Create;
Bitmap.LoadFromResourceName(HInstance, 'Sammy');
```

在这个示例中，名称是你在 res 文件中为资源指定的名称。例如，标识符 `Monk2`、`TileMap` 和 `MessageD1g` 是本节开头所示 rc 文件中的类似字符串。

这种类型的示例程序名为 `LoadBitmapFromRes`，可以在随书附带的光 CD 中的 `Chapter07` 目录中找到。该程序的源代码见代码列表 7.4。
