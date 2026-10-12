
### 解释

- 打印数字 0 到 10。
- 创建一个名为 `@alpha` 的数组，在数组中存储从 A 到 Z 范围内的所有大写字母。上下文是列表。打印该数组。
- 创建一个名为 `@letters` 的数组。范围运算符创建两个列表，一个是小写字母，另一个是大写字母。逗号将这两个列表连接起来。字母被赋值给 `@letters`，并打印该数组。
- 创建一个名为 `@n` 的数组，在 -5 和 20 之间范围内存储所有数字。打印该数组。

### 6.3.13 特殊字符串运算符和函数

可以对字符串执行多种操作。例如，连接运算符将两个字符串拼接在一起，而字符串重复运算符则按照指定次数重复连接其操作数的副本。

Perl 还支持一些用于操作字符串的特殊函数（见表 6.14）。`substr` 函数返回原始字符串中找到的子串，从原始字符串中的字符偏移量开始，到该偏移量右侧的字符位置数结束。`index` 函数返回在原始字符串中找到的子串的第一个字符的字符偏移量。`length` 函数返回给定表达式中的字符数。

**表 6.14 字符串操作**

| 示例 | 含义 |
| :--- | :--- |
| `$str1 . $str2` | 连接字符串 `$str1` 和 `$str2`。 |
| `$str1 x $num` | 重复 `$str1` `$num` 次。 |
| `substr($str1, $offset, $len)` | `$str1` 中位于 `$offset` 处、长度为 `$len` 字节的子串。 |
| `index($str1, $str2)` | 字符串 `$str2` 在字符串 `$str1` 中的字符偏移量。 |
| `length($str)` | 返回表达式 `$str` 的字符长度。 |
| `rindex($str, $substr, POSITION)` | 返回 `$substr` 在 `$str` 中最后一次出现的位置。如果指定了 `POSITION`，则从那里开始查找。如果未指定 `POSITION`，则从字符串末尾开始。 |
| `chr(NUMBER)` | 返回 Unicode 字符集中由该 `NUMBER` 表示的字符。例如，`chr(65)` 是字母 A，`chr(0x263a)` 是一个 Unicode 笑脸。 |
| `lc($str)` | 返回小写字符串。 |
| `uc($str)` | 返回大写字符串。 |

## 6.3 优先级和结合性

### 示例 6.26

```perl
use warnings;

my $x="pop";

my $y="corn";

my $z="*";

print $z x 10, "\n";  # Print 10 stars; repetition operator

print $x . $y, "\n";  # Concatenate "pop" and "corn"

print $z x 10, "\n";  # Print 10 stars

print uc($y), "\n";   # Convert string to uppercase
```

**输出**
```text
********

popcorn

********

CORN
```

### 解释

1. 标量 `$x` 被赋值 `pop`。
2. 标量 `$y` 被赋值 `corn`。
3. 标量 `$z` 被赋值 `*`。
4. 字符串 `*` 被重复 10 次并打印到 STDOUT。
5. `$x` 的值，即字符串 `pop`，与 `$y` 的值，即字符串 `corn`，被连接并打印到 STDOUT。
6. `$z` 的值（注：原文写的是 `$x`，但根据前一行和输出推断应为 `$z`），字符串 `*`，被重复 10 次并打印到 STDOUT。
7. `uc` 函数将字符串转换并返回为大写形式。`lc` 函数将把字符串转换为小写。

### 示例 6.27

```perl
use warnings;

my $line="Happy New Year";

print substr($line, 6, 3),"\n";  # Offset starts at zero

print index($line, "Year"),"\n";

print substr($line, index($line, "Year"))," \n";

substr($line, 0, 1)="Ethel";

print $line,"\n";

substr($line, -1, 1)="r to you!";

print $line,"\n";

print $line,"\n";

my $string="I'll eat a tomato tomorrow.\n";

print index($string, "tom"), "\n";
```

**输出**
```text
New

10

Year

Ethelppy New Year

Ethelppy New Yearr to you!

Ethelppy New Yearr to you!

18
```
