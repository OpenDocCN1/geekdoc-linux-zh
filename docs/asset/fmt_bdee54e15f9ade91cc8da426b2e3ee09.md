
实现 `Comparable<T>` 的类的程序员负责声明该类比较两个同类对象的内容并返回比较结果。如果对象相等，方法必须返回 0；如果 `object1` 小于 `object2` 则返回 -1，如果 `integer1` 大于 `object2` 则返回 1。例如，类 `compareTo` 方法返回两个 `Integer` 对象中的 `int`。实现 `Comparable<T>` 接口的好处是 `Comparable<T>` 对象可以用于 `Collections`（`java.util` 包）的排序和搜索方法。我们在第 19 章 Collections 中讨论这些方法。

泛型方法 `maximum`（第 7–18 行）使用类型参数 `T` 作为方法的返回类型（第 7 行）、方法参数 `x`、`y` 和 `z` 的类型以及局部变量 `max` 的类型（第 9 行）。类型参数指定 `T` extends `Comparable<T>`，只有实现了 `Comparable<T>` 接口的类才能用于此方法。在这种情况下，`Comparable` 被称为类型参数的上界。默认情况下，`Object` 是上界。注意类型参数声明无论如何始终使用 `extends`

```java
// Fig. 18.5: MaximumTest.java
// Generic method maximum returns the largest of three objects.
public class MaximumTest
{
    // determines the largest of three Comparable objects
    public static <T extends Comparable<T>> T maximum(T x, T y, T z)
    {
        T max = x; // assume x is initially the largest
        if (y.compareTo(max) > 0)
            max = y; // y is the largest so far
        if (z.compareTo(max) > 0)
            max = z; // z is the largest
        return max; // returns the largest object
    } // end method
    public static void main(String[] args)
    {
        System.out.printf("Maximum of %d, %d and %d is %d\n", 3, 4, 5);
        maximum(3, 4, 5);
        System.out.printf("Maximum of %.1f, %.1f and %.1f is %.1f\n", 6.6, 8.8, 7.7, maximum(6.6, 8.8, 7.7));
        System.out.printf("Maximum of %s, %s and %s is %s\n", "pear", "apple", "orange", maximum("pear", "apple", "orange"));
    } // end method
} // end class MaximumTest
```

`Maximum of 3, 4 and 5 is 5`
`Maximum of 6.6, 8.8 and 7.7 is 8.8`
`Maximum of pear, apple and orange`

Fig. 18.5 | 类型参数带有上界的泛型方法。

参数 `extends` 继承一个类或实现一个接口。这个类型参数比 18.3 中为 `printArray` 指定的参数更具限制，后者能够输出包含任何类型对象的数组。使用 `Comparable<T>` 的限制是重要的，因为并不是所有对象都可以比较的。然而，`Comparable<T>` 对象保证具有 `compareTo` 方法。

`maximum` 方法使用了我们在第 6.4 节中使用的算法来确定三个对象中的最大值。该方法假设第一个参数 `x` 是最大的，并将其赋值给局部变量 `max`（第 9 行）。接下来，第 11-12 行的语句判断 `y` 是否大于 `max`。该条件通过调用 `y` 的 `compareTo` 方法（表达式为 `y.compareTo(max)`），它返回 -1 或 0，以确定其与 `max` 的关系。如果 `compareTo` 的返回值大于 0，则 `y` 较大并赋值给变量 `max`。同样地，第 14-15 行的语句判断 `z` 是否大于 `max`。如果是，第 15 行将 `z` 赋值给 `max`。然后，第 17 行将结果返回给调用者。

## 18.4 使用类型参数作为返回类型的方法

在 `main` 方法（第 20–28 行）中，第 23 行使用整数 3, 4 和 5 调用了 `maximum`。当编译器遇到这种情况时，它首先寻找接受三个 `int` 类型参数的 `maximum` 方法。不存在这样的方法，因此编译器寻找一个可以使用的泛型方法和泛型 `maximum`。然而，请记住，泛型方法的参数必须是引用类型，因此编译器将自动装箱 `autobox` 三个 `Integer` 对象并传递给 `maximum`。注意，`Integer` 类（`java.lang` 包）实现了 `Comparable<Integer>` 接口，该方法 `compare` 比较 `Integer` 对象中的两个值。因此，`Integer` 是 `maximum` 的有效参数。当返回表示最大值的 `Integer` 时，我们尝试用 `%d` 格式指定符输出它，它输出一个 `int` 原始类型值。因此，`maximum` 的返回值作为 `int` 值输出。

第 25 行传递给 `maximum` 的 `double` 参数也发生了类似的过程。每个 `double` 都被自动装箱为 `Double` 并传递给 `maximum`。同样，这是允许的，因为 `Double` 类（`java.lang` 包）实现了 `Comparable<Double>` 接口。`maximum` 返回的 `Double` 使用 `%f` 格式指定符输出，它输出一个原始类型值。因此，`maximum` 的返回值被自动装箱并作为 `double` 输出。第 27 行对 `maximum` 的调用接收两个 `String`，它们也是 `Comparable<String>` 对象。我们特意在每次调用中将最大值放在不同的位置（第 25 行和第 27 行），以说明泛型方法无论其在参数列表中的位置如何，都能找到最大值。

当编译器将泛型 `maximum` 翻译为 Java 字节时，它使用擦除机制将类型参数替换为实际类型。在 18.3 中，所有泛型类型都被替换为 `Object`。实际上，所有参数都被替换为类型参数的上界——除非另有指定，`Object` 是默认的上界。类型参数的上界在类型参数部分指定，使用泛型 `extends` 的名称以及代表上界的类或接口名称。在 `maximum` 的类型参数部分（图 18.5）中，我们将上界指定为 `Comparable<T>`。因此，只有 `Comparable<T>` 对象可以作为参数传递给 `maximum`——任何其他内容都会导致错误。

```java
// Fig. 18.5: MaximumTest.java
// Generic method maximum returns the largest of three objects.
... (省略部分)
    public static <T extends Comparable<T>> T maximum(T x, T y, T z)
    {
        T max = x; // assume x is initially the largest
        if (y.compareTo(max) > 0)
            max = y; // y is the largest so far
        if (z.compareTo(max) > 0)
            max = z; // z is the largest
        return max; // returns the largest object
    } // end method
...
```
