个返回地址在图中未显示，但它应该刚好在栈中的 **name** 实参上方），M1 的栈帧展开（unwind），恢复成图 4-2 的样子。之后，调用 M1 的方法继续执行 M1 调用之后的代码，那个方法的栈帧将准确反映它需要的状态。

现在，让我们围绕 CLR 来调整一下讨论。假定有以下两个类定义：

```
internal class Employee {
    public              Int32          GetYearsEmployed()  { ... }
    public virtual      String         GetProgressReport() { ... }
    public static       Employee       Lookup(String name) { ... }
}

internal sealed class Manager : Employee {
    public override String             GetProgressReport() { ... }
}
```

Windows 进程已启动，CLR 已加载到其中，托管堆已初始化，而且已创建一个线程（连同它的 1 MB 栈空间）。线程已执行了一些代码，马上就要调用 M3 方法。图 4-6 展示了目前的状态。M3 方法包含的代码演示了 CLR 是如何工作的。平时不这样写代码，因为它们没有做什么真正有用的事情。

![](bbox=[0.166, 0.406, 0.873, 0.719])

**图 4-6**　CLR 已加载到进程中，堆已初始化，线程栈已创建，马上调用 M3 方法

JIT 编译器将 M3 的 IL 代码转换成本机 CPU 指令时，会注意到 M3 内部引用的所有类型，包括 **Employee、Int32、Manager** 以及 **String**（因为 “Joe”）。这时 CLR 要确认定义了这些类型的所有程序集都已加载。然后，利用程序集的元数据，CLR 提取与这些类型有关的信息，创建一些数据结构来表示类型本身。图 4-7 展示了为 **Employee** 和 **Manager** 类型对象使用的数据结构。由于线程在调用 M3 前已执行了一些代码，所以不妨假定 **Int32** 和 **String** 类型对象已经创建好了（这是极有可能的，因为它们都是很常用的类型），所以图中没有显示它们。