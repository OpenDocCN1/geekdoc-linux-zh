
在这种特殊情况下，我调用了名为 `LoadLibrary` 和 `FreeLibrary` 的方法。许多读者可能知道，这些方法是 Microsoft Windows API 的一部分。然而，Kylix 在 `SysUtils.pas` 单元中实现了这些方法的封装。通过在这里使用它们，我能够编写跨平台代码。简而言，当在 Linux 中编译时，`LoadLibrary` 调用 `dlopen`。当在 Windows 中编译时，`LoadLibrary` 映射到名为 `LoadLibrary` 的 Windows API 函数。

> 注意

关于处理共享对象和调用 `dlopen` 的讨论位于第 8 章“代码打包与共享”的多个部分，包括“动态加载共享对象”节。

以下是创建 `PrimarySurface`、`BackSurface` 和 `WorkSurface` 的代码：

```delphi
function TDelphiDraw.InitObjects: Boolean;

function MakeSurface(x, y: Integer): TBitmap;

  var

    Surface: TBitmap;

  begin

    Surface := TBitmap.Create;

    Surface.Width := x;

    Surface.Height := y;

    Result := Surface;

  end;

begin

  FPrimarySurface := FForm.Canvas;

  FBackSurface := MakeSurface(FSizeX, FSizeY);

  FWorkSurface := MakeSurface(FSizeX, FSizeY);

  GetBitmapFromDLL(FWorkSurface, FBackgroundColor);

  FActive := True;

  Result := True;

end;
```

`PrimarySurface` 直接赋值给应用程序主表单的画布。`BackSurface` 和 `WorkSurface` 都不需要包含预定义的位图，因此它们分别由空的 `Bitmap` 对象组成，其画布的宽度和高度与应用程序的主表单相等。相比之下，那些包含墙面各个部分图像的表面，不同表面会将位图加载到内存中。`BackSurface` 和 `WorkSurface` 并不持有任何特定的位图；相反，它们成为了程序中使用的几乎所有位图的临时存放地。

## 图形 第 11 章

## 11

## 注意

注意，这里显示的 `MakeSurface` 过程与上一节末尾讨论的假设方法 `CreateBlankSurface` 相对应。你可能对 `MakeSurface` 是一个嵌套过程（它出现在 `InitObjects` 方法的声明内部）这一事实感兴趣。嵌套过程是 Object Pascal 有趣特性之一，我们将在书中很快回顾它们。坦率地说，我对嵌套过程持保留意见，因为如果使用得不当，它们可能会导致问题。然而，CLX 课程中充满了这种语法的实例。

如果你查看代码列表 11.8 中很长的 `DrawRoot2.pas` 单元，你会发现有一个方法用于创建每个包含（代表墙面段的）位图的表面：

```delphi
FDDSBackExtLeft := FTools.CreateSurface('BackExtLeft');
FDDSBackLeft := FTools.CreateSurface('BackLeft');
FDDSBackCenter := FTools.CreateSurface('BackCenter');
FDDSBackRight := FTools.CreateSurface('BackRight');
FDDSBackExtRight := FTools.CreateSurface('BackExtRight');
```

```delphi
FDDSMidExtLeft := FTools.CreateSurface('MidExtLeft');
FDDSMidLeft := FTools.CreateSurface('MidLeft');
FDDSMidCenter := FTools.CreateSurface('MidCenter');
FDDSMidRight := FTools.CreateSurface('MidRight');
FDDSMidExtRight := FTools.CreateSurface('MidExtRight');
```

```delphi
FDDSForeLeft := FTools.CreateSurface('ForeLeft');
FDDSForeCenter := FTools.CreateSurface('ForeCenter');
FDDSForeRight := FTools.CreateSurface('ForeRight');
```

```delphi
FDDSFrontLeft := FTools.CreateSurface('FrontLeft');
FDDSFrontRight := FTools.CreateSurface('FrontRight');
```

正如你所记得，传递给 `CreateSurface` 方法的名字代表包含描绘每个特定墙段位图的资源名称。以下是该资源 RC 文件的相关声明：

```rc
BackExtLeft BITMAP "BackExtLeft.bmp";
BackLeft BITMAP "BackLeft.bmp";
BackCenter BITMAP "BackCenter.bmp";
BackRight BITMAP "BackRight.bmp";
BackExtRight BITMAP "BackExtRight.bmp";
MidExtLeft BITMAP "MidExtLeft.bmp";
MidLeft BITMAP "MidLeft.bmp";
MidCenter BITMAP "MidCenter.bmp";
MidRight BITMAP "MidRight.bmp";
MidExtRight BITMAP "MidExtRight.bmp";
ForeLeft BITMAP "ForeLeft.bmp";
ForeCenter BITMAP "ForeCenter.bmp";
ForeRight BITMAP "ForeRight.bmp";
FrontLeft BITMAP "FrontLeft.bmp";
FrontRight BITMAP "FrontRight.bmp";
```

# CLX
第二部分

掌握的关键点在于，如果你想从 DirectX 切换到原生图形代码，整个程序只需要修改一行。具体来说，在一种情况下你可以调用 `GetDelphiTools`，另一种情况下你将调用 `GetDrawTools`。

以下是 `DrawTools.pas` 中 `TCityMap` 对象定义的开头：

```pascal
TCityBoard = class(TObject)
private
  FDrawTools: IDrawTools;
  FDDSBackExtLeft: ISimpleSurface;
  FDDSBackLeft: ISimpleSurface;
```

你可以看到，`DrawTools` 被声明为任何 `IDrawTools` 类型，而不是任何特定的对象类型。简而言之，它是一个接口，而不是类。然而，在整个程序中，你可以像使用对象一样使用它：

```pascal
FDrawTools.BackgroundBlits;
if FMazeTown.CurrentViewID(ptBackExtLeft).Value = 1 then begin
  R := GetBackPos(ExtLeft)
  FDrawTools.BltIntoBackSurface(0, 174, FDDSBackExtLeft, R);
end;
```

如果 `DrawTools` 指向 DirectX 实现，`BltIntoBackSurface` 将调用 DirectX 代码。如果它指向本章中的实现，它则会调用原生 X 代码或 GDI 代码。

以下是为 `DrawTools` 赋值的方法：

```pascal
constructor TCityBoard.Create;
begin
  inherited Create;
  FDrawTools := GetDelphiTools;
  FDrawTools.SizeX := PageWidth;
  FDrawTools.SizeY := PageHeight;
  FDrawTools.UsePalette := False;
  FMazeTown := TMazeTown.Create(East);
end;
```
