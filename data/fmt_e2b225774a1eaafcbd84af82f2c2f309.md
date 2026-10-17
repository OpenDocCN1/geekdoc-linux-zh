
```pascal
unit Main;

interface

uses SysUtils, Classes, Graphics, Controls, Dialogs, StdCtrls, ExtCtrls;

type
  TForm = class(TForm)
    ListBox1: TListBox;
    RadioGroup: TRadioGroup;
    procedure RadioGroupClick(Sender: TObject);
  private
    procedure DoLongInt;
    procedure DoInteger;
    procedure DoCardinal;
    procedure DoLongWord;
    procedure DoWord;
    procedure DoShortInt;
    procedure DoSmallInt;
  public
  end;

var
  Form1: TForm;

implementation

{$R *.dfm}

type
  MethodType = (mtInteger, mtCardinal, mtLongInt, mtLongWord, mtWord, mtShortInt, mtSmallInt);

procedure TForm.DoInteger;
var
  Value: Integer;
begin
  ListBox1.Items.Add('Integer high value: ' + IntToStr(High(Value)));
  ListBox1.Items.Add('Integer low value: ' + IntToStr(Low(Value)));
  ListBox1.Items.Add('Size of Integer: ' + IntToStr(SizeOf(Value)) + ' bytes or ' + IntToStr(8 * SizeOf(Value)) + ' bits.');
end;

procedure TForm.DoLongInt;
var
  Value: LongInt;
begin
  ListBox1.Items.Add('LongInt high value: ' + IntToStr(High(Value)));
  ListBox1.Items.Add('LongInt low value: ' + IntToStr(Low(Value)));
  ListBox1.Items.Add('Size of LongInt: ' + IntToStr(SizeOf(Value)) + ' bytes or ' + IntToStr(8 * SizeOf(Value)) + ' bits.');
end;

procedure TForm.RadioGroupClick(Sender: TObject)
begin
  case MethodType(RadioGroup.ItemIndex) of
    Integer: DoInteger;
    Cardinal: DoCardinal;
    LongInt: DoLongInt;
    LongWord: DoLongWord;
    Word: DoWord;
    ShortInt: DoShortInt;
    SmallInt: DoSmallInt;
  end;
end;

procedure TForm.DoCardinal;
var
  Value: Cardinal;
begin
  ListBox1.Items.Add('Cardinal high value: ' + IntToStr(High(Value)));
  ListBox1.Items.Add('Cardinal low value: ' + IntToStr(Low(Value)));
  ListBox1.Items.Add('Size of Cardinal: ' + IntToStr(SizeOf(Value)) + ' bytes or ' + IntToStr(8 * SizeOf(Value)) + ' bits.');
end;

procedure TForm.DoLongWord;
var
  Value: LongWord;
begin
  ListBox1.Items.Add('LongWord high value: ' + IntToStr(High(Value)));
  ListBox1.Items.Add('LongWord low value: ' + IntToStr(Low(Value)));
  ListBox1.Items.Add('Size of LongWord: ' + IntToStr(SizeOf(Value)) + ' bytes or ' + IntToStr(8 * SizeOf(Value)) + ' bits.');
end;
```

### 列表 3.1 继续

```pas
begin
ListBox1.Items.Add('Word high value: ' + IntToStr(High(Value)));
ListBox1.Items.Add('Word low value: ' + IntToStr(Low(Value)));
ListBox1.Items.Add('Size of Word: ' + IntToStr(SizeOf(Value)) + ' bytes or ' + 
  + IntToStr(8 * SizeOf(Value)) + ' bits.');
end;

procedure TForm1.DoShortInt;
var
  Value: ShortInt;
begin
  ListBox1.Items.Add('ShortInt high value: ' + IntToStr(High(Value)));
  ListBox1.Items.Add('ShortInt low value: ' + IntToStr(Low(Value)));
  ListBox1.Items.Add('Size of ShortInt: ' + IntToStr(SizeOf(Value)) + ' bytes ' 
  or + IntToStr(8 * SizeOf(Value)) + ' bits.');
end;

procedure TForm1.DoSmallInt;
var
  Value: SmallInt;
begin
  ListBox1.Items.Add('SmallInt high value: ' + IntToStr(High(Value)));
  ListBox1.Items.Add('SmallInt low value: ' + IntToStr(Low(Value)));
  ListBox1.Items.Add('Size of SmallInt: ' + IntToStr(SizeOf(Value)) + ' bytes ' 
  or + IntToStr(8 * SizeOf(Value)) + ' bits.');
end;
```

此程序费力地对所有整数类型调用了 `High` 和 `Low` 函数。注意，它还使用了 `SizeOf` 函数，该函数返回任何变量或类型以字节为单位的大小。这个程序的目的是展示你可以在运行时发现这些信息。

你可以通过运行时类型信息（`RTTI`）学习更多关于类型的知识。在接下来的章节“浮点类型”中将出现关于 `RTTI` 的介绍。

## 枚举类型

所有主流编程语言都有枚举类型。这是一种序数类型。事实上，枚举类型实际上只是几个从 0 开始的数字，其范围很少超过 10 多。这些数字有趣的地方在于，你可以给它们命名。

## 理解 Delphi 与 Linux

### 第一部分

考虑以下示例：

```pascal
procedure TForm1.ButtonClick(Sender:TObject);
type
  TComputerLanguage = (clC, clCpp, clJava, clPascal, clVB);
var
  ComputerLanguage: TComputerLanguage;
begin
  ComputerLanguage := clPascal
end;
```

这里的值 `clC`、`clCpp`、`clJava`、`clPascal` 和 `clVB` 只是编写 0、1、2、3 和 4 的一种花花哨表示方式。简而言之，枚举类型只是将数字与名称关联起来的方法。然而，如果你想将数字与名称关联，你总是面临忘记哪个数字属于哪个名称的风险。例如，你可能在引用 Java 时意外写了 3，而本想写的是 2。为了避免混淆，枚举类型允许你将名称与数字关联。此外，你可以通过 Pascal 的强类型检查来强制这种关系。例如，除非 `clunaFish` 是 `TComputerLanguage` 的一部分，否则你甚至无法将名为 `clunaFish` 的有效标识符赋值给变量 `ComputerLanguage`。
