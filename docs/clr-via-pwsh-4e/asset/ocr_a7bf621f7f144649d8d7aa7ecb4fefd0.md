# ## 12.8 可验证性和约束

编译泛型代码时，C#编译器会进行分析，确保代码适用于当前已有或将来可能定义的任何类型。看看下面这个方法：

```
```
private static Boolean MethodTakingAnyType<T>(T o) {
    T temp = o;
    Console.WriteLine(o.ToString());
    Boolean b = temp.Equals(o);
    return b;
}
```
```

这个方法声明了 **T** 类型的临时变量(**temp**)。然后，方法执行两次变量赋值和几次方法调用。这个方法适用于任何类型。无论 **T** 是引用类型，是值类型或枚举类型，还是接口或委托类型，它都能工作。这个方法适用于当前存在的所有类型，也适用于将来可能定义的任何类型，因为所有类型都支持对 **Object** 类型的变量的赋值，也支持对 **Object** 类型定义的方法的调用(比如 **ToString** 和 **Equals**)。

再来看看下面这个方法：

```
```
private static T Min<T>(T o1, T o2) {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```
```

**Min** 方法试图使用 **o1** 变量来调用 **CompareTo** 方法。但是，许多类型都没有提供 **CompareTo** 方法，所以 C#编译器不能编译上述代码，它不能保证这个方法适用于所有类型。强行编译上述代码会报告消息：

**error CS0117: “T”不包含“CompareTo”的定义，并且找不到可接受类型为“T”的第一个参数的扩展方法“CompareTo”(是否缺少 using 指令或程序集引用?)。**

所以从表面看，使用泛型似乎做不了太多事情。只能声明泛型类型的变量，执行变量赋值，再调用 **Object** 定义的方法，如此而已！显然，假如泛型只能这么用，可以说它几乎没有任何用。幸好，编译器和 CLR 支持称为约束的机制，可通过它使泛型变得真正有用！

约束的作用是限制能指定成泛型实参的类型数量。通过限制类型的数量，可以对那些类型执行更多操作。以下是新版本的 **Min** 方法，它指定了一个约束(加粗显示)：

```
```
public static T Min<T>(T o1, T o2) where T : IComparable<T> {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```
```

C#的 **where** 关键字告诉编译器，为 **T** 指定的任何类型都必须实现同类型(T)的泛型 **IComparable** 接口。有了这个约束，就可以在方法中调用 **CompareTo**，因为已知 **IComparable<T>** 接口定义了 **CompareTo**。

现在，当代码引用泛型类型或方法时，编译器要负责保证类型实参符合指定的约束。例如，假如编译以下代码：