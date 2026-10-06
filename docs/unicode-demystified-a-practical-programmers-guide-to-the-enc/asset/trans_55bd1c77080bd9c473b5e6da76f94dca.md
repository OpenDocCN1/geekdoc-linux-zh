

# 1328 sort

-b 选项导致 sort 将多个前导空格视为单个字段分隔符字符。如果你不使用此选项，sort 会将每个前导空格都视为排序字段中的一个字符，并将其纳入排序比较中。

你可以通过紧跟在选项 b、d、f、i、n 或 r 之后跟特定排序字段，来指定仅适用于该排序字段的选项。在这种情况下，你不能在这些选项前加连字符（-）。

当你指定了多个排序字段时，`sort` 将按照你于命令行上指定的顺序对它们进行检查。如果两行的第一个排序字段相同，`sort` 将检查第二个排序字段。如果这些也相同，`sort` 将查看第三个字段。此过程将持续到你指定的所有排序字段为止。如果所有排序字段都相同，`sort` 将检查整行。

如果你不使用任何选项或参数，`sort` 将对整行进行排序。

## 示例

本节中的示例演示了 `sort` 工具的一些功能和用法。示例假设列表文件位于工作目录：

```
$ cat list
```

| Tom Winstrom | 94201 |
| Janet Dempsey | 94111 |
| Alice MacLeod | 94114 |
| David Mack | 94114 |
| Toni Barnett | 95020 |
| Jack Cooper | 94072 |
| Richard MacDonald | 95510 |

该文件包含姓名和邮政编码列表。文件的每行包含三个字段：名、姓和邮政编码字段。为了使示例生效，请确保文件中所有的空白都是空格而不是制表符。

第一个示例演示了除了文件名外不带任何选项或参数的 `sort`。随后，`sort` 按行对文件进行排序。如果两行的字符相同，`sort` 将查看第二个字符以确定正确的排序顺序。如果第二个字符相同，`sort` 将查看第三个字符。此过程一直持续到 `sort` 找到两行之间不同的字符为止。如果行完全相同，哪一行排在前面并不重要。在这种情况下，`sort` 只需要检查每行的前三个字母（最多）。`sort` 工具显示了一个按名字字母顺序排列的列表：

```
$ sort list
```

| Alice MacLeod | 94114 |
| David Mack | 94114 |
| Jack Cooper | 94072 |
| Janet Dempsey | 94111 |
| Richard MacDonald | 95510 |
| Tom Winstrom | 94201 |
| Toni Barnett | 95020 |

你可以指示 `sort` 在比较时跳过任意数量的字段和字符。空白通常将一个字段与另一个字段分开。下一个示例按姓（第二个字段）对列表进行排序。`+1` 参数表示 `sort` 在开始比较之前跳过一个字段；`sort` 跳过了名字段。因为没有第二个指针，排序字段一直延伸到行尾。现在 `sort` 几乎是按姓的排序的，但出现了一个问题——

```
$ sort +1 list
Toni Barnett 95020
Jack Cooper 94072
Janet Dempsey 94111
Richard MacDonald 95510
Alice MacLeod 94114
David Mack 94114
Tom Winstrom 94201
```

在前面的示例中，MacLeod 排在 Mack 之前。在通过第三个字母（Mac）发现这两行的排序字段相同后，`sort` 将 L 放在 k 之前，因为它是按照 ASCII 字符编码顺序排列行的，在其中大写字母在小写字母之前。

- `-f` 选项使 `sort` 将大写字母和小写字母视为相等，并解决了 MacLeod 和 Mack 的问题：

```
$ sort -f +1 list
Toni Barnett 95020
Jack Cooper 94072
Janet Dempsey 94111
Richard MacDonald 95510
David Mack 94114
Alice MacLeod 94114
Tom Winstrom 94201
```

下一个示例尝试按第三个字段（邮政编码）对列表进行排序。随后，`sort` 并没有对数字进行排序，而是将最短的名字放在排序列表的前面，最长的姓放在最后。通过 `+2` 参数，`sort` 跳过了两个字段，并将第二个字段（姓）之后的空格视为排序字段的一部分。空格的 ASCII 值小于任何可打印字符，因此 `sort` 将前导空格最多的邮政编码放在前面，前导空格最少的邮政编码放在后面：

```
$ sort +2 list
David Mack 94114
Jack Cooper 94072
Tom Winstrom 94201
Toni Barnett 95020
Janet Dempsey 94111
Alice MacLeod 94114
Richard MacDonald 95510
```

`-b` 选项导致 `sort` 忽略前导空格。使用 `-b` 选项，邮政编码将按正确的顺序出现，如下。当 `sort` 确定 McLeod 和 Mack 的邮政编码相同时，它会比较整行，将 Alice McLeod 放在 David Mack 之前（因为 A 在 D 之前）：

```
$ sort -b +2 list
Jack Cooper 94072
Janet Dempsey 94111
Alice MacLeod 94114
David Mack 94114
Tom Winstrom 94201
Toni Barnett 95020
Richard MacDonald 95510
```

为了在邮政编码相同时按姓的字母顺序排序，你需要一个对姓字段进行第二次排序。下一个示例演示了如何通过指定第二个排序字段来实现这次排序，并使用 `-f` 选项来防止 Mack/MacLeod 问题再次出现：

```
$ sort -b -f +2 +1 list
Jack Cooper 94072
Janet Dempsey 94111
David Mack 94114
Alice MacLeod 94114
Tom Winstrom 94201
Toni Barnett 95020
Richard MacDonald 95510
```

`-f` 选项并没有解决 MacLeod 和 Mack 的问题，因为 `sort` 从不比较姓。当它确定 MacLeod 和 Mack 的邮政编码的最后两位相同时，它会从名字开始比较整行。这两行是按名字顺序排列的。下一个示例演示了如何按第一个字段、第二个、第三个字段进行排序。下一个示例演示了如何按第一个字段、第二个、第三个字段进行排序。下一个示例演示了如何按第一个字段、第二个、第三个字段进行排序。下一个示例演示了如何按第一个字段、第二个、第三个字段进行排序。下一个示例演示了如何按第一个字段、第二个、第三个字段进行排序。下一个示例演示了如何按第一个字段、第二个、第三个字段进行排序。下一个示例演示了如何按第一个字段、第二个、第三个字段进行排序。

