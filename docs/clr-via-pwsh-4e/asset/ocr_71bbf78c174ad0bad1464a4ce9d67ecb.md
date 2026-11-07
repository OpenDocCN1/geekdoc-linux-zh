```
```
}
return o;
}
}
```
```

编译并运行上述代码得到以下输出：

```
```
无法创建 System.Collections.Generic.Dictionary`2[TKey,TValue] 的实例，
因为 Type.ContainsGenericParameters 为 True

无法创建 DictionaryStringKey`1[TValue] 的实例，
因为 Type.ContainsGenericParameters 为 True

已创建 DictionaryStringKey`1[System.Guid] 的实例。
对象类型 = DictionaryStringKey`1[System.Guid]
```
```

可以看出，**Activator** 的 **CreateInstance** 方法会在试图构造开放类型的实例时抛出 **ArgumentException** 异常。注意，异常的字符串消息指明类型中仍然含有一些泛型参数。

从输出可以看出，类型名以 “`” 字符和一个数字结尾。数字代表类型的元数，也就是类型要求的类型参数个数。例如，**Dictionary** 类的元数为 2，要求为 **TKey** 和 **TValue** 这两个类型参数指定具体类型。**DictionaryStringKey** 类的元数为 1，只要求为 **TValue** 指定具体类型。

还要注意，CLR 会在类型对象内部分配类型的静态字段(本书第 4 章“类型基础”对此进行了讨论)。因此，每个封闭类型都有自己的静态字段。换言之，假如 `List<T>` 定义了任何静态字段，这些字段不会在一个 `List<DateTime>` 和一个 `List<String>` 之间共享；每个封闭类型对象都有自己的静态字段。另外，假如泛型类型定义了静态构造器(参见第 8 章“方法”)，那么针对每个封闭类型，这个构造器都会执行一次。泛型类型定义静态构造器的目的是保证传递的类型实参满足特定条件。例如，我们可以像下面这样定义只能处理枚举类型的泛型类型：

```
```
internal sealed class GenericTypeThatRequiresAnEnum<T> {
    static GenericTypeThatRequiresAnEnum() {
        if (!typeof(T).IsEnum) {
            throw new ArgumentException("T must be an enumerated type");
        }
    }
}
```
```

CLR 提供了名为**约束**的功能，可以更好地指定有效的类型实参。本章稍后会详细讨论。遗憾的是，约束无法将类型实参限制为“仅枚举类型”。正是因为这个原因，所以上例需要用静态构造器来保证类型是一个枚举类型。

# ### 12.2.2 泛型类型和继承

泛型类型仍然是类型，所以能从其他任何类型派生。使用泛型类型并指定类型实参时，实际是在 CLR 中定义一个新的类型对象，新的类型对象从泛型类型派生自的那个类型派生。换言之，由于 `List<T>` 从 `Object` 派生，所以 `List<String>` 和 `List<Guid>` 也从 `Object` 派生。类似地，由于 `DictionaryStringKey<TValue>` 从 `Dictionary<String, TValue>` 派生，所以 `DictionaryStringKey<Guid>` 也从 `Dictionary<String, Guid>` 派生。指定类型实参不影响继承层次结构——理解这一点，有助于你判断哪些强制类型转换是允许的，哪些不允许。