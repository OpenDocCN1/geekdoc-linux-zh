
`D:\Perl\book\figure3.pl`

`the statement block has executed 1 times`

`the statement block has been executed 2 times`

`the statement block has been executed 3 times`

`the statement block has been executed 4 times`

`the statement block has been executed 5 times`

`the statement block has been executed 6 times`

`the statement block has been executed 7 times`

`the statement block has been executed 8 times`

`the statement block has been executed 9 times`

`D:\>`

```
![](img/2070407c4a70134aab89572f10d21e60_116_0.png)
```

之前示例中的 `for` 语句读取“for `$a` 等于 1 到小于 10，`$a++`”。`$a` 的值是 `for` 语句第一次执行时的。在语句块执行之前，`$a` 的值加 1，因此在块执行后，新的 `$a` 值可以被求值以确保它仍然小于 10。每当评估为 `true` 时，`$a` 再次加 1 并执行语句块。在这个示例中，语句块执行了九次。

## 1 分钟训练

- 在之前的编程示例中，`$a` 的最终值是多少？
- 如果表达式 2 变为 `$a <= 10`，语句块将执行多少次，`$a` 的最终值将会是多少？

- 10
- 10, 11

# 项目 3-1：创建一个计数循环

编写一个程序，创建一个与上一个编程示例中类似的计数循环，但不要使用条件语句（conditional statement）。你可以使用在本模块中学到的任何其他条件语句。该程序应该显示语句块执行的次数，以及你使用的计数器变量的最终值。

如果你正在使用条件语句，并且需要使用语句、条件表达式或这三个组件的任何组合来连接多个语句，你可以使用逗号 `,` 将它们隔开。这里有一个演示此用点的编程示例。

```
#/usr/bin/perl

for ($a = 1; $a < 10; $a++) { print "the value of a is now $a \n"

print "the statement block has been executed $a times\n"; }
```

| `for` 条件语句的迭代部分包含两个用逗号隔开的语句 | `print` 语句将与自增运算符一起执行 |

下面的插图显示了使用逗号的编程示例生成的屏幕输出。

```
D:\Perl\book\figure3.code.pl

the statement block has been executed 1 times

the value of a is now 2

the statement block has been executed 2 times

the value of a is now 3

the statement block has been executed 3 times

the value of a is now 4

the statement block has been executed 4 times

the statement block has been executed 5 times

the value of a is now 6

the statement block has been executed 6 times

the value of a is now 7

the statement block has been executed 7 times

the value of a is now 8

the statement block has been executed 8 times

the value of a is now 9

the statment block has been executed 9 times

the value of a is now 10

D:\>
```
*(注：此处原文代码块中的输出内容保持原样)*

# 模块 3：控制结构 95

这个编程示例记录了语句块执行的次数，以及 `$a` 在整个执行过程中包含的值。现在已经详细介绍了条件语句，让我们继续讨论最后两个条件语句。

# The foreach 条件语句

`foreach` 条件语句可以用于遍历数组变量的内容。这允许你为循环指定不同的迭代范围，而不是只能指定起始和结束点。

> 注意
> 数组变量是一个我们还没有涵盖的话题。现在，将数组变量看作包含一组关联的所有数字或字符串列表。这些标量数据称为数组的元素（elements）。该主题将在本书的下一个模块中详细介绍。

在详细讨论之前，让我们先看下 `foreach` 条件语句的语法。

```
foreach scalar variable (array variable)

{

  'foreach' statement block

}
```

`foreach` 语句中的标量变量将设置为当前从数组中使用的元素。请注意，一旦 `foreach` 语句执行完成，该标量变量将重置为语句开始执行之前的值。仅在程序某些部分有效的变量被称为在这些部分中具有“作用域”（scope）。因为标量变量只在 `foreach` 循环内部具有作用域，所以它在循环内部赋值的值在循环外部是无效的。这听起来有点困惑，所以这里有一个编程示例让你更容易理解。

# 96 Perl：初学者指南

在屏幕上打印进入循环前的 `$b` 值 标进入 `foreach` 循环前的标量变量赋值

```
#!/usr/bin/perl

$b = 10;

print "the value of b is $b \n";

@a = (1,3,4,7,9,12);
### 数组赋值

foreach (@a) {
    # foreach 条件语句
    print "the value of b inside the loop is $b \n";
}

print "the value of b after the loop has executed $b \n";
```

这是使用数组变量 `@a` 和标量变量 `$b` 的 `foreach` 语句

我们正在打印循环结束后的 `$b` 值

这是一个数组赋值。数组等于右侧的标量数字列表

接下来的插图显示了 `foreach` 编程示例的屏幕输出。

```
Command Prompt

C:\>perl foreach\ue9.code.pl

the value of b before entering the loop is 10

the value of b inside the loop is 1

the value of b inside the loop is 3

the value of b inside the loop is 4

the value of b inside the loop is 7

the value of b inside the loop is 9

the value of b after the loop has executed 12

C:\>
```

你应该注意到进入循环前和退出循环后 `$b` 的值保持不变，即使它在 `foreach` 循环内部被赋值了不同的值。再次，这是因为 `$b` 在循环内部赋值的值在循环外部超出了作用域。

由于我们使用了隐式的 `$_` 标量变量，当你没有给 `print` 语句任何参数时，Perl 会自动知道指的是该变量。这只是使用 `foreach` 语句的一种简便方法，可以在编程时节省时间。
我们涵盖的最后一个条件语句使用了你在模块中学学会的大部分语句并并更简单的形式重新应用它们。

# 单行条件语句

当你不需要语句块时，可以使用单行条件语句。单行条件语句可以节省你的打字量。这里是它们的语法。

![](img/270407c470134ab89572f10d21e60_121.png)

接下来的插图显示了单行条件语句的屏幕输出。

```
#!/usr/bin/perl

$a = 15;

$b = 10;

while ($b < 20) {
  $a++;
  next if ($b == 20);
  print "$a was incremented by one \n" if ($b == 20);
}
```

![](img/270407c470134ab89572f10d21e60_122.png)

从插图中可以看到，循环语句被跳过了直到正常结束。

### 控制语句

Perl 提供了三种可以在循环内部使用的控制语句。这些语句非常直观，让我们直接进入。

### next 语句

`next` 控制语句可以在循环内部跳过迭代的剩余部分，直到正常结束。`next` 语句的语法如下：
```
