方法的生存期中自始至终地存活。这会对应用程序产生有趣的影响。例如以下代码：

```
```csharp
using System;
using System.Threading;

public static class Program {
    public static void Main() {
        // 创建每 2000 毫秒就调用一次 TimerCallback 方法的 Timer 对象
        Timer t = new Timer(TimerCallback, null, 0, 2000);

        // 等待用户按 Enter 键
        Console.ReadLine();
    }

    private static void TimerCallback(Object o) {
        // 当调用该方法时，显示日期和时间
        Console.WriteLine("In TimerCallback: " + DateTime.Now);

        // 出于演示目的，强制执行一次垃圾回收
        GC.Collect();
    }
}
```
```

在命令行上，不用任何特殊编译器开关编译代码。运行可执行文件，会发现 TimerCallback 方法只被调用了一次！

观察代码，可能以为 TimerCallback 方法每隔 2000 毫秒调用一次。毕竟，代码创建了一个 Timer 对象，而且有一个变量 t 引用该对象。只要计时器对象存在，计时器就应该一直触发。但要注意，TimerCallback 方法调用 GC.Collect() 强制执行了一次垃圾回收。

回收开始时，垃圾回收器首先假定堆中的所有对象都是不可达的(垃圾)；这自然也包括 Timer 对象。然后，垃圾回收器检查应用程序的根，发现在初始化之后，Main 方法再也没有用过变量 t。既然应用程序没有任何变量引用 Timer 对象，垃圾回收自然会回收分配给它的内存；这使计时器停止触发，并解释了为什么 TimerCallback 方法只被调用了一次。

现在，假定用调试器单步调试 Main，而且在将新 Timer 对象的地址赋给 t 之后，立即发生了一次垃圾回收。然后，用调试器的“监视”窗口查看 t 引用的对象，会发生什么事情呢？因为对象已被回收，所以调试器无法显示该对象。大多数开发人员都没有料到这个结果，认为不合常理。所以，Microsoft 提出了一个解决方案。

使用 C# 编译器的 /debug 开关编译程序集时，编译器会应用 System.Diagnostics.DebuggableAttribute，并为结果程序集设置 DebuggingModes 的 DisableOptimizations 标志。运行时编译方法时，JIT 编译器看到这个标志，会将所有根的生存期延长至方法结束。在我的例子中，JIT 编译器认为 Main 的 t 变量必须存活至方法结束。所以在垃圾回收时，GC 认为 t 仍然是一个根，t 引用的 Timer 对象仍然“可达”。Timer 对象会在回收中存活，TimerCallback 方法会被反复调用，直至 Console.ReadLine 方法返回而且 Main 方法退出。

这很容易验证，只需在命令行中重新编译程序，但这一次指定 C# 编译器的 /debug 开关。运行可执行文件，会看到 TimerCallback 方法被反复调用。注意，C# 编译器的 /optimize+ 编译器开关会将 DisableOptimizations 禁止的优化重新恢复，所以实验时不要指定该开关。

JIT 编译器这样做的目的是帮助进行 JIT 调试。现在可以用正常方式启动应用程序(不用调