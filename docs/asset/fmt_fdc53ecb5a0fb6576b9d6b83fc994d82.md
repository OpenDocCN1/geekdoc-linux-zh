
| `sub age {` | | |
| `my $Person = shift;` | | |
| `if (@_) {` | | |
| `$Person->{AGE} = shift;` | | |
| `} return $Person->{AGE}; }` | 该类中的其余子程序都是可以调用以执行特定操作的方法 |
| `sub position {` | | |
| `my $Person = shift;` | | |
| `if (@_) {` | | |
| `$Person->{POSITION} = shift;` | | |
| `} return $Person->{POSITION}; }` | | |

# 426 Perl：初学者指南

之前的代码列表是包文件（package file），它包含了我们在本节中使用的示例类。

你在包中看到的第一个内容是它的名称。我们给类起的名称是 `Record`。程序中使用类名称是为了将该类的功能整合到该程序中。当我们查看实际使用该类的示例程序时，将具体看到这是如何实现的。

文件的第二行包含 `1;`。包含此行是为了当类在程序中被调用使用时，过程将会成功，因为包含类的模块返回了一个真值（在本例中为 1）。当你读到程序本身时，你将更好地理解我们的意思。

该类的下部分从第三行开始，是一个名为 `new` 的子程序。这就是它调用的该类的构造函数。此方法（或子程序）在被调用时会创建一个新对象。这个新对象拥有构造函数分配给它的所有属性。这个方法之所以被称为构造函数，并不是因为它的名称，而是因为它所包含的功能。`my` 函数在 Perl 中有特殊含义，我们会在“封装”（encapsulation）章节中详细讨论。此构造函数创建了一个哈希的引用，该哈希包含三个键：`NAME`、`AGE` 和 `POSITION`。你在这里看到的另一个函数对你来说可能是陌生的 `bless()`。该函数在我们查看使用该类的示例程序后进行介绍。该方法的最后一行返回新创建的对象。

该类中最后三个方法中的每一个都设计为对已创建的对象执行特殊功能。正因如此，我们可以将其称为对象方法（object methods）。

查看第一个对象方法——`name`，你可以看到它的目的是设置对象哈希的名称字段并返回它的新名称。如果没有指定要设置的名称，它也会简单地返回对象的名称。

## 注意

记住，`@_` 是分配给子程序的自动变量。 `if (@_)` 实际上意味着如果向此方法传递了任何内容，则执行某些操作。此外，`shift()` 函数也作用于当前默认数组，如果没有传递新名称，则数组中的最后一个名称将被移出并作为名称返回。

# 第 13 模块：高级特性与概念

该类中的最后两个方法与我们刚刚讨论的那个相似，因此我们不会对它们进行非常详细的阐述。

现在你已经看到了一个示例类，让我们来看一个使用该类的程序：

```
这是 use 语句，告诉程序
它将使用来自 Record 类的功能
```

```perl
#!/usr/bin/perl
use Record;
$Person = Record->new();
$Person->name("Donald");
$Person->age(26);
$Person->position("Engineer");
$name = $Person->name;
$age = $Person->age;
$position = $Person->position;
push @ostorage, $Person;
print "$name is a $position and he or she is $age years old.\n";
```

![](img/2070407c4a70134aab89572f10d21e60_450_0.png)

![](img/2070407c4a70134aab89572f10d21e60_450_1.png)

![](img/2070407c4a70134aab89572f10d21e60_450_2.png)

![](img/2070407c4a70134aab89572f10d21e60_450_3.png)

![](img/2070407c4a70134aab89572f10d21e60_450_4.png)

![](img/2070407c4a70134aab89572f10d21e60_450_5.png)

![](img/2070407c4a70134aab89572f10d21e60_450_6.png)

之前的程序示例（使用类创建对象）的输出如图所示。

之前的程序被用来创建对象，但它是做到的呢？关键在于 `bless()` 函数。该函数告诉解释器它刚刚构造的内容可以作为对象使用。表达式“可以作为对象使用”简单意味着执行某些任务创建的方法现在可以被调用

## 一 分钟训练

* 在类或包中

* `bless()`

* 定义对象行为的类中的方法

# 451 Perl：初学者指南

OOP 带来的的另一个重要概念是继承。不，你不会收到任何意外的金额来自

# 430 | Perl: 入学者指南

```perl
$person->{AGE} = shift;
}
return $person->{AGE};

sub position {
my $person = shift;
if (@_) {
$person->{POSITION} = shift;
}
return $person->{POSITION};
}
```

如你所见，此类中唯一添加的内容是使用了 `@ISA` 语句。

现在让我们来看看新的 `workweek` 类，它包含了 `Record` 类将继承的新功能。

```perl
package workweek;
1;
sub hours {
my $person = shift;
if (@_) {
$person->{HOURS} = shift;
}
return $person->{HOURS};
}
sub overtime {
my $person = shift;
if (@_) {
$person->{OVERTIME} = shift;
}
return $person->{OVERTIME};
}
```

现在让我们来看看使用这些新函数的程序。注意通过 `use` 语句包含的唯一类是 `Record` 类。

# 模块 13：高级特性与概念 | 431

```perl
#!/usr/bin/perl 这是一个 use 语句，告诉程序它将使用来自 Record 类的功能
```

```perl
$employee1 = Record->new();
$employee->name("Donald");
$employee->age(26);
$employee->position("Engineer");
$employee->hours(40);
$employee->overtime(12); 这些是从 workweek 类继承的两个新函数
$name = $employee->name;
$age = $employee->age;
$position = $employee->position;
$hours = $employee->hours;
$overtime = $employee->overtime;
push @storage, $employee;
print "Name is a $position and he or she is $age years old.\n";
print "He or she worked $hours regular hours and $overtime \n";
print "Hours of overtime this week \n";
```

上一个使用继承类创建对象的编程示例的输出，见此插图。

![](img/2070407c4a70134aab89572f10d21e60_454_0.png)

这涵盖了继承，现在，我们转向多态。

# 多态

多态是一个思想，即方法可以根据调用它的对象类型执行不同的操作。这种思想经常被 C++ 程序员使用，他们需要方法对不同对象做出不同的反应。一个很好的例子是，假设你有一个 `shift` 方法，它存在于两个不同的类中——一个用于手动挡，另一个用于自动挡——设计用于改变从汽车、卡车到割草机的任何设备的挡位。此方法需要根据车辆是自动挡还是手动挡做出不同的反应。多态意味着语言可以在运行时选择任一种方法，而不会因为类型差异产生任何问题。

![](img/2070407c4a70134aab89572f10d21e60_455_0.png)

# 1分钟训练

- 使用什么函数来创建继承？

- 使用什么函数来保留特定于封闭块的数据？

现在让我们进入下一节，我们将讨论 PerlScript 及其用途。

# PerlScript

PerlScript 是我们 ActiveState 的朋友们开发的一种技术，是 ActivePerl 发行版的一部分。其核心，PerlScript 是一个用于解释和执行 Perl 脚本和程序的解释引擎。但它与 Perl 解释器不同，因为它包含了扩展，允许这些 Perl 脚本在 Windows 环境中原生执行。

- `Use()` 和 `@ISA`

- `my()`
