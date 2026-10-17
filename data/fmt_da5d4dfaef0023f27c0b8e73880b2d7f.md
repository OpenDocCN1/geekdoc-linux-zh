
# 列表 9.3 延续

```
FLabel.Width := 50;

FLabel.Show;

FPanel := TPanel.Create(Self);

FPanel.Parent := Self;

FPanel.Top := ATop;

FPanel.BevelInner := bvRaised;

FPanel.BevelWidth := ABevelWidth div 2;

FPanel.Height := Height - (2 * ATop);

FPanel.Left := FLabel.Width + (FPanel.BevelWidth);

FPanel.Width := Width - FPanel.Left - (FPanel.BevelWidth * 4);

Caption := 'Panel';

FPanel.ParentFont := False;

FPanel.Show;
```

```pascal
procedure TElLabelPanel.TextChanged
begin
  inherited;
  FPanel.Caption := Caption;
end;
```

```pascal
function TElLabelPanel.GetLabelStr: string;
begin
  Result := FLabel.Caption;
end;
```

```pascal
procedure TElLabelPanel.SetLabelStr(S: string);
var
  Extent: TSize;
begin
  FLabel.Caption := S;
  Extent := Canvas.TextExtent(S);
  FPanel.Left := Extent.cx;
  FPanel.Width := Width - FPanel.Left - (BevelWidth * 2);
  FPanel.Color := Color;
end;
```

```pascal
{ --- TRadio2Panel -- }
```

```pascal
constructor TElRadio2Panel.Create(AOwner: TComponent)
begin
  inherited Create(AOwner);
  Width := 175;
  Height := 60;
  FRadio1 := TRadioButton.Create(Self);
  FRadio1.Parent := Self;
  FRadio1.Caption := 'Radio1';
  FRadio1.Left := 20;
  FRadio1.Top := 10;
  FRadio1.Show;
```

```pascal
FRadio2 := TRadioButton.Create(Self);
FRadio2.Parent := Self;
FRadio2.Caption := 'Radio2';
FRadio2.Left := 20;
FRadio2.Top := 32;
FRadio2.Show;
```

```pascal
function TelfRadio2Panel.GetRadio1Caption: string;
begin
  Result := Radio1.Caption;
end;
```

```pascal
function TelfRadio2Panel.GetRadio2Caption: string;
begin
  Result := Radio2.Caption;
end;
```

```pascal
procedure TelfRadio2Panel.SetRadio1Caption(const Value: string);
begin
  Radio1.Caption := Value;
end;
```

```pascal
procedure TelfRadio2Panel.SetRadio2Caption(const Value: string);
begin
  Radio2.Caption := Value;
end;
```

```pascal
// In Windows, this was caused by wms
procedure TelfRadio2Panel.Resize;
begin
  inherited;
  if FRadio1 <> nil then
    FRadio1.Width := Width - (FRadio1.Left + 15);
  if FRadio2 <> nil then
    FRadio2.Width := Width - (FRadio2.Left + 15);
end;
```

```pascal
procedure Register;
begin
    RegisterComponents('Elves', [TelfSmallEdit, TelfBigEdit, TelfMousePanel,
TelfSmallLabel, TelfBigLabel, TelfKeyCheckbox, TelfEmptyPanel,
TelfRadio2Panel, TelfLabelPanel, TCheckPanel]);
end;
```

```pascal
{ TelfCheckPanel }
constructor TCheckPanel.Create(AOwner: TComponent)
begin
    inherited
  FCaptions := TStringList.Create;
  TStringList(FCaptions).OnChange := Captions;
  Width := 175;
  Height := 50;
end;
```

```pascal
procedure TCheckPanel.ClearButtons;
var
    i: Integer;
begin
    for i := 0 to High(FCheckArray)
        if FCheckArray[i] <> nil then
            Free(FCheckArray[i]);
end;
```

```pascal
procedure TCheckPanel.MakeButtons(NumButtons: Integer);
var
    i: Integer;
begin
    ClearButtons;
    Height := (5 + (20 * NumButtons)) + 15;
    if High(FCheckArray) <> NumButtons then
        SetLength(FCheckArray, NumButtons);
    for i := 0 to NumButtons do
        FCheckArray[i] := CreateCheck(i);
end;
```

```pascal
function TCheckPanel.CreateCheck(Index: Integer): TCheckBox;
var
    C: TCheckBox;
begin
    C := TCheckBox.Create(Self);
    Font.Size := 12;
    Font.Color := ClBlack;
    C.Parent := Self;
    C.Caption := FCaptions[Index];
    C.Name := 'Check' + IntToStr(Index);
    C.Left := 20;
    C.Top := 5 + (20 * Index);
    C.Show;
    Result := C;
end;
```

```pascal
destructor TCheckPanel.Destroy;
begin
  FCaptions.Free;
  inherited;
end;
```

```pascal
procedure TCheckPanel.CaptionsChange(Sender: TObject);
begin
  MakeButtons(FCaptions.Count);
end;
```

```pascal
procedure TCheckPanel.Resize;
begin
  inherited;
end;
```

```pascal
procedure TCheckPanel.SetCaptions(const Value: TStrings)
begin
  FCaptions.Assign(Value);
end;
```

```pascal
function TCheckPanel.GetCheckBoxes: TCheckArray;
begin
  Result := FCheckArray;
end;
```

```pascal
initialization
  RegisterClasses([TRadioButton, TCheckBox]);
```
