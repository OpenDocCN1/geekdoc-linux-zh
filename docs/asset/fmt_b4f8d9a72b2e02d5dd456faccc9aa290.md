
图 30.9 | `String` 类的 `valueOf` 方法。（共 2 部分中的第 2 部分）

第 18 行的表达式 `String.valueOf(charArray)` 使用字符数组 `charArray` 创建一个新的 `String` 对象。第 20 行的表达式 `String.valueOf(charArray, 3, 3)` 使用字符数组 `charArray` 的部分内容创建一个新的 `String` 对象。第二个参数指定了使用字符的起始索引。第三个参数指定了要使用的字符数量。

还有七种版本的 `valueOf` 方法，它们分别接收类型为 `boolean`、`char`、`int`、`float` 和 `double` 的参数。这些方法在第 21–30 行中进行了演示。接收 `Object` 作为参数的 `valueOf` 版本也可以执行此操作；所有对象都可以通过 `toString()` 字符串。

[注意：第 12–13 行分别使用字面量 `10000000000` 和 `2.5` 作为 `long longValue` 和 `float floatValue` 的初始值。默认情况下，Java 将整数视为 `int`，将浮点数字面量视为 `double`。在 `10000000000` 后面添加字母 `L` 并在字面量 `2.5` 后面追加字母 `f`，是指示编译器 `10000000000` 应该被视为 `long`，而 `2.5` 应该被视为 `float`。可以使用大写的 `F` 或小写的 `f` 表示 `long` 类型的变量，可以使用大写的 `F` 或小写的 `f` 表示 `float` 类型的变量。]

## 30.4 `StringBuilder` 类

一旦创建了 `String` 对象，其内容就永远无法改变。我们现在讨论 `StringBuilder` 类的特征，用于创建和操作动态字符串信息——即可变字符串。每个 `StringBuilder` 都能存储由其 `capacity` 指定的数量的字符。如果超过了 `StringBuilder` 的容量，容量将自动扩展以容纳额外的字符。`StringBuilder` 类还用于实现用于字符串拼接的 `+` 和 `+=` 运算符。

## 性能提示 30.2

Java 可以对涉及 `String` 对象的某些操作进行优化（例如在多个引用之间共享一个 `String`），因为它知道这些对象不会改变。如果数据不会改变，则应该使用 `String`（而不是 `StringBuilder`）。

## 性能提示 30.3

在频繁执行字符串拼接或其他字符串修改的程序中，使用 `StringBuilder` 类来实现修改会更高效。

## 软件工程观察 30.2

`StringBuilder` 不是线程安全的。如果多个线程需要访问同一个动态字符串信息，请在代码中使用 `StringBuilder` 类。`StringBuilder` 类和 `StringBuffer` 类是等同的，但 `StringBuffer` 类是线程安全的。

### 30.4.1 `StringBuilder` 构造函数

`StringBuilder` 类提供了四个构造函数。我们在图 30.10 中演示了其中三个。第 8 行使用无参数的 `StringBuilder` 构造函数来创建一个不包含字符且初始容量为 16 个字符的 `StringBuilder`（`StringBuilder` 的默认值）。第 9 行使用接收整数参数的构造函数来创建一个不包含字符且初始容量由整数参数指定的 `StringBuilder`（即 10）。第 10 行使用接收 `String` 参数的 `StringBuilder` 构造函数（在本例中为字符串字面量）来创建一个包含 `String` 参数中字符的 `StringBuilder`。
