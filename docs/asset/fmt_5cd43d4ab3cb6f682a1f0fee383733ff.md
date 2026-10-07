
由于 `strncasecmp` 定义为将两个输入字符串都转换为小写，这等同于调用 `strings`。另一个选项将是不使用函数指针以便。

## 总结

本章介绍了从通过 Instruments 剖析器从命令行工具进行性能测量，到内部测量和性能测试。虽然掌握这些工具是重要的并可以为你改进代码提供良好的开端，但重要的是始终记住不要被工具所蒙蔽。它们帮助你收集的数据只是支持或反驳你所假设的手段，而不是终点。如果你记住这一点，并对需要优化的地方进行优化，你已经领先了大多数竞争对手。

# CPU：陷阱与技术

在查看了驱动性能的参数和识别慢代码的技术之后，让我们现在转向让代码运行更快速的技术。我们将查看高效的对象表示以及这些对象通信和访问数据的方法。我们将优化计算。在这一切中，目标将有效地结合 Objective-C 的“Objective”和“C”部分，以实现性能与封装之间所需的平衡。

## 表示

程序的主要任务之一（特别是面向对象的程序）是表示数据。由于该语言的混合性质，Objective-C 程序员在此任务上有许多可用方案。在不声称完整的情况下，结构化数据可以使用 C 结构体、Objective-C 对象以及各种形式的键值存储（最著名的是）来表示。

Foundation 的 `NSDictionary` 和 CoreFoundation 的 `CFDictionary` 都在变得越来越常用。简单的标量可以表示为 C `float`、`double` 或 `int` 及其多种变体，Foundation 的 `NSInteger` 和 CoreGraphics 的 `CGFloat` 定义，以及 CoreFoundation 的 `CFNumber` 对象。注意，命名规范有些令人困惑：`NSInteger` 和 `NSNumber` 的名称强烈暗示这两个类型是相关的——例如 `NSInteger` 是 `NSNumber` 的一个特定子类——但它们完全没有关系。`NSInteger` 是一个定义，在 32 位架构上解析为 32 位的 `int`，在 64 位架构上解析为 64 位的 `long`，而 `int` 在两种情况下都是 32 位的。`CGFloat` 也是如此，它在 32 位架构上变为 32 位的 `float`，在 64 位架构上变为 64 位的 `double`。示例 3.1 显示了几种可能的数字表示形式。

### 示例 3.1 作为原始类型和对象的数字

```c
#import <Foundation/Foundation.h>

int main() {

    int a=1;

    float b=2.0;

    NSNumber *c=[NSNumber numberWithInt:3];

    CFNumberRef d=CFNumberCreate(kCFAllocatorDefault, kCFFloatType, (const void*)&b);

    NSNumber *e=@(5);

    NSLog("%a=%%d b=%%f c=%@ d=%@f e=%@",a,b,c,d,e);

    return 0;

}
```

为了获得良好的解决方案，程序员必须在解耦与封装与性能之间进行权衡，理想情况是在不损害性能的情况下获得尽可能的解耦和封装，或者反之，在最小化耦合的同时最大化性能。

## 原始类型 (Primitive Types)

可能是最容易做的决定是在字符/字节、整数和浮点数等简单标量类型的表示上：尽可能使用内置的 C 原始类型，尽可能避免使用对象。

由于语言原生支持这些类型，标量使用起来非常方便，且性能比其对应的 Foundation 对象 `NSNumber` 或其 CoreFoundation 等效对象 `CFNumber` 高出 10 到 100 倍以上。表 3.1 给出了详细信息：前三列是标量类型进行不同算术操作的时间。32 位和 64 位加法及乘法的时间差异可能是测量误差，尽管在准备这些测量结果时它们是稳定的，但重要的是报告测得的实际结果，而不是我们认为结果应该是怎样的。

### 表 3.1 32 位和 64 位架构下的原始操作

| 操作 | add | multiply | divide | -intVal | NS(int) | CF(float) | NS(float) |
|---|---|---|---|---|---|---|---|
| 64-bit (ns) | 0.67 | 0.79 | 14 | 15 | 44 | 169 | 190 |
| 32-bit (ns) | 0.72 | 0.76 | 7.8 | 22 | 232 | 182 | 211 |

除法比其他算术操作慢，是因为 CPU 中的除数处理器通常一次只处理几位，而不是整个字长，这解释了为什么 64 位除法明显比 32 位除法慢。

与其他通常可以存储在寄存器并在单个周期内进行操作（或在不那么理想的设计中）的类型相比，任何对象表示都有过度的开销，而 Objective-C 相当沉重的对象更是如此。Foundation 和 Core 通过仅提供不可变对象使得这种开销变得更糟糕，这意味着任何操作都必须创建新对象。最后，像数字和字符这样的标量位于任何对象图的末端，因此是程序中数量最多的实体，每个对象都包含一个或多个此类实例。

相反，很少有变体或私有数据能从对象表示提供的封装和多态中获益，而且数字对象在许多方面不如原始类型强大，例如，它们不提供算术能力。如果 Foundation 或任何其他框架提供一种类似于 Smalltalk 或 LISP 的数字和数量级层次结构（其中小整数根据需要自动转变为精度整数、浮点数甚至复数），这可能会改变未来。Foundation 目前尚未提供这些能力，但 OS X 10.7 在 64 位运行时中引入的标记整数（tagged integers）以及在 10.8 中添加数字字面量，可能是未来改进的信号。

当然，在某些其他接口需要对象时，例如当向 `NSArray` 或 `NSDictionary` 添加内容时。在这种情况下，你必须使用 `NSNumber` 或等效方案来提供这些接口——我们将在本书中更多地探讨选项。

表 3.1 的一个异常在于，虽然 32 位和 64 位之间大部分时间相似，但有两个数字不同。除法结果在 64 位上一样慢，而 `NSNumber` 对象的创建速度快了六倍。除法很容易解释：所用特定 CPU 整数除法硬件每个周期处理固定的位数，而 64 位操作数的位数正好是两倍。另一方面，乘法和加法电路一次性处理整个 64 位字。

## 第 3 章 CPU：陷阱与技巧

### 表 3.2 标记指针与普通指针

| Bits | 8-32/64 | 4-7 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|
| Regular pointer | | | | | | 0 |
| Tagged pointer | | | | | | 1 |

# 第3章 CPU：陷阱与技巧

### 表 3.3 NSString 与 C-String 的操作

| 操作 | 1 ns | !strcmp(10) | ns2 | !nscmp(10) | append | nscmp(32) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 ns | | 3.3 | 10 | 76 | 77 | 82 |
| !strcmp(10) | | 1 | 3 | 23 | | 25 |
| strcmp(32) | | | 1 | 7.5 | 7.6 | 8.2 |
| !nscmp(10) | | | | 1 | | 1.1 |
| append | | | | | 1 | 1.1 |
| nscmp(32) | | | | | | 1 |

虽然 `NSString` 的开销很大，但当主题确实是人类可读的内容时，这种开销是值得的。实现正确的 Unicode 处理是复杂的、易错且本质上昂贵的。此外，拥有具有通用接口的多种表示形式是有价值的，这允许不同使用场景的字符串表示互换使用。例如，字面量 `NSString` 由 `NSConstantString` 类表示，该类存储 8 位字符；而标准的 `NSCFString` 类（由 `CFStringFoundation` 对象支持）的子类也可以交替提供更复杂的实现，如绳（rope），它们将字符串存储为较小字符串的二进制序列，并在大字符串中高效地插入/删除。

从 OS X 10.1 开始，64 位运行时上的字符串对象也获得了我们之前在整数中看到的标记指针（tagged pointer）。这看起来可能很奇怪，因为字符串是变长度的数据结构，即字符数组。然而，64 位是一个非常大的位数，足以存储 7-8 位字符以及一些额外的标识（如长度）。事实上，当我在 2007 年提出指针字符串时，我曾有过 7 位 ASCII 字符串的变体，或者更紧凑的打包方式，将大多数控制字符和特殊字符聚集仅使用 6 位，并为 9 个字符留出空间。我不知道这些变体是否已经已实现。

示例 3.3 展示了不同的 `NSString` 实现：字面量是 `NSConstantString` 的实例，它是 `NSConstantString` 的一个 CF 变体。创建一个可变副本会创建一个新字符串，而对该副本创建一个拷贝会创建一个标记字符串，因为该字符串只有 5 个字符长。所有这些都取决于实现，但在查看 `NSDictionary` 性能时，这些差异是有意义的。

### 示例 3.3 显示了普通、常量和标记字符串之间的差异

```objc
#import <Foundation/Foundation.h>

void printString(NSString *a ) {
```

# 表示 47

```objc
NSLog("string=%@ p class: %@", a, [a class]);
}
```

```objc
int main() {
    NSString *cs="Const";
    printString(cs);
    printString([cs mutableCopy]);
    printString([[cs mutableCopy] copy]);
    return 0;
}
cc -Wall -o taggedstring taggedstring.string -framework Foundation
./taggedstring
string* Const=0x108fe2040 class: __NSConstantString
string* Const=0x7fb359c0630 class: __NSConstantString
string* Const=0x74736ef435 class: __NSTaggedPointerString
```

```json
[
  {"name": "AAPL", "price": 650.1, "change": 20.41 },
  {"name": "MSFT", "price": 62.79, "change": -0.9 },
  {"name": "GOOG", "price": 340.79, "change": -5.2 }
]
```

即使此类文件中的字符串倾向于结构化而非实际内容（例如示例 3.4 中的字典键），这类结构化字符串在 Cocoa 中也表示为 `NSString` 对象，就像人类可读的文本一样。

# 第3章 CPU：陷阱与技巧

虽然由于字面量 `NSString` 语法（`@"This is a constant string"`）非常方便，但这种将人类可读文本与功能性字符串混用的做法在性能有时是不利的。幸运的是，许多类型的键有更优化的存在——例如，基础 C 字符串、消息名称和实例变量名。

## 对象

由于你正在使用 Objective-C 编程，对象可能会成为你的主要数据结构化机制。

在对象内部使用 C。消息接口隐藏了表示形式，用户对此一无所知。尽量避免使用细粒度、无语义的对象来实现粗粒度、带有语义的对象。

## 访问器（Accessors）

访问器是仅用于读取或写入对象内部数据的方法，大致对应于内存读写指令。根据良好的面向对象风格，对象的属性不应被直接访问，尤其不能从对象外部访问，最好从内部访问。Objective-C 2.0 属性处理了访问器的负担。

然而，访问器也应该被降至最低，理想情况下应完全消除，因为它们变成了智能代理，响应对数据承载结构的高级服务请求，从而导致更高的访问成本。除了更清晰的设计外，从性能角度来看，将高级请求传递到对象中也是意义的，因为这意味着消息的事务成本仅支付一次，在那个点上，相关方法可以访问消息的所有参数和对象的实例变量，而无需使用多次消息来收集某条数据。

### 示例 3.5 访问器 (int)new

```objc
-(void)setInteger:(int)newInteger {
    _integer = newInteger;
}
-(void) setObject:(id)newObject {
    _object = newObject;
}
```

对象 51

仅仅掩盖了错误的代码。程序崩溃会提醒程序员逻辑存在问题。第二种情况是程序员实际上想要存下旧值。在这种情况下，代码本身也是明显的 Bug，因为程序员很清楚新值将使旧值失效——他们正在将其存起来！示例 3.8 中修正后的代码不仅不需要 `atomic`，而且让代码的意图变得清晰。

## 示例 3.8 非保留（Non-retain）的指针引用

```objc
...
id oldWindowTitle=[[window title] retain autorelease];
[window setTitle:@New Window title
```

注意，ARC 防止了崩溃，并且也隐藏了指针的过时性，这正是 `atomic` 所做的——通过在即使将对象存储到局部变量中时也激进地对其进行保留（retain）。优点是你不需要过多考虑对象的生命周期。缺点是，你不再需要过多考虑对象的生命周期，而且你会获得显著更多的引用计数流量，这会影响性能。

因此，虽然在没有性能开销的情况下，`atomic` 是否有益尚不清楚，但这种常见操作的显著减速使其即使在乐观的情况下也非常值得怀疑。集合不支持这种模式（出于性能考虑）以及 iOS UIKit 显式地将其超过 99% 的属性声明设置为 `nonatomic`，这表明 Apple 自身在这种情况下并没有忽视这一点。更慢的 `atomic` 访问是通过键值编码（KVC）实现的：调用诸如 `[tester forKey:@"attribute"]` 的方法不仅比等效直接发送消息 `[tester attribute]` 更冗长，而且由于编译器无法检查 `valueForKey` 字符串的有效性更容易出错；它还慢 20 倍。在运行时对要获取的值进行参数化，使用 `[tester performSelector:@selector(attribute)]` 只比消息发送慢一倍，比 `valueForKey` 快十倍。

你可能根据这些性能参数预计，构建在 KVC 之上的技术（如键值观察 KVO 和 Cocoa 绑定 Cocoa Bindings）不会是速度很快的，你是对的：添加单个 KVO 观察者会使基础 setter 时间增加 100 倍（100 ns 对比 6 ns），添加单个绑定会增加 150 倍（900 ns）。

KVO 和绑定无法防止级联更新通知，如果存在传递依赖（b 依赖 a 且 c 同时依赖于 a 和 b，将导致 c 被评估两次，并导致平方级的性能下降；如果存在依赖循环，则会导致无限递归和崩溃）。

## 第 3 章 CPU：陷阱与技巧

对于较大的数据集或复杂的依赖关系，使用适当的约束求解器可能是个主意，遵循 1978 年 Xerox PARC ThingLab 或后来的开发，如 DeltaBlue、Amulet 或 Cassowary。事实上，Cassowary 似乎已被 Apple 采用 Mountain Lion 的自动布局机制。

## 公共访问（Public Access）

当通过发送消息访问实例变量很慢时，这些实例变量可以为 `@public`。在这种情况下，访问时间本质上与结构体（struct）相同（非询问式实例变量意味着在类中查找偏移量，而不是在编译时硬编码，这会略微影响结果），但安全性和封装也是如此；两者都不复存在了。因此可以认为，如果需要 `@public` 访问，应该使用结构体。事实上，结构体具有一些优点，主要是它可以被分配在自动变量的栈上，通过值传递给函数，或者直接嵌入另一个对象或结构体中，而 Objective-C 对象必须昂贵地在堆上分配，并且只能通过指针访问。

然而，保持这种开放的 Objective-C 对象也有优点——即，它可以附加额外的功能，可以按字段授予或拒绝访问权限，并且它可能与不感知公共访问实例变量的其他对象兼容。例如，第 1 章提到的 PostScript 解释器使用了示例 3.9 中共享的字符串，但对于对象来说，释放内存是有问题的。

## 示例 3.9 完整的字符串定义

```objc
@interface MPWString : NSObject
{
@public
    unsigned char *bytes;
    unsigned length,capacity;
}
```
