码可简化成以下形式：

```
    Color[] colors = GetEnumValues<Color>();
```

前面的讨论展示了可以对枚举类型执行的一些很“酷”的操作。在程序的 UI 元素(列表框、组合框等)中显示符号名称时，我认为经常使用的会是 ToString 方法(常规格式)，前提是字符串不需要本地化(因为枚举类型没有提供本地化支持)。除了 GetValues 方法，System.Enum 和 System.Type 类型还提供了以下方法来返回枚举类型的符号：

```
    // 返回数值的字符串表示
    public static String GetName(Type enumType, Object value);        // System.Enum 中定义
    public String GetEnumName(Object value);                          // System.Type 中定义

    // 返回一个 String 数组，枚举中每个符号都对应一个 String
    public static String[] GetNames(Type enumType);                   // System.Enum 中定义
    public String[] GetEnumNames();                                   // System.Type 中定义
```

前面讨论了用于查找枚举类型中的符号的多种方法。但还需要一个方法来查找与符号对应的值。例如，可利用这个操作转换用户在文本框中输入的一个符号。利用 Enum 提供的静态 Parse 和 TryParse 方法，可以很容易地将符号转换为枚举类型的实例：

```
    public static Object Parse(Type enumType, String value);
    public static Object Parse(Type enumType, String value, Boolean ignoreCase);
    public static Boolean TryParse<TEnum>(String value, out TEnum result) where TEnum: struct;
    public static Boolean TryParse<TEnum>(String value, Boolean ignoreCase, out TEnum result)
        where TEnum : struct;
```

以下代码演示了如何使用这些方法：

```
    // 因为 Orange 定义为 4，'c'被初始化为 4
    Color c = (Color) Enum.Parse(typeof(Color), "orange", true);

    // 因为没有定义 Brown，所以抛出 ArgumentException 异常
    Color c = (Color) Enum.Parse(typeof(Color), "Brown", false);

    // 创建值为1的 Color 枚举类型实例
    Enum.TryParse<Color>("1", false, out c);

    // 创建值为23的 Color 枚举类型实例
    Enum.TryParse<Color>("23", false, out c);
```

以下是 Enum 的静态 IsDefined 方法和 Type 的 IsEnumDefined 方法：

```
    public static Boolean IsDefined(Type enumType, Object value);   // System.Enum 中定义
    public Boolean IsEnumDefined(Object value);                      // System.Type 中定义
```

可利用 IsDefined 方法判断数值对于某枚举类型是否合法：

```
    // 显示"True"，因为 Color 将 Red 定义为1
    Console.WriteLine(Enum.IsDefined(typeof(Color), 1));

    // 显示"True"，因为 Color 将 White 定义为0
    Console.WriteLine(Enum.IsDefined(typeof(Color), "White"));

    // 显示"False"，因为检查要区分大小写
    Console.WriteLine(Enum.IsDefined(typeof(Color), "white"));

    // 显示"False"，因为 Color 没有和值10对应的符号
    Console.WriteLine(Enum.IsDefined(typeof(Color), 10));
```