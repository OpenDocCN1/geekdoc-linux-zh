
```pascal
function TelfLabel.GetLabelText: WideString;
begin
  //为了兼容性。Qt Label 不使用它。
  Result := Caption;
end;
```

```pascal
procedure TelfLabel.DoDrawText(var Rect: TRect; Flags: Integer);
var
  Text: string;
  HighColor: TColor;
  LowColor: TColor;
  SaveColor: TColor;
  ThreeRect: TRect;
begin
  Text := GetLabelText;
  if Enabled then
    Canvas.Font.Color := cBtnHigh;
    Canvas.TextOut(0, 0);
    Canvas.Font.Color := cBtnShadow;
    Canvas.TextOut(1, 1);
  end;
  case FTextType of
    ttInset:
      HighColor := cBtnHigh;
      LowColor := cBtnShadow;
    ttEmbossed:
      HighColor := cBtnShadow;
      LowColor := cBtnHigh;
    else
      HighColor := cBtnShadow;
      LowColor := cBtnHigh;
  end;
  if TextType in [ttInset, ttEmbossed] then
    SaveColor := Canvas.Font.Color;
    // 绘制一种
    Canvas.Font.Color := HighColor;
    Canvas.TextOut(0, 0);
    // 绘制另一种
    ThreeRect := Rect;
    Canvas.Font.Color := LowColor;
    Canvas.TextOut(2, 2);
    Canvas.Font.Color := SaveColor;
  end;
  // 绘制常规
  TextRect(Rect, 1, 1);
end;

procedure TfLabel.SetTypeText(const Value: TTypeText)
begin
  FTypeText := Value;
  Invalidate;
end;

function TfLabel.TextWidth(S: string): Integer
begin
  Result := Canvas.TextWidth(S);
end;

procedure TfLabel.Paint;
var
  R: TRect;
begin
  inherited;
  R := BoundsRect;
  DoDrawText(R, 0);
end;

function TLabelEdit.GetEditColor: TColor
begin
  Result := Edit.Color;
end;

procedure TLabelEdit.SetEditColor(const Value: TColor)
begin
  Edit.Color := Value;
end;
```

# 创建组件

## 第九章

这个对象类似于 `RadioPanel` 控件，但有用得多。考虑以下声明：

```pascal
TElLabelEdit = class(TCustomControl)
private
  FEdit: TEdit;
  FGap: Integer;
  FLabel: TLabel;
  FLabelType: TLabelType;
  function GetEditTextText: string;
  procedure SetLabelText(const Value: string);
  procedure SetEditText(const Value: string);
  function GetEditReadOnly: Boolean;
  function GetEditVisible: Boolean;
  function GetLabelVisible: Boolean;
  function GetTextType: TTypeText;
  procedure SetReadOnly(const Value: Boolean);
  procedure SetPositionBottom;
  procedure SetPositionLeft;
  procedure SetPositionRight;
  procedure SetPositionTop;
  procedure SetEditVisible(Value: Boolean);
  procedure SetGap(Value: Integer);
  procedure SetLabelType(Value: TLabelType);
  procedure SetLabelVisible(Value: Boolean);
  procedure SetTextType(const Value: TTypeText);
  function GetEditColor: TColor;
  procedure SetEditColor(const Value: TColor);
protected
  procedure Resize; override;
  procedure FontChanged; override;
  procedure SizeChanged; override;
public
  constructor Create(AOwner: TComponent); override;
  property Edit: TEdit read FEdit write FEdit;
  property CSLabel: TLabel read FLabel write FLabel;
published
  property EditColor: TColor read GetEditColor write SetEditColor;
  property EditReadOnly: Boolean read GetEditReadOnly write EditReadOnly;
  property EditText: string read GetEditText write SetEditText;
  property EditVisible: Boolean read GetEditVisible write EditVisible;
  property Font: T;
end;
```

![](img/cb7f288580e05eab3a6dcf42bcc2f2_486_0.png)

# CLX

## 第二部分

`property Gap: Integer read FGap write SetGap;`

`property LabelPosition: TLabel read FLabel write SetLabelType;`

`property LabelText: string read GetLabel write SetLabelText;`

`property LabelTypeText: TTypeText read GetTypeText write SetTypeText;`

`property LabelVisible: Boolean read GetLabelVisible write LabelVisible;`

你可以看到这个控件聚合了一个自定义标签和一个编辑控件。它有三个关键属性：

- 用于读取和写入标签的标题（`caption`）。
- 用于读取和写入编辑控件的标题。
- 用于更改标签和编辑控件的字体。注意，我不需要为 `Font` 控件声明 `set` 和 `get` 方法。这是因为 `Font` 控件是通过 `TControl` 继承自 `TCustomControl` 的，我只需要将将其暴露为发布属性（`published property`）。在 `TControl` 中，该属性被声明为保护（`protected`），这意味着它不会出现在对象检查器（`Object Inspector`）中。我的代码仅表示我希望该属性对用户在对象检查器可见。

这个控件在表面上与 `TEditPanel` 相似。这里的区别在于该控件继承自 `TCustomControl`，而不是继承自已知控件（如 `TPanel`）。这意味着 `TEditLabelEdit` 并不继承面板控件中的花哨边框和倒角技术。另一方面，它也没有携带与 `TPanel` 控件相关的包袱。并不是说 `TPanel` 控件很笨肿，但它包含了此控件不需要的属性，例如倒角和边框，为什么不包含它们呢？

所有的 `TEditLabelEdit` 都继承了作为具有宽度和高度的可视控件的能力，并且可以存储在组件面板上。这正是你这种情况下需要的，而 `TPanel` 则太大材小用了。
