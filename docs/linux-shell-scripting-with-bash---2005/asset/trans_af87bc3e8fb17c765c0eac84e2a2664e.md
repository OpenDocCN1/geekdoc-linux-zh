
## 文件编辑 (sed)

Linux 的 **sed** (*流编辑器*) 命令对文本文件进行逐行更改。虽然名称中包含“编辑器”一词，但它并不是通常意义上的文本编辑器。你不能使用它交互式地修改文件。而 **grep** 命令是在文件中定位正则表达式模式，**sed** 命令则是在定位模式后，在发现模式的位置进行更改。

**sed** 的主要参数是一个由斜杠分隔的复杂四部分字符串。

```bash
$ sed "s/dog/canine/g" animale.txt
```

第一部分指示 **sed** 将执行何种编辑。第二部分是 **sed** 正在查找的字符模式。第三部分是要通过命令应用的字符模式。第四部分是编辑的范围（如果目标模式出现多次）。在此示例中，在 **sed** 表达式 “s/**dog**/canine/g” 中，**编辑** 命令是 **s**，要匹配的模式是 **dog**，要应用的模式是 **canine**，范围是 **g**。使用该表达式，**sed** 将把文件 **animale.txt** 中所有字符串 **dog** 的出现替换为 **canine**。

围绕 **sed** 表达式使用引号非常重要。许多对 shell 有特殊含义的字符对 **sed** 也有特殊含义。为了防止 shell 在 **sed** 有机会分析表达式之前解释这些字符，必须对表达式加上引号。

与 **grep** 类似，**sed** 使用正则表达式来描述模式。此外，Linux 版本的 **sed** 处理的行长度没有限制。

一些 **sed** 命令可以通过包含行号来操作特定行。也可以通过初始行和步进因子指定行号。**1-2** 从第 1 行开始搜索所有行，步长为 2。也就是说，它选择文件中的所有奇数行。可以通过第一行、逗号和最后一行指定地址范围。**1,10** 搜索前 10 行。末尾的感叹号会反转搜索的方向。**1,10!** 搜索除前 10 行以外的所有行。如果没有指定行，则搜索所有行。

### s (替换) 命令

**sed s** (*替换*) 命令将匹配的模式替换为新的文本。

要在订单文件的前 10 行中将单词 **Pine** 替换为 **Cedar**，请使用以下命令：

```bash
$ head order5.txt | sed 's/Pine/Cedar/g'
Birdwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Cedar Round Table,375.99,1,757

Pine Round Table becomes Cedar Round Table.
```

如果替换字符串为空，则会删除该模式的出现。

```bash
$ head orders.txt | sed 's/757//g'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,
Bunk Bed,705.99,2,
Queen Bed,925.99,1,
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,
Six-drawer Dresser,525.99,1,
Pine Round Table,375.99,1,
```

脱字符 (^) 表示行的开始。

```bash
$ head orders.txt | sed '/^Bunk/a DISCONTINUED - Bunk'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
DISCONTINUED - Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

可以使用 I (不区分大小写) 修饰符执行不区分大小写的测试。

```bash
$ head orders.txt | sed 's/BED/BED/Ig'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk BED,705.99,1,757
Queen BED,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

**sed** 支持 GNU 字符类。若要隐藏价格，请将所有数字替换为下划线。

```bash
$ head orders.txt | sed 's/[[:digit:]]/_/g'
Birchwood China Hutch,____,__-__-
Bookcase Oak Veneer,____,____'-__
Small Bookcase Oak Veneer,____,'__'__
Reclining Chair,_ . ' ' _
Bunk Bed, _ . ' ' _
Queen Bed, _ . ' ' _
Two-drawer Nightstand, _ . ' ' _
Cedar Toy Chest, _ . ' ' _
Six-drawer Dresser, _ . ' ' _
Pine Round Table, _ . ' '
```

### d (删除) 命令

**d** (*删除*) 命令删除匹配的行。你可以使用模式 `'/$'` 删除空行（也就是说，空行是行首、行尾，中间什么都没有）。

```bash
$ head orders.txt | sed '/^$/d'
```

如果没有模式，你可以在 d 之前放置行号来删除特定行。例如，`1d` 删除第一行。

```bash
$ head orders.txt | sed '1d'
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

单独的 d 会删除所有行。

### 面向行的命令

有几个面向行的命令。**a** (*追加*) 命令在匹配行之后插入新文本。**i** (*插入*) 命令在匹配行之前插入文本。**c** (*更改*) 命令替换一组行。

要在 Cedar Toy Chest 之前插入标题 DISCOUNTED ITEMS:，请执行以下操作：

```bash
$ head orders.txt | sed '/Cedar Toy Chest/i\
DISCOUNTED ITEMS:'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
DISCOUNTED ITEMS:
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

要将 Bunk Bed、Queen Bed 和 Two-drawer Nightstand 替换为 Items deleted 消息，可以使用：

```bash
$ head orders.txt | sed \
'/^Bunk Bed/;/^Two-drawer/c/\n<Items deleted>\n'
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
<Items deleted>
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

您必须在 *插入*、*追加* 和 *更改* 命令后跟随一个转义的行结束符。

### l (列表) 命令

**l** (*list*) 命令用于显示不可打印的字符。它显示字符的 ASCII 码或反斜杠序列。

```bash
$ printf "%s\015\t\004\n" "ABC" | sed -n "l"
ABC^M^I^D$
```

在这种情况下，`\015`（回车）显示为 `^M`，`\t` 制表符字符显示为 `^I`，`\n` 换行符显示为 `$` 和一个换行符。没有反斜杠等价物的字符 `\004` 显示为 `^D`。`A`、`B` 和 `C` 显示为它们本身。

### y (转换) 命令

**y** (*转换*) 命令是 *替换* 命令的一种特殊短格式。它执行一对一的字符替换。它本质上等同于单字符替换的一组操作。

例如，`y/a/b` 等同于 `s/a/b/`：

```bash
$ head orders.txt | sed "y/a/A/"
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
Queen Bed,925.99,1,757
Two-drawer Nightstand,125.99,1,756
Cedar Toy Chest,65.99,1,757
Six-drawer Dresser,525.99,1,757
Pine Round Table,375.99,1,757
```

然而，对于多字符模式，*转换* 将第一个模式的任何出现替换为第二个模式的第一个字符，第二个字符替换为第二个模式的第二个字符，依此类推。其工作方式类似于 `tr` 命令。

```bash
$ printf "%s\n" "order code B priority 1" | sed "y/B1/C2/"
order code C priority 2
```

## tr 命令参考

**tr** 支持字符等价性。例如，要将名为 FOREIGN_STRING 的变量中的任何 e 类字符转换为普通 e，请使用：

```bash
$ printf "$FOREIGN_STRING" | tr "[eeé]" "e"
```

**-truncate-set-n**（或 **-t**）忽略第一个参数中没有第二个参数中匹配字符的任何字符。

**-complement**（或 **-c**）开关反转匹配的含义。第一个参数中的字符不会映射到第二个参数中，但不在第一个参数中的字符会被更改为指定的字符。

```bash
$ printf "%s\n" "The cow jumped over the moon" | tr -complement 'aeiou' '?'
???e???o??uu???o??e???e???e???moo??
```

**-squeeze-repeats**（或 **-s**）开关将多个出现的字母减少为每个指定字母的单个字符：

```bash
$ printf "%s\n" "aaabbbccc" | tr -squeeze-repeats 'c'
aaabbbc
```

**tr** 最普遍的用途是将 MS-DOS 文本文件转换为 Unix 文本文件。DOS 文本文件具有回车符和换行符，而 Linux 仅使用换行符标记行尾。需要删除多余的回车符。

```bash
$ tr -d '\r' < dos.txt > linux.txt
```

Apple 文本文件使用回车符而不是换行符。**tr** 也可以通过替换回车符来处理这种情况。

```bash
$ tr '\r' '\n' < apple.txt > linux.txt
```

**tr** 识别的其他转义字符如下：

- `\o` — ASCII 八进制值 o（一到三个八进制数字）
- `\\` — 反斜杠
- `\a` — 可听蜂鸣声
- `\b` — 退格符
- `\f` — 换页符
- `\n` — 换行
- `\r` — 回车
- `\t` — 水平制表符
- `\v` — 垂直制表符

你可以使用接下来讨论的 **sed** 命令执行更复杂的文件编辑。

