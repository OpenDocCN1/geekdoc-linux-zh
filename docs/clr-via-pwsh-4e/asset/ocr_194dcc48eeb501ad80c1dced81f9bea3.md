Swap 调用中，C#发现 s1 是 String，而 s2 是 Object(即使它恰好引用一个 String)。由于 s1 和 s2 是不同数据类型的变量，编译器拿不准要为 Swap 传递什么类型实参，所以会报告以下消息：**error CS0411: 无法从用法推断出方法"Program.Swap<T>(ref T, ref T)"的类型参数。请尝试显式指定类型参数。**

类型可定义多个方法，让其中一个方法接受具体数据类型，让另一个接受泛型类型参数，如下例所示：

```
private static void Display(String s) {
    Console.WriteLine(s);
}

private static void Display<T>(T o) {
    Display(o.ToString());    // 调用 Display(String)
}
```

下面展示了 **Display 方法**的一些调用方式：

```
Display("Jeff");                 // 调用 Display(String)
Display(123);                    // 调用 Display<T>(T)
Display<String>("Aidan");       // 调用 Display<T>(T)
```

在第一个调用中，编译器可调用接受一个 String 参数的 Display 方法，也可调用泛型 Display 方法(将 T 替换成 String)。但 C#编译器的策略是先考虑较明确的匹配，再考虑泛型匹配。所以，它会生成对非泛型 Display 方法的调用，也就是接受一个 String 参数的版本。对于第二个调用，编译器不能调用接受 String 参数的非泛型 Display 方法，所以必须调用泛型 Display 方法。顺便说一句，编译器优先选择较明确的匹配，开发人员应对此感到庆幸。假如编译器优先选择泛型方法，那么由于泛型 Display 方法会再次调用 Display(但传递由 ToString 返回的一个 String)，所以会造成无限递归。

对 Display 的第三个调用明确指定了泛型类型实参 String。这告诉编译器不要尝试推断类型实参。相反，应使用显式指定的类型实参。在本例中，编译器还假定我肯定是想调用泛型 Display 方法，所以会毫不犹豫地调用泛型 Display 方法。在内部，泛型 Display 方法会为传入的字符串调用 ToString 方法，然后将转换所得的字符串传给非泛型 Display 方法。

# 12.7 泛型和其他成员

在 C#中，属性、索引器、事件、操作符方法、构造器和终结器本身不能有类型参数。但它们能在泛型类型中定义，而且这些成员中的代码能使用类型的类型参数。

C#之所以不允许这些成员指定自己的泛型类型参数，是因为 Microsoft C#团队认为开发人员很少需要将这些成员作为泛型使用。除此之外，为这些成员添加泛型支持的代价是相当高的，因为必须为语言设计足够的语法。例如，在代码中使用一个+操作符时，编译器可能要调用一个操作符重载方法。而在代码中，没有任何方法能伴随+操作符指定类型实参。