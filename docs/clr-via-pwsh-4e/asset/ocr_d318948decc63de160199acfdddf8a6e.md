```
x: HasValue=True, Value=5
y: HasValue=False, Value=0
```

# 19.1 C#对可空值类型的支持

C#允许使用相当简单的语法初始化上述两个 Nullable<Int32>变量 x 和 y。事实上，C#开发团队的目的是将可空值类型集成到 C#语言中，使之成为“一等公民”。为此，C#提供了更清晰的语法来处理可空值类型。C#允许用问号表示法来声明并初始化 x 和 y 变量：

```
Int32? x = 5;
Int32? y = null;
```

在 C#中，Int32?等价于 Nullable<Int32>。但 C#在此基础上更进一步，允许开发人员在可空实例上执行转换和转型①。C#还允许向可空实例应用操作符。以下代码对此进行了演示：

```
private static void ConversionsAndCasting() {
    // 从非空 Int32 隐式转换为 Nullable<Int32>
    Int32? a = 5;

    // 从'null'隐式转换为 Nullable<Int32>
    Int32? b = null;

    // 从 Nullable<Int32>显式转换为非空 Int32
    Int32 c = (Int32) a;

    // 在可空基元类型之间转型
    Double? d = 5;    // Int32 转型为 Double? (d is double 值 5.0)
    Double? e = b;    // Int32?转型为 Double? (e is null)
}
```

C#还允许向可空实例应用操作符，例如：

```
private static void Operators() {
    Int32? a = 5;
    Int32? b = null;

    // 一元操作符 (+ ++ - -- ! ~)
    a++;    // a = 6
    b = -b;    // b = null

    // 二元操作符 (+ - * / % & | ^ << >>)
    a = a + 3;    // a = 9
    b = b * 3;    // b = null;

    // 相等性操作符 (== !=)
    if (a == null) { /* no */ }  else { /* yes */ }
    if (b == null) { /* yes */ } else { /* no */ }
    if (a != b) { /* yes */ }    else { /* no */ }

    // 比较操作符 (< > <= >=)
    if (a < b)       { /* no */ } else { /* yes */ }
}
```

下面总结了 C#如何解析操作符。

① 作者在这里区分了转换和转型。例如，从 Int32 的可空版本到非空版本(或相反)，称为“转换”。但是，涉及不同基元类型的转换，就称为“转型”或“强制类型转换”。——译注