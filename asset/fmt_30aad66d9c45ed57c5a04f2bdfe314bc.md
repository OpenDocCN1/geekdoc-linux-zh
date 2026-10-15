
在这里我们用数据初始化变量。`angle` 的值为 90，`days` 数组包含每个月的天数。`letter` 包含 'a'，`word` 被设置为 flowers。专注于 `word` 数组，它的初始化遵循与初始化整数数组相同的语法，但看起来非常混乱。因此，字符字符串有一个快捷方法。

`char word[50] = "Flowers";`

第 9 行可以像上面那样编写。通过使用双引号，你可以用这种更整洁的语法初始化字符数组。这两个初始化语句之间的区别在于 `\0`。

所有的字符串必须以 NULL 字符（`\0`）结束。双引号语法会自动为你添加。所有处理字符串的标准函数都期望一个 NULL 终止符。不要忘记为 `\0` 留空间。

数组的大小并不是字符串的大小。重要的是，知道没有什么可以阻止你分配数组边界之外字符（尽管你的程序可能无法正确运行）。

你现在准备好比较数组和指针了，例如：

```
01: char word[12];
02: char *ptr;
```

`word` 是一个 12 个字符的数组。`ptr` 是指向字符的指针；没有为字符分配存储空间。图 B.2 应该会更清晰。

# 图 B.2

内存分配。

![](img/7fa9959a9d28ad339fa75e44952feeb9_696_0.png)

# C 编程回顾

第一语句显示了：

```
01: char word[12];
02: char *ptr;
```

`word` 是一个 12 个字符的数组。`ptr` 是指向字符的指针；没有为字符分配存储空间。图 B.2 应该会更清晰。

第一语句显示了：

```
01: char word[12];
02: char *ptr;
```

`word` 是一个 12 个字符的数组。`ptr` 是指向字符的指针；没有为字符分配存储空间，它是常量无法更改。

# 字符串中的转义码

到为止，你已经看到了几个标准函数的示例（`printf()`、`fopen()` 等）。本节介绍创建自己的函数。

函数的创建可以分为部分——声明和定义。

声明告知编译器某个函数的存在。它提供了一个描述传递给函数的变量数量和类型的原型，同时也给出了返回值类型。

定义描述了函数将执行的操作。列表 B.17 给出了创建函数 `first_function()` 并调用它的三次示例。

## 列表 B.17 函数简介

```
01: #include <stdio.h>
02:
03: /* 声明函数。也称为函数原型。 */
04:
05: void first_function(void);
06:
07: /* 定义 main()。这是一个特殊函数
08: 不需要显式声明。 */
09:
10: void main()
11: {
12:     /* 调用你的新函数几次。 */
13:
14:     first_function();
15:     first_function();
16:     first_function();
17: }
18:
19: /* 定义 first_function。 */
20:
21: void first_function(void)
22: {
23:     printf("Function was executed\n");
24: }
```

输出 Function was executed
Function was executed
Function was executed

此程序显示了第 5 行 `first_function` 的声明。该函数在第 14-16 行被调用，并在第 21-24 行定义。我们还引入了一个新的类型说明符 `void`，用于表示没有输入参数和返回值。

列表 B.18 在此列表的基础上扩展了如何向函数传递变量并向调用者返回值的用法。

## 列表 B.18 接收两个整数并向调用者返回整数

```
01: #include <stdio.h>
02:
03: /* 定义 maximum。它有两个整数
04:  * 输入参数，a 和 b，返回一个整数 */
05:
06: int maximum(int a, int b);
07:
08: void main(){
09: {
10:     int first = 25;
11:     int second = 10;
12:     int
13:     large;
14:     /* 将 first 和 second 传入 maximum 并将
15:      * 赋值给 large。
16:     */
17:
18:     large = maximum(first, second);
19:
20:     /* 显示 large 的值。 */
21:
22:     printf("The largest number is %d\n", large);
23:
24:     /* 再次调用 maximum 但传入两个常量。
25:      * 将整数结果传递给 printf。 */
26:     */
27:
28:     printf("The largest number is %d\n", maximum(30, 50));
29: }
30:
31: /* 定义 'maximum' 函数。
32:  * I/P 参数均为整数
33:  * 返回值是一个整数。
34:  */
35:
36: int maximum(int a, int b)
37: {
38:     int
39:     result;
40:
41:     /* 比较输入值
42:      * 并相应地设置 result。
43:     */
44:
45:     if (a > b)
46:     {
47:         result = a;
48:     }
49:     else
50:     {
51: result = b;
52: }
53:
54: return(result);
55: }
```

输出 最大的数字是 25
最大的数字是 50

当一个值被传递给函数时，它接收的是原始值的副本。这意味着当控制返回给调用者时，函数对该值做的任何更改都不会被保留。列表 B.19 展示了这一特性。

## 列表 B.19 值传递示例

```
01: #include <stdio.h>
02:
03: /* 定义 double_it() */
04:
05: int double_it(int number)
06:
07: void main()
08: {
09:     int original = 25;
10:     int doubled = 0;
11:
12:     /* 调用 double_it() 使 'original'
13:     * 的值翻倍。 */
14:
15:     doubled = double_it(original);
16:
17:     /* 显示值 */
18:
19:     printf("Original number was %d\n", original);
20:     printf("Doubled value is %d\n", doubled);
21: }
22:
23: int double_it(int number)
24: {
25:     /* 将参数的值翻倍。 */
26:
27:     number += number;
28:
29:     /* 将新值返回给调用者。 */
30:
31:     return(number);
32: }
```

# 附录 B

输出 原始数字是 25
翻倍后的值是 50

分析 此示例显示变量 `number` 在第 27 行值翻倍，但在打印时，原始值被保留了。这种特性存在于 C 中，以便可以将常量传递给函数。

尽管变量被复制到函数中，但你可以编写一个函数，让调用者看到对变量的更改。要实现这一点，你需要传递变量的指针。指针的值不会改变，但它指向的数据会改变。考虑列表 B.20，它是对列表 B.19 中程序的重写。

## 列表 B.20 引用传递

```
01: #include <stdio.h>
02:
03: /* 定义 double_it() */
04:
05: int double_it(int *number_ptr);
06:
07: void main()
08: {
09:     int         original = 25;
10:     int         doubled = 0;
11:
12:     /* 调用 double_it() 使 'original'
13:     * 的值翻倍。 */
14:
15:     doubled = double_it(original); /* 传递地址 */
16:
17:     /* 显示值 */
18:
```
