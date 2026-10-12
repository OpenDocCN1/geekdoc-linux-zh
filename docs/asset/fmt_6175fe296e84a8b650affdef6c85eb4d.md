
- 数组 `@pal` 被赋予了 `@names` 数组的元素 1、2 和 3。`@names` 数组的元素被选中并复制到 `@pal` 数组中。
- `@friend` 数组是通过从 `@names` 数组复制所有值并将它们赋值给 `@friend` 的元素 0、1 和 2 而创建的。

## 多维数组——列表的列表

多维数组有时被称为 *表格* 或 *矩阵*。它们由行和列组成，可以用多个下标表示。在二维数组中，第一个下标代表行，第二个下标代表列。

Perl 允许这种类型的数组，但它需要理解引用。我们将在第 12 章“这项工作是否需要引用？”中详细讨论这一点。

## 5.2.3 哈希——无序列表

*哈希*（在某些语言中称为关联数组、映射、表或字典）是一个由一对或多对标量（字符串或数字）组成的变量。哈希通常用于创建表格、复杂数据结构、查找文件或数组中的重复条目，或者创建 Perl 对象。我们将在第 14 章“祝福那些事物！（面向对象 Perl）”中详细介绍对象。

哈希（Hash）被定义为键/值对的无序列表，类似于一个表格，其中键位于左侧，与该键关联的值位于右侧。哈希的名称前缀为 `%`，键和值之间由 `=>` 分隔，该符号称为**胖逗号**或**双字符**运算符。

与数组是带有从 0 开始的数字索引的有序列表不同，哈希是带有字符串索引（称为键）的无序列表，这些索引是随机存储的。（当你打印出哈希时，不要期望看到的输出顺序与你输入的顺序一致！）

总结一下，哈希中的键必须是唯一的。除非键以数字开头，或者包含连字符、空格或特殊字符，否则键无需加引号。由于键本质上只是字符串，为了安全起见，给键加上引号（单引号或双引号）可以防止意外的副作用。这取决于你。与键关联的值可以比这里展示的更复杂，并且需要理解 Perl 引用。这些复杂类型将在第 12 章“这项工作是否需要引用？”中进行讨论。

```perl
my %pet = ("Name"  => "Sneaky",
           "Type"  => "cat",
           "Owner" => "Carol",
           "Color" => "yellow",
          );
```

因此，在这个例子中，名为 `$pet` 的哈希的键和值如下：

| 键    | 值      |
| :----- | :------- |
| "Name" | "Sneaky" |
| "Type" | "cat"    |
| "Owner"| "Carol"  |
| "Color"| "yellow" |

## 赋值

与标量和数组一样，在引用其元素之前，必须定义哈希变量。由于哈希由值对组成，并通过每对中的第一个元素进行索引，如果某一对中的某个元素缺失，键与其相应值的关联将受到影响。在分配键和值时，请确保键与其对应的值相关联。在对哈希进行索引时，使用花括号而不是方括号。

### 示例 5.18

```perl
1  my %seasons = ("Sp" => "Spring",
               "Su" => "Summer",
               "Fa" => "Fall",
               "Wi" => "Winter",
              );

2  my %days = ("Mon" => "Monday",
               "Tue" => "Tuesday",
               "Wed" => undef,
              );
3  $days{"Wed"} = "Wednesday";
```

### 解释

- 哈希 `%seasons` 被赋予了键和值。每个键和值由胖逗号 `=>` 分隔。字符串 `"Sp"` 是关键，其对应的值是 `"Spring"`，字符串 `"Su"` 是关键，其对应的值是 `"Summer"`，等等。如果键是单个单词，且不以数字开头或不包含空格，则无需给键加引号。
- 哈希 `%days` 被赋予了键和值。第三个键 `"Wed"` 被赋值 `undef`。`undef` 函数评估为一个未定义值；在这个例子中，它作为一个占位符，具有空值，稍后将被填充。
- 哈希的单个元素是标量。键 `"Wed"` 被赋字符串值 `"Wednesday"`。索引包含在花括号中。注意：键没有连续的编号顺序，且键值对可以包含数字和/或字符串。

**访问哈希值。** 在访问哈希的值时，下标或索引由包含在花括号中的键组成。Perl 提供了一组函数来列出哈希的键、值以及每个元素。由于用于存储键的内部哈希技术，Perl 不保证整个哈希打印时的顺序。

### 示例 5.19

```perl
(The Script)
    use warnings;
    # 将键和值分配给哈希
    my($department, $school);  # 声明变量
1  $department = (
2        "Eng"  =>  "Engineering",      # 键不需要引号
        "M"    =>  "Math",
        "S"    =>  "Science",
        "CS"   =>  "Computer Science",
        "Ed"   =>  "Education",
3      );
4  $department = $department{'M'};        # 使用单引号或双引号
5  $school = $department{'Ed'};
6  print "I work in the $department section\n";
7  print "Funds in the $school department are being cut.\n";
8  print qq{I'm currently enrolled in a $department{'CS'} course.\n};
9  print qq/The department hash looks like this:\n/;
10 print $department, "\n";  # 由于内部哈希机制，打印顺序不符合预期
    # order due to internal hashing
```

(Output)

```text
6 I work in the Math section
7 Funds in the Education department are being cut.
8 I'm currently enrolled in a Computer Science course.
9 The department hash looks like this:
10 EngEngineeringMScienceCSComputer ScienceEd
```

*注意：原始输出行 10 的 OCR 文本是乱码 `$SscienceCSComputer Science$EduMathEngEngineering`。根据标准的 Perl 哈希打印行为和上下文，这很可能代表连接的键和值。*

### 解释

- 哈希被称为 *%department*。它被赋予了键和值。
- 第一个键是字符串 `Eng`，与之关联的**值**是 `Engineering`。右括号和分号结束赋值。
- 标量 `$department` 被赋值 `Math`，这是与 `M` 键关联的值。用相同的名称为不同类型的变量命名有时令人困惑。在这个例子中，最好将 `$department` 更改为例如 `$subject` 或 `$course`。
- 标量 `$school` 被赋值 `Education`，这是与 `Ed` 键关联的值。打印带引号的字符串；标量 `$department` 被插值。
- 打印带引号的字符串；标量 `$school` 被插值。
- 打印带引号的字符串以及与 `CS` 键关联的值。
- 打印整个哈希，键和值紧密连接，且没有特定顺序。然而，一个键及其值始终会保持成对出现。

**哈希切片。** 哈希切片是哈希键的列表。哈希名称前缀为 `@` 符号，并被赋予一个包含在花括号中的键列表。哈希切片允许你在一条语句中访问一个或多个哈希元素，而不是通过循环。

### 示例 5.20

```perl
(The Script)

use warnings;
# 哈希切片

1 my %officer = ("name" => "Tom Savage",
                "rank" => "Colonel",
                "dob"  => "05/19/66"
               );

2 my @info=@officer{"name", "rank", "dob"};  # 哈希切片
3 print "@info\n";
4 @officer{"phone", "base"}=('730-123-4455', 'Camp Lejeune');
5 print %officer, "\n";
```

(Output)
