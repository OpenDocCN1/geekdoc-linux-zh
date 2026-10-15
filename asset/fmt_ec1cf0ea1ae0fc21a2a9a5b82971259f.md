
# Perl 基础

## PERL 包

`Perl` 包是一组存在于其命名空间中的代码。`Perl` 模块是定义在与包同名且扩展名为 `.pm` 文件中的包。同名的变量或函数可能存在于两个不同的模块中。任何不属于包的变量都属于主包（`main` package）。因此，所有使用的变量都是 `main` 包的一部分。额外包的声明确保了来自不同包的变量互不干扰。

## Perl 模块声明

模块名称必须与包名相同，并具有 `.pm` 扩展名。

## 示例：

```perl
package Calculator;

# 定义加法的子程序
sub addition
{
  # 初始化变量 x & y
  $x = $_[0];
  $y = $_[1];
  # 执行操作
  $x = $x + $y;
  # 打印和的函数
  print "\n***Addition is $x";
}

# 定义减法的子程序
sub subtraction
{
  # 初始化变量 x & y
  $x = $_[0];
  $y = $_[1];
  # 执行操作
  $x = $x - $y;
  # 打印差的函数
  print "\n***Subtraction is $x"
}

1;
```

文件名为 `Calculator.pm`，存储在 `Calculator` 目录中。要向解释器返回真值，在函数后写入 `1`。除了 `1` 之外，`Perl` 接受任何真值。

## 使用 Perl 模块

我们利用 `need` 或 `use` 函数来导入此计算器模块；`::` 用于访问模块中的函数或变量。这里有一个示例：

```perl
#!/usr/bin/perl

# 使用包 'Calculator'
use Calculator;

print "Enter the two numbers to multiply";

# 为变量赋值
$x = 15;
$y = 20;

# （此处省略了原文中重复的逻辑合并）
print "\nEnter the two numbers to divide";

# 为变量赋值
$x = 55;
$y = 65;

# 调用子程序
Calculator::division($x, $y);
```

## 利用模块变量

在使用之前声明来自各个包的变量，允许它们被利用。

## 示例：

```perl
#!/usr/bin/perl

package Message;

# 变量创建
$username;

# 定义-子程序
sub Hello
{
    print "Hello $username\n"
}

1;
```

（注：提供的文本包含大量重复的 OCR 内容，上述翻译已根据逻辑流进行了合并和清理。）

## 示例:

`2`, `4`, `-6`, `7.6`, `-8.9`, `057`, `1.87e-10`, `0xFFFF`

这些数字可以根据它们的应用分为几类：

- 整数（`Integers`）：`Perl` 整数以 10 进制的小数表示。这些数字可能是正数也可以是负数。另一方面，`Perl` 使用 `_` 来表示大整数值以提高可读性。
  示例：`213,254,484` 表示为 `213_254_484`。

  ```perl
  #!/usr/bin/perl

  # Positive-Integer
  $c = 30;

  # Negative-Integer
  $d = -25;

  # Big Integer-Number
  $e = 213_254_484;

  # Printing these numbers
  print("Positive Integer: ", $c, "\n");
  print("Negative Integer: ", $d, "\n");
  print("Big Integer: ", $e, "\n");
  ```

- 浮点数（`Floating point numbers`）：在 `Perl` 中，浮点数由整数部分和小数部分组成，用小数点分隔。浮数的整数部分可以是正数或负数，而小数部分只能是正数。在 `Perl` 中，浮点数可以用两种方式表示：
  - 定点法（`Fixed point`）：这种格式下小数点是固定的。这个小数点标记了小数部分的开始。
    示例: `22.5978`
  - 科学计数法（`Scientific`）：这种表示法包含两个部分：系数（实际数字）和指数（10 的幂次），系数乘以该指数得到结果。
    示例：`1.23567e-3` represents `1235.67`

    ```perl
    #!/usr/bin/perl

    # Positive Floating-Number
    $c = 20.5647;

    # Negative Floating-Number
    $d = -15.2451;

    # Scientific-value
    $e = 123.5e-10;

    # Printing these numbers
    print("Positive Number: ", $c, "\n");
    print("Negative Number: ", $d, "\n");
    print("Scientific Number: ", $e, "\n");
    ```

- 十六进制数（`Hexadecimal numbers`）：十六进制数字的基数为 16，范围从 0 到 15，写为 `0xa`，即在数字前加上 "0x"，其中 "a" 代表十六进制中的值 10。这些字母代表 10–15，范围从 "a" 到 "f"。十六进制数字可以是正值也可以是负值。
  示例：`0xe` represents `14` in the Hex, and `0xc` represents `12`

  ```perl
  #!/usr/bin/perl

  # Positive Hexadecimal Number
  $c = 0xc;

  # Negative Hexadecimal Number
  $d = -0xe;

  # 打印这些值
  print("Positive Hex Number: ", $c, "\n");
  print("Negative Hex Number: ", $d, "\n");

  # 打印十六进制值
  printf("Value in the Hex Format: %c", $c);
  ```
  
  结果，`%x` 用于以十六进制格式显示数字的值，如上所示。

- 八进制数（`Octal numbers`）：八进制数是基数为 8 的数字，范围从 0 到 7。这些数字表示为 `057`，数字前有一个 "0"，剩余部分是所需十进制数的八进制值。八进制数和其他数字一样，可以是正数也可以是负数。
  示例：
  对于八进制数 `057`，其十进制值为 `47`。

  ```perl
  #!/usr/bin/perl

  # Positive Octal Number
  $c = 074;

  # Negative Octal Number
  $d = -074;

  print("The Positive Octal number: ", $c, "\n");
  print("The Negative Octal number: ", $d, "\n");

  # 以八进制形式打印值
  printf("Value in Octal Form: %o", $c);
  ```
  
  `%o` 在此处被用于输出该形式的值。

- 二进制数（`Binary numbers`）：二进制数的基数为 2，意味着它们只有两个值：0 和 1。这些数字写为 `0b1010`，在数字前带有字母 "0b"。
  示例：
  对于二进制数 `0b1010` 其十进制值为 `10`

  ```perl
  #!/usr/bin/perl

  # Positive Binary-Number
  $c = 0b10110;

  # Negative Binary-Number
  $d = -0b101110;

  # 打印这些值
  print("The Positive Binary Number: ", $c, "\n");
  print("The Negative Binary Number: ", $d, "\n");

  # 以无符号二进制形式打印
  printf("Value in unsigned Binary Form: %b", $c);
  ```
  
  `%b` 在上述代码中用于以二进制形式显示数字。

# Perl 中带有 CRUD 操作的目录

`Perl` 是一种通用且跨平台的编程语言，主要用于文本处理。（注：原文中后半部分存在大量重复乱码，已根据要求进行处理）。

```perl
print (cwd);
print "\n";
```
