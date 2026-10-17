
```pascal
implementation
uses
CodeBox;

const
TownArray: TTownArray =
  ((1,1,1,1,1,1,1,1),
  (1,0,0,0,0,0,0,1),
  (1,0,0,0,1,1,0,1),
  (1,0,0,0,1,1,0,1),
  (1,0,0,0,0,0,0,1),
  (1,1,1,1,0,1,0,1),
  (1,0,0,0,0,1,0,1),
  (1,1,1,0,0,0,0,1),
  (1,1,1,1,1,1,1,1));

constructor TMazeTown.Create(Dir: TDirection)
begin
  Inherited Create;
  FDirection := Dir;
  FMapList := TMapPointList.Create;
  FileName := GetDir + 'maze1.txt';
  FMapList.ReadText(FileName);
  FXSpot := FMapList.StartX;
  FYSpot := FMapList.StartY;
  FillOutCurrentView;
end;

destructor TMazeTown.Destroy;
begin
  FMapList.WriteText(MazeFile, FXSpot, FYSpot);
  FMapList.Free;
  inherited Destroy;
end;

procedure TMazeTown.CurrentView(Offset: Integer; Value: Integer);
var
begin
  View: TWallSegment;
  View := FCurrentView[Offset];
  FMapList.Tiles[View.X, View.Y] := Value;
end;

function TMazeTown.GetWallSegment(X, Y: Integer):
begin
  Result := FMapList.Tiles[X, Y];
end;

{ 填充描述城市位置的记录 }
function TMazeTown.GetPlace(X, Y: Integer): TWallSegment
var
  C: TWallSegment;
begin
  C.X := X;
  C.Y := Y;
  if (X < 0) or (X > FMapList.MaxCols) or
    (Y < 0) or (Y > FMapList.MaxRows) then
    C.Value := -1
  else
    C.Value := FMapList.Tiles[X, Y];
  Result := C;
end;

procedure TMazeTown.FillOutCurrentView;
begin
  case FDirection of
    North: begin
      CurrentView[1] := GetPlace(FXSpot - 1, FYSpot);
      CurrentView[2] := GetPlace(FXSpot, FYSpot);
      CurrentView[3] := GetPlace(FXSpot + 1, FYSpot);
      CurrentView[4] := GetPlace(FXSpot - 1, FYSpot + 1);
      CurrentView[5] := GetPlace(FXSpot, FYSpot + 1);
      CurrentView[6] := GetPlace(FXSpot + 1, FYSpot + 1);
      CurrentView[7] := GetPlace(FXSpot + 2, FYSpot - 2);
      CurrentView[8] := GetPlace(FXSpot - 1, FYSpot + 2);
      CurrentView[9] := GetPlace(FXSpot, FYSpot + 2);
      CurrentView[10] := GetPlace(FXSpot + 1, FYSpot + 2);
      CurrentView[11] := GetPlace(FXSpot + 2, FYSpot + 2);
      CurrentView[12] := GetPlace(FXSpot + 3, FYSpot - 2);
      CurrentView[13] := GetPlace(FXSpot - 1, FYSpot + 3);
      CurrentView[14] := GetPlace(FXSpot, FYSpot + 3);
      CurrentView[15] := GetPlace(FXSpot + 1, FYSpot + 3);
      CurrentView[16] := GetPlace(FXSpot + 2, FYSpot + 3);
    end;
    East: begin
      CurrentView[1] := GetPlace(FXSpot, FYSpot - 1);
      CurrentView[2] := GetPlace(FXSpot, FYSpot);
      CurrentView[3] := GetPlace(FXSpot + 1, FYSpot);
      CurrentView[4] := GetPlace(FXSpot - 1, FYSpot);
      CurrentView[5] := GetPlace(FXSpot + 1, FYSpot);
      CurrentView[6] := GetPlace(FXSpot + 1, FYSpot + 1);
      CurrentView[7] := GetPlace(FXSpot + 2, FYSpot - 2);
      CurrentView[8] := GetPlace(FXSpot + 2, FYSpot - 1);
      CurrentView[9] := GetPlace(FXSpot + 2, FYSpot);
      CurrentView[10] := GetPlace(FXSpot + 2, FYSpot + 1);
      CurrentView[11] := GetPlace(FXSpot + 2, FYSpot + 2);
      CurrentView[12] := GetPlace(FXSpot + 3, FYSpot - 2);
      CurrentView[13] := GetPlace(FXSpot + 3, FYSpot - 1);
      CurrentView[14] := GetPlace(FXSpot + 3, FYSpot + 3);
      CurrentView[15] := GetPlace(FXSpot + 3, FYSpot + 1);
      CurrentView[16] := GetPlace(FXSpot + 3, FYSpot + 2);
    end;
    {$if LookingFromAbove} begin
    South: begin
      CurrentView[1] := GetPlace(FXSpot, FYSpot - 1);
      CurrentView[2] := GetPlace(FXSpot, FYSpot);
      CurrentView[3] := GetPlace(FXSpot + 1, FYSpot);
      CurrentView[4] := GetPlace(FXSpot - 1, FYSpot + 1);
      CurrentView[5] := GetPlace(FXSpot, FYSpot + 1);
      CurrentView[7] := GetPlace(FXSpot + 1, FYSpot + 1);
      CurrentView[8] := GetPlace(FXSpot - 1, FYSpot + 2);
      CurrentView[9] := GetPlace(FXSpot, FYSpot + 2);
      CurrentView[10] := GetPlace(FXSpot + 1, FYSpot + 2);
      CurrentView[11] := GetPlace(FXSpot + 2, FYSpot + 2);
    end;
    {$endif}
  end;
end;

# 列表 11.9 续

```pascal
FCurrentView[12] := GetCurrentPlace(FXSpot - 2, FYSpot + 3);

CurrentCurrentView[13] := GetCurrentPlace(FXSpot - 1, FYSpot + 3);
```
