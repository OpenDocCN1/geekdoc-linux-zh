
注意，`${IF}` 终止的指令与前两个不同。它使用 `${ENDIF}` 指令来终止块。额外的指令 `${ELSEIF}` 也是可用的。符号通过使用以下之一进行定义。在下一节中将讨论 `${ELSE}` 指令。通常使用 `${MESSAGE}` 指令来禁用调试代码。这里有一个示例：

```
${undef DEBUG} // 关闭调试

${IFDEF DEBUG}
// 执行一些调试工作
${ENDIF}

${DEFINE DEBUG} // 开启调试
```

## 表达式

表达式是 Kylix 和 Delphi 6 的新特性。`${IF}` 指令测试如下所示。使用 `${IF}` 指令时，编译时的常量表达式是可用的。引入 `ConditionalExpressions` 符号对于兼容旧版本的 Delphi 非常有用，如下所示：

```
${IFDEF ConditionalExpressions
${IF MyCondition}
// 在传统的样式 中使用 ELSE 指令
// 编译器会将 ELSE 匹配到 ${IFDEF} 而。
```

`${ELSEIF AnotherCondition > 10`

// 更适当的代码

`${ENDIF}`

```

Kylix 允许通过使用 `${IFOPT}` 指令确定编译器选项的状态。某些函数的行为取决于编译器选项的状态。一个很好的例子是输入和输出函数。在 `${I-}` 状态下，通过使用 `IORes` 函数来检测输入输出错误。当使用 `${I+}` 状态时，输入输出错误会抛出异常。以下代码演示了过程如何使用 `${IFOPT}` 指令来处理 `${I}` 编译选项的两种情况。

```
var

  f : file;

  ${I-} // 使用 IORes 时才需要这个

  ioError : integer;

${ENDIF}
begin

  AssignFile(F,'ANExistentFile');

  ${IFOPT} I+

try

  Reset(F);

  ${IFOPT} I+ // 捕获任何 IO 异常

except

  on e : EInOutError do

    ShowMessage('Exception: ' + e.message);

end;

${ELSE} // 不使用异常，因此使用 IOResult 检测错误

  ioError := IOResult;

  if ioError < 0 then

    ShowMessage('I/O Error: ' + IntToStr(ioError));

${ENDIF}
```

// 此处更多代码。应该将其封装在 try/finally 中以便
// 在结束时关闭文件。

end;

`${IFOPT}` 在适当的情况下使用 `${ELSE}` 和 `${ENDIF}` 指令。

## 运行时库 (Run-time Library)

运行时库是一组跨平台程序和一种称为 `variant` 的特殊类型。通过使用这些程序而非 `Libc.pas` 或其他单元中的程序，应用程序在 Linux 和 Windows 之间的迁移变得更加容易。这些程序从内存分配到复杂的数学函数以及字符串处理不等。`variant` 是一种特殊的数据类型，允许同一个变量在运行时分配不同的数据类型。

Kylix 有二十个单元组成运行时库。它们列如下表所示：

### 表 9-2

| 单元 | 说明 |
| --- | --- |
| System | 隐式包含在每个程序中，`System.pas` 包含了编译器需要特殊方式处理的程序。出于性能考虑，某些参数以非标准方式传递。另一些则需要编译特殊知识。 |
| SysUtils | `SysUtils.pas` 包含了运行时库的大部分。异常在此单元中声明。 |
| Types | 包含各种数据类型和流的接口声明。 |
| Contrns | 容器资源，如列表、栈、队列和桶。 |
| ConvUtils | 转换支持程序。 |
| DateUtils | 许多许多与日期和时间相关的程序。 |
| HelpInt | VCL/CLX 帮助系统的接口。 |
| InFiles | 用于操作 ini/配置文件的类。 |
| MaskUtils | 掩码程序。 |
| Masks | 掩码匹配。 |
| Math | `Math.pas` 包含数学和财务程序。 |
| RTLConsts | 运行时库错误、警告和消息资源。 |
| StdConv | 物理、流体和热单位的转换程序。 |
| StrUtils | 字符串工具程序。 |
| SyncObjs | 用于多线程应用程序的同步对象。 |
| TypInfo | Variant 类型支持函数。 |
| VarComp | 包含用于复数自定义 variant 类型的程序。 |
| VarConv | 提供测量转换自定义 variant 类型的程序。 |
| Variants | 有有用的相关函数，以及一些类和接口。 |
| VarUtils | 仅用于非 Windows 操作系统，它包含了操作 variants 的平台中性程序。 |

运行时库中发现众多程序列在附录 H，“运行时库程序”中。

## Variants (变体)

最初 `variants` 用于 Windows 平台上的 OLE 自动化。为了在 Linux 平台上支持 `variants`，Borland 写了一个平台无关的版本。`Variants` 是一种特殊数据类型，可以包含许多不同类型的数据，其实际类型在运行时确定。然而，这种运行时类型信息是有代价的。由于代码大小增加，应用程序运行会变慢且体积更大。只要提前知道数据类型且类型无法更改，请使用特定数据类型而不是 `variant`。

## Variant 类型 (Variant Types)

`Variants` 可以包含许多不同的数据类型。在内部，它们由以下常量表示。

```
const

varEmpty = $0000;

varNull = $0001;

varSmallInt = $0002;

varInteger = $0003;

varSingle = $0004;

varDouble = $0005;

varCurrency = $0006;

varDate = $0007;

varOleStr = $0008;

varDispatch = $0009;

varError = $000A;

varBoolean = $000B;

varVariant = $000C;

varUnknown = $0000;

//varDecimal = $000E; (不支持)

{ undefined $0f } (不支持)

varShortInt = $0010;

varByte = $0011;

varWord = $0012;

varLongInt = $0013;

varInt64 = $0014;

//varword64 = $0015; (不支持)

varStrArg = $0048;

varString = $0100;
```

运行时库中发现的众多程序列在附录 H，“运行时库程序”中。`VType` 字段被编译器用于确定如何访问 `variant` 的数据。

Variant 的内部表示 (Internal Representation of Variant)

`Variant` 由类型和数据组成。注意 `variant` 可以包含的各种数据类型，从整数到字符串不等。仔细观察并注意 `variants` 不能包含类、类引用、记录、集合、静态数组、文件或指针。它们可以包含特殊的动态数组——`TVArray`，稍后会讨论。`VType` 字段被编译器用于确定如何访问 `variant` 的数据。

> 提示：`TVRec` 也在 `System.pas` 单元中声明。它不用于 `variant` 数据类型；而是被编译器用于接收常量数组的参数。

使用 `variant` 单词作为数据类型声明的 `variants` 如下：

```pascal
var

MyVariant : Variant;
```

### 空 Variant (Empty Variants)

声明时，`variants` 被分配了一个特殊值 — `Empty`。`Empty` 表示 `variant` 尚未被赋值。使用 `VarEmpty` 函数来判断 `variant` 是否为空。可以使用 `VarClear` 函数将 `variant` 置为赋值。

```pascal
if VarEmpty(MyVariant) then

MyVariant := '你想放在这里的任何'

else

VarClear(MyVariant);
```

### Null Variant (Null Variants)

`Variants` 可以拥有的另一个特殊值是 `Null`。`Null` 与空不同，因为它是一个实际分配的值。使用 `VarIsNull` 函数来判断 `variant` 是否被分配了空值。

```pascal
MyVariant := null;

if VarIsNull(MyVariant) then

// 进行适当处理
```
