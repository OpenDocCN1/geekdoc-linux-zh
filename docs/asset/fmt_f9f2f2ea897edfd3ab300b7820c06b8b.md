
## 解释

1. `$fh` 是一个词法作用域的、用户自定义的文件句柄，Perl 将使用它将自身与外部的 `datebook` 文件关联起来。该文件以只读方式打开。
2. 进入 `while` 循环。从 `datebook` 文件中读取一行，并隐式地赋值给 `$_`。
3. 该行通过冒号进行分割，创建两个标量：`$name` 和 `$phone`。
4. 修饰性的 `if` 控制 `print` 函数将显示什么；在这个例子中，只有当 `$name` 完全等于字符串 `"Betty Boop"` 时，才会显示 `$name` 和 `$phone` 的值。

### 7.2.2 unless 修饰符

*除非*（*unless*）修饰符用于控制由两个表达式组成的简单语句。如果 *表达式1* 为假，则执行 *表达式2*。与 *if* 修饰符类似，*unless* 放置在语句的末尾。

#### 格式

`表达式2 unless 表达式1;`

## 示例 7.8

```perl

(脚本)

$x=5;

print $x unless $x == 6;

(输出)

5

```

## 示例 7.8（续）

```perl

(脚本)

use warnings;

open (my $fh, "datebook") or die $!;

while(<$fh>){

  (my $name,my $phone)=split(":", $_);

  print "$phone\n" unless $name eq "Betty Boop";

  }

close $fh;

(输出)

238-923-7366

385-375-8395

397-857-2735

548-834-2348

408-253-3122

< 这里打印更多号码>

```

## 解释

这个例子与上一个完全相同，只是没有使用 `if` 修饰符，而是使用了 `unless` 修饰符。`print` 函数显示所有名字不是 Betty Boop 的行。

### 7.3 使用循环进行重复

有时，您可能希望重复执行一条语句或一组语句，直到满足某个条件为止；例如，继续询问用户一个问题，直到他给出正确的回答；或者您可能想创建一个计时器，从 10 倒数到 0；或者您可能想修改列表中的每个项目，直到达到列表的末尾。这就是循环发挥作用的地方。它们被用来反复执行一段代码。Perl 的基本循环结构如下：

- `while`
- `until`
- `for`
- `foreach`

每个循环后面都跟着一个用大括号括起来的语句块。

#### 7.3.1 while 循环

`while` 语句会在 `while` 后面的控制表达式为真时执行该代码块。如果一个表达式求值为非零（真），则该表达式为真；`while(1)` 总是为真，会无限循环。如果一个表达式求值为零，则该表达式为假；`while(0)` 为假，永远不会循环。参见图 7.2。

![](img/8556abcb353c0991f12099420ec28735_220_0.png)

**图 7.2 while 循环的工作原理。**

#### 格式

`while (表达式) {代码块}`

## 示例 7.9

```perl

(脚本)

use warnings;

my $num=0;              # 初始化 $num

while ($num < 10){     # 测试表达式

        # 当表达式为假或 0 时循环退出

  print "$num ";

        $num++;           # 更新循环变量 $num；对 $num 进行自增

} 

print "\nOut of the loop.\n";

(输出)

0 1 2 3 4 5 6 7 8 9

Out of the loop.

```

## 解释

1. 标量 `$num` 被初始化。初始化在进入循环之前进行。
2. 评估测试表达式。如果结果为真，则执行大括号内的语句块。
3. 标量 `$num` 自增。如果不这样做，测试表达式将始终返回真值，循环将永远不会结束。

## 示例 7.10

```perl

(脚本)

use warnings;

my($count, $beers, $remain, $where);

$count=1;              # 初始化变量

$beers=10;

$remain=$beers;

$where="on the shelf";

while ($count <= $beers) {

      if ($remain == 1){print "$remain bottle of beer $where.\n"; }

      else {print "$remain bottles of beer $where.\n";}

      print "Take one down and pass it around.\n";

      print "Now ", $beers - $count , " bottles of beer $where!\n";

      $count++;

      $remain--;

      if ($count > 10){print "Party's over.\n";}

}

print "\n";

```

## 示例 7.10（续）

(输出)
10 bottles of beer on the shelf. Take one down and pass it around.
Now 9 bottles of beer on the shelf!
9 bottles of beer on the shelf. Take one down and pass it around.
Now 8 bottles of beer on the shelf!
8 bottles of beer on the shelf. Take one down and pass it around.
Now 7 bottles of beer on the shelf!
7 bottles of beer on the shelf. Take one down and pass it around.
Now 6 bottles of beer on the shelf!
6 bottles of beer on the shelf. Take one down and pass it around.
Now 5 bottles of beer on the shelf!
5 bottles of beer on the shelf. Take one down and pass it around.
Now 4 bottles of beer on the shelf!
4 bottles of beer on the shelf. Take one down and pass it around.
Now 3 bottles of beer on the shelf!
3 bottles of beer on the shelf. Take one down and pass it around.
Now 2 bottles of beer on the shelf!
2 bottles of beer on the shelf. Take one down and pass it around.
Now 1 bottle of beer on the shelf!
1 bottle of beer on the shelf. Take one down and pass it around.
Now 0 bottles of beer on the shelf!
Party's over.

## 解释

1. 标量 `$count`、`$beers`、`$remain` 和 `$where` 被初始化。
2. 进入 `while` 循环；测试并评估控制表达式。
3. 标量 `$count` 自增。
4. 标量 `$remain` 自减。
5. 当 `$count` 的值大于 10 时，打印这一行。

#### 7.3.2 until 循环

*until* 语句会在 *until* 后面的控制表达式为假时执行该代码块。当表达式求值为真时，循环退出。参见图 7.3。

![](img/8556abcb353c0991f12099420ec28735_222_0.png)

**图 7.3 until 循环的工作原理。**

#### 格式

`until (表达式) {代码块}`

## 示例 7.11

```perl

(脚本)

use warnings;

$num=0;                 # 初始化

until ($num == 10){

      # 测试表达式；当表达式为真或 1 时循环退出

    print "$num ";

    $num++;      # 更新循环变量 $num；对 $num 进行自增

}

print "\nOut of the loop.\n";

(输出)

0 1 2 3 4 5 6 7 8 9
```
