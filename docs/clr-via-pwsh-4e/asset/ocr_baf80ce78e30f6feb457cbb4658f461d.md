> 注意　FCL 定义了 IComparable、ICollection、IList 和 IDictionary 等接口的泛型和非泛型版本。定义类型时要实现其中任何接口，一般应实现泛型版本。FCL 保留非泛型版本是为了向后兼容，照顾在 .NET Framework 支持泛型之前写的代码。非泛型版本还允许用户以较常规的、类型较不安全(more general, less type-safe)的方式处理数据。
> 
> 有的泛型接口继承了非泛型版本，所以必须同时实现接口的泛型和非泛型版本。例如，泛型 IEnumerable<out T> 接口继承了非泛型 IEnumerable 接口，所以实现 IEnumerable<out T> 就必须实现 IEnumerable。
> 
> 和其他代码集成时，有时必须实现非泛型接口，因为接口的泛型版本并不存在。这时，如果接口的任何方法获取或返回 Object，就会失去编译时的类型安全性，而且值类型将发生装箱。可利用本章 13.9 节“用显式接口方法实现来增强编译时类型安全性”介绍的技术来缓解该问题。

泛型接口的第二个好处在于，类可以实现同一个接口若干次，只要每次使用不同的类型参数。以下代码对这个好处进行了演示：

```
    using System;

    // 该类实现泛型 IComparable<T>接口两次
    public sealed class Number: IComparable<Int32>, IComparable<String> {
        private Int32 m_val = 5;

        // 该方法实现 IComparable<Int32>的 CompareTo 方法
        public Int32 CompareTo(Int32 n) {
            return m_val.CompareTo(n);
        }

        // 该方法实现 IComparable<String>的 CompareTo 方法
        public Int32 CompareTo(String s) {
            return m_val.CompareTo(Int32.Parse(s));
        }
    }

    public static class Program {
        public static void Main() {
            Number n = new Number();

            // 将 n 中的值和一个 Int32(5)比较
            IComparable<Int32> cInt32 = n;
            Int32 result = cInt32.CompareTo(5);

            //将 n 中的值和一个 String("5")比较
            IComparable<String> cString = n;
            result = cString.CompareTo("5");
        }
    }
```

接口的泛型类型参数可标记为逆变和协变，为泛型接口的使用提供更大的灵活性。欲知协