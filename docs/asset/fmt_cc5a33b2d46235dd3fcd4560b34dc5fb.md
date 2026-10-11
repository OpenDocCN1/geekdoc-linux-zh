
整个程序中唯一需要从一个后端切换到另一个后端的行是包含 `GetTools` 用的一行。具体来说，它可以更改为读取 `DirectXTools`。我在这里实现的模式是一种交换后端的非常干净的方法。

# 图形

## 第 11 章

## 注意

如果你没有使用模式的经验，可能想读读 Erich Gamma 等人写的《设计模式》（Design Patterns）这本书。该模式是书中讨论的“抽象工厂模式”的派生。Delphi 奇才 Xavier Pacheco 预计将出一本关于用 Object Pascal 实现模式的书。来自 Eagle Software 著名的 Mark Miller 是另一位 Delphi 程序员，他就模式写过一些非常有趣的文章。

## 11 图形

### 在正确的位置绘制墙段

在此阶段，你已经拥有了创建游戏引擎所需工具。唯一缺失的是关于何时以及何位扫（blit）位图的解释。

`MTown.pas` 定义了用户走的迷宫。假设用户位于迷宫中特定的 X 和 Y 位置。程序员需要知道在片段之前的 15 块墙中哪些应该被绘制，哪些应该留空。例如，如果用户面向北方，场景在概念上看起来像：

```
+   12 13 14 15 16

7 8 9 10 11

4 5 6

1 2 3
```

问题的在于位置 4、5、6 等包含的是 1 还是 0。每个位置是否有墙段，还是空白？以下是来自 `MTown.pas` 的代码，回答了用户面向由 `FXSpot` 和 `FYSpot` 定义的 x, y 位置北方的问题：

```pascal
procedure TMaze.FillCurrentView;
begin
  North: begin
    FCView[1] := GetCityPlace(FXSpot - 1, FYSpot);
    FCView[2] := GetCityPlace(FXSpot, FYSpot);
    FCView[3] := GetCityPlace(FXSpot + 1, FYSpot);
    FCView[4] := GetCityPlace(FXSpot - 1, FYSpot);
    FCView[5] := GetCityPlace(FXSpot, FYSpot - 1);
    FCView[6] := GetCityPlace(FXSpot + 1, FYSpot - 1);
    FCView[7] := GetCityPlace(FXSpot - 2, FYSpot);
    FCView[8] := GetCityPlace(FXSpot - 1, FYSpot - 2);
    FCView[9] := GetCityPlace(FXSpot, FYSpot - 2);
    FCView[10] := GetCityPlace(FXSpot + 1, FYSpot - 2);
    FCurView[11] := GetCityPlace(FXSpot + 2, FYSpot - 2);
    FCurView[12] := GetCityPlace(FXSpot - 2, FYSpot - 3);
    FCurView[13] := GetCityPlace(FXSpot - 1, FYSpot - 3);
    FCurView[14] := GetCityPlace(FXSpot, FYSpot - 3);
    FCurView[15] := GetCityPlace(FXSpot + 1, FYSpot - 3);
    FCurView[16] := GetCityPlace(FXSpot + 2, FYSpot - 3);
  end;
```

如果你仔细观察这段代码，你会发现它通过在当前 x, y 位置上加减 3 到 -3 之间的数字，触了 16 个可能的墙位置。`GetCityPlace` 确保特定位置在范围内，然后从数组中返回值：

```pascal
function TMaze.GetCityPlace(X, Y: Integer): TSegment;
var
  C: TSegment;
begin
  if (X <= 0) or (X > FMapList.MaxCols) or (Y <= 0) or (Y > FMapList.MaxRows) then
    C.Value := -1
  else
    C.Value := FMapList[X, Y];
  Result := C;
end;
```
