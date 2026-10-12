
## 解释

`$fh` 是一个词法作用域、用户定义的标量，用作文件句柄。`open` 函数将系统文件 `datebook` 附加到它并打开文件用于读取。如果 `open` 失败，因为文件 `datebook` 不存在，`die` 运算符将向屏幕打印，*Can't open datebook: No such file or directory.*

`while` 循环中的表达式是文件句柄 `$fh`，被尖括号包围。尖括号运算符用于读取输入，不是文件句柄名称的一部分。当循环开始时，读取的第一行将存储在 `$_` 标量变量中。（记住，`$_` 变量保存文件的每一行输入。）如果未到达文件末尾，循环将继续从文件中获取一行输入，执行第 3 和第 4 行语句，并继续直到到达文件末尾。

默认输入变量 `$_` 被隐式使用，用于保存从文件句柄读取的当前输入行。如果该行包含正则表达式 `Sir Lancelot`，则该行（存储在 `$_` 中）将被打印到 STDOUT。对于每次循环迭代，读取的下一行将存储在 `$_` 中并进行测试。

在循环结束时，控制将返回循环顶部（第 2 行），并从文件中读取下一行输入；此过程将持续直到所有行都被读取。

遍历完文件后，文件句柄被关闭。

## 文件句柄与用户定义的标量变量

除了默认的 `$_` 变量外，Perl 允许你创建自己的用户定义标量变量来保存来自文件的输入。

## 示例 10.5

```text
（文本文件：datebook）

Steve Blenheim

Betty Boop

Lori Gartz

Sir Lancelot

Norma Cord

Jon Deborah

Karen Enich
```

## 示例 10.5（续）

```perl
（脚本）

use warnings;

# Open a file with a filehandle

open(my $fh, "<", "datebook") || die "Can't open datebook: $!\n";

while(my $line = <$fh>) { # Each line, in turn, is assigned to $line

    print "$line" if $line =~ /Lori/i;

}

close($fh);
```

（输出）

```text
Lori Gartz
```

## 解释

-   1. `datebook` 文件被打开用于读取。
-   2. 当进入 `while` 循环时，从文件中读取一行并存储在标量 `$line` 中。
-   3. 如果标量 `$line` 的值包含模式 `Lori`，且 `Lori` 位于行首，则打印该值。
-   4. 当到达右花括号时，控制返回第 2 行，并从文件中读取另一行。当文件中没有更多行时，循环结束。
-   5. 通过关闭文件句柄来关闭文件。

## 将文件“吸入”数组

当将文件的输入赋值给数组时，Perl 将每一行（以 `\n` 结尾）作为数组的一个元素，“吸入”文件的每一行并将其添加到数组中，直到到达文件末尾。

## 示例 10.6

```perl
（脚本）

use warnings;

# Open a file with a filehandle

open(my $fh, "<", "datebook") || die "Can't open datebook: $!\n";

@lines = <$fh>;      # Contents of the entire file are printed

print "\nThe datebook file contains ", scalar @lines,

      " lines of text.\n";

close($fh);
```

（输出）

```text
The datebook file contains 7 lines of text.
```

## 解释

-   `datebook` 文件被打开用于读取。
-   通过文件句柄从文件中读取所有行，并赋值给 `@lines`，其中每行是数组的一个元素。换行符终止每个元素。
-   数组 `@lines` 被打印。
-   标量函数返回数组 `@lines` 中的元素数量（即行数）。

## 使用 map 从文件创建字段

你可以使用 `map` 函数结合 `split` 函数将输入拆分为数组的几个元素。

## 示例 10.7

```perl
5

{

    （脚本）

    use warnings;

    my (@lines, @fields, $field, $fh);

    # Map using a block

    1 open(my $fh, "<", "datebook.master") or die $!;

    2 @lines=<$fh>;

    3 @fields = map { split(":") } @lines;

    4 foreach $field (@fields){

    5 print $field, "\n";

    }
```

（输出）

```text
Sir Lancelot

837-835-8257

474 Camelot Boulevard, Bath, WY 28356

5/13/69

24500

Tommy Savage

408-724-0140

1222 Oxbow Court, Sunnyvale, CA 94087

5/19/66

34200

Yukio Takeshida

387-827-1095

13 Uno Lane, Asheville, NC 23556

7/1/29

57000

Vinh Tran

438-910-7449

8235 Maple Street, Wilmington, VT 29085

9/23/63

68900

}
```

## 说明

-   1 打开 `datebook` 主文件用于读取，使用 `$fh` 文件句柄。每一行由冒号分隔的字段组成，并以换行符结束。
-   2 读取文件的内容并赋值给 `@lines`。文件中的每一行都是该数组的一个元素。
-   3 `map` 函数使用了块格式。（在使用块格式时，不要在块的闭合符号后添加逗号。）`split` 函数按冒号拆分输入 `@lines`，生成一个列表，其中每个字段都成为数组的一个元素。
-   4 `foreach` 循环遍历该数组，依次将每个元素赋值给 `$field`。
-   5 `display` 展示了映射的结果。在映射之前，该行为：
  *Sir Lancelot/837-835-8257/474 Camelot Boulevard, Bath, WY 28356/513/69-24500*

### 使用 `read` 函数将文件一次性读入字符串

`read` 函数允许您读取指定数量的字符，并将其放入一个变量中。它返回读取的字符数。如果您知道文件的大小，可以将整个文件读入字符串，如下面的示例所示。

#### 语法

```
read FILEHANDLE, SCALAR, LENGTH, OFFSET
read FILEHANDLE, SCALAR, LENGTH
```

#### 示例 10.8

```
read($fh, $str, 100);
```

#### 示例 10.9

**（脚本）**
```perl
use warnings;

1 open(my $fh, "<", "datebook") or die;

2 $size = -s $fh;

3 read($fh, $buffer, $size);

4 @fields = split(/\n|:/, $buffer);

5 foreach $f (@fields){

6   print "$f\n";

7   print " \x35, "\n" if $f =~ /\d+$f/;
}
close $fh;
```

**（输出）**
```
Steve Blenheim

238-923-7366

95 Latham Lane, Easton, PA 83755

11/13/56

20300

---------------------------

Betty Boop

245-836-8357

635 Cutesy Lane, Hollywood, CA 91464

6/23/23

14500

---------------------------

Igor Chevsky

385-375-8395

3567 Populus Place, Caldwell, NJ 23875

6/18/68

23400
```
