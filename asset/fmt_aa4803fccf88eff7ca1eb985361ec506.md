
## Creating Data Objects

数据是程序所知道或可以计算的事实。程序的数据可以采用多种形式，例如字符字符串、整数、浮点值、数组和结构体。本章探讨这些基本数据类型对象，并包括调试程序数据的建议。

> Note
>
> 我在此使用的“object”一词不一定指面向对象编程。所有数据项都正确地称为对象。有关使用 C++ 类创建对象的面向对象编程技术的介绍，请参阅第三部分“面向对象编程”。

## DATA DECLARATIONS

C++ 要求您在程序中首次使用数据对象之前声明它。要声明数据对象，请指定其类型和名称，并以分号结束声明。以下是一个示例：

```
int counter;
```

这声明了一个名为 `counter` 的变量，其类型为 `int`。运行程序会在内存中创建空间来保存变量的值。它是一个变量，因为尽管它一次只能保存一个值，但程序可以按需要频繁更改该值。一种方法是使用为变量赋值语句。以下语句将值 100 分配给 `counter`：

```
counter = 100;
```

将值分配给 `counter` 会替换变量先前保存的值。特别重要的是要理解等号并不表示 `counter` 等于 100；它执行在运行时将值 100 移动到 `counter` 中的操作（或技术上，移动到程序为变量保留的内存中）。您也可以将表达式的结果分配给变量。以下语句将 `counter` 的当前值增加十：

```
counter = counter + 10;
```

编写该语句的简写方式是

```
counter += 10;
```

简写只引用一次 `counter`，在某些情况下这可能更高效（例如，如果 `counter` 是一个复杂表达式而不是简单的变量）。您也可以在表达式中使用类型兼容的变量。如果您像这样声明另一个 `int` 变量：

```
int total;
```

程序可以初始化 `total` 为 10，然后使用以下语句将 `counter` 加到它上面：

```
total = 10;
total = total + counter;
```

如果在这些语句之前 `counter` 等于 100，那么现在 `total` 等于 110。与所有赋值一样，表达式 `(total + counter)` 的结果必须是与接收该值的对象兼容的类型。前面的语句也可以使用简写形式编写：

```
total += counter;
```

这仅仅避免了不得不输入两次 `total`。两种形式都是正确的，但简写形式很流行，而且如前所述，可能更高效。

## 类型转换

赋给对象的值必须是合适的类型。如果你尝试将一种类型的值赋给另一种类型的变量，如下面的语句所示，编译器会尝试将该值转换为兼容的类型。理解这一点很重要，尤其是如果你熟悉 Pascal 等其他编程语言，在这些语言中，赋值操作的数据类型必须与目标对象的类型严格匹配。考虑以下语句：

```
double p1 = 3.14159;
int counter = p1; // ???
```

`double` 类型将 `p1` 指定为浮点值。将 `p1` 赋给 `int` 类型的 `counter` 变量会将其值设为 3，但由于该赋值涉及不同类型的对象，编译器会发出以下警告：

```
x.cpp:8: warning: initialization to 'int' from 'double'
```

通过使用类型转换表达式，可以“修复”关于不兼容数据类型的警告。将前面的赋值改为以下形式即可消除警告：

```
int count = (int)p1;
```

以这种方式在括号中指定对象的数据类型，会将其值转换为指定的类型。这也告诉编译器，你意识到这些对象属于不同类型，并且你是有意将一个值赋给另一个。然而，你不能随意使用类型转换来执行转换。例如，你不能使用类型转换表达式将字符串转换为 `int` 值——为此，你必须调用库函数（有关更多信息，请参阅本章后面的“字符串转换”）。

> 注意
>
> `double` 数据类型之所以这样命名，来源于“双精度”（double precision）一词，指的是用于浮点值的内部存储格式。

## 标识符：好、坏与丑

对象的名称，即标识符，必须符合一定的规则。一个格式正确的标识符必须以字母字符或下划线开头，并且只能包含字母字符、数字和下划线。它可以包含大写和小写字母。标识符的长度可以从 1 到 255 个字符，但编译器只识别前 32 个字符。对于通用变量，通常使用单个字母标识符，如 `i` 和 `x`，但较长的名称如 `index` 和 `x_coordinate` 可以使程序更易于理解。

> 提示
>
> 虽然标识符的法定长度限制为 255，但在实践中，标识符不应超过大约 15 到 20 个字符。

GNU C++ 标识符命名规则有一些深奥且大多无用的变体。例如，你可以在标识符中使用美元符号，但其他编译器可能接受也可能不接受。你最好只使用字母、数字和下划线。一些好标识符的例子有：

- `counter`
- `y2k_fix`
- `date_of_birth`
- `speedOfLight`

许多 C 程序员反对在标识符中使用大写字母，更喜欢 `speed_of_light` 而不是 `speedOfLight`。无论你的偏好如何，都必须保持一致。这是因为 C++ 区分大小写，编译器会将标识符 `speed_of_light`、`speedOfLight` 和 `speedoflight` 视为三个不同的对象。以下是一些坏标识符的例子：

- `10times`
- `user-name`
- `xq29b`

第一个标识符以数字开头，这是绝不允许的。第二个包含连字符，但只允许使用字母、数字和下划线。第三个标识符只是丑陋。如果你创建这样的标识符，那么在调试程序时，你会想知道 `xq29b` 到底是什么意思。始终选择能描述其用途的标识符。不要含糊不清；要清晰。

> 提示
>
> 尽管标识符可以以一个或多个下划线开头，如 `_username` 和 `__user_value`，但这种约定被标准库用来避免与用户程序标识符冲突。因此，不要用自己的标识符以下划线开头。

## GNU C++ 保留字

C++ 保留了 97 个标识符供其自身使用（这个数字可能因编译器版本而异）。表 6.1 列出了 GNU C++ 中的所有保留字。不要使用表中的任何单词作为你自己的标识符。

### 表 6.1 GNU C++ 保留字

| __alignof | __const__ | __inline | reinterpret_cast | try |
|---|---|---|---|---|
| __alignof__ | const | __inline__ | return | typedef |
| and | const_cast | inline | short | typeid |
| and_eq | continue | int | __signature__ | typename |
| __asm | default | __label__ | signature | __typeof |
| __asm__ | delete | long | __signed | __typeof__ |
| asm | do | mutable | __signed__ | typeof |
| __attribute | double | namespace | signed | union |
| __attribute__ | dynamic_cast | new | __sigof__ | unsigned |
| auto | else | not | sigof | using |
| bitand | enum | not_eq | sizeof | virtual |
| bitor | explicit | operator | static | void |
| bool | __extension__ | or | static_cast | __volatile |
| break | extern | or_eq | struct | __volatile__ |
| case | false | overload | switch | volatile |
| catch | float | private | template | __wchar_t |
| char | for | protected | this | while |
| class | friend | public | throw | xor |
| compl | goto | register | true | xor_eq |
| __const | if | | | |

> Tip
>
> 如果编译器返回“parse error”但源代码看起来是正确的，请检查是否不小心使用了表 6.1 中的某个词。

## 简单数据对象

简单数据对象保存数值，如整数或浮点值。其他简单数据类型包括表示真或假条件的布尔值、字符和枚举。枚举只不过是对一系列值赋予名称的集合，例如一周中的天数。

本节介绍 C++ 的简单数据类型，并列出一些程序来解释相关主题，例如如何确定对象的大小和类型，以及如何计算表达式的结果。

## 整数变量
