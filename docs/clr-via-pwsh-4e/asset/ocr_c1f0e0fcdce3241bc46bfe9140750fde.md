```
```csharp
int              a = 0;                  // 最方便的语法
System.Int32     a = 0;                  // 方便的语法
int              a = new int();          // 不方便的语法
System.Int32     a = new System.Int32(); // 最不方便的语法
```
```

表 5-1 列出的 FCL 类型在 C#中都有对应的基元类型。只要是符合公共语言规范(CLS)的类型，其他语言都提供了类似的基元类型。但是，不符合 CLS 的类型语言就不一定要支持了。

# ### 表 5-1 C#基元类型与对应的 FCL 类型

| C#基元类型 | FCL 类型 | 符合 CLS | 说明 |
| --- | --- | --- | --- |
| sbyte | System.SByte | 否 | 有符号 8 位值 |
| byte | System.Byte | 是 | 无符号 8 位值 |
| short | System.Int16 | 是 | 有符号 16 位值 |
| ushort | System.UInt16 | 否 | 无符号 16 位值 |
| int | System.Int32 | 是 | 有符号 32 位值 |
| uint | System.UInt32 | 否 | 无符号 32 位值 |
| long | System.Int64 | 是 | 有符号 64 位值 |
| ulong | System.UInt64 | 否 | 无符号 64 位值 |
| char | System.Char | 是 | 16 位 Unicode 字符(char 不像在非托管 C++中那样代表一个 8 位值) |
| float | System.Single | 是 | IEEE 32 位浮点值 |
| double | System.Double | 是 | IEEE 64 位浮点值 |
| bool | System.Boolean | 是 | true/false 值 |
| decimal | System.Decimal | 是 | 128 位高精度浮点值，常用于不容许舍入误差的金融计算。128 位中，1 位是符号，96 位是值本身(N)，8 位是比例因子(k)。decimal 实际值是±N×10^k，其中 -28 <= k <= 0。其余位没有使用 |
| string | System.String | 是 | 字符数组 |
| object | System.Object | 是 | 所有类型的基类型 |
| dynamic | System.Object | 是 | 对于 CLR，dynamic 和 object 完全一致。但 C#编译器允许使用简单的语法让 dynamic 变量参与动态调度。详情参见本章最后的 5.5 节“dynamic 基元类型” |

从另一个角度，可认为 C#编译器自动假定所有源代码文件都添加了以下 using 指令(参考第 4 章):

```
```csharp
using sbyte  = System.SByte;
using byte   = System.Byte;
using short  = System.Int16;
using ushort = System.UInt16;
using int    = System.Int32;
using uint   = System.UInt32;
...
```
```

C#语言规范称：“从风格上说，最好是使用关键字，而不是使用完整的系统类型名称。” 我不同意语言规范；我情愿使用 FCL 类型名称，完全不用基元类型名称。事实上，我希望编译器根本不提供基元类型名称，而是强迫开发人员使用 FCL 类型名称。理由如下。