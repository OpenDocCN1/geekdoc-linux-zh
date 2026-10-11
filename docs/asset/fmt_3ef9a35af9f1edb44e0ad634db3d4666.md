
# 列表 11.4 TElfMandy 组件在你点击并拖动其上或调用其 Run 方法时绘制曼德博集合

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

# CLX

第二部分

## 列表 11.4 续

```pascal
// SaveStyle: TPenMode;
begin
  if FDragging = True then begin
    // SaveStyle := Canvas.Pen.Mode;
    Canvas.Pen.Mode := pmNotXor;
    if FDownOnce = True then
      Canvas.Rectangle(Rect(FOoldRect));
    FOLDRect := Rect(FScOrgX, FScOrgY, X, Y);
    Canvas.Rectangle(FScOrgX, FScOrgY, X, Y);
  end;
  //  Canvas.Pen.Mode := SaveStyle;
  FDownOnce := True
end;
```

```pascal
procedure TElFMandy.Paint;
begin
  inherited;
  if Assigned(OnPaint) then
    OnPaint(self);
end;
```

## 列表 11.5 TestElMandel 程序展示了如何将屏幕区域保存为位位图

```pascal
unit Main;

interface

uses

  SysUtils, Types, Classes,

  Variants, QGraphics, QControls,

  QForms, QDialogs, ElfMandy,

  QStdCtrls, QComCtrls, QImgList;

type
```
