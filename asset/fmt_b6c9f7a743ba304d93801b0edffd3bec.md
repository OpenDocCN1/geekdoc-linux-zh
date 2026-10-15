
# Perl 全局变量与包变量说明

```perl
# 打印新变量的值。
print "Given names are : @copy\n"
print "Number of names are : $size\n"
# 用于说明全局变量
# 作用域的 Perl 程序
```

```perl
# 声明全局变量
$name = "PFP";
```

```perl
# 打印全局变量
print "$name\n";
```

```perl
# 全局变量可以在
# 块内部使用，因此我们
# 我们取一个块
# 在其中我们将打印
# $name 的值，即全局变量
{
```

```perl
# 这里 GFG 会打印
print "$name\n";
```

```perl
# 在块内将全局变量更改为 Peeksforeks
$name = "Peeksforeks";
```

```perl
# 打印全局变量
print "$name\n";
```

```perl
# 在块内部进行的更改
# 反映在整个程序中
# 所以这里打印 Peeksforeks
print "$name\n";
```

## 第二个示例

```perl
# 用于说明全局
# 作用域的程序
```

```perl
# 全局变量声明
$name = "PFP";
$count = 1;
```

```perl
# 打印全局变量
print $count. ".\name\n"
$count++;
```

```perl
# 块可以在块可以使用
{
```

```perl
# 所以下面的语句将打印
# PFG 和 1
print $count. ".\name\n"
```

```perl
# 增加 count 的值
# 在这里它变为 3
$count++;
```

```perl
}
```

```perl
# 调用函数
sub func {
```

```perl
    # 此私有变量声明
    # 隐藏了程序开头定义的
    # 全局变量
    my $name = "Hide"
    # 全局变量在块内部
    # 可的
    print $count. ".\name\n"
```

```perl
}
```

```perl
# 调用函数
func();
```

```perl
print "在上述块定义的变量: \$new_name\n";
```

# 局部变量的作用域（私有变量）

Perl 中的私有变量通过在变量前加上 `my` 来定义。`my` 关键字限制变量在函数、块、while 循环或 for 循环（大括号之间）的作用域。变量只能在不同的命名空间中使用。在每个 Perl 程序中，默认命名空间是 `main.`。

## 示例

```perl
# 用于说明
包变量
```

```perl
# 在 main 命名空间中声明变量
$varl = "Main Namespace";
```

```perl
print "The Value of varl: .$varl."\n";
```

```perl
# 包声明
# Pack1 是包
package Pack1;
```

```perl
# 因为 $varl 属于 main 命名空间
# 所以在 Pack1 命名空间内什么都不会打印
print "The Value of varl: .$varl."\n";
```

# Perl 基础 ■ 53

# 在 Pack1 命名空间中定义的变量

# 与主命名空间同名

$var1 = "Pack1 Namespace";

# 此处 $var1 属于 Pack1 命名空间

print "The Value of var1: \$var1.\n";

# 为了打印两个命名空间

# 中的变量，使用

# 以下方法

print "The Value of var1: \$main::var1.\n";

print "The Value of var1: \$Pack1::var1.\n";

在 Perl 中，`our` 关键字为同名的现有包变量创建一个别名。在 `our` 声明的词法作用域内，可以在不指定包名的情况下使用包变量。使用 `our` 关键字声明的变量是包变量的别名，在它的整个词法作用域内均可见，包括包边界。

```perl
# 用于说明 our 关键字使用的程序
# 使用 package 关键字声明
# Pack1 命名空间
package Pack1;
```

```perl
# 为剩余的词法作用域
# 声明 $Pack1::first_name
our $first_name;
$first_name = "Shashank";
```

```perl
# 仅为此命名空间
# 声明 $Pack1::second_name
$second_name;
$second_name = "Sharma";
```

```perl
# 声明 Pack2 命名空间
package Pack2;
```

```perl
# 输出 $first_name 的值，因为它
# 指向 $Pack1::first_name
print "first_name = \$first_name.\n";

# 由于 $second_name
# 在 Pack2 包作用域不存在，将打印任何内容
print "second_name = \$second_name.\n";
```

# 54 精通 Perl

在 Perl 中，模块（module）是一组连接的子程序和变量，用于执行一组编程任务。Perl 模块可以重用。全面的 Perl 存档 (CPAN) 托管了多个 Perl 模块。这些模块分为几类，包括网络、CGI、XML 处理和数据库接口。

## 创建一个 Perl 模块

模块名称必须与包（Package）名称相同，并以 `.pm` 扩展名结尾。

### 示例

```perl
package Calculator;

# 定义乘法的子程序
sub multiplication
{
  # 初始化变量 x & y
  $x = $_[0];
  $y = $_[1];
  # 执行操作
  $x = $x * $y;
  # 打印和的函数
  print "\n***Multiplication is \$x";
}

# 定义除法的子程序
sub division
{
  # 初始化变量 x & y
  $x = $_[0];
  $y = $_[1];
  # 执行操作
  $x = $x / $y;
  # 打印答案的函数
  print "\n**Division is $x";
};
```

文件名为 `Calculator.pm`，位于 `Calculator` 目录。要向解释器返回真值，在函数末尾放置 `1`。除了 `1` 之外，Perl 任何真值。

## 导入和使用 Perl 模块

我们利用 `need` 或 `use` 函数来导入此计算器模块；`::` 用于访问模块中的函数或变量。这里有一个示例：

```perl
#!/usr/bin/perl
```

```perl
# 使用包 'Calculator'
use Calculator;
print "Enter the two numbers to multiply";
# 为变量赋值
$x = 15;
$y = 20;
# 调用子程序
Calculator::multiplication($x, $y);
print "\nEnter the two numbers to divide";
# 为变量赋值
$x = 55;
$y = 65;
# 调用子程序
Calculator::division($x, $y);
```

## 利用模块变量

在 `ways` 之前声明来自各个包的变量，可以允许它们被利用。

### 示例

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

该模块的 Perl 文件如下：

```perl
#!/usr/bin/perl
# 使用 Message.pm 包
use Message;
# 为变量赋值
$Message::username = "Peeks";
# 调用子程序
Message::Hello();
```

## 使用预定义模块

Perl 有若干个预定义模块，可以随时在 Perl 应用程序中使用。例如 `strict` 和 `warnings`。

### 示例

```perl
#!/usr/bin/perl
use strict;
use warnings;
print" Hello This program uses the pre-defined Modules";
```
