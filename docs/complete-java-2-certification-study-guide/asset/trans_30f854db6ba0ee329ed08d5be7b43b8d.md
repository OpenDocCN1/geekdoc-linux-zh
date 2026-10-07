

## 包装类

每个 Java 基本数据类型都有对应的包装类。包装类简单来说就是一个封装了单个值的类。例如，`Integer` 类封装了一个 `int` 值，而 `Float` 类封装了某个 `float` 值。包装类的名称与对应的基本类型名称并不完全匹配。表 8.2 列出了基本类型和包装类。

表 8.2 基本类型与包装类

| 基本数据类型 | 包装类 |
|---|---|
| boolean | Boolean |
| byte | Byte |
| char | Character |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |

可以通过将要包装的值传递给适当的构造函数来构造这些包装类。以下代码展示了如何构造每个包装类型的实例：

```
boolean primitiveBoolean = true;
Boolean wrappedBoolean = new Boolean(primitiveBoolean);
byte primitiveByte = 4;
Byte wrappedByte = new Byte(primitiveByte);
char primitiveChar = 'M';
Character wrappedChar = new Character(primitiveChar);
short primitiveShort = 3133;
Short wrappedShort = new Short(primitiveShort);
int primitiveInt = 1234568;
Integer wrappedInt = new Integer(primitiveInt);
long primitiveLong = 12345678965421L;
Long wrappedLong = new Long(primitiveLong);
float primitiveFloat = 1.1f;
Float wrappedFloat = new Float(primitiveFloat);
double primitiveDouble = 1.111111;
Double wrappedDouble = new Double(primitiveDouble);
```

除了 `Character` 之外，还有另一种构造这些类类的方法：你可以向构造函数传递一个表示该值的 `String`。这些构造函数大部分会抛出 `NumberFormatException`，因为构造函数可能无法表示有效的值。`Boolean` 不抛出此异常；它的构造函数接受任何字符串，如果字符串（忽略大小写）为 true，则返回 true。以下代码片段展示了如何从字符串构造包装类：

```
try {
    boolean primitiveBoolean = "true";
    Boolean wrappedBoolean = new Boolean(primitiveBoolean);
    byte primitiveByte = "4";
    Byte wrappedByte = new Byte(primitiveByte);
    short primitiveShort = "3133";
    Short wrappedShort = new Short(primitiveShort);
    int primitiveInt = "1234568";
    Integer wrappedInt = new Integer(primitiveInt);
    long primitiveLong = "12345678965421";
    Long wrappedLong = new Long(primitiveLong);
    float primitiveFloat = "1.1f";
    Float wrappedFloat = new Float(primitiveFloat);
    double primitiveDouble = "1.111111";
    Double wrappedDouble = new Double(primitiveDouble);
} catch (NumberFormatException e) {
    System.out.println("Bad Number");
}
```

封装在相同类型包装类中的值可以使用之前讨论过的 `equals()` 方法来检查相等性。例如，以下代码片段检查了两个 `Double` 实例：

```
Double d1 = new Double(1.0105);
Double d2 = new Double(1.11348);
if (d1.equals(d2)) {
    // 做一些操作。
}
```

在值被封装后，你可能最终需要提取它。对于 `Boolean` 实例，你可以调用 `booleanValue()`。对于 `Character` 实例，你可以调用 `charValue()`。其他六个类继承了抽象父类 `Number`，该类提供了将封装的值作为 `byte`、`short`、`int`、`long`、`float` 或 `double` 获取的方法。换句话说，任何封装的值都可以作为任何数值类型获取。获取方法为：

- public byte byteValue()
- public short shortValue()
- public int intValue()
- public long longValue()
- public float floatValue()
- public double doubleValue()

当方便将某个基本类型当作对象处理时，包装类就非常有用。一个很好的例子是 `Vector` 类，它是一个包含任意类型对象的动态增长集合。向 vector 添加对象的方法是：

`public boolean add(Object obj)`

使用此方法，你可以向 vector 添加任何类型的对象；你甚至可以添加一个数组（你已经在第 4 章“转换与强制类型转换”中见过原因了）。但是，你不能向它添加 `int`、`long` 或任何其他基本类型。不存在专门的特殊方法，且 `add(Object obj)` 将无法工作，因为从基本类型到对象没有自动转换。因此，以下代码将无法编译：

```
Vector vec = new Vector();
boolean boo = false;
vec.add(boo); // 非法
```

解决方案是封装 `boolean` 基本类型，如下：

```
Vector vec = new Vector();
boolean boo = false;
Boolean wrapper = new Boolean(boo);
vec.add(wrapper); // 合法
```

包装类在另一个方面也很有用：它们提供了多种实用方法，其中一些是静态的。例如，静态方法 `Character.isDigit(char ch)` 返回一个布尔值，告知该字符是否表示十进制数字。所有的包装类除

