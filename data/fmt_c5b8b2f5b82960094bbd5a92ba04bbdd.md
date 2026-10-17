
# Kylix 2 开发第 9 章：编译器、运行时库与变体 221

```pascal
procedure TRomanNumeralType.BinaryOp(var Left: TVData;
  const Right: TVData; const Operator: TVarOp);
begin
    case Left.VType of
        varSingle,
        varDouble :
            begin
                // 对于左侧，不创建 RomanNumerals。
                // 数值类型，我们将罗马数字转换为相应的类型
                // 并执行操作。对于字符串，我们将罗马数字转换为字符串
                // 仅允许加操作，执行拼接。
                case Right.VType of
                    varSingle,
                    varDouble :
                        case Operator of
                            opAdd := Left.VDouble := Left.VDouble + RomanNumeralsToFloat( Right );
                            opSubtract := Left.VDouble := Left.VDouble - RomanNumeralsToFloat( Right );
                            opMultiply := Left.VDouble := Left.VDouble * RomanNumeralsToFloat( Right );
                            opDivide := Left.VDouble := Left.VDouble / RomanNumeralsToFloat( Right );
                        else
                            inherited;
                        end;
                    varString,
                    varOleStr :
                        begin
                            if Operator = opAdd then
                                string(Left.VString) := string(Left.VString) + RomanNumeralsToString( Right )
                            else
                                begin
                                    // 基类将抛出异常
                                    // 这不应该发生，因为 Left & Right Promotion 只允许
                                    // opAdd 传递下去..
                                    inherited;
                                end;
                        end;
                    else
                        inherited;
                end;
            end
            // ... (剩余实现)
    end;
end;
```

```pascal
varOleStr :
begin
  if Operator = opAdd then
    WideString(Pointer(Left.VOleStr)) :=
    WideString(Pointer(Left.VOleStr)) + RomanNumeralsToString(Right)
  else
    begin
      // 基类将抛出异常
      // 这不应该发生，因为 Left & Right Promotion 只允许
      // opAdd  own传递下去..
      inherited;
    end;
end;
else // 不是 Single, Double, String 或 OleStr
begin
  if Left.VType = varRomanNumerals then
    begin
      case Right.VType of
        varString:
          begin
          if Operator = opAdd then
            Variant(Left) := RomanNumeralsToString(Left) + string(Right.VString)
          else
            begin
              // 基类将抛出异常
              // 这不应该发生，因为 Left & Right Promotion 只允许
              // 将 opAdd 传递通过。
              inherited;
            end;
          end;
    end;
varOleStr :
begin
  if Operator = opAdd then
  else
    Variant(Left) := RomanNumeralsToString(Left) +
    WideString(Pointer(Right.VOleStr));
  begin
    // 基类将抛出异常
    // 这不应该发生，因为 Left & Right Promotion 只允许
allow
```

```pascal
// 将 opAdd 传递通过。
inherited;
end;
```

```pascal
varSingle :
begin
case Operator of
opAdd      : Left.VSingle := RomanNumeralsToFloat(Left) + Right.VSingle;
opSubtract  : Left.VSingle = RomanNumeralsToFloat(Left) - Right.VSingle;
opMultiply  : Left.VSingle = RomanNumeralsToFloat(Left) * Right.VSingle;
opDivide   : Left.VSingle = RomanNumeralsToFloat(Left) / Right.VSingle;
else
  inherited; // 让基类处理这个...
end;
end;
```

```pascal
varDouble :
begin
case Operator of
opadd      : Left.VDouble := RomanNumeralsToFloat(Left) + Right.VDouble;
opubtract  : Left.VDouble = RomanNumeralsToFloat(Left) - Right.VDouble;
opMultiply  : Left.VDouble = RomanNumeralsToFloat(Left) * Right.VDouble;
opdivide   : Left.VDouble = RomanNumeralsToFloat(Left) / Right.VDouble;
else
  inherited; // 让基类处理这个...
end;
else
```

```pascal
begin
if Right.VType <> varRomanNumerals then
  inherited // 让基类处理这个
else
begin
case Operator of
opAdd      : SetRomanNumeralValue(Left,
```

# 第 9 章：编译器、运行时库与变体
