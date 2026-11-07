
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

## 8.3 类构造器

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

在这个例子中，C#编译器只生成一个类型构造器方法。它首先将 s_x 初始化为 5，再把它修改成 10。换言之，当 C#编译器为类型构造器生成 IL 代码时，它首先生成的是初始化静态字段所需的代码，然后才会添加你的类型构造器方法中显式包含的代码。

![](img/6fa065e17c4549db7260fbfaf4fd384e_186_0.png)

> **重要提示** 偶尔有开发人员问我，是否可以在卸载类型时执行一些代码。首先要搞清楚的是，类型只有在 AppDomain 卸载时才会卸载。AppDomain 卸载时，用于标识类型的对象（类型对象）将成为“不可达”的对象（不存在对它的引用），垃圾回收器会回收类型对象的内存。这个行为导致许多开发人员认为可以为类型添加一个静态 **Finalize** 方法。当类型卸载时，就自动地调用这个方法。遗憾的是，CLR 并不支持静态 **Finalize** 方法。但也不是完全没有办法，要在 AppDomain 卸载时执行一些代码，可向 **System.AppDomain** 类型的 **DomainUnload** 事件登记一个回调方法。

## 8.4 操作符重载方法

有的语言允许类型定义操作符应该如何操作类型的实例。例如，许多类型（比如 **System.String**）都重载了相等（==）和不等（!=）操作符。CLR 对操作符重载一无所知，它甚至不知道什么是操作符。是编程语言定义了每个操作符的含义，以及当这些特殊符号出现时，应该生成什么样的代码。

例如在 C# 中，向基元类型的数字应用 + 符号，编译器生成将两个数加到一起的代码。将 + 符号应用于 **String** 对象，C# 编译器生成将两个字符串连接到一起的代码。测试不等性时，C# 使用 != 符号，而 Microsoft Visual Basic 使用 <>。最后，^ 在 C# 中的含义为异或（XOR），在 Visual Basic 中则为求幂。

虽然 CLR 对操作符一无所知，但它确实规定了语言应该如何公开操作符重载，以便由另一种语言的代码使用。每种编程语言都要自行决定是否支持操作符重载，如果决定支持，还要决定用什么语法来表示和使用它们。至于 CLR，操作符重载只是方法而已。

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
