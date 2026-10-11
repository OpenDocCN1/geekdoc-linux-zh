

C 语言、Java、PHP 等语言中的 switch 语句设计如下：

```perl
switch (expression) {
    case value1 :
        /* statements */
        break;
    case value2 :
        /* statements */
        break;
    case value3 :
        /* statements */
        break;
    default:
        /* statements */
        break;
}
```

虽然 switch/case 机制是大多数现代编程语言提供的常见控制结构，但在核心 Perl 中并不存在。你可以使用传统的 if/elsif/else 结构或创建带标签的代码块来实现相同的目标，如下所示。由于代码块（无论是否有标签）都相当于执行一次的循环，并且你可以通过 last、next 和 redo 等循环控制语句在该代码块内部使用这些控制，因此可以通过添加一个 do 块来创建一个伪 switch 语句，该块将执行一系列位于该代码块内部的命令（参见示例 7.32）。从 5.10.1 版本开始，Perl 6 的实验性功能可用，这使得创建 switch 风格语句的方式有了全新的变化，引入了新的 Perl 结构：given 和 when（参见示例 7.33 和 7.34）。

### 示例 7.32

（脚本）

```perl
1   my $hour=0;
2   while($hour < 24) {
3       SWITCH: {           # SWITCH 只是一个用户定义的标签
4           $hour < 12      && do { print "Good morning!\n";
                    last SWITCH;};
5
6           $hour == 12     && do { print "Lunch!\n";
                    last SWITCH;};
7
8           $hour > 12 && $hour <= 17     && do { print "Siesta time!\n";
                    last SWITCH;};
9
10          $hour > 17      && do { print "Good night. \n";
                    last SWITCH;};
11      } # End of block labeled SWITCH
12      $hour++;
13  } # End of loop block
```

### 示例 7.32（续）

（输出）

Good morning!
Good morning!
Good morning!

<输出继续>

Good morning!
Good morning!
Good morning!
Lunch!
Siesta time!
Siesta time!
Siesta time!
Siesta time!
Siesta time!
Good night.
Good night.
Good night.
Good night.
Good night.

### 解释

- 1. 在进入循环之前，`$hour` 标量被赋予初始值 `0`。
- 2. 评估 `while` 循环表达式。
- 3. 标签 `SWITCH` 标记了该代码块。它仅仅是一个标签，没有更多含义。
- 4. 进入代码块后，表达式被评估。该表达式读取为*如果* $hour *小于* 12...，则 `&&` 右侧的表达式被评估。这是一个 `do` 块。该代码块内的每条语句按顺序执行。最后一个被评估的语句的值被返回。
- 5. *last* 语句使控制分支跳转到标记为 `SWITCH` 的代码块末尾的第 8 行。
- 6. 如果前一条语句中的表达式评估为 `false`，则评估此语句。该表达式读取为*如果* $hour *等于* 12...
- 7. 如果前一条语句中的表达式评估为 `false`，则评估此语句。该表达式读取为*如果* $hour *大于* 12 *且小于或等于* 17...
- 8. 如果此语句为真，则执行 `do` 块。该表达式读取为*如果* $hour *大于* 17...
- 9. 每次完成循环遍历后，$hour 标量增加 1。

#### *switch* 特性 (*given*/*when*/*say*)

从 Perl 5.10.1 及更高版本开始，你可以使用实验性的 `switch` 特性，该特性启用了 Perl 6 的 *given*/*when* 结构，`use feature qw(switch);`

只要声明你的代码偏好在 Perl 5.10.1 或更高版本下运行，你就可以获得 `switch` 特性。例如：

```perl
use v5.10.1;
```

Perl 5 版本 18.0 的文档说明：

在 "switch" 特性下，Perl 获得了实验性的关键字 *given*、*when*、*default*、*continue* 和 *break*。从 Perl 5.18 开始，你可以使用 CORE:: 作为前缀来访问这些特性，而无需包含 use feature。在下面的示例中，每个特性都带有 CORE:: 标签：

```perl
CORE::given ( $some_variable) {   
CORE::when( /abc/ ) { statements }
```

（CORE 命名空间提供了访问 Perl 原始内置函数的功能。有关 CORE 的更多信息，请参阅 http://perldoc.perl.org/CORE.html。）

示例 7.33 中的代码可以重写为示例 7.34 所示的形式。

### 示例 7.33

```perl
use v5.10.1;  
for (1..24) {  
 when([1..11]) { say "Morning" }  
 when(12) { say "Lunch" }  
 when([13..17]) { say "Afternoon"}  
 default {say "Night"}  
}
```

（输出）

Morning
Morning
Morning
Morning
Morning
Morning
Morning
Morning
Morning
Morning
Morning
Lunch
Afternoon
Afternoon
Afternoon
Afternoon
Afternoon
Night
Night
Night
Night
Night
Night

### 解释

- 1. 使用至少 v5.10 版本以实现 `when` 特性。
- 2. for 循环将迭代 24 次。

### 示例 7.34

```perl
use feature qw(switch say);

my @weeks=("Sunday",
           "Monday",
           "Tuesday",
           "Wednesday",
           "Thursday",
           "Friday",
           "Saturday");

foreach $wday (0..6){
	$today=$weeks[$wday];
	given ($wday) {
		when([1..5]) { say "$today is Work, work, work" }
		when (6) {say "$today is Play!"}
		default { say "$today is Rest" }
	}
}
```

（输出）

Sunday is Rest
Monday is Work, work, work
Tuesday is Work, work, work
Wednesday is Work, work, work
Thursday is Work, work, work
Friday is Work, work, work
Saturday is Play

### 解释

- 1. 必须使用 Perl 5.10.1 或更高版本才能运行此脚本。使用 `feature` 模块来包含 `switch` 和 `say`。
- 2. 数组 `@weeks` 定义为星期几的列表。
- 3. `foreach` 循环遍历代表星期几的数字列表。
- 4. 每一天的星期都以字符串形式分配给 `$today`，例如 "Sunday"。
- 5. `given` 和 `when` 的参数处于标量上下文，且 `given` 将其主题值分配给 `$_` 变量。
- 6. `when` 的含义是：当 `given` 的值匹配 1 到 5 范围内的数字时，进入以下代码块并说它是星期几以及 Work, work, work。
- 7. 如果没有任何 `when` 表达式匹配 `given` 的值，则进入 `default` 代码块，类似于 `if/elsif` 条件结构中的 `else`。

## 7.5 你应该知道什么

- 1. 什么是控制结构？
- 2. 什么是代码块？
- 3. 在 *if* 或 *else* 结构之后，花括号是可选的吗？
- 4. *else* 代码块的目的是什么？
- 5. 哪种结构允许多个选择？
- 6. *while* 循环与 *do/while* 有何不同？与 *until* 呢？
- 7. 如何在到达外围代码块末尾之前跳出循环？
- 8. 什么是 *redo* 语句？它与 *next* 语句有何不同？
- 9. 为什么要使用 *next* 而不是 *redo* 来控制循环？
- 10. 什么是无限循环？
- 11. *foreach* 循环是如何工作的？
- 12. Perl 支持 *switch* 语句吗？什么是 *switch* 特性？
- 13. 什么是 *CORE::*？
- 14. *continue* 代码块用于什么目的？

## 7.6 接下来是什么？

在下一章中，你将学习使用正则表达式进行模式匹配，这是该语言最优秀且最重要的特性之一。你将学习表达式修饰符以及如何在文本字符串中查找模式。如果你熟悉 UNIX *grep* 或 *vi* 编辑器，你会看到 Perl 如何通过其匹配和替换运算符以及大量的正则表达式元字符来增强和简化模式匹配的功能。

# 练习 7
你的条件是什么？

- 1. 物理学家告诉我们，最低可能温度是绝对零度。绝对零度是 $-459.69$ 华氏度。
  - a. 接受用户输入：起始温度、结束温度和一个增量值（均为华氏度）。
  - b. 检查不良输入：低于绝对零度的温度以及小于起始温度的结束温度。如果检测到任一条件，程序将向 STDERR 发送消息。
  - c. 打印表头显示：华氏度 摄氏度。打印从起始到结束温度的所有值。使用循环机制。转换公式为 $C = (F - 32) / 1.8$。
- 2. 询问用户一组成绩，用空白字符分隔。这些成绩将存储在一个名为 `$input` 的字符串中。
  - a. 拆分字符串 `$input` 并创建一个数组。
  - b. 使用 foreach 循环获取所有成绩的总和。
  - c. 打印平均值。
- 3. 编写一个脚本，从一副牌中打印 10 张随机牌。
  - a. 该脚本将通过使用嵌套的 foreach 循环来构建一副 52 张的牌。
  - b. 外层循环将遍历由每种花色的牌组成的列表：梅花、方块、红心、黑桃。内层循环将遍历每种花色内每种牌类型的列表：A, 2 到 10, J, Q, K。每种花色的牌将分配给一个数组。
  - c. 将使用 `rand()` 函数从牌堆中获取随机牌。从牌堆中选出的 10 张牌中不应有重复。（提示：splice 函数通常用于删除重复的牌。）
- 4. 从数组 @colors 中移除 @drop 中的颜色；也就是说，从数组 @colors 中移除 pink 和 brown。
  ```perl
  @colors=qw(red green blue yellow pink purple brown);
  @drop=qw(pink brown);
  ```

