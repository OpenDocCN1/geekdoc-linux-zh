
`MemberAccessTest.java:9: hour has private access in Time1`
`time.hour = 7; // error: hour has private access in Time1`

`MemberAccessTest.java:10: minute has private access in Time1`
`time.minute = 15; // error: minute has private access in Time1`

`MemberAccessTest.java:11: second has private access in Time1`
`time.second = 30; // error: second has private access in Time1`

3 个错误

图 8.3 | `Time1` 类的私有成员不可访问。

## 8.4 使用 this 引用引用当前对象的成员

每个对象都可以通过关键字 `this`（有时称为 `this` 引用）来获取指向它自身的引用。当为特定对象调用非静态方法时，方法体会隐式地使用关键字 `this` 来引用该对象的实例变量和其他方法。正如你将在将在 8.4 节中看到的，你也可以在非静态方法中显式地使用 `this` 关键字。第 8.5 节展示了 `this` 关键字的另一个有趣用法。

我们现在演示隐式和显式使用 `this` 引用，以使 `SimpleTest` 类的方法能够显示 `SimpleTime` 对象的私有数据（图 8.4）。注意，这个例子是第一个在一个文件中声明两个类的例子——`class ThisTest` 和 `class SimpleTime` 定义在第 14–47 行。我们这样做是为了证明，当你编译一个包含多个类的 `.java` 文件时，编译器会为每个编译类生成一个具有 `.class` 扩展名的独立类文件。在这种情况下，产生了两个独立的文件——`SimpleTime.class` 和 `ThisTest.class`。当一个源文件（`.java`）包含多个类声明时，编译器会将这两个类的类文件都放在同一个目录下。此外请注意，在图 8.4 中只有一个 `ThisTest` 被声明为 `public`。一个源文件只能包含一个 `public` 类——否则会发生编译错误。

```java
// ThisTest.java
// this 被隐式和显式地使用以引用对象的成员。
public class ThisTest {
    public static void main(String args[]) {
        SimpleTime time = new SimpleTime(15, 30, 19);
        System.out.println(time.buildString());
    }
} // end main
// SimpleTime 展示了 "this" 引用
class SimpleTime {
    private int hour; // 0-23
    private int minute; // 0-59
    private int second; // 0-59
    // 如果构造函数使用的参数名与
    // 实例变量名相同，则需要 "this" 
    // 来区分这些名称
    public SimpleTime(int hour, int minute, int second) {
        this.hour = hour; // 设置 "this" 对象的 hour
        this.minute = minute; // 设置 "this" 对象的 minute
        this.second = second; // 设置 "this" 对象的 second
    } // end SimpleTime constructor
```

图 8.4 | `this` 被隐式和显式地使用以引用对象的成员。（部分 1，共 2 部分）

```java
// 使用显式和隐式的 "this" 调用 buildUniversalString
public String buildString() {
    return String.format("%24s: %s\n%24s: %s",
        this.toUniversalString(),
        toUniversalString(),
        this.toUniversalString());
} // end method buildString
// 转换为通用时间格式 (HH:MM:SS) 的字符串
public String toUniversalString() {
    // 这里不需要 "this" 来访问实例变量；
    // 因为方法没有与实例变量同
    // 名的局部变量
    return String.format("%02d:%02d:%02d",
        this.hour,this.minute,this.second);
} // end method toUniversalString
// end class SimpleTime
```

```
toUniversalString(): 15:30:19
toUniversalString(): 15:30:19
```

**图 8.4** `this` 被隐式和显式地使用以引用对象的成员。（部分 2，共 2 部分。）

`class SimpleTime` 展示了 "`this`" 引用
```java
class SimpleTime {
    private int hour; // 0-23
    private int minute; // 0-59
    private int second; // 0-59
    // 如果构造函数使用的参数名与
    // 实例变量名相同，则需要 "this" 
    // 来区分这些名称
    public SimpleTime(int hour, int minute, int second) {
        this.hour = hour; // 设置 "this" 对象的 hour
        this.minute = minute; // 设置 "this" 对象的 minute
        this.second = second; // 设置 "this" 对象的 second
    } // end SimpleTime constructor
```

## 8.5 时间 类研究：重载构造函数

如你所知，你可以声明自己的构造函数来指定如何初始化对象。接下来，我们演示一个具有多个重载构造函数的类。要重载构造函数，只需提供具有不同签名的多个构造声明。回顾第 6.12，编译器通过参数数量、参数类型以及参数顺序来区分签名。

### 带重载构造函数的 Time2

`Time` 类的默认构造函数（图 8.1）将 `hour`、`minute` 和 `second` 初始化为默认值 0（即通用时间中的午夜）。默认构造函数未允许类的客户端使用非零值初始化时间。`Time2` 类（图 8.5）包含了五个重载构造函数，提供了实例化类的便捷方法。每个构造函数都确保对象从一致的状态开始初始化。在该程序中，四个构造函数调用了第五个，后者又调用 `set` 方法以确保 `hour` 的值在 0 到 23 之间，`minute` 和 `second` 的值在 0 到 59 之间。如果值超出范围，它将被设置为 0 以确保每个实例变量保持一致状态。编译器通过匹配构造函数调用指定的参数数量、类型和顺序与构造函数声明中指定的参数数量、类型和顺序来调用相应的构造函数。注意 `Time2` 还为每个实例变量提供了 `set` 和 `get` 方法。

> 错误提示 8.1
> 避免与字段冲突的方法参数名或局部变量。

> 性能提示 8.1
> Java 通过为每个类维护一个方法副本来节省存储。然而，每个对象都有它们自己的非静态字段副本。

```java
// Fig. 8.5: Time2.java
// 带重载构造函数的 Time2 类声明
public class Time2 {
    private int hour; // 0-23
    private int minute; // 0-59
    private int second; // 0-59
}
```

```java
// Time2 无参数构造函数：将每个实例变量初始化
// 为 0；确保 Time2 对象从一致的状态开始
public Time2()
{
    this(0, 0, 0, 0); // 调用带有三个参数的 Time2 构造函数
} // Time2 无参数构造函数
```
