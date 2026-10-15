
`package Dog;` # 声明一个名为 `Dog` 的包

`print "This is package ", __PACKAGE__, "\n";`

`package Cat;` # 声明一个名为 `Cat` 的包

`print "This is package ", __PACKAGE__, "\n";`

(输出)

`2 This is package Dog`

`4 This is package Cat`

```
## 解释

- `1.` `Dog` 包被声明，其作用域持续到定义它的块、`eval` 或文件结束，或者直到声明另一个包。通常每个文件只有一个包。这个包在另一包 `Cat` 在第 3 行被声明之前可见。
- `2.` 特殊字面量包含当前包名。
- `3.` 声明了另一个包。`Cat` 包从这里到文件结束均可见。

**从另一个包引用包变量和子程序。** 虽然我们在整本教材中都使用 **全局**（global）一词来描述变量的作用域（可见性），并以此来区分它们与私有的词法作用域变量（`my` 或 `state` 变量），但请记住，全局变量在技术上只是 **包**（package）变量。它们存在于某个包中，并位于该包的命名空间中。而词法变量没有包的概念，它们生活在自己的小世界里（即为当前作用域创建了一个私有的 *scratchpad*，当它们离开作用域时被清除）。当你启用 `strict` 时，除非完全限定包变量的名称，否则你不能使用包变量。然而，子程序名称位于全局命名空间中，并且不受此限制。

要引用另一个包中的包变量，请在包名之前加上表示变量数据类型的记号（奇怪的字符），后跟两个冒号和变量名：例如，如果包名是 `Dog`，而另一个包需要访问 `Dog` 中的包变量，你可能会看到以下内容：

```perl
$Dog::name
@Dog::treats
$Dog::treats[1]
```

`1.` 在古老的 Perl 4 中，且现在仍然有效，使用撇号代替双冒号，即 `$Dog'name`。撇号在版本 5.003 及之后的 Perl 3 脚本中仍可接受。

# 第 13 章 • 模块化、封装并交给图书馆！

双冒号让人想起 C++ 的作用域解析运算符。当从另一个包引用主包时，你可以省略包名。你可以将 `:main::friend` 简写为 `::friend`。要引用其他包中的子程序，例如包名为 `Dog` 时，从另一个包调用子程序的方式可能如下：

```
Dog::play("catch")
Dog::sit()
```

在下面的示例中，你将看到同一文件内的包声明、它们的作用域，以及如何从一个包切换到另一个包。

## 示例 13.2

```
1  package Dog; # 包声明
2  our $name="Lassie"; # 包变量
3  my $gender="female"; # 词法私有变量
4  @treats=("rawhide", "pork bone", "bacon twists", "milkbone");
5  sub play{
     my $dogname = shift;
     print "$dogname catches a tennis ball.\n";
  }
6  package Cat; # 包声明
7  $name = "Skiddy";
8  print "Treats are: @treats\n"; # 在此包中未定义
9  print "$name says hello to $Dog::name.\n";
10 print "$Dog::name is a $Dog::gender.\n";
11 print "$name prefers chicken flavored Temptations\n";
12 print "$Dog::name loves ",join(", ", @Dog::treats),
       " but prefers $Dog::treats[0].\n";
13 Dog::play($name); # 调用 Dog 包中的函数
```
