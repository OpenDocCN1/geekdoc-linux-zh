## 第七章 常量和字段

**本章内容：**

- 常量
- 字段

本章介绍如何向类型添加数据成员，具体就是常量和字段。

### 7.1 常量

常量是值从不变化的符号。定义常量符号时，它的值必须能在编译时确定。确定后，编译器将常量值保存到程序集元数据中。这意味着只能定义编译器识别的基元类型的常量。在 C#中，以下类型是基元类型，可用于定义常量：Boolean, Char, Byte, SByte, Int16, UInt16, Int32, UInt32, Int64, UInt64, Single, Double, Decimal 和 String。然而，C# 也允许定义非基元类型的常量变量(constant variable)，前提是把值设为 null：

```csharp
using System;

public sealed class SomeType {
    // SomeType 不是基元类型，但 C# 允许
    // 值为 null 的这种类型的常量变量
    public const SomeType Empty = null;
}
```

> 注：PowerShell 没有 `const` 关键字。脚本中的“恒定值”常用 `Set-Variable -Option Constant`（或 `-Option ReadOnly`）的变量，或通过类只定义不修改的静态字段来约定；由于脚本没有编译期常量折叠，值在每次运行时重新求值，也就不存在“把值嵌入调用方 IL”的行为。

由于常量值从不变化，所以常量总是被视为类型定义的一部分。换言之，常量总是被视为静态成员，而不是实例成员。定义常量将导致创建元数据。

代码引用常量符号时，编译器在定义常量的程序集的元数据中查找该符号，提取常量的值，将值嵌入生成的 IL 代码中。由于常量的值直接嵌入代码，所以在运行时不需要为常量分配任何内存。除此之外，不能获取常量的地址，也不能以传引用的方式传递常量。这些限制意味着常量不能很好地支持跨程序集的版本控制。因此，只有确定一个符号的值从不变化才应定义常量。(将 MaxInt16 定义为 32767 就是一个很好的例子)。下面来演示我刚才所说的内容。首先，请输入以下代码，并将其编译成一个 DLL 程序集。

```csharp
using System;

public sealed class SomeLibraryType {
    // 注意：C# 不允许为常量指定 static 关键字，
```

```csharp
    // 因为常量总是隐式为 static
    public const Int32 MaxEntriesInList = 50;
}
```

接着用以下代码生成一个应用程序集①：

```csharp
using System;

public sealed class Program {
    public static void Main() {
        Console.WriteLine("Max entries supported in list: "
            + SomeLibraryType.MaxEntriesInList);
    }
}
```

> 注：这是编译为应用程序集后带 `Main` 入口的 C# 代码。PowerShell 脚本没有 `Main` 方法和程序集入口点，等效写法是直接引用常量/静态字段（如 `[SomeLibraryType]::MaxEntriesInList`）；「把常量值嵌入调用方 IL」的行为在脚本中也不存在。

注意代码引用了在 **SomeLibraryType** 类中定义的 **MaxEntriesInList** 常量。编译器生成应用程序代码时，会注意到 **MaxEntriesInList** 是值为 **50** 的常量符号，所以会将 **Int32** 值 **50** 嵌入应用程序的 IL 代码，如下所示。事实上，在生成了应用程序集之后，运行时根本不会加载 DLL 程序集，可以把它从磁盘上删除。

```cil
  .method public hidebysig static void Main() cil managed
  {
    .entrypoint
    // Code size       25 (0x19)
    .maxstack 8
    IL_0000:  nop
    IL_0001:  ldstr      "Max entries supported in list: "
    IL_0006:  ldc.i4.s   50
    IL_0008:  box        [mscorlib]System.Int32
    IL_000d:  call       string [mscorlib]System.String::Concat(object, object)
    IL_0012:  call       void [mscorlib]System.Console::WriteLine(string)
    IL_0017:  nop
    IL_0018:  ret
  } // end of method Program::Main
```

这个例子清楚地展示了版本控制问题。如果开发人员将常量 **MaxEntriesInList** 的值更改为 **1000**，并且只是重新生成 DLL 程序集，那么应用程序集不受任何影响。应用程序要获得新值，也必须重新编译。如果希望在运行时从一个程序集中提取另一个程序集中的值，那么不应该使用常量，而应该使用 **readonly** 字段，详情参见下一节。

> 注：上述“重新生成/重新编译”的场景依然只属于编译型语言。PowerShell 每次运行脚本都会重新读取定义，调用方看到的一定是最新值；对应模块可借助 `ModuleVersion` 管理版本。

### 7.2 字段

字段是一种数据成员，其中容纳了一个值类型的实例或者对一个引用类型的引用。表 7-1 总结了可应用于字段的修饰符。

如表 7-1 所示，CLR 支持类型(静态)字段和实例(非静态)字段。如果是类型字段，容纳字段数据所需的动态内存是在类型对象中分配的，而类型对象是在类型加载到一个 AppDomain 时创建的(参见第二十二章 “CLR 寄宿和 AppDomain”)。那么，什么时候将类型加载到一个 AppDomain 中呢？这通常是在引用了该类型的任何方法首次进行 JIT 编译的时候。如果是实例字段，容纳字段数据所需的动态内存是在构造类型的实例时分配的。

表 7-1 字段修饰符

| CLR 术语 | C#术语 | 说明 |
| --- | --- | --- |
| Static | static | 这种字段是类型状态的一部分，而不是对象状态的一部分 |
| Instance | (默认) | 这种字段与类型的一个实例关联，而不是与类型本身关联 |
| InitOnly | readonly | 这种字段只能由一个构造器方法中的代码写入 |
| Volatile | volatile | 编译器、CLR 和硬件不会对访问这种字段的代码执行“线程不安全”的优化措施。只有以下类型才能标记为 volatile：所有引用类型，Single，Boolean，Byte，SByte，Int16，UInt16，Int32，UInt32，Char，以及基础类型为 Byte，SByte，Int16，UInt16，Int32 或 UInt32 的所有枚举类型。volatile 字段将在第二十九章“基元线程同步构造”讨论① |

> 注：PowerShell 类支持静态字段（`static`）和实例字段，但没有 `readonly`、`volatile` 这些修饰符，也不支持 C# 的 `static`/`readonly` 组合。可用 `hidden` 关键字把成员从默认输出中隐藏；需要线程间可见性时，通常用 `[System.Threading.Volatile]` 类型或锁对象，而不是 volatile 字段。

由于字段存储在动态内存中，所以它们的值在运行时才能获取。字段还解决了常量存在的版本控制问题。此外，字段可以是任何数据类型，不像常量那样仅仅局限于编译器内置的基元类型。

CLR 支持 **readonly** 字段和 **read/write** 字段。大多数字段都是 **read/write** 字段，意味着在代码执行过程中，字段值可多次改变。但 **readonly** 字段只能在构造器方法中写入。(构造器方法只能调用一次，即对象首次创建时。)编译器和验证机制确保 **readonly** 字段不会被构造器以外的任何方法写入。注意，可利用反射来修改 **readonly** 字段。

现在，让我们以 7.1 节“常量”的代码为例，改用静态字段来修正版本控制问题。下面是等效的 PowerShell 类定义：

```powershell
class SomeLibraryType {
    # PowerShell 无 readonly，静态字段只按约定不在构造器外修改
    static [int] $MaxEntriesInList = 50
}
```

这是唯一需要修改的，应用程序的代码不必修改。但是，为了观察新的行为，必须重新生成它。当应用程序的 **Main** 方法运行时，CLR 将加载 DLL 程序集(现在运行时需要该程序集了)，并从分配给它的动态内存中提取 **MaxEntriesInList** 字段的值。当然，该值是 **50**。

① 文档将 volatile 翻译为“可变”。其实它是“短暂存在”、“易变”的意思，因为可能有多个线程都想对这种字段进行修改，所以“易变”或“易失”更佳。——译注

假设 DLL 程序集的开发人员将 50 改为 1000，并重新生成程序集。当应用程序代码重新执行时，它将自动提取字段的新值 1000。应用程序不需要重新生成，可以直接运行（尽管性能会受到一点影响）。要注意的是，当前假定的是 DLL 程序集的新版本没有进行强命名，而且应用程序的版本策略是让 CLR 加载这个新版本。

下例演示如何定义与类型本身关联的静态字段，以及静态 read/write 字段和实例字段。C# 版本用 readonly 表达"只读"意图，PowerShell 类没有该修饰符，只能靠约定：

```powershell
class SomeType {
    # 静态字段：类首次使用时由静态构造器计算并保存
    static [System.Random] $s_random = [System.Random]::new()

    # 静态 read/write 字段
    hidden static [int] $s_numberOfWrites = 0

    # 实例字段（PowerShell 无 readonly，只约定不修改）
    [string] $Pathname = "Untitled"

    # 实例 read/write 字段
    hidden [System.IO.FileStream] $m_fs

    SomeType([string] $pathname) {
        $this.Pathname = $pathname
    }

    [string] DoSomething() {
        # 读写静态 read/write 字段
        [SomeType]::s_numberOfWrites = [SomeType]::s_numberOfWrites + 1

        # 读取实例字段
        return $this.Pathname
    }
}
```

在上述代码中，许多字段都是内联初始化的①。C# 允许使用这种简便的内联初始化语法来初始化类的常量、read/write 字段和 readonly 字段。第八章“方法”会讲到，C# 实际是在构造器中对字段进行初始化的，字段的内联初始化只是一种语法上的简化。另外，在 C# 中初始化字段时，如果使用内联语法，而不是在构造器中赋值，有一些性能问题需要考虑。这些性能问题也将在第八章讨论。

> 注：PowerShell 类的属性可以在声明时给默认值，引擎会把它放进类构造器中逐个初始化，与 C# 的内联初始化语义类似；但 PowerShell 类只能定义一个构造器（不支持重载），所以本节“编译器为每个重载构造器都生成初始化代码”的讨论在脚本层不适用。

① 内联(inline)初始化是指在代码中直接赋值来初始化，而不是将对构造器的调用写出来。——译注

![](img/6fa065e17c4549db7260fbfaf4fd384e_175_0.png)

**重要提示**　当某个字段是引用类型，并且该字段被标记为 `readonly` 时，不可改变的是引用，而非字段引用的对象。以下代码对此进行了演示：

```csharp
public sealed class AType {
    // InvalidChars 总是引用同一个数组对象
    public static readonly Char[] InvalidChars = new Char[] { 'A', 'B', 'C'};
}

public sealed class AnotherType {
    public static void M() {
        // 下面三行代码是合法的，可通过编译，并可成功
        // 修改 InvalidChars 数组中的字符
        AType.InvalidChars[0] = 'X';
        AType.InvalidChars[1] = 'Y';
        AType.InvalidChars[2] = 'Z';

        // 下一行代码是非法的，无法通过编译，
        // 因为不能让 InvalidChars 引用别的什么东西
        AType.InvalidChars = new Char[] { 'X', 'Y', 'Z' };
    }
}
```

> 注：PowerShell 类没有 `readonly`，字段保存的引用和引用指向的对象都可被修改。若要把数组当作“只读集合”，应约定不重新赋值，并用 `[System.Collections.ObjectModel.ReadOnlyCollection[T]]` 之类包裹，而不是依赖 `readonly`。

构造 **SomeType** 的对象时，它的 **m_x** 字段被初始化为 **5**。这是如何发生的呢？检查一下 **SomeType** 的构造器方法(也称作 **.ctor**)的 IL 代码就明白了，如下所示：

```cil
.method public hidebysig specialname rtspecialname
    instance void .ctor() cil managed
{
    // Code size 14 (0xe)
    .maxstack 8
    IL_0000: ldarg.0
    IL_0001: ldc.i4.5
    IL_0002: stfld int32 SomeType::m_x
    IL_0007: ldarg.0
    IL_0008: call instance void [mscorlib]System.Object::.ctor()
    IL_000d: ret
} // end of method SomeType::.ctor
```

可以看出，**SomeType** 的构造器把值 **5** 存储到字段 **m_x**，再调用基类的构造器。换句话说，C#编译器提供了一个简化的语法，允许以“内联”(其实就是嵌入)方式初始化实例字段。但在幕后，它会将这种语法转换成构造器方法中的代码来执行初始化。这同时提醒我们注意代码的膨胀效应。如以下类定义所示：

```csharp
internal sealed class SomeType {
    private Int32   m_x = 5;
    private String  m_s = "Hi there";
    private Double  m_d = 3.14159;
    private Byte    m_b;

    // 下面是一些构造器
    public SomeType()                  { ... }
    public SomeType(Int32 x)           { ... }
    public SomeType(String s)          { ...; m_d=10; }
}
```

编译器为这三个构造器方法生成代码时，在每个方法的开始位置，都会包含用于初始化 **m_x**、**m_s** 和 **m_d** 的代码。在这些初始化代码之后，编译器会插入对基类构造器的调用。再然后，会插入构造器自己的代码。例如，对于获取一个 **String** 参数的构造器，编译器生成的代码首先初始化 **m_x**、**m_s** 和 **m_d**，再调用基类(Object)的构造器，再执行自己的代码(最后是用值 **10** 覆盖 **m_d** 原先的值)。注意，即使没有代码显式初始化 **m_b**，**m_b** 也保证会被初始化为 **0**。

> **注意**　编译器在调用基类构造器前使用简化语法对所有字段进行初始化，以维持源代码给人留下的“这些字段总是有一个值”的印象。但假如基类构造器调用了虚方法并回调由派生类定义的方法，就可能出问题。在这种情况下，使用简化语法初始化的字段在调用虚方法之前就初始化好了。

由于有三个构造器，所以编译器生成三次初始化 **m_x**、**m_s** 和 **m_d** 的代码——每个构造器一次。如果有几个已初始化的实例字段和许多重载的构造器方法，可考虑不是在定义字段时初始化，而是创建单个构造器来执行这些公共的初始化。然后，让其他构造器都显式调用这个公共初始化构造器。这样能减少生成的代码。下例演示了如何在 C# 中利用 **this** 关键字显式调用另一个构造器：

```csharp
using System;
internal sealed class SomeType {
    // 不要显式初始化下面的字段
    private Int32  m_x;
    private String m_s;
    private Double m_d;
    private Byte   m_b;

    // 该构造器将所有字段都设为默认值，
    // 其他所有构造器都显式调用该构造器
    public SomeType() {
        m_x = 5;
        m_s = "Hi there";
        m_d = 3.14159;
        m_b = 0xff;
    }

    // 该构造器将所有的字段都设为默认值，然后修改 m_x
    public SomeType(Int32 x) : this() {
        m_x = x;
    }

    // 该构造器将所有的字段都设为默认值，然后修改 m_s
    public SomeType(String s) : this() {
        m_s = s;
    }

    // 该构造器首先将所有字段都设为默认值，然后修改 m_x 和 m_s
    public SomeType(Int32 x, String s) : this() {
        m_x = x;
        m_s = s;
    }
}
```

> 注：PowerShell 类的构造器不能用 `: this()` 链接到另一个构造器，也不支持构造器重载。应把公共初始化逻辑放进一个私有方法（如 `Initialize()`），由唯一的构造器调用。

### 8.2 实例构造器和结构（值类型）

值类型(struct)构造器的工作方式与引用类型(class)的构造器截然不同。CLR 总是允许创建值类型的实例，并且没有办法阻止值类型的实例化。所以，值类型其实并不需要定义构造器，C#编译器根本不会为值类型内联(嵌入)默认的无参数构造器。来看下面的代码：

> 注：本小节及后续 8.2 小节讨论的“结构（值类型）构造器”不适用于 PowerShell——PowerShell 的 `class` 只能定义引用类型，没有 `struct` 关键字，也没有定义值类型的途径。脚本层可用的值类型只有 .NET 内置类型（`[int]`、`[double]`、`[datetime]` 等）；自定义值类型只能通过 `Add-Type` 用 C# 编译。

```csharp
internal struct Point {
    public Int32 m_x, m_y;
}

internal sealed class Rectangle {
    public Point m_topLeft, m_bottomRight;
}
```

为了构造一个 **Rectangle**，必须使用 **new** 操作符，而且必须指定构造器。在这个例子中，调用的是 C#编译器自动生成的默认构造器。为 **Rectangle** 分配内存时，内存中包含 **Point** 值类型的两个实例。考虑到性能，CLR 不会为包含在引用类型中的每个值类型字段都主动调用构造器。但是，如前所述，值类型的字段会被初始化为 0 或 **null**。

CLR 确实允许为值类型定义构造器。但必须显式调用才会执行。下面是一个例子。

```csharp
internal struct Point {
    public Int32 m_x, m_y;

    public Point(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
    }
}

internal sealed class Rectangle {
    public Point m_topLeft, m_bottomRight;

    public Rectangle() {
        // 在 C# 中，向一个值类型应用关键字 new，
        // 可以调用构造器来初始化值类型的字段
        m_topLeft = new Point(1, 2);
        m_bottomRight = new Point(100, 200);
    }
}
```

值类型的实例构造器只有显式调用才会执行。因此，如果 Rectangle 的构造器没有使用 new 操作符来调用 Point 的构造器，从而初始化 Rectangle 的 m_topLeft 字段和 m_bottomRight 字段，那么两个 Point 字段中的 m_x 和 m_y 字段都将为 0。

前面展示的 Point 值类型没有定义默认的无参构造器。现在进行如下改写：

```csharp
internal struct Point {
    public Int32 m_x, m_y;

    public Point() {
        m_x = m_y = 5;
    }
}

internal sealed class Rectangle {
    public Point m_topLeft, m_bottomRight;

    public Rectangle() {
    }
}
```

现在，构造新的 Rectangle 类时，两个 Point 字段中的 m_x 和 m_y 字段会被初始化成多少？是 0 还是 5？（提示：小心上当！）

许多开发人员（尤其是那些有 C++背景的）都觉得 C#编译器会在 Rectangle 的构造器中生成代码，为 Rectangle 的两个字段自动调用 Point 的默认无参构造器。但是，为了增强应用程序的运行时性能，C#编译器不会自动生成这样的代码。实际上，即便值类型提供了无参构造器，许多编译器也永远不会生成代码来自动调用它。为了执行值类型的无参构造器，开发人员必须增加显式调用值类型构造器的代码。

基于前面这一段的信息，可以确定在前面示例代码中，Rectangle 类的两个 Point 字段的 m_x 和 m_y 字段会初始化为 0，因为代码中没有在任何地方显式调用了 Point 的构造器。

但我说过，这是一个容易让人上当的问题。这里的关键在于 C#编译器不允许值类型定义无参数构造器。所以，前面的代码实际上是编译不了的。试图编译上述代码时，C#编译器会显示以下消息：error CS0568：结构不能包含显式的无参数构造器。

C#编译器故意不允许值类型定义无参构造器，目的是防止开发人员对这种构造器在什么时候

候调用产生迷惑。由于不能定义无参构造器，所以编译器永远不会生成自动调用它的代码。没有无参构造器，值类型的字段总是被初始化为 0 或 null。

> **注意** 严格地说，只有当值类型的字段嵌套到引用类型中时，才保证被初始化为 0 或 null。基于栈的值类型字段则无此保证。但是，为了确保代码的“可验证性” (verifiability)，任何基于栈的值类型字段都必须在读取之前写入(赋值)。允许先读再写会造成安全漏洞。对于所有基于栈的值类型中的字段，C#和其他能生成“可验证”代码的编译器可以保证对它们进行“置零”，或至少保证在读取之前赋值，确保不会在运行时因验证失败而抛出异常。所以，你完全可以忽略本“注意”的内容，假定自己的值类型的字段都会被初始化为 0 或 null。

注意，虽然 C#不允许值类型带有无参构造器，但 CLR 允许。所以，如果不在乎前面描述的问题，可以使用另一编程语言(比如 IL 汇编语言)定义带有无参构造器的值类型。

由于 C#不允许为值类型定义无参构造器，所以编译以下类型时，C#编译器将显示消息：**error CS0573: "SomeValType.m_x": 结构中不能有实例字段初始值设定项。**

```csharp
internal struct SomeValType {
    // 不能在值类型中内联实例字段的初始化
    private Int32 m_x = 5;
}
```

另外，为了生成“可验证”代码，在访问值类型的任何字段之前，都需要对全部字段进行赋值。所以，值类型的任何构造器都必须初始化值类型的全部字段。以下类型为值类型定义了一个构造器，但没有初始化值类型的全部字段：

```csharp
internal struct SomeValType {
    private Int32 m_x, m_y;

    // C#允许为值类型定义有参构造器
    public SomeValType(Int32 x) {
        m_x = x;
        // 注意 m_y 没有在这里初始化
    }
}
```

编译上述类型，C#编译器会显示消息：**error CS0171: 在控制返回到调用方之前，字段 "SomeValType.m_y" 必须完全赋值。** 为了修正这个问题，需要在构造器中为 m_y 赋一个值(通常是 0)。下面是对值类型的全部字段进行赋值的一个替代方案：

```csharp
// C#允许为值类型定义有参构造器
public SomeValType(Int32 x) {
    // 看起来很奇怪，但编译没问题，会将所有字段初始化为 0/null
    this = new SomeValType();

    m_x = x;  // 用 x 覆盖 m_x 的 0
    // 注意 m_y 已初始化为 0
}
```

在值类型的构造器中，this 代表值类型本身的一个实例，用 new 创建的值类型的一个实例可以赋给 **this**。在 **new** 的过程中，会将所有字段置为零。而在引用类型的构造器中，**this** 被认为是只读的，所以不能对它进行赋值。

### 8.3 类构造器

除了实例构造器，CLR 还支持类型构造器(type constructor)，也称为静态构造器(static constructor)、类构造器(class constructor)或者类型初始化器(type initializer)。类型构造器可应用于接口(虽然 C#编译器不允许)、引用类型和值类型。实例构造器的作用是设置类型的实例的初始状态。对应地，类型构造器的作用是设置类型的初始状态。类型默认没有定义类型构造器。如果定义，也只能定义一个。此外，类型构造器永远没有参数。以下代码演示了如何在 C#中为引用类型和值类型定义一个类型构造器：

```csharp
internal sealed class SomeRefType {
    static SomeRefType() {
        // SomeRefType 被首次访问时，执行这里的代码
    }
}

internal struct SomeValType {
    // C#允许值类型定义无参的类型构造器
    static SomeValType() {
        // SomeValType 被首次访问时，执行这里的代码
    }
}
```

可以看出，定义类型构造器类似于定义无参实例构造器，区别在于必须标记为 **static**。此外，类型构造器总是私有；C#自动把它们标记为 **private**。事实上，如果在源代码中显式将类型构造器标记为 **private**(或其他访问修饰符)，C#编译器会显示以下消息：**error CS0515：静态构造函数中不允许出现访问修饰符**。之所以必须私有，是为了防止任何由开发人员写的代码调用它，对它的调用总是由 CLR 负责。

> 注：PowerShell 类同样支持静态（类型）构造器，写法是 `static <ClassName>() { ... }`，引擎会在类首次被访问时执行一次。PowerShell 没有 JIT 编译步骤，但静态字段初始化时机与本节描述一致；「类型构造器只能初始化静态字段」这一约束同样适用。

类型构造器的调用比较麻烦。JIT 编译器在编译一个方法时，会查看代码中都引用了哪些类型。任何一个类型定义了类型构造器，JIT 编译器都会检查针对当前 AppDomain，是否已经执行了这个类型构造器。如果构造器从未执行，JIT 编译器会在它生成的本机(native)代码中添加对类型构造器的调用。如果类型构造器已经执行，JIT 编译器就不添加对它的调用，因为它知道类型已经初始化好了。

现在，当方法被 JIT 编译完毕之后，线程开始执行它，最终会执行到调用类型构造器的代码。事实上，多个线程可能同时执行相同的方法。CLR 希望确保在每个 AppDomain 中，一个类型构造器只执行一次。为了保证这一点，在调用类型构造器时，调用线程要获取一个互斥线程同步锁。这样一来，如果多个线程试图同时调用某个类型的静态构造器，只有一个线程才可以获得锁，其他线程会被阻塞(blocked)。第一个线程会执行静态构造器中的代码。当第一个线程离开构造器后，正在等待的线程将被唤醒，然后发现构造器的代码已被执行过。因此，这些线程不会再次执行代码，将直接从构造器方法返回。除此之外，如果再次调用这样的一个方法，CLR 知道类型构造器已被执行过，从而确保构造器不被再次调用。

![](img/6fa065e17c4549db7260fbfaf4fd384e_184_0.png)

**重要提示** 虽然能在值类型中定义类型构造器，但永远都不要真的那么做，因为 CLR 有时不会调用值类型的静态类型构造器。下面是一个例子：

```csharp
internal struct SomeValType {
    static SomeValType() {
        Console.WriteLine("这句话永远不会显示");
    }
    public Int32 m_x;
}

public sealed class Program {
    public static void Main() {
        SomeValType[] a = new SomeValType[10];
        a[0].m_x = 123;
        Console.WriteLine(a[0].m_x); // 显示 123
    }
}
```

![](img/6fa065e17c4549db7260fbfaf4fd384e_184_1.png)

> **注意** 由于 CLR 保证一个类型构造器在每个 AppDomain 中只执行一次，而且(这种执行)是线程安全的，所以非常适合在类型构造器中初始化类型需要的任何单实例(Singleton)对象。

单个线程中的两个类型构造器包含相互引用的代码可能出问题。例如，假定 ClassA 的类型构造器包含了引用 ClassB 的代码，ClassB 的类型构造器包含了引用 ClassA 的代码。在这种情况下，CLR 仍然保证每个类型构造器的代码只被执行一次；但是，完全有可能在 ClassA 的类型构造器还没有执行完毕的前提下，就开始执行 ClassB 的类型构造器。因此，应尽量避免写会造成这种情况的代码。事实上，由于是 CLR 负责类型构造器的调用，所以任何代码都不应要求以特定的顺序调用类型构造器。

最后，如果类型构造器抛出未处理的异常，CLR 会认为类型不可用。试图访问该类型的任何字段或方法都会抛出 System.TypeInitializationException 异常。

类型构造器中的代码只能访问类型的静态字段，并且它的常规用途就是初始化这些字段。和实例字段一样，C# 提供了一个简单的语法来初始化类型的静态字段：

```csharp
internal sealed class SomeType {
    private static Int32 s_x = 5;
}
```

![](img/6fa065e17c4549db7260fbfaf4fd384e_184_2.png)

> **注意** 虽然 C# 不允许值类型为它的实例字段使用内联字段初始化语法，但可以为静态字段使用。换句话说，如果将前面定义的 SomeType 类型从 class 改为 struct，那么代码也能通过编译，而且会像你预期的那样工作。

① 每个 AppDomain 只能有一个实例，这种类型就是单实例类型。——译注

生成上述代码时，编译器自动为 SomeType 生成一个类型构造器，好像源代码本来是这样写的：

```csharp
internal sealed class SomeType {
    private static Int32 s_x;
    static SomeType() { s_x = 5; }
}
```

使用 ILDasm.exe 查看类型构造器的 IL，很容易验证编译器实际生成的东西。类型构造器方法总是叫 .cctor（代表 class constructor）。

在以下代码中，可以看到 .cctor 方法是 private 和 static 的。另外，注意方法中的代码确实将值 5 加载到静态字段 s_x 中。

```il
.method private hidebysig specialname rtspecialname static
        void .cctor() cil managed
{
    // Code size 7 (0x7)
    .maxstack 8
    IL_0000: ldc.i4.5
    IL_0001: stsfld int32 SomeType::s_x
    IL_0006: ret
} // end of method SomeType::.cctor
```

类型构造器不应调用基类型的类型构造器。这种调用之所以没必要，是因为类型不可能有静态字段是从基类型分享或继承的。

> **注意** 有的语言（比如 Java）希望在访问类型时自动调用它的类型构造器，并调用它的所有基类型的类型构造器。此外，类型实现的接口也必须调用接口的类型构造器。CLR 不支持这种行为。但是，使用由 **System.Runtime.CompilerServices.RuntimeHelpers** 提供的 **RunClassConstructor** 方法，编译器和开发人员可以实现这种行为。任何语言想要实现这种行为，可以告诉它的编译器在一个类型的类型构造器中生成代码，为所有基类型都调用这个方法。用 **RunClassConstructor** 方法调用一个类型构造器，CLR 就知道类型构造器之前是否执行过。如果是，CLR 不会再次调用它。

最后，假定有以下代码：

```csharp
internal sealed class SomeType {
    private static Int32 s_x = 5;

    static SomeType() {
        s_x = 10;
    }
}
```

> 注：PowerShell 类中，静态字段声明时的初始化同样由引擎并入类型构造器执行；若类中还显式写了 `static <ClassName>()`，两段代码都会执行，且字段初始化在前。与 C# 一样，最终只存在一个类型构造器。

在这个例子中，C#编译器只生成一个类型构造器方法。它首先将 s_x 初始化为 5，再把它修改成 10。换言之，当 C#编译器为类型构造器生成 IL 代码时，它首先生成的是初始化静态字段所需的代码，然后才会添加你的类型构造器方法中显式包含的代码。

![](img/6fa065e17c4549db7260fbfaf4fd384e_186_0.png)

> **重要提示** 偶尔有开发人员问我，是否可以在卸载类型时执行一些代码。首先要搞清楚的是，类型只有在 AppDomain 卸载时才会卸载。AppDomain 卸载时，用于标识类型的对象（类型对象）将成为“不可达”的对象（不存在对它的引用），垃圾回收器会回收类型对象的内存。这个行为导致许多开发人员认为可以为类型添加一个静态 **Finalize** 方法。当类型卸载时，就自动地调用这个方法。遗憾的是，CLR 并不支持静态 **Finalize** 方法。但也不是完全没有办法，要在 AppDomain 卸载时执行一些代码，可向 **System.AppDomain** 类型的 **DomainUnload** 事件登记一个回调方法。

### 8.4 操作符重载方法

有的语言允许类型定义操作符应该如何操作类型的实例。例如，许多类型（比如 **System.String**）都重载了相等（==）和不等（!=）操作符。CLR 对操作符重载一无所知，它甚至不知道什么是操作符。是编程语言定义了每个操作符的含义，以及当这些特殊符号出现时，应该生成什么样的代码。

例如在 C# 中，向基元类型的数字应用 + 符号，编译器生成将两个数加到一起的代码。将 + 符号应用于 **String** 对象，C# 编译器生成将两个字符串连接到一起的代码。测试不等性时，C# 使用 != 符号，而 Microsoft Visual Basic 使用 <>。最后，^ 在 C# 中的含义为异或（XOR），在 Visual Basic 中则为求幂。

虽然 CLR 对操作符一无所知，但它确实规定了语言应该如何公开操作符重载，以便由另一种语言的代码使用。每种编程语言都要自行决定是否支持操作符重载，如果决定支持，还要决定用什么语法来表示和使用它们。至于 CLR，操作符重载只是方法而已。

> 注：PowerShell 不支持操作符重载——`operator` 关键字在 PowerShell 类语法中直接报错。PowerShell 的 `-` 语法（`-eq`、`-ne`、`-lt`、`+` 等）含义由引擎固定，自定义类是引用类型（引用相等性比较语义，但 `-eq` 在 PowerShell 中仍调用 `Equals`）。需要类似功能时，应像 CLS 友好名那样定义 `Add`、`CompareTo` 等方法。

对编程语言的选择决定了你是否获得对操作符重载的支持，以及具体的语法是什么。编译源代码时，编译器会生成一个标识操作符行为的方法。CLR 规范要求操作符重载方法必须是 **public** 和 **static** 方法。另外，C#（以及其他许多语言）要求操作符重载方法至少有一个参数的类型与当前定义这个方法的类型相同。之所以要进行这样的限制，是为了使 C# 编译器能在合理的时间内找到要绑定的操作符方法。

以下 C# 代码展示了在一个类中定义的操作符重载方法：

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) {...}
}
```

编译器为名为 **op_Addition** 的方法生成元数据方法定义项；这个方法定义项还设置了 **specialname** 标志，表明这是一个“特殊”方法。编程语言的编译器（包括 C# 编译器）看到源代码中出现一个 + 操作符时，会检查是否有一个操作数的类型定义了名为 **op_Addition** 的 **specialname** 方法，而且该方法的参数兼容于操作数的类型。如果存在这样的方法，编译器就生成调用它的代码。不存在这样的方法就报告编译错误。

表 8-1 和表 8-2 总结了 C# 允许重载的一元和二元操作符，以及由编译器生成的对应的 CLS(Common Language Specification，公共语言规范)方法名。下一节会解释表的第 3 列。

表 8-1　C#的一元操作符及其相容于 CLS 的方法名

| C#操作符 | 特殊方法名 | 推荐的相容于 CLS 的方法名 |
|---|---|---|
| `+` | `op_UnaryPlus` | `Plus` |
| `-` | `op_UnaryNegation` | `Negate` |
| `!` | `op_LogicalNot` | `Not` |
| `~` | `op_OnesComplement` | `OnesComplement` |
| `++` | `op_Increment` | `Increment` |
| `--` | `op_Decrement` | `Decrement` |
| （无） | `op_True` | `IsTrue { get; }` |
| （无） | `op_False` | `IsFalse { get; }` |

表 8-2　C#的二元操作符及其相容于 CLS 的方法名

| C#操作符 | 特殊方法名 | 推荐的相容于 CLS 的方法名 |
|---|---|---|
| `+` | `op_Addition` | `Add` |
| `-` | `op_Subtraction` | `Subtract` |
| `*` | `op_Multiply` | `Multiply` |
| `/` | `op_Division` | `Divide` |
| `%` | `op_Modulus` | `Mod` |
| `&` | `op_BitwiseAnd` | `BitwiseAnd` |
| \| | `op_BitwiseOr` | `BitwiseOr` |
| `^` | `op_ExclusiveOr` | `Xor` |
| `<<` | `op_LeftShift` | `LeftShift` |
| `>>` | `op_RightShift` | `RightShift` |
| `==` | `op_Equality` | `Equals` |
| `!=` | `op_Inequality` | `Equals` |
| `<` | `op_LessThan` | `Compare` |
| `>` | `op_GreaterThan` | `Compare` |
| `<=` | `op_LessThanOrEqual` | `Compare` |
| `>=` | `op_GreaterThanOrEqual` | `Compare` |



CLR 规范定义了许多额外的可重载的操作符，但 C# 不支持这些额外的操作符。由于是非主流，所以此处不列出它们。如果对完整的列表感兴趣，请访问 CLI 的 ECMA 规范 (www.ecma-international.org/publications/standards/Ecma-335.htm) 并阅读 Partition 1: Concepts and Architecture 的 Section 10.3.1(一元操作符)和 Section 10.3.2(二元操作符)。

**注意** 检查 Framework 类库(FCL)的核心数值类型(Int32，Int64 和 UInt32 等)，会发现它们没有定义任何操作符重载方法。之所以不定义，是因为编译器会(在代码中)专门查找针对这些基元类型执行的操作(运算)，并生成直接操作这些类型的实例的 IL 指令。如果类型要提供方法，而且编译器要生成代码来调用这些方法，方法调用就会产生额外的运行时开销。另外，方法最终都要执行一些 IL 指令来完成你希望的操作。这正是核心 FCL 类型没有定义任何操作符重载方法的原因。对于开发人员，这意味着假如选择的编程语言不支持其中的某个 FCL 类型，便不能对该类型的实例执行任何操作。

#### 操作符和编程语言互操作性

操作符重载是很有用的工具，允许开发人员用简洁的代码表达自己的想法。但并不是所有编程语言都支持操作符重载。使用不支持操作符重载的语言时，语言不知道如何解释 + 操作符(除非类型是该语言的基元类型)，编译器会报错。使用不支持操作符重载的编程语言时，语言应该允许你直接调用希望的 op_* 方法(例如 op_Addition)。

如果语言不支持在类型中定义 + 操作符重载，这个类型仍然可能提供了一个 op_Addition 方法。在这种情况下，可不可以在 C# 中使用 + 操作符来调用这个 op_Addition 方法呢？答案是否定的。C# 编译器检测到操作符 + 时，会查找关联了 specialname 元数据标志的 op_Addition 方法，以确定 op_Addition 方法是要作为操作符重载方法使用。但由于现在这个 op_Addition 方法是由不支持操作符重载的编程语言生成的，所以方法没有关联 specialname 标记。因此，C# 编译器会报告编译错误。当然，用任何编程语言写的代码都可以显式调用碰巧命名为 op_Addition 的方法，但编译器不会将一个 + 号的使用翻译成对这个方法的调用。

**注意** FCL 的 System.Decimal 类型很好地演示了如何重载操作符并根据 Microsoft 的设计规范定义友好方法名。

##### Microsoft 操作符方法的命名规则之我见

操作符重载方法什么时候能调用，什么时候不能调用，这些规则会使人感觉非常迷惑。如果支持操作符重载的编译器不生成 specialname 元数据标记，规则会简单得多，而且开发人员使用提供了操作符重载方法的类型也会更轻松。支持操作符重载的语言都支持操作符符号语法，而且所有语言都支持显式调用各种 op_ 方法。我不理解为什么 Microsoft 非要把它搞得这么复杂。希望 Microsoft 在编译器未来的版本中放宽这些限制。

如果一个类型定义了操作符重载方法，Microsoft 还建议类型定义更友好的公共静态方法，并在这种方法的内部调用操作符重载方法。例如，根据 Microsoft 的设计规范，重载了 op_Addition 方法的类型应定义一个公共的、名字更友好的 Add 方法。表 8-1 和表 8-2 中的第 3 列展示了每个操作符推荐使用的友好名称。因此，前面的示例类型 Complex 应该像下面这样定义：

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
    public static Complex Add(Complex c1, Complex c2) { return(c1+c2); }
}
```

用任何语言写的代码都能调用 Add 这样的友好操作符方法，这一点毋庸置疑。Microsoft 要求类型提供友好方法名的设计规范使局面进一步复杂化。在我看来，这种额外的复杂性完全没必要。而且，除非 JIT 编译器能内联(直接嵌入)友好方法的代码，否则调用它们将导致额外的性能损失。内联代码可使 JIT 编译器优化代码，移除额外的方法调用，并提升运行时性能。

### 8.5 转换操作符方法

有时需要将对象从一种类型转换为另一种类型(例如将 Byte 转换为 Int32)。当源类型和目标类型都是编译器识别的基元类型时，编译器自己就知道如何生成转换对象所需的代码。

> 注：PowerShell 没有 `implicit`/`explicit` 转换操作符重载。类型转换用 `[类型]$x`（失败抛异常）或 `-as` 操作符（失败得 `$null`）；`[Byte]$x`/`[int]$x` 这类转换执行的是 PowerShell 的类型转换规则，对自定义类型无效。自定义类型的转换应遵循本节建议：提供转换构造器和 `ToXxx()` 方法。需要真正的 C# 转换操作符时，用 `Add-Type` 编译。

如果源类型或目标类型不是基元类型，编译器会生成代码，要求 CLR 执行转换(强制转型)。这种情况下，CLR 只是检查源对象的类型和目标类型(或者从目标类型派生的其他类型)是不是相同。但有时需要将对象从一种类型转换成全然不同的其他类型。例如，System.Xml.Linq.XElement 类允许将 XML 元素转换成 Boolean, (U)Int32, (U)Int64, Single, Double, Decimal, String, DateTime, DateTimeOffset, TimeSpan, Guid 或者所有这些类型(String 除外)的可空版本。另外，假设 FCL 包含了一个 Rational(有理数)类型，那么如果能将 Int32 或 Single 转换成 Rational 会显得很方便；反之亦然。

为了进行这样的转换，Rational 类型应该定义只有一个参数的公共构造器，该参数要求是源类型的实例。还应该定义无参的公共实例方法 ToXxx(类似于你熟悉的 ToString 方法)，每个方法都将定义类型①的实例转换成 **Xxx** 类型。以下代码展示了如何为 Rational 类型正确定义转换构造器和方法。

```csharp
public sealed class Rational {
   // 由一个 Int32 构造一个 Rational
   public Rational(Int32 num){ ... }

   // 由一个 Single 构造一个 Rational
   public Rational(Single num){ ... }

   // 将一个 Rational 转换成一个 Int32
   public Int32 ToInt32(){ ... }

   // 将一个 Rational 转换成一个 Single
   public Single ToSingle(){ ... }
}
```

调用这些构造器和方法，使用任何编程语言的开发人员都能将 Int32 或 Single 对象转换成 Rational 对象，反之亦然。这些转换能给编程带来很多方便。设计类型时，应认真考虑类型需要支持的转换构造器和方法。

上一节讨论了某些编程语言如何提供操作符重载。事实上，有些编程语言(比如 C#)还提供了转换操作符重载。**转换操作符**是将对象从一种类型转换成另一种类型的方法。可以使用特殊的语法来定义转换操作符方法。CLR 规范要求转换操作符重载方法必须是 **public** 和 **static** 方法。此外，C#(以及其他许多语言)要求参数类型和返回类型二者必有其一与定义转换方法的类型相同。之所以要进行这个限制，是为了使 C# 编译器能在一个合理的时间内找到要绑定的操作符方法。以下代码为 Rational 类型添加了 4 个转换操作符方法：

```csharp
public sealed class Rational {
   // 由一个 Int32 构造一个 Rational
   public Rational(Int32 num){ ... }

   // 由一个 Single 构造一个 Rational
   public Rational(Single num){ ... }

   // 将一个 Rational 转换成一个 Int32
   public Int32 ToInt32(){ ... }

   // 将一个 Rational 转换成一个 Single
   public Single ToSingle(){ ... }

   // 由一个 Int32 隐式构造并返回一个 Rational
   public static implicit operator Rational(Int32 num) {
      return new Rational(num);
   }

   // 由一个 Single 隐式构造并返回一个 Rational
   public static implicit operator Rational(Single num) {
      return new Rational(num);
   }
}
```

① 定义该方法的类型。——译注

```csharp
}
}
```

定义好这个方法后，可以在代码中使用它，如下所示：

```csharp
StringBuilder sb=new StringBuilder("Hello. My name is Jeff."); //初始字符串

// 将句点更改为感叹号，获取!字符的索引(5)
Int32 index = StringBuilderExtensions.IndexOf(sb.Replace('.', '!'), '!');
```

上述代码工作起来没问题，但从程序员的角度看不理想。第一个问题是，要获取一个 StringBuilder 中的某个字符的索引，必须先知道 StringBuilderExtensions 类的存在。第二个问题是，代码没有反映出在 StringBuilder 对象上执行的操作的顺序，使代码很难写、读和维护。程序员希望先调用 Replace，再调用 IndexOf。但从左向右读最后一行代码，先看到的是 IndexOf，然后才看到 Replace。当然，可以像下面这样重写，使代码的行为看起来更容易理解：

```csharp
// 首先，将句点更改成感叹号
sb.Replace('.', '!');

// 接着，获取!字符的索引(5)
Int32 index = StringBuilderExtensions.IndexOf(sb, '!');
```

但这两个版本都存在另一个不容忽视的问题，它影响了我们对代码行为的理解。使用 StringBuilderExtensions 显得“小题大做”，造成程序员无法专注于当前要执行的操作：IndexOf。如果 StringBuilder 类定义了自己的 IndexOf 方法，上述代码就可以重写为：

```csharp
// 把句点更改为感叹号，获取!字符的索引(5)
Int32 index = sb.Replace('.', '!').IndexOf('!');
```

哇，是不是立刻就显得高端大气上档次了？一眼就能看出在 StringBuilder 对象中，是先将句点更改为感叹号，再获取感叹号的索引。

有了这个例子作为铺垫，就很容易理解 C# 扩展方法的意义了。它允许定义一个静态方法，并用实例方法的语法来调用。换言之，现在既能定义自己的 IndexOf 方法，又能避免上述三个问题。要将 IndexOf 方法转变成扩展方法，只需在第一个参数前添加 this 关键字：

> 注：PowerShell 没有 C# 的扩展方法 `this` 语法。等价的惯用法是 `Add-Member -MemberType ScriptMethod`（仅当前对象实例）、`Update-TypeData`（该类型当前会话的所有实例），或封装 `System.Management.Automation.TypeAccelerators` 把参数写为第一个参数的普通函数。扩展能力都是会话级的，不会写入类型元数据。

```csharp
public static class StringBuilderExtensions {
    public static Int32 IndexOf(this StringBuilder sb, Char value) {
        for (Int32 index = 0; index < sb.Length; index++)
            if (sb[index] == value) return index;
        return -1;
    }
}
```

现在，当编译器看到以下代码：

```csharp
Int32 index = sb.IndexOf('X');
```

就首先检查 StringBuilder 类或者它的任何基类是否提供了获取单个 Char 参数、名为 IndexOf 的一个实例方法。如果是，就生成 IL 代码来调用它。如果没有找到匹配的实例方法，就继续检查是否有任何静态类定义了名为 IndexOf 的静态方法，方法的第一个参数的类型和当前用于调用方法的那个表达式的类型匹配，而且该类型必须用 this 关键字标识。在本例中，表达式是 sb，类型是 StringBuilder。所以编译器会查找一个 IndexOf 方法，它有两个参数：一个 StringBuilder(用 this 关键字标记)，以及一个 Char。编译器找到了这个 IndexOf 方法，所以生成相应的 IL 代码来调用这个静态方法。

OK——这解释了编译器如何解决前面提到的、会影响代码理解的最后两个问题。但是，还没有说第一个问题是如何解决的：程序员怎么知道有这样的一个 IndexOf 方法，可以用它操作 StringBuilder 对象呢？这个问题是通过 Microsoft Visual Studio 的“智能感知”功能来解决的。在编辑器中输入句点符号，会弹出 Visual Studio 的“智能感知”窗口，列出当前可用的实例方法。现在，这个窗口还会列出可作用于句点左侧表达式类型的扩展方法。图 8-1 展示了 Visual Studio 的“智能感知”窗口；扩展方法的图标中有一个下箭头，方法旁边的“工具提示”表明该方法实际是一个扩展方法。这是相当实用的一个功能，因为现在可以轻松定义自己的方法来操作各种类型，其他程序员在使用这些类型的对象时，也能轻松地发现你的方法。

![](img/6fa065e17c4549db7260fbfaf4fd384e_194_0.png)

图 8-1 Visual Studio 的“智能感知”窗口能列出扩展方法

#### 8.6.1 规则和原则

关于扩展方法，有一些附加的规则和原则需要注意。

- C# 只支持扩展方法，不支持扩展属性、扩展事件、扩展操作符等。
- 扩展方法(第一个参数前面有 this 的方法)必须在非泛型的静态类中声明。然而，类名没有限制，可以随便叫什么名字。当然，扩展方法至少要有一个参数，而且只有第一个参数能用 this 关键字标记。

```csharp
// 并向它传递对字符串 "Jeff" 的引用
a();
}
```

在上述代码中，C# 编译器生成 IL 代码来构造一个 Action 委托。创建委托时，会向构造器传递应调用的方法，同时传递一个对象引用，这个引用应传给方法的隐藏 this 参数。正常情况下，创建引用静态方法的委托时，对象引用是 null，因为静态方法没有 this 参数。但在这个例子中，C# 编译器生成特殊代码创建一个委托来引用静态方法（ShowItems），而静态方法的目标对象是对 "Jeff" 字符串的引用。稍后，当这个委托被调用（invoke）时，CLR 会调用（call）静态方法，并向其传递对 "Jeff" 字符串的引用。这是编译器耍的小“花招”，但效果不错，而且只要你不去想内部发生的事情，整个过程还是感觉非常自然的。

#### 8.6.3 ExtensionAttribute 类

扩展方法的概念要不是 C# 特有的就好了！具体地说，我们希望程序员能用一种编程语言定义一组扩展方法，并让其他语言的程序员利用它们。要实现这一点，选择的编译器必须能够搜索静态类型和方法来寻找匹配的扩展方法。另外，速度慢了还不行。编译器必须快速完成上述搜索，将编译时间控制在合理范围内。

在 C# 中，一旦用 this 关键字标记了某个静态方法的第一个参数，编译器就会在内部向该方法应用一个定制特性。该特性会在最终生成的文件的元数据中持久性地存储下来。该特性在 System.Core.dll 程序集中定义，它看起来像下面这样：

```csharp
// 在 System.Runtime.CompilerServices 命名空间中定义
[AttributeUsage(AttributeTargets.Method | AttributeTargets.Class |
               AttributeTargets.Assembly)]
public sealed class ExtensionAttribute : Attribute {
}
```

> 注：`ExtensionAttribute` 是 C# 编译器写入元数据的标记，PowerShell 脚本没有 `this` 扩展方法语法，也不会生成该特性。脚本层的扩展能力见 8.6 节关于 `Add-Member`、`Update-TypeData` 的说明。

除此之外，任何静态类只要包含至少一个扩展方法，它的元数据中也会应用这个特性。类似地，任何程序集只要包含了至少一个符合上述特点的静态类，它的元数据中也会应用这个特性。这样一来，如果代码调用了一个不存在的实例方法，编译器就能快速扫描引用的所有程序集，判断它们哪些包含了扩展方法。然后，在这些程序集中，可以只扫描包含了扩展方法的静态类。在每个这样的静态类中，可以只扫描扩展方法来查找匹配。利用这个技术，代码能以最快速度编译完毕。

### 8.7 分部方法

假定用某个工具生成了包含类型定义的 C# 源代码文件，工具知道你想在代码的某些位置定制类型的行为。正常情况下，是让工具生成的代码调用虚方法来进行定制。工具生成的代码还必须包含虚方法的定义。另外，这些方法的实现是什么事情都不做，直接返回了事。现在，如果想定制类的行为，就必须从基类派生并定义自己的类，重写虚方法来实现自己想要的行为。下面是一个例子：

> 注：PowerShell 没有 `partial` 关键字，也不支持分部方法。定制“生成的类”的常见替代方案是：在类方法中把留空点做成内部可调用的脚本块/委托，或在模块层提供可在导入后覆盖的函数（函数可被再次定义覆盖）。8.7 的剩余例子依赖 C# 编译器的分部类型缝合，PowerShell 无法复现。

```csharp
// 工具生成的代码，存储在某个源代码文件中:
internal class Base {
    private String m_name;

    // 在更改 m_name 字段前调用
    protected virtual void OnNameChanging(String value) {
    }

    public String Name {
        get { return m_name; }
        set {
            OnNameChanging(value.ToUpper());  // 告诉类要进行更改了
            m_name = value;                   // 更改字段
        }
    }
}

// 开发人员生成的代码，存储在另一个源代码文件中:
internal class Derived : Base {
    protected override void OnNameChanging(string value) {
        if (String.IsNullOrEmpty(value))
            throw new ArgumentNullException("value");
    }
}
```

遗憾的是，上述代码存在两个问题。

- 类型必须是非密封的类。这个技术不能用于密封类，也不能用于值类型(值类型隐式密封)。此外，这个技术不能用于静态方法，因为静态方法不能重写。
- 效率问题。定义一个类型只是为了重写一个方法，这会浪费少量系统资源。另外，即使不想重写 OnNameChanging 的行为，基类代码仍需调用一个什么都不做、直接返回的虚方法。另外，无论 OnNameChanging 是否访问传给它的实参，编译器都会生成对 ToUpper 进行调用的 IL 代码。

利用 C# 的分部方法功能，可以在解决上述问题的同时覆盖类的行为。以下代码使用分部方法实现和上述代码完全一样的语义：

```csharp
// 工具生成的代码，存储在某个源代码文件中:
internal sealed partial class Base {
    private String m_name;

    // 这是分部方法的声明
    partial void OnNameChanging(String value);

    public String Name {
        get { return m_name; }
        set {
            OnNameChanging(value.ToUpper());  // 通知类要进行更改了
            m_name = value;                   // 更改字段
        }
    }
}
```

```csharp
// 开发人员生成的代码，存储在另一个源代码文件中:
internal sealed partial class Base {

    // 这是分部方法的实现，会在 m_name 更改前调用
```

![](img/6fa065e17c4549db7260fbfaf4fd384e_200_0.png)

> **注意**　分部方法的工作方式类似于 `System.Diagnostics.ConditionalAttribute` 特性。然而，分部方法只能在单个类型中使用，而 `ConditionalAttribute` 能用于对另一个类型中定义的方法进行有选择的调用。

#### 规则和原则

关于分部方法，有一些附加的规则和原则需要注意。

- 它们只能在分部类或结构中声明。
- 分部方法的返回类型始终是 `void`，任何参数都不能用 `out` 修饰符来标记。之所以有这两个限制，是因为方法在运行时可能不存在，所以不能将变量初始化为方法也许会返回的东西。类似地，不允许 `out` 参数是因为方法必须初始化它，而方法可能不存在。分部方法可以有 `ref` 参数，可以是泛型方法，可以是实例或静态方法，而且可标记为 `unsafe`。
- 当然，分部方法的声明和实现必须具有完全一致的签名。如果两者都应用了定制特性，编译器会合并两个方法的特性。应用于参数的任何特性也会合并。
- 如果没有对应的实现部分，便不能在代码中创建一个委托来引用这个分部方法。这同样是由于方法在运行时不存在。编译器报告以下消息：`error CS0762: 无法通过方法 "Base.OnNameChanging(string)" 创建委托，因为该方法是没有实现声明的分部方法。`
- 分部方法总是被视为 `private` 方法，但 C# 编译器禁止在分部方法声明之前添加 `private` 关键字。
