
## 排序

Linux 的 `sort` 命令用于对单个文件或多个文件进行排序。文件可以显式命名，也可以通过重定向标准输入进行排序。`sort` 的开关与其他命令（如 `grep` 或 `cut`）完全不同。`sort` 是最后几个支持长选项版本的命令之一；因此，这里使用的是短选项。即便如此，常用选项的开关也与其他 Linux 命令不同。

要正确地对*文件*进行排序，`sort` 命令需要知道*排序键*，即每行中决定行顺序的字符。对于排序而言，键以外的任何内容都会被忽略。默认情况下，整行被视为键。

`-f`（*合并大小写*）开关执行不区分大小写的排序（不像许多其他 Linux 命令那样使用 `-i` 开关）。

```
$ sort -f orders.txt
Bar Stool,45.99,1,756
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Bunk Bed,705.99,1,757
Cedar Armoire,825.99,1,757
Cedar Toy Chest,65.99,1,757
Chair - Rocking,287.99,1,757
Garden Bench,149.99,1,757
Grandfather Clock,2045.99,1,756
Lawn Chair,55.99,1,756
Mahogany Writing Desk,463.99,1,756
Pine Round Table,375.99,1,757
Queen Bed,925.99,1,757
Reclining Chair,1599.99,1,757
Rocking Chair,287.99,1,757
Six-drawer Dresser,525.99,1,757
Small Bookcase Oak Veneer,205.99,1,756
Two-drawer Nightstand,125.99,1,757
Victorian-style Sofa,1225.99,1,757
Walnut TV Stand,388.99,1,756
```

`-r`（*反向*）开关会反转排序顺序。

```
$ head orders.txt | sort -f -r
Two-drawer Nightstand,125.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Six-drawer Dresser,525.99,1,757
Reclining Chair,1599.99,1,757
Queen Bed,925.99,1,757
Pine Round Table,375.99,1,757
Cedar Toy Chest,65.99,1,757
Bunk Bed,705.99,1,757
Bookcase Oak Veneer,205.99,1,756
Birchwood China Hutch,475.99,1,756
```

如果只使用行的一部分作为键，则使用 `-k`（*键*）开关来确定使用哪些字符。字段分隔符是任何一组空格或制表符字符，但你可以使用 `-t` 开关更改此设置。

要对订单文件的前 10 行按第二个及后续字段进行排序，请使用以下命令：

```
$ head orders.txt | sort -f -t, -k2
Two-drawer Nightstand, 125.99, 1,756
Reclining Chair, 1599.99, 1,757
Bookcase Oak Veneer, 205.99, 1,756
Small Bookcase Oak Veneer, 205.99, 1,756
Pine Round Table, 375.99, 1,757
Birchwood China Hutch, 475.99, 1,756
Six-drawer Dresser, 525.99, 1,757
Cedar Toy Chest, 65.99, 1,757
Bunk Bed, 705.99, 1,757
Queen Bed, 925.99, 1,757
```

键的位置后可以跟随结束位置，用逗号分隔。例如，要仅根据第二个字段进行排序，请使用键 `-k 2,2`。

如果字段编号包含小数部分，则它表示键开始的该字段中的字符。字段中的第一个字符为 1。第一个字段始终从行首开始。例如，要忽略第一个字符进行排序，请指定键从第一个字段的第二个字符开始。

```
$ head orders.txt | sort -f -k1.2
Reclining Chair, 1599.99, 1,757
Cedar Toy Chest, 65.99, 1,757
Pine Round Table, 375.99, 1,757
Birchwood China Hutch, 475.99, 1,756
Six-drawer Dresser, 525.99, 1,757
Small Bookcase Oak Veneer, 205.99, 1,756
Bookcase Oak Veneer, 205.99, 1,756
Queen Bed, 925.99, 1,757
Bunk Bed, 705.99, 1,757
Two-drawer Nightstand, 125.99, 1,756
```

有许多影响键解释方式的开关。`-b`（*空白*）开关表示键是带有前导空格的字符串，这些空格应被忽略。`-n`（*数值*）开关将键视为数字。此开关识别负号和十进制部分，但不识别正号。`-g`（*通用数字*）开关将键视为 C 语言浮点数表示法，允许无穷大、非数字（NaN）和科学计数法。此选项比 `-n` 慢。数值开关总是隐含 `-b`。`-d`（*电话簿*）开关在排序键中仅使用字母数字字符，忽略句点、连字符和其他标点符号。`-i`（*忽略不可打印字符*）开关在排序键中仅使用可打印字符。`-M`（*月份*）开关按月份名称缩写进行排序。

可以有多个排序键。可以通过将字符附加到键数量末尾来对单个键应用键解释开关，例如 `-k4,4M`，其含义为“按包含月份名称的第四个字段排序”。`-x` 和 `-f` 开关也可以这样使用。

作为一个更复杂的示例，以下 `sort` 命令按 `account` 号码反向排序，然后按 `product` 名称排序。该排序不区分大小写，并跳过前导空格：

```
$ head orders.txt | sort -t, -k4,4rn -k1,1fb
Bunk Bed,705.99,1,757
Cedar  Toy  Chest,65.99,1,757
Pine Round Table,375.99,1,757
Queen Bed,925.99,1,757
Reclining Chair,1599.99,1,757
Six-drawer Dresser,525.99,1,757
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Two-drawer Nightstand,125.99,1,756
```

对于长排序，`-c`（*仅检查*）开关在尝试排序之前检查文件是否需要排序。如果文件已排序，此开关返回状态码 `0`。

`sort` 开关的完整列表出现在参考部分。

## 字符编辑（`tr`）

Linux 的 `tr`（*转换*）命令替换或删除标准输入中的字符，并将结果写入标准输出。

`-d`（*删除*）开关删除特定字符。

```
$ printf "$a\n" 'The total is $234.45 US'
The total is $234.45 US
$ printf "$a\n" 'The total is $234.45 US' | tr -d '$'
The total is 234.45 US
```

字符范围表示为第一个字符、减号和最后一个字符。

```
$ printf "$a\n" 'The total is $234.45 US' | tr -d 'A-Z'
The total is $234.45
```

`tr` 支持 GNU 字符类。

```
$ printf "$a\n" 'The total is $234.45 US' | tr -d '[:upper:]'
The total is $234.45
```

在没有选项的情况下，`tr` 将一个字符集映射到另一个字符集。第一个参数中的第一个字符更改为第二个参数中的第一个字符。第一个参数中的第二个字符更改为第二个参数中的第二个字符。（以此类推。）

```
$ printf "$a\n" "The cow jumped over the moon" | tr 'aeiou' 'AEIOU'
The cOw jUmPed OvEr tHe mOoN
```

