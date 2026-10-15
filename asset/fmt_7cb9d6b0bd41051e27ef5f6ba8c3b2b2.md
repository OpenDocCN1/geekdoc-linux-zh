
有很多不同的 IDE，选择其中一个就像选择汽车一样——每个人都有自己的喜好。有些人认为少即是多，并乐于使用简单的文本编辑器工作，而另一些人则倾向于全功能 IDE 的所有花哨。为了快速高效地编写代码，你需要对你选择的任何环境得游自如——而且有很多环境供你选择！

## 快速启动迷你指南

那么，这些“快速启动迷你指南”的意图是什么？嗯，这一部分实际上是一种“备忘录”（cheat sheet）——我们开始编写代码时希望别人给我们的代码片段。许多人通过观察别人如何做来学习——编码也是如此。只要具备基本的智力、Google 以及对实现目标的强烈渴望，一切皆可能的。作为安全从业人员（区别于专业开发人员），我们并不总是要写出最整洁、最高效——它必须运行，并且应该现在就就绪！因此，有一个免责声明：如果你看到代码很糟糕（smelly），就随它去。但是，如果你看到无法运行的代码，请联系作者并戳他们的眼睛（用脏棍子！）。我们首先查看如何在 `PERL` 中执行基本操作——该章节将重复如何在 `C#` 中执行相同的操作。

## PERL 迷你指南

我们的 `PERL` 程序或脚本将在 `UNIX` 平台上执行，我们的“IDE”将是一个简单的文本编辑器和一个 shell。虽然脚本应该适用于任何版本的 `PERL`，但我们将使用 `5.8.5`。这些脚本在 `Active PERL` 上也可以正常运行。

## 基础程序结构、数据结构、条件和循环

这个 `PERL` 程序演示了程序结构、数据结构、条件和循环的基本用法。

```perl
#!/usr/bin/perl -w
use strict;

### 3 种基础数据结构
### 标量 (Scalars)
my $scalar_A = "A single thing";
my $scalar_B = 42;
print "Scalar A = [$scalar_A] and Scalar B = [$scalar_B]\n";

### 数组 (Arrays)
my $array_A = ("*","list","*","things");
my $array_B = (3,21,42);
print "Array A = [$array_A] and Array B = [$array_B]\n";

### 哈希数组 (Hash arrays)
my $hasharray;
$hasharray("Roelof") = "Temmingh";
$hasharray("Haroon") = "Meer";
$hasharray("Charl") = "van der Wat";

### 条件语句 (Conditionals)
my $int_A = 5;
my $int_B = 10;
my $int_ADD = $int_A + $int_B; # 15

# 比较数字标量
if ($int_A == $int_B) {
    print "Pigs can fly\n";
} else {
    print "Pigs cannot fly\n";
}

my $string_A = "This is a test";
my $string_B = "test";
my $string_ADD = $string_A.$string_B; # This is a testtest

# 比较字符串标量
if ($string_A eq $string_B) {
    print "Pigs should fly\n";
} else {
    print "Pigs should not fly\n";
}

# 比较不等于字符串
if ($string_A ne $string_B) {
    print "Birds can fly\n";
}

# 使用正则表达式比较字符串
if ($string_A =~ $string_B) {
    print "String_A contains the string String_B\n";
}

### 循环 (Loops)
# For 循环
my $index;
print "Red World - we've had this before: \n";
for ($index = 0; $index < 10; $index++) {
    print $index.\n";
}
print "\n";

# While 循环
print "And counting down...";
while ($index > 0) {
    print $index.\n";
    $index--;
}
print "\n";

### 枚举 (Enumeration)
# 分割 (Split)
my $array_of_words = split(/\s/, $scalar_A);
foreach my $single_word (@array_of_words) {
    print "$single_word\n";
}

# 哈希数组键 (Keys from hash array)
foreach my $ref (keys %hasharray) {
    print "Key = [$ref], Value = [$hasharray{$ref}]\n";
}
```

我们可以通过两种方式运行脚本——通过 `PERL` 解释器（图 7.2 中的第一个区块），或者通过设置可执行权限并运行（第二个区块）。

## PERL 脚本功能解释

```perl
#!/usr/bin/perl -w
use strict;

# basic.pl
my $scalar_A = "A single thing";
my $scalar_B = 42;
my $array_A = ("*","list","*","things");
my $array_B = (3,21,42);
my $hasharray;
$hasharray("Roelof") = "Temmingh";
$hasharray("Haroon") = "Meer";
$hasharray("Charl") = "van der Wat";

my $int_A = 5;
my $int_B = 10;
my $int_ADD = $int_A + $int_B;

if ($int_A == $int_B) {
    print "Pigs can fly\n";
} else {
    print "Pigs cannot fly\n";
}

my $string_A = "This is a test";
my $string_B = "test";
my $string_ADD = $string_A.$string_B;

if ($string_A eq $string_B) {
    print "Pigs should fly\n";
} else {
    print "Pigs should not fly\n";
}

if ($string_A ne $string_B) {
    print "Birds can fly\n";
}

if ($string_A =~ $string_B) {
    print "String_A contains the string String_B\n";
}

my $index;
print "Red World - we've had this before: \n";
for ($index = 0; $index < 10; $index++) {
    print $index.\n";
}
print "\n";

print "And counting down...";
while ($index > 0) {
    print $index.\n";
    $index--;
}
print "\n";

my $array_of_words = split(/\s/, $scalar_A);
foreach my $single_word (@array_of_words) {
    print "$single_word\n";
}

foreach my $ref (keys %hasharray) {
    print "Key = [$ref], Value = [$hasharray{$ref}]\n";
}
```

脚本开头的 `#!/usr/bin/perl` 告诉我们 `PERL` 解释器的位置——如果不确定，应该相应地更改脚本。`#!/usr/bin/perl` 中的 `-w` 确保我们不会写粗糙的代码。代码的其他部分自而易懂。

## 基础文件 IO 和子程序 (Subroutines)

以下脚本读取 `/etc/passwd` 文件，解析文件中的用户名，如果不是 `/sbin/nologin`，则将用户名写入命令行指定的指定文件中：
