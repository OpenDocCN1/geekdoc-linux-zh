假设 DLL 程序集的开发人员将 50 改为 1000，并重新生成程序集。当应用程序代码重新执行时，它将自动提取字段的新值 1000。应用程序不需要重新生成，可以直接运行（尽管性能会受到一点影响）。要注意的是，当前假定的是 DLL 程序集的新版本没有进行强命名，而且应用程序的版本策略是让 CLR 加载这个新版本。

下例演示了如何定义一个与类型本身关联的 readonly 静态字段。还定义了 read/write 静态字段，以及 readonly 和 read/write 实例字段。

```
public sealed class SomeType {
    // 这是一个静态 readonly 字段：在运行时对这个类进行初始化时，
    // 它的值会被计算并存储到内存中
    public static readonly Random s_random = new Random();

    // 这是一个静态 read/write 字段
    private static Int32 s_numberOfWrites = 0;

    // 这是一个实例 readonly 字段
    public readonly String Pathname = "Untitled";

    // 这是一个实例 read/write 字段
    private System.IO.FileStream m_fs;

    public SomeType(String pathname) {
        // 该行修改只读字段 pathname，
        // 在构造器中可以这样做
        this.Pathname = pathname;
    }

    public String DoSomething() {
        // 该行读写静态 read/write 字段
        s_numberOfWrites = s_numberOfWrites + 1;

        // 该行读取 readonly 实例字段
        return Pathname;
    }
}
```

在上述代码中，许多字段都是内联初始化的①。C# 允许使用这种简便的内联初始化语法来初始化类的常量、read/write 字段和 readonly 字段。第 8 章“方法”会讲到，C# 实际是在构造器中对字段进行初始化的，字段的内联初始化只是一种语法上的简化。另外，在 C# 中初始化字段时，如果使用内联语法，而不是在构造器中赋值，有一些性能问题需要考虑。这些性能问题也将在第 8 章讨论。

① 内联(inline)初始化是指在代码中直接赋值来初始化，而不是将对构造器的调用写出来。——译注