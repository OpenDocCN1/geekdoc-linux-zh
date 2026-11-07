除了 **ToString** 方法，**System.Enum** 类型还提供了静态 **Format** 方法，可调用它格式化枚举类型的值：

```
public static String Format(Type enumType, Object value, String format);
```

个人倾向于调用 **ToString** 方法，因为它需要的代码更少，而且更容易调用。但 **Format** 有一个 **ToString** 没有的优势：允许为 **value** 参数传递数值。这样就不一定要有枚举类型的实例。例如，以下代码将显示“Blue”：

```
// 以下代码显示"Blue"
Console.WriteLine(Enum.Format(typeof(Color), 3, "G"));
```

![](bbox=[0.109, 0.266, 0.169, 0.31])

> **注意**　声明有多个符号的枚举类型时，所有符号都可以有相同的数值。使用常规格式将数值转换为符号时，**Enum** 的方法会返回其中一个符号，但不保证具体返回哪一个符号名称。另外，如果没有为要查找的数值定义符号，会返回包含该数值的字符串。

也可调用 **System.Enum** 的静态方法 **GetValues** 或者 **System.Type** 的实例方法 **GetEnumValues** 来返回一个数组，数组中的每个元素都对应枚举类型中的一个符号名称，每个元素都包含符号名称的数值：

```
public static Array GetValues(Type enumType);    // System.Enum 中定义
public Array GetEnumValues();                     // System.Type 中定义
```

该方法可以结合 **ToString** 方法使用以显示枚举类型中的所有符号名称及其对应数值，如下所示：

```
Color[] colors = (Color[]) Enum.GetValues(typeof(Color));
Console.WriteLine("Number of symbols defined: " + colors.Length);
Console.WriteLine("Value\tSymbol\n-----\t------");
foreach (Color c in colors) {
    // 以十进制和常规格式显示每个符号
    Console.WriteLine("{0,5:D}\t{0:G}", c);
}
```

以上代码的输出如下：

```text
Number of symbols defined: 5
Value  Symbol
-----  ------
    0  White
    1  Red
    2  Green
    3  Blue
    4  Orange
```

我个人不喜欢 **GetValues** 和 **GetEnumValues** 方法，因为两者均返回一个 **Array**，必须转型成恰当的数组类型。所以我总是定义自己的方法：

```
public static TEnum[] GetEnumValues<TEnum>() where TEnum : struct {
    return (TEnum[])Enum.GetValues(typeof(TEnum));
}
```

使用我的泛型 **GetEnumValues** 方法可获得更好的编译时类型安全性，而且上例的第一行代