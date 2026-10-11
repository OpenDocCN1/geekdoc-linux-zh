
`TRomanNumeralInteger` = 1..High(`longint`);

```
...
implementation
...
```pascal

function `GetRomanNumeralValue`(const V : `TVarData`) : `TRomanNumeralInteger`;

begin

  //我们将存储映射到 VLongs 成员数组的第一个位置。

  Result := V.`VLongs`[0];

end;

```pascal

procedure `SetRomanNumeralValue`(var V : `TVarData`; data : `TRomanNumeralInteger`);

begin

  V.`VLongs`[0] := data;

end;

```

### 第 2 步 – 创建自定义变体的函数

在其他单元中创建自定义变体时，需要编写额外的函数。例如，编写了两个函数。一个函数接受 `TRomanNumeralInteger` 类型的参数，另一个接受一个需要符合罗马数字有效表示法的字符串。它们显示所示：

interface

...

```pascal
// 这些函数允许创建 RomanNumeral 变体
```

// 传入一个非零长整数值或一个符合 正确罗马数字格式的字符串

```pascal
function `RomanNumeralsCreate`(intData : `TRomanNumeralInteger`) : Variant; overload;
function `RomanNumeralsCreate`(strData : string) : Variant; overload;
```

...

## implementation

...

// 步骤 2。编写一个创建自定义变体实例的方法。这 // 将填充第 1 步中定义的变体数据。

// 前两个 RomanNumeralsCreate 过程在该单元内部被使用 //
procedure `RomanNumeralsCreate`(var Result : `TVData`; data : `TRomanNumeralInteger`); overload;

```pascal
begin
  Result.`VType` := varRomanNumerals;
  `SetRomanNumeralValue`(Result, data);
end;
```

```pascal
procedure `RomanNumeralsCreate`(var Result : `TVData`; data : string); overload;
begin
  Result.`VType` := varRomanNumerals;
  `SetRomanNumeralValue`(Result, `RomToInt`(data));
end;
```

// 这两个 RomanNumeralsCreate 过程可以从其他单元访问 // 它们只是调用内部使用的过程。

```pascal
function `RomanNumeralsCreate`(intData : `TRomanNumeralInteger`) : Variant;
begin
  `RomanNumeralsCreate`(`TVData`(Result), intData);
end;
```

```pascal
function `RomanNumeralsCreate`(strData : string) : Variant; overload;
begin
  `RomanNumeralsCreate`(`TVData`(Result), strData);
end;
```

...

## 第 3 步 – 创建派生类

对于此示例，罗马数字变体将派自 `CustomVariantType`，因为不需要额外的属性或方法。
由于该类不应被其他单元使用，因此它被放置在实现部分。该类的定义如下：

```pascal
implementation
--
type
// 该类实现了用于我们的
// RomanNumeral 变体 (varRomanNumerals) 的方法
//
// 注意这不在接口部分，因为它只在
// 此单元的初始化部分创建一次。
RomanNumeralType = class(TCustomVariantType)
protected
  function `LeftPromotion`(const V: `TVData`; const Operator: `TVarOp`;
    out RequiredVarType: TType); Boolean; override;
  function `RightPromotion`(const V: `TVData`; const Operator: `TVarOp`;
    out RequiredVarType: TType); Boolean; override;
public
  procedure `CastTo`(var Dest: `TVData`; const Source: `TVData`); override;
  procedure `CastTo`(var Dest: `TVData`; const Source: `TVData`;
    const AVarType: TType); override;
  procedure `Clear`(var V: `TVData`); override;
  procedure `Copy`(var Dest: `TVData`; const Source: `TVData`;
    const Indirect: Boolean); override;
  procedure `BinaryOp`(var Left: `TVData`; const Right: `TVData`;
    const Operator: `TVarOp`); override;
  procedure `UnaryOp`(var Right: `TVData`; const Operator: `TVarOp`); override;
  procedure `Compare`(const Left, Right: `TVData`;
    var Relationship: `TVarCompareResult`); override;
```

## 第 4 步 – 重写适当的虚方法

在这一步中，重写了适当的方法。由于 `RomanNumeralType` 是 `TCustomVariantType` 的派生类，必须实现抽象方法 `Clear` 和 `Copy`。此外，将解释每个重写的方法。

## 第 4a 步 – 重写 Clear 方法

当变体需要清理时，会调用 `Clear` 方法。对于在 `TVarData` 记录中存储数据的变体类型，使用 `VariantInit` 运行时库例程。当变体为存储其数据分配额外的内存时，务确保释放内存并将 `TVarData.Type` 字段置为空。

```pascal
procedure `TRomanNumeralType.Clear`(var V: `TVData`);
begin
  `VariantInit`(V);
end;
```

## 第 4b 步 – 重写 Cast 方法

当变体需要清理时，调用 `Cast`。对于在 `TVarData` 记录中存储数据的变体类型，使用 `VariantInit` 运行时库例程。当变体为存储变体数据分配额外的内存时，务确保释放内存并将 `TVarData.Type` 字段置为空。（此处注：原文此处存在描述重复混乱，已根据逻辑整合翻译）

```pascal
procedure `TRomanNumeralType.Clear`(var V: `TVData`);
begin
  `VariantInit`(V);
end;
```

### 第 4b 步 – 重写 Cast 方法（修正逻辑）

`Cast` 在变体需要清理时被调用。对于在 `TVarData` 记录中存储数据的变体类型，使用 `VariantInit` 运行时库例程。

```pascal
procedure `TRomanNumeralType.Clear`(var V: `TVData`);
begin
  `VariantInit`(V);
end;
```

## 第 4c 步 – 重写 CastTo 方法

`CastTo` 在尝试将变体转换为另一种变体时被调用。如果转换允许，变体将转换为请求类型。如果转换不允许，使用 `RaiseError` 运行时库例程告知调用者不支持。

```pascal
procedure `TRomanNumeralType.CastTo`(var Dest: `TVData`;
  const Source: `TVData`; const AVarType: TType);
begin
  case AVarType of
    varSingle:
      Dest.`VLongs`[0] := `LongToSingle`(Source.`VLongs`[0]);
    varDouble:
```
