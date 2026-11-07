![](bbox=[0.1098, 0.0858, 0.1741, 0.1216])

> > **重要提示**　如果关心应用程序的性能，就应清楚编译器何时生成代码执行这些操作。遗憾的是，许多编译器都隐式生成代码来装箱对象，所以有时并不知道自己的代码会造成装箱。如果关心特定算法的性能，可用 ILDasm.exe 这样的工具查看方法的 IL 代码，观察 IL 指令 box 都在哪些地方出现。

再来看几个装箱和拆箱的例子：

```
```csharp
public static void Main() {
    Int32 v = 5;        // 创建未装箱值类型变量
    Object o = v;       // o 引用已装箱的、包含值 5 的 Int32
    v = 123;            // 将未装箱的值修改成 123

    Console.WriteLine(v + ", " + (Int32) o); // 显示"123, 5"
}
```
```

能从上述代码中看出发生了多少次装箱吗？如果说 3 次，会不会觉得意外？让我们仔细分析一下代码，理解具体发生的事情。为了帮助理解，下面列出为这个 **Main** 方法生成的 IL 代码。我为这些代码加上了注释，方便你看清楚发生的每个操作：

```
```il
.method public hidebysig static void Main() cil managed
{
    .entrypoint
    // 代码大小       45 (0x2d)
    .maxstack 3
    .locals init ([0]int32 v,
                  [1] object o)

    // 将 5 加载到 v 中
    IL_0000: ldc.i4.5
    IL_0001: stloc.0

    // 对 o 装箱，将引用指针存储到 o 中
    IL_0002: ldloc.0
    IL_0003: box       [mscorlib]System.Int32
    IL_0008: stloc.1

    // 将 123 加载到 v 中
    IL_0009: ldc.i4.s 123
    IL_000b: stloc.0

    // 对 v 装箱，将指针保留在栈上以进行 Concat（连接）操作
    IL_000c: ldloc.0
    IL_000d: box       [mscorlib]System.Int32

    // 将字符串加载到栈上以执行 Concat 操作
    IL_0012: ldstr ", "

    // 对 o 拆箱：获取一个指针，它指向栈上的 Int32 字段
    IL_0017: ldloc.1
    IL_0018: unbox.any [mscorlib]System.Int32

    // 对 Int32 装箱，将指针保留在栈上以进行 Concat 操作
    IL_001d: box       [mscorlib]System.Int32

    // 调用 Concat
    IL_0022: call string [mscorlib]System.String::Concat(object,
                                                         object,
                                                         object)
```
```