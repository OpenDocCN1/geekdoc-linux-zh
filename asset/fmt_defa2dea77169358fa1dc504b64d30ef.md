
```pascal
///////////////////////////////////////////////////////
// Purpose: Draw the Mandelbrot set
// Component: TElfMandy
// Copyright © 2001 by Charlie Calvert
//
unit ElfMandy;

interface

uses
    QForms, QControls, Types,
    Classes;

type
TElfMandy = class(TCustomControl)
private
    FDragging: Boolean;
    FDrawnOnce: Boolean;
    FDepth: Integer;
    FXRange: Double;      // The width and height of the
    FYRange: Double;      // Mandelbrot plane. Starts at 3.
    FScOrgX: Integer;
    FScOrgY: Integer;
    FScMaxX: Integer;
    FBaseOrgX: Double;
    FBaseOrgY: Double;
    FRect: TRect;
    FQuitDrawing: Boolean;
    FPaint: TNotifyEvent;
    FBeginDraw: TNotifyEvent;
    FEndDraw: TNotifyEvent;
  function Distance(X, Y: Double): Double;
  procedure Calculate(X, Y: Double);
  var Xiter, Yiter: Double;
  function GetColor(Steps: Integer): Integer;
  procedure GetOriginsWidths(var XOrg, YOrg, XMax, YMax: Double);
  constructor Create(Owner: TComponent); override;
  procedure Boundary(ScX, ScY, ScX1, ScY1: Integer);
  procedure SetMousePos(ScX, ScY: Integer);
  procedure SetMouseUp(ScX1, ScY1: Integer);
  function Run: Boolean;
  property Drawing: Boolean read FDrawing write;
  procedure Paint;
  procedure MouseDown(Button: TMouseButton; Shift: TShiftState; X, Y: Integer) override;
  procedure MouseMove(Shift: TShiftState; X, Y: Integer) override;
  procedure MouseUp(Button: TMouseButton; Shift: TShiftState; X, Y: Integer) override;
  procedure Resize; override;
  property Align;
  property Depth: Integer read FDepth write;
  property Canvas;
  property OnPaint: TNotifyEvent = FPaint;
  property OnEndDraw: TNotifyEvent = FEndDraw;
  property OnBeginDraw: TNotifyEvent = FBeginDraw;
end;
procedure Register;

implementation

uses QGraphics;

procedure Register;
begin
  RegisterComponents('Mandy');
end;

constructor TMMandy.Create(Owner: TComponent)
begin
  inherited Create(Owner);
  FXRange := 3;
  FYRange := 3;
  FBaseOrgX := -2.5;
  FBaseOrgY := -1.5;
  Width := 25;
  Height := 25;
end;

procedure TMMandy.GetOriginsWidths(var XOrg, YOrg, XMax, YMax: Double)
var
  VXOrg,
  VYOrg,
  VMax,
  VYMax: Double;
  XPercent, YPercent,
  MaxPercent, MaxPercent: Double;
begin
  VXOrg = FScOrgX;
  VYOrg = FScOrgY;
  VMax = FScMaxX;
  VYMax = FScMaxY;
  XPercent = VXOrg / Width;
  YPercent = VYOrg / Height;
  MaxPercent = VMax / Width;
  MaxPercent = VYMax / Height;
  XOrg = XPercent * FXRange + FBaseOrgX;
  YOrg = YPercent * FYRange + FBaseOrgY;
// ... (rest of the code remains as provided)
```
# 图形

第 11 章

## 11

第五个编辑控件允许你设置笔画宽度。此程序使用了两个颜色对话框，允许你设置形状的颜色以及其周围线条的颜色。

单选组是此程序的核心。要设置单选组，你需要在对象检查器（Object Inspector）中设置 `RadioGroup1` 的 `items` 属性。如果你点击对象检查器中 `Items` 属性旁边的省略号按钮，然后在每行分别输入每个形状的名称，Kylix 将自动为你设置单选按钮。每个单选按钮的 `ItemIndex` 将自动为你设置，从第一个按钮开始为零。

由单选按钮触发的 `case` 语句包含了实际绘制形状的代码。如果单选组的 `ItemIndex` 为 0，则绘制一个矩形；如果为 1，则绘制一个椭圆……

要创建 `Form1.RadioGroup1Click` 过程，你首先需要在设计视图中双击 `RadioGroup1`。Kylix 将创建一个代码桩，你可以在其中调用 `DrawShape` 过程。

如果你愿意，可以添加更多的编辑控件和形状，以便你可以使用此程序尝试需要更多参数的形状。

> 最经常引起人们困惑的形状绘制方法是 `TCanvas` 对象的 `Polygon` 和 `Polyline` 方法。使用这些方法的技术在第 7 章“CLX 架构与视觉开发”末尾的名为“绘制表单形状”的部分进行了演示。

这是描述 CLX 图形单元核心功能的章节的结束。本章的其余部分展示了如何在复杂程序中使用这些强大工具的高级示例。这些章节中探索了一些新对象。例如，`TBitmap` 对象将在文本的几个章节中被详细研究。

# 曼德博集合（Mandelbrot）示例

随书光盘提供的 `TestMandel` 程序为你提供了一个观察 Kylix 图形系统运行的机会。该程序包含一个绘制经典曼德博集合的组件。使用鼠标，你可以反复放大感兴趣的集合部分。程序使用了橡皮带技术来帮助你在想要调查的区域周围画一个矩形。程序有一个内置功能，允许你保存所创建图片的截图，并且当你切换离开主窗口时，它能够很好地重绘你创建的图片。

图 11.4 显示了程序的一个界面。列表 11.4 和 11.5 包含了程序的代码。第一个列表显示了绘制曼德博集合的组件代码。第二个列表显示了保存完成后的截图的程序，它还处理了重绘。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_585_0.png)

图 11.4 `TestMandel` 让你能够体验放大和对曼德博集合拍照的乐趣。
