
```pascal
procedure Initialize; virtual; abstract;
procedure SetPropEntry(Index: Integer; AInstance: TPersistent;
APropInfo: PPropInfo; virtual; abstract;
public
  constructor Create(const ADesigner: IDesigner; APropCount: Integer);
  virtual;
  end;
```

`InterfaceObject` 在第 4 章中讨论过。如你所见，`Initialize` 和 `SetPropEntry` 都是抽象方法，必须由该类以及派生自类的类重写。在这种情况下，它是 `TPropertyEditor`。`TPropertyEditor` 的职责之一就是实现这些方法。构造函数看起来如下：

```pascal
constructor BasePropertyEditor.Create(const ADesigner: IDesigner;
APropCount: Integer);
begin
  inherited Create;
end;
```

如你所见，构造函数什么都没做。

## 注意

到这里，大多数普通人可能已经有些沮丧了。这里 `BasePropertyEditor` 有三个方法，其中两个是抽象的，而第三个什么都不做！何何费劲声明这个类呢？嗯，可能的原因是它为所有实现 `TProperty` 接口的类建立了创建规范。如果你想创建一个属性编辑器，建议你拥有一个看起来像这样的构造函数的类，以及两个实现 `Initialize` 和 `SetPropEntry` 方法的过程。

我必须承认，这一切对我来说有点太复杂了。我感到有点迷茫，仿佛我们需要一个 Scott Myers 来出现为我们裁决这一切，就好像我们正在 C++ 中工作一样。事实上，Danny Thorpe 在 Object Pascal 开发中扮演的角色就像 Scott Myers 在 C++ 开发世界中的角色。我唯一的抱怨是，如果我想用 C++，Object Pascal 理论上不应该那么晦涩。

在现阶段，我已经准备好看看 `TColorProperty` 类本身到底是怎么了。这里是引导你从 `TPropertyEditor` 到 `TColorProperty` 的层级剩余部分：

```pascal
TOrdinalProperty = class(TPropertyEditor)
  function AllEqual(Value: Boolean); override;
  function GetEditLimit(Value: Integer); override;
  end;
```

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_546_0.png)

# CLX

## 第二部分

```pascal
TIntegerProperty = class(TOrdinalProperty)
public
  function GetValue: string; override;
  procedure SetValue(const Value: string); override;
end;

TColorProperty = class(TIntegerProperty)
public
  procedure Edit; override;
  function GetAttributes(Proc: TPropertyAttributes); override;
  function GetValue: string; override;
  procedure GetValues(Proc: TGetStrProc); override;
  procedure SetValue(const Value: string); override;
end;
```

`TOrdinalProperty` 和 `TIntegerProperty` 都是相对简单的对象。例如，这里是 `GetEditLimit` 方法：

```pascal
function TOrdinalProperty.GetEditLimit: Integer;
begin
  Result := 63;
end;
```

该方法定义了你输入到实现此属性编辑器的编辑控件中的字符串长度。例如，如果你在一个整数基属性编辑器中（如 Width 字段）中，你可以输入最多 63 个字符的值。

在这里，你看到了 Tools API 良好的一面。如果你想更改在控件中输入的字符串长度，你需要做的就是重写这个简单的方法并返回一个新值。这正是 OOP 设计的初。一旦你超越了 Tools API 的表面复杂性，它的大部分都是非常优雅的。

`TIntegerProperty` 的 `GetValue` 和 `SetValue` 方法同样直观且易用。在这里，例如是 `GetValue` 方法：

```pascal
function TOrdinalProperty.GetValue: string;
begin
  with GetDataType(GetPropType) do
    if OrdType = otLong then unsigned
      Result := IntToStr(Cardinal(GetOrdValue))
    else
      Result := IntToStr(GetOrdValue);
end;
```

该方法简单地将此属性中的整数值转换为编辑控件显示的字符串。不用说，`SetValue` 反过来。再次，这些方法的清晰性和编写面向对象代码的极佳示例。

# 高级组件设计

## 第 10 章

Tools API 的创建者对此了如指掌。因此，在使用工具之前，他掌握了一些理论。然而，一旦你理解了理论，结果是非常令人满意的。为了创建一个灵活的多态层级，`SetValue` 要求将你编辑的值转换为字符串。因此，整数、浮点数和 `TColor` 属性的 `SetValue` 方法具有相同的声明。不用说，底层 `SetValue` 方法必须将字符串转换回整数、浮点数、`TColor` 对象或任何内容。

此时，你应该能够开始猜测 `TColorProperty` 方法可能是什么样了。在这里，例如是 `GetValue` 方法：

```pascal
function TColorProperty.GetValue: string;
begin
  Result := ToString(TColor(GetOrdinalValue));
end;
```

这是非常简单的。事实上，`TColorProperty` 中的代码并没有这复杂。一旦你开始掌握这一点，你就会发现 `Designf.pas` 中声明的原始接口并没有最初看起来那么可怕。然而，这样做意义不大，因为 `DesignEditors` 中的实现满足了大多数开发者的需求。

`TPropertyEditor` 的 `Edit` 方法是你想要重写的以改变属性编辑器数据的方式：

```pascal
procedure TColorNameProperty.Edit;
var
  S: String;
begin
  S := '';
  InputQuery('New Color', 'Enter Color', S);
  SetValue(S);
end;
```

在这种情况下，我正在为在 Object Inspector 中点击省略号时弹出的 `TColorDialog` 创建替代品。当然，我用一个更简单的对话框让用户输入如“blue”或“green”之类的字符串。然而，重点在于你正在学习创建自己的属性编辑器。

在更复杂的示例中，你可能会打开一个允许用户对属性进行大量更改的表。这就是我在 `TColorClock` 组件中所做的。特别是，我创建了一个包含 `TColorGrid`、两个边框和两个按钮的对话框，如图 10.4 所示。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_548_0.png)

# CLX

## 第二部分

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_549_0.png)

图 10.4 `TColorClock` Color 属性的属性编辑器

这可能仍然 CLX 使用的对话框那么漂亮，但它作为如何创建自己的编辑器的良好示例。这里是 `TColorNameProperty.Edit` 方法的样子：

```pascal
procedure TColorNameProperty.Edit;
var
  S: String;
  ColorPicker: TColorPicker;
begin
  S := '';
  ColorPicker := TColorPicker.Create(nil);
  ColorPicker.ShowModal;
  S := ToString(ColorPicker.ColorChoice);
  ColorPicker.Free;
  SetValue(S);
end;
```

该代码创建了 `TPicker` 的实例，将其显示给用户，然后使用用户选择的颜色。在此过程结束时调用的 `SetValue` 是 `PropertyEditor` 的另一个方法。
