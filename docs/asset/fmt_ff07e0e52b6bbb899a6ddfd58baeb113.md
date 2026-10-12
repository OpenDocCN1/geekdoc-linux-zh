
### 14.5.4 将 pod 文档翻译为文本

将 `pod` 命令翻译为终端屏幕文本最简单的方法是使用随 Perl 发行版提供的 `perldoc` 命令。它可能不在你的搜索路径中，但通常可以在 `perl` 下的 `bin` 目录中找到。以下命令将显示 `BigFloat.pm` 模块的所有文档：

```
perldoc Math::BigFloat
```

将 `pod` 指令翻译为文本的另一种方法是让 `pod` 解释器过滤模块，并创建一个输出文件来保存翻译后的文本。如果你不将输出重定向到文件，它将直接显示在屏幕上。

```
$ pod2text BigFloat.pm > BigFloat.Text

$ cat BigFloat.Text    (这是 pod 命令翻译成文本后的输出文件。)
```

NAME

`Math::BigFloat` - 任意长度浮点数学包

SYNOPSIS

`use Math::BigFloat;`

`$E = Math::BigFloat->new($string);`

```
$$->{fadd(NSTR)  return  NSTR

$$->{fsub(NSTR)  return  NSTR

$$->{fmul(NSTR, SCRN)  return  NSTR

$$->{fdvy(NSTR, [SCALE])  returns NSTR

$$->{fneq() return  NSTR

$$->{fabsl}  return  NSTR

$$->{icmp(NSTR)  return CODE

$$->{frond(SCALE)  return NSTR

$$->{frond(SCALE)  return NSTR

$$->{fnorm(l)  return (NSTR

$$->{fsqrt([SCALE])  return NSTR
```

加法

减法

乘法

除法至 SCALE 位

取负

绝对值

比较 undef, <=0, >=0

舍入至 SCALE 位数字

在 SCALE 位舍入

标准化

平方根至 SCALE 位

## 描述

如果你声明大型浮点数为

```
$float=newMath:'BigInt::2.123123123123123123123123123123';
```

数字格式

规范字符串的形式为 `(/+-])d+E[-+]:d+/`。输入值可以包含嵌入的空格。

错误返回 `'NaN'`

输入参数为“非数字”，或发生了除以零，或对负数开平方。

除法默认计算至

```
'max($div_scale, length(dividend)+length(divisor))' 位数字。这也用于默认的平方根精度。
```

## 缺陷

本模块的当前版本是真实版本的预研版，目前（截至 Perl 5.002）正在开发中。

## 作者

Mark Biggar

### 14.5.5 将 pod 文档翻译为 HTML

要创建 HTML 文档，请使用 `pod2html` 命令：

```
$ pod2html BigInt.pm Bigfloat.pm.html
```

`pod2html` 翻译器将创建一个名为 `Bigfloat.pm.html` 的文件。现在打开浏览器窗口，点击 文件 > 打开 或 `<Ctrl>+O`，并在 URL 位置框中通过 `file` 协议获取 `Bigfloat.pm.html`；例如，`<file:///yourdirectory path/Bigfloat.pm.html>`。10

![](img/8556abcb353c0991f12099420ec28735_537_0.png)

**图 14.7** 在浏览器中查看的普通旧式文档（Plain Old Documentation）。

## 14.6 使用 Perl 库中的对象

在第 13 章“模块化它、封装它，并将其发送到库！”中，我们首先查看了随此发行版 Perl 5.16 提供的标准 Perl 库。该库中包含许多 Perl 模块以及包含额外模块和子目录的子目录或文件夹。第 13 章中涵盖的示例涉及不需要了解 Perl 对象用法的模块。这些文件使用的是标准子例程，而不是方法。现在，既然你知道对象和方法在 Perl 中是如何使用的，接下来的示例将演示如何使用那些需要 OOP（面向对象编程）方法论的模块。

### 14.6.1 标准 Perl 库中的一个面向对象模块

以下模块 `BigFloat` 是一个面向对象模块，允许使用任意长度的浮点数。数字字符串的形式为 `/([+-]?d+\.?d*E[+\-]d?)/`。当返回 `NaN` 时，意味着输入了一个非数字，或者你试图除以零，或者你试图对负数开平方。`BigFloat` 使用 `overload` 模块，该模块允许你将 Perl 的内置运算符定义为方法，从而使运算符以新的方式工作。如以下示例所示，运算符是关键，分配的方法是值。（请参阅标准 Perl 库中的 `overload.pm`。）

```perl
# 示例 14-27
# （文件：BigFloat.pm）
package Math::BigFloat;
use Math::BigInt;
use Exporter;	# 只是为了让 use 开心
@ISA = (Exporter);
use overload
	'+	' => sub {new Math::BigFloat $add},
	'-	' => sub [new Math::BigFloat
		$_[2]? fsub($_[1],$_[0][0]) : fsub(${$_[0]},$_[1])},
	'-<=>' => sub {new Math::BigFloat
		$_[2]? fcmp($_[1],$_[0][0]) : fcmp(${$_[0]},$_[1])},
	'cmp	' => sub {new Math::BigFloat
		$_[2]? $_[1] cmp ${$_[0]} : (${$_[0]}) cmp ${$_[1]}},
	'*	' => sub {new Math::BigFloat $fmul},
	'/	' => sub {new Math::BigFloat
		$_[2]? scalar fdiv($_[1],${$_[0]}) :
		scalar fdiv(${$_[0]},$_[1])},
	'neg	' => sub {new Math::BigFloat $fneg},
	'abs	' => sub {new Math::BigFloat $fabs},
	qw(
		""	stringify
		"0" mummify	# 参数顺序无意义
	);
sub new {
	my ($class) = shift;
	my ($foo) = fnorm(shift);
	panic("Not a number initialized to Math::BigFloat"
		if $foo eq "NaN");
	bless \$foo, $class;
}
# <方法在此处继续。模块太长，无法在此列出>
```

# **示例 14.27**（续）

```perl
8  # Addition
   sub fadd ( #($fnum_str, $fnum_str) return $fnum_str
   {
       local($x,$y) = ($norm(_($[1]),$norm(_($[1])));
       if ($x eq 'NaN' || $y eq 'NaN') {
           'NaN';
       } else {
           local($x0, $xe) = split('E', $x);
           local($y0, $ye) = split('E', $y);
           ($x0, $xe, $y0, $ye) = ($y0, $ye, $x0, $xe) if ($xe < $ye);
           &norm(Math::BigInt->badd($y0, $x0, ('0' x ($xe-$ye)), $ye));
       }
   }
< Methods continue here>
# divisionbb
# $arje are dividend, divisor, scale (optional)
# result has at most max(scale, length(dividend),
# length(divisor)) digits
9 sub fdv   #($fnum_str, $fnum_str[, $scale]) return $fnum_str
{
    local($x, $y, $scale) = ($norm(_($[1]),
                          $norm(_($[1])_($[2]+1)));
    if ($x eq 'NaN' || $y eq 'NaN') {
```
