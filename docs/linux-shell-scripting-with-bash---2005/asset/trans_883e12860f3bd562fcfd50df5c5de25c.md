

直到所有行都被写完为止。如果一个文件比另一个文件短，缺失的行将使用空白行来填充。

`–delimiters (–d)` 开关是一个由一个或多个分隔符组成的列表，用于替代制表符（Tab）。如果 `paste` 命令需要的分隔符数量多于列表中提供的数量，它会循环使用该列表，如清单 11.9 所示。

### 清单 11.9 two\_columns.sh

```bash
#!/bin/bash
#
# two\_columns.sh

shopt -s -O nounset

declare -r ORDERS="orders.txt"
declare -r COLUMN1="column1.txt"
declare -r COLUMN2="column2.txt"
declare -i LINES

LINES=`wc -l < "$ORDERS"`
LINES=LINES/2

head -SLINES < "$ORDERS" > "$COLUMN1"

LINES=LINES+1
tail +$LINES < "$ORDERS" > "$COLUMN2"

paste -delimiters="|" "$COLUMN1" "$COLUMN2"

rm $COLUMN1
rm $COLUMN2
exit 0
```

运行此脚本后，`orders.txt` 的内容会被分隔成两列，由垂直线界定。

```bash
$ sh two_columns.sh

Birchwood China Hutch,475.99,1,756|Bar Stool,45.99,1,756
Bookcase Oak Veneer,205.99,1,756|Lawn Chair,55.99,1,756
Small Bookcase Oak Veneer,205.99,1,756|Rocking Chair,287.99,1,756
Reclining Chair,1599.99,1,757|Cedar Armoire,825.99,1,757
Bunk Bed,705.99,1,757|Mahogany Writing Desk,463.99,1,756
Queen Bed,925.99,1,757|Garden Bench,149.99,1,757
Two-drawer Nightstand,125.99,1,756|Walnut TV Stand,388.99,1,756
Cedar Toy Chest,65.99,1,757|Victorian-style Sofa,1225.99,1,757
Six-drawer Dresser,525.99,1,757|Chair - Rocking,287.99,1,757
Pine Round Table,375.99,1,757|Grandfather Clock,2045.99,1,756
```

假设你有一个名为 `order1.txt` 的文件，其中包含从 `orders.txt` 中分离出来的项目，字段在单行中以列表形式分隔。

```text
Birchwood China Hutch
475.99
1
756
```

`paste` 的 `--serial (-s)` 开关将每个文件的所有行粘贴到一个条目中，而不是逐个地将每个文件的一行合并到一行中。此开关将分散的字段重新组合成单行。

```bash
$ paste -serial -delimiter="" order1.txt
Birchwood China Hutch,475.99,1,756
```

要合并两个或多个文件的行，使这些行依次排列，请在使用 `-m` 开关时使用 `sort` 命令。

## 列

使用 `paste` 命令创建的列并不适用于所有场景。为了美观的显示效果，Linux 的 `column` 命令可以创建固定宽度的列。列的大小会根据 `COLUMNS` 环境变量确定的屏幕大小进行适配，或者使用 `-c` 开关适配特定的行宽。

```bash
$ column < orders.txt
Birchwood China Hutch,475.99,1,756     Bar Stool,45.99,1,756
Bookcase Oak Veneer,205.99,1,756      Lawn Chair,55.99,1,756
Small Bookcase Oak Veneer,205.99,1,756 Rocking Chair,287.99,1,757
Reclining Chair,1599.99,1,757         Cedar Armoire,825.99,1,757
Bunk Bed,705.99,1,757                Mahogany Writing Desk,463.99,1,756
Queen Bed,925.99,1,757                Garden Bench,149.99,1,757
Two-drawer Nightstand,125.99,1,756    Walnut TV Stand,388.99,1,756
Cedar Toy Chest,65.99,1,757           Victorian-style Sofa,1225.99,1,757
Six-drawer Dresser,525.99,1,757       Chair - Rocking,287.99,1,757
Pine Round Table,375.99,1,757         Grandfather Clock,2045.99,1,756
```

`-t` 开关通过由 `-s` 开关指定的字符分隔的条目创建表格。

```bash
$ column -s ', ' -t < orders.txt | head -5
Birchwood China Hutch        475.99  1  756
Bookcase Oak Veneer          205.99  1  756
Small Bookcase Oak Veneer    205.99  1  756
Reclining Chair             1599.99  1  757
Bunk Bed                     705.99  1  757
```

表格的填充顺序可以使用 `-x` 开关进行调换。

## 折叠

Linux 的 `fold` 命令确保一行不超过特定的字符数。如果一行过长，会插入回车符。`fold` 默认在 80 个字符处换行，但可以使用 `-width=n`（或 `-w`）开关在任何字符处进行折叠。`-spaces`（或 `-s`）开关会在最近的空间处折叠以保留单词。`-bytes`（或 `-b`）开关将制表符计为一个字符，而不是将其展开。

```bash
$ head -3 orders.txt | cut -d, -f 1
Birchwood China Hutch
Bookcase Oak Veneer
Small Bookcase Oak Veneer
$ head -3 orders.txt | cut -d, -f 1 | fold -width=10
Birchwood
China Hutch
h
Bookcase O
ak Veneer
Small Book
case Oak V
eneer
$ head -3 orders.txt | cut -d, -f 1 | fold -width=10 -spaces
Birchwood
China
Hutch
Bookcase
Oak Veneer
Small
Bookcase
Oak Veneer
```

## 连接

Linux 的 `join` 命令将两个文件合并在一起。`join` 每次检查每个文件的一行。如果行的某个段匹配，它们将被合并为一行。相同段只输出一个实例。假设文件已按相同顺序排序。

行段（或字段）是通过三个开关选择的。`-1` 开关选择第一个文件的字段号。`-2` 开关选择第二个文件的字段号。`-t` 开关指定分隔一个字段和另一个字段的那个字符。如果使用这些开关，`join` 会按空格分隔字段，并检查每行的第一个字段。

假设 `orders.txt` 文件中的数据被分成两个文件，一个包含定价信息（`orders1.txt`），另一个包含数量和账户信息（`orders2.txt`）。

要合并这两个文件，使用逗号作为字段分隔符，并将第一个文件的第 1 个字段与第二个文件的第 1 个字段进行比较。

```bash
$ join -1 1 -2 1 -t, orders1.txt orders2.txt
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
```

如果任一文件包含具有唯一字段的行，该字段将被丢弃。只有当两个文件中都找到匹配字段时，行才会被连接。要打印未配对的行，使用 `-a 1` 打印第一个文件中的唯一行，或使用 `-a 2` 打印第二个文件中的唯一行。这些行将按照它们在文件中出现的顺序打印。

匹配的方向可以使用 `-v` 开关反转。`-v 1` 打印第一个文件中的唯一行，`-v 2` 打印第二个文件中的唯一行。

当使用 `-ignore-case`（或 `-i`）开关时，测试是不区分大小写的。

可以使用 `-o`（output）开关重新排列字段。使用逗号分隔的字段列表来指定字段顺序。字段通过文件编号（1 或 2）、一个点号以及该文件中的字段号来指定。零是连接字段的简写形式。

```bash
$ join -1 1 -2 1 -t, -o '1.2,2.3,2.2,0' orders1.txt orders2.txt
475.99,756,1,Birchwood China Hutch
205.99,756,1,Bookcase Oak Veneer
205.99,756,1,Small Bookcase Oak Veneer
1599.99,757,1,Reclining Chair
705.99,757,1,Bunk Bed
```

## 合并

`merge` 命令执行三方文件合并。这通常用于合并来自两个不同源对同一个文件的修改。合并是按行进行的。如果存在冲突的修改，`merge` 会显示警告。

为了便于阅读，可以使用 `-L (label)` 开关为文件指定标题，而不是使用文件名来报告冲突。此开关可以重复使用三次，分别对应三个文件。

例如，假设有三组冰淇淋订单。原始订单集（`file1.txt`）如下所示：

```text
1 quart vanilla
2 quart chocolate
```

这些订单已被两个人修改。Barrie 商店现在有（`file2.txt`）以下内容：

```text
1 quart vanilla
1 quart strawberry
2 quart chocolate
```

而 Orillia（`file3.txt`）如下所示：

```text
1 quart vanilla
2 quart chocolate
4 quart butter almond
```

`merge` 命令将这三个文件重新组合成一个文件。

```bash
$ merge -L "Barrie Store" -L "Original Orders" -L "Orillia Store" file2.txt
file1.txt file3.txt
```

`file1.txt file3.txt` 将修改 `file2.txt`，使其包含：

```text
1 quart vanilla
1 quart strawberry
2 quart chocolate
4 quart butter almond
```

然而，如果 *butter almond* 和 *strawberry* 订单都被添加为第三行，`merge` 会报告冲突：

```bash
$ merge -L "Barrie Store" -L "Original Orders" -L "Orillia Store" file2.txt
file1.txt file3.txt
merge: warning: conflicts during merge
```

`file2.txt` 将包含冲突的详细信息：

```text
««««« Barrie Store
1 quart strawberry
=======
4 quart butter almond
>>>>>>> Orillia Store
```

如果没有合并问题，`merge` 返回零退出状态。

`-q (quiet)` 开关抑制冲突警告。`-p (print)` 将输出写入标准输出，而不是覆盖原始文件。`-3` 开关以 `diff3 -A` 格式报告冲突。

