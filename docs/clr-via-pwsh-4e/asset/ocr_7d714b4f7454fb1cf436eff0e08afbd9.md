操作符(方法)。以下 Point 值类型重载了==和!=操作符：

```
```csharp
using System;

internal struct Point {
    private Int32 m_x, m_y;
    public Point(Int32 x, Int32 y) { m_x = x; m_y = y; }

    public static Boolean operator==(Point p1, Point p2) {
        return (p1.m_x == p2.m_x) && (p1.m_y == p2.m_y);
    }

    public static Boolean operator!=(Point p1, Point p2) {
        return !(p1 == p2);
    }
}
```
```

然后可以使用 Point 类型的可空实例，编译器能自动调用你重载的操作符(方法)：

```
```csharp
internal static class Program {
    public static void Main() {
        Point? p1 = new Point(1, 1);
        Point? p2 = new Point(2, 2);

        Console.WriteLine("Are points equal? " + (p1 == p2).ToString());
        Console.WriteLine("Are points not equal? " + (p1 != p2).ToString());
    }
}
```
```

生成并运行上述代码得到以下输出：

```
```text
Are points equal? False
Are points not equal? True
```
```

# 19.2　C#的空接合操作符

C#提供了一个“空接合操作符”(null-coalescing operator)，即??操作符，它要获取两个操作数。假如左边的操作数不为 null，就返回这个操作数的值。如果左边的操作数为 null，就返回右边的操作数的值。利用空接合操作符，可以方便地设置变量的默认值。

空接合操作符的一个好处在于，它既能用于引用类型，也能用于可空值类型。以下代码演示了如何使用??操作符：

```
```csharp
private static void NullCoalescingOperator() {
    Int32? b = null;

    // 下面这行等价于：
    // x = (b.HasValue) ? b.Value : 123
    Int32 x = b ?? 123;
    Console.WriteLine(x); // "123"

    // 下面这行等价于：
    // String temp = GetFilename();
    // filename = (temp != null) ? temp : "Untitled";
    String filename = GetFilename() ?? "Untitled";
}
```
```

有人争辩说??操作符不过是?:操作符的“语法糖”而已，所以C#编译器团队不应该将这个操作符添加到语言中。实际上，??提供了重大的语法上的改进。第一个改进是??操作符能