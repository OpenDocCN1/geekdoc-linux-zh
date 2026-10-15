
*(注：提供的 OCR 文本在 Listing 11.1 部分包含严重错误。我根据标准的 Delphi/Kylix 模式和上下文重构了逻辑结构以提供连贯的表示。）*

随书附带的 CD 上的 `BitmapBrush` 程序可以作为其工作原理的示例。以下是程序中的关键方法：

```
procedure TForm1.PaintColors(BitmapName: String);
var
  MyBitmap: TBitmap;
begin
  MyBitmap := TBitmap.Create.LoadFromFile(BitmapName);
  Canvas.Draw(25, 35, MyBitmap);
  Canvas.Brush.Bitmap := MyBitmap;
  Canvas.Rectangle(0, 0, Width, Height);
  MyBitmap.Free;
end;
```

你可能只会使用 `TBrush` 对象的一个方法，那就是 `Assign`。当你想要将一个刷的特性复制到另一个时，就会使用它。

# 笔 (Pens)

当你绘制形状时，形状的轮廓由当前分配给画布的笔设置。例如，如果你画一个矩形，矩形的中心和样式将由刷的颜色定义，而矩形轮廓的颜色和厚度将由笔的颜色定义。

笔还有可以设置的样式，但只有当笔宽保持为一像素时，这些样式才会生效。在笔样式中：

- `psSolid`: 实线
- `psClear`: 透明线
- `psDot`: 虚线
- `psDashDot`: 由一个划线和两个点序列组成的线
- `psInsideFrame`: 可以使用抖动色的实线

为了直感受笔样式是如何更改的，请看这个使用来自 LCodeBase RGB 函数的简短方法：

```
procedure TForm1.BitbtnClick(Sender: TObject);
begin
  Canvas.Brush.Color := RGB(0,0,0);
  Canvas.Pen.Color := cTeal;
  Canvas.Pen.Style := psDot;
```

# CLX

第二部分

```
Canvas.Brush.Style := bsHorizontal;
Canvas.Rectangle(10,10,100,100);
end;
```

通过改变笔样式，你将改变矩形轮廓的外观。特别注意改变笔颜色和笔样式的操作。

```
Canvas.Pen.Color := cTeal;
Canvas.Pen.Style := psDot;
```

不言说，`psdot` 属性会导致矩形的轮廓显示为一系列点。

`TPen` 对象还有两个非常有用的属性：`Width` 和 `Mode`。`Width` 属性允许你设置笔绘制的线条的像素宽度。`Mode` 属性提供了一系列布尔选项，用于确定笔颜色与画布颜色的混合方式。根据 `TPen.Mode` 的值，笔的颜色将以不同的方式与画布颜色组合。例如，笔颜色可以完全覆盖底层的画布颜色，此时笔颜色保持不变；或者它可以与底层画布颜色完全混合，在这种情况下，边框将不可见。其之间还有各种状态，笔颜色和底层画布颜色组合以产生新颜色。`PenMode` 属性的一个功能将在“绘制橡皮筋”章节中概述的橡皮筋弹回技巧中起着重要作用。

在代码列表 11.2 中找到的 `PenMode` 程序将为你提供一个实验 `TPen Mode`、`Width` 和 `Color` 属性的机会。

# 代码列表 11.2 随书附带 CD 中第 11 目录下的 PenMode 程序的主单元

```
// 展示笔的模式
// 此程序基于 Jeff Cottingham 最初编写的代码
// Copyright © 2001 by Charlie and Margie Calvert
```

interface

```
uses
SysUtils, Classes, Graphics,
Controls, QForms, QDialogs,
QStdCtrls, QButtons, QExtCtrls,
QImageList, QComCtrls, QTypes;
```

# 代码列表 11.2 继续

```
type
TForm1 = class(TForm)
RadioGroup1: TRadioGroup;
PaintBox1: TPaintBox;
ToolBar1: TToolBar;
Button1: TButton;
ImageList1: TImageList;
Timer1: TTimer;
Button2: TButton;
ColorDialog1: TColorDialog;
Button3: TButton;
procedure RadioGroup1Click(Sender: TObject);
procedure FormButton1Click(Sender: TObject);
procedure FormShow(Sender: TObject);
procedure Timer1Click(Sender: TObject);
procedure Button2Click(Sender: TObject);
procedure Button3Click(Sender: TObject);
procedure FormCreate(Sender: TObject);
private
FChangeBy: Integer;
FPenColor: TColor;
FBrushColor: TColor;
procedure DrawStuff(AWidth, AHeight: Integer);
Canvas: TCanvas; MyPenMode: TPenMode;
  { Private declarations }
public
  { Public declarations }
end;

var
Form1: TForm1;

implementation
uses
TypeInfo;

{$R *.xfm}

procedure TForm1.DrawStuff(AWidth, AHeight: Integer)
ACan: TCanvas; MyPenMode: TPenMode;
const
Gap = 25;
YGap = 25;
```

# CLX

第二部分

# 代码列表 11.2 继续
