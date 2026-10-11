
# 对象与接口 第4章

```pascal
function GetVariantType(V: Variant): string;
var
  VarData: TVarData;
  S: string;
begin
  VarData := TVarData(V);
  case VarData.VType of
    varEmpty: S := 'varEmpty';
    varNull: S := 'varNull';
    varSmallInt: S := 'varSmallInt';
    varInteger: S := 'varInteger';
    varSingle: S := 'varSingle';
    varDouble: S := 'varDouble';
    varCurrency: S := 'varCurrency';
    varDate: S := 'varDate';
    varOleStr: S := 'varOleStr';
    varDispatch: S := 'varDispatch';
    varError: S := 'varError';
    varBoolean: S := 'varBoolean';
    varVariant: S := 'varVariant';
    varUnknown: S := 'varUnknown';
    varString: S := 'varString';
    varTypeMask: S := 'varTypeMask';
    varByRef: S := 'varByRef';
    varByte: S := 'varByte';
    varArray: S := 'varArray';
end;
  Result := S;
```

```pascal
varVariant: S := 'varVariant';
varUnknown: S := 'varUnknown';
varString: S := 'varString';
varTypeMask: S := 'varTypeMask';
varByRef: S := 'varByRef';

end;
Result : S;
```

这段代码首先将变体转换为 `TVData` 类型的变量。这样做，它仅仅暴露了变体的真实类型。然而，`TVData` 类型的变体不会作为 `Variant` 变量运行。这是因为编译器为变体提供了特殊服务，而不会为像 `TVData` 这样的简单记录提供这些服务。

注意的是，编写此函数的开头行至少有两种方法。我是这样写的：

```pascal
function GetVariantType(V: Variant): string;
var
  i: Integer;
  S: string;
begin
  i := VarType(V);
  case i of
    varEmpty: S := 'varEmpty';
    varNull: S := 'varNull';
...
end;
```

这段代码的工作方式与随书实际程序代码相同。

无论你如何实现该函数，关键点在于变体可以呈现某种类型的外观。变体变色龙的行为是由赋值它的变量类型触发的。如果你愿意，可以将变体看作一只变色龙，它通过假设赋值它的变量的颜色来隐藏自己。变体从不是 `Variant` 类型；它要么是 `NULL`，要么是赋值它的变量的类型。同样，变色龙没有自己的颜色，但总是在改变以适应周围的环境。要么它未出生、已死亡、不存在且完全没有颜色！

以下例程均可与变体一起使用。要了解更多关于这些例程的信息，请在线帮助。

## 了解 Delphi 与 Linux

### 第一部分

```go
function VarType(const V: Variant): TVart;
function VarAsType(const V: Variant; AVArray: TVType): Variant;
function VarIsType(const V: Variant; AVArray: TVType): Boolean; overload;
function VarIsType(const V: Variant): Variant;
const AVTypes: array of TVType; Boolean; overload;
function VarByRef(const V: Variant): Boolean;
function VarIsEmpty(const V: Variant): Boolean;
procedure VarCheckEmpty(const V: Variant): Boolean;
function VarNull(const V: Variant): Boolean;
function VarClear(const V: Variant): Boolean;
function VarCustom(const V: Variant): Boolean;
function VarOrdinal(const V: Variant): Boolean;
function VarFloat(const V: Variant): Boolean;
function VarNumeric(const V: Variant): Boolean;
function VarToStr(const V: Variant): string;
function VarToStrDef(const V: Variant; const ADefault): string;
function VarToStr(const V: Variant): WideString;
function VarToStrDef(const V: Variant; const ADefault): WideString;
WideString;
function VarDateTime(const V: Variant): TDateTime;
function VarFromDateTime(const A: TDateTime): Variant;
function VarInRange(const AValue, AMin, AMax: Variant): Boolean;
function VarEnsureRange(const AValue, AMin, AMax: Variant): Variant;
function VarIsEmptyParam(const V: Variant): Boolean;
function VarSupports(const V: Variant; const IUID; out Int): Boolean;
Variant copy support
procedure VarCopyNoID(var Dest: Variant; const Source: Variant);
```
是一些用于变体数组的例程，遗憾的是，书中没有空间讨论它们：

```pascal
function VarArrayCreate(const Bounds: array of Integer; AVType: TType): Variant;
function VarArrayOff(const Values: array of Variant): Variant;
function VarArrayDimCount(const A: Variant): Integer;
function VarArrayLowBound(const A: Variant; Dim: Integer): Integer;
function VarArrayHighBound(const A: Variant; Dim: Integer): Integer;
function VarArrayLock(const A: Variant): Pointer;
procedure VarArrayUnlock(const A: Variant);
function VarArrayRef(const A: Variant): Variant;
function VarIsArray(const A: Variant): Boolean;
function VarTypeIsValidArrayType(const AVType: TVType): Boolean;
function VarTypeIsValidElementType(const AVType: TVType): Boolean;
```

### 第 4 章

在结束本节之前，我想明确一点：变体 `variants` 并不是为了让你在任何需要处理变量的地方就可以在程序中广泛使用的。我不怀疑实际上会有许多人那样的编程，但我想强调的是，开发者们并不真的希望这样使用变体，主要因为它们带有一些开销。`variants` 所执行的某些技巧，例如字符串处理，恰好经过了高度优化。然而，你永远不应该认为变体像标准的 Pascal 类型（如 `Integer`、`Cardinal` 或 `string`）那样快速或高效。
