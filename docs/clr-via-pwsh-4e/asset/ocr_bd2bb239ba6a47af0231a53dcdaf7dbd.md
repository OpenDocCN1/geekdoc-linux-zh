调用这个公共初始化构造器。这样能减少生成的代码。下例演示了如何在 C# 中利用 **this** 关键字显式调用另一个构造器：

```
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

# 8.2 实例构造器和结构（值类型）

值类型(struct)构造器的工作方式与引用类型(class)的构造器截然不同。CLR 总是允许创建值类型的实例，并且没有办法阻止值类型的实例化。所以，值类型其实并不需要定义构造器，C#编译器根本不会为值类型内联(嵌入)默认的无参数构造器。来看下面的代码：

```
internal struct Point {
    public Int32 m_x, m_y;
}
internal sealed class Rectangle {
    public Point m_topLeft, m_bottomRight;
}
```

为了构造一个 **Rectangle**，必须使用 **new** 操作符，而且必须指定构造器。在这个例子中，调用的是 C#编译器自动生成的默认构造器。为 **Rectangle** 分配内存时，内存中包含 **Point** 值类型的两个实例。考虑到性能，CLR 不会为包含在引用类型中的每个值类型字段都主动调用构造器。但是，如前所述，值类型的字段会被初始化为 0 或 **null**。

CLR 确实允许为值类型定义构造器。但必须显式调用才会执行。下面是一个例子。

```
internal struct Point {
```