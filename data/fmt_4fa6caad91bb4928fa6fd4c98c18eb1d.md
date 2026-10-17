
### d (删除) 命令

`d` (*删除*) 命令删除匹配的行。你可以使用模式 `/^$/` 删除空行（也就是说，空行是行首、行尾，中间什么都没有）。

```bash
$ head orders.txt | sed '/^$/d'
```

如果没有模式，你可以在 `d` 之前放置行号来删除特定行。例如，`1d` 删除第一行。

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

单独的 `d` 会删除所有行。

### 面向行的命令

有几个面向行的命令。`a` (*追加*) 命令在匹配行之后插入新文本。`i` (*插入*) 命令在匹配行之前插入文本。`c` (*更改*) 命令替换一组行。

要在 `Cedar Toy Chest` 之前插入标题 `DISCOUNTED ITEMS:`，请执行以下操作：

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

要将 `Bunk Bed`、`Queen Bed` 和 `Two-drawer Nightstand` 替换为 `Items deleted` 消息，可以使用：

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

`l` (*list*) 命令用于显示不可打印的字符。它显示字符的 `ASCII` 码或反斜杠序列。

```bash
$ printf "%s\015\t\004\n" "ABC" | sed -n "l"
ABC^M^I^D$
```

在这种情况下，`\015`（回车）显示为 `^M`，`\t` 制表符字符显示为 `^I`，`\n` 换行符显示为 `$` 和一个换行符。没有反斜杠等价物的字符 `\004` 显示为 `^D`。`A`、`B` 和 `C` 显示为它们本身。

### y (转换) 命令

`y` (*转换*) 命令是 *替换* 命令的一种特殊短格式。它执行一对一的字符替换。它本质上等同于单字符替换的一组操作。

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

`tr` 支持字符等价性。例如，要将名为 `FOREIGN_STRING` 的变量中的任何 `e` 类字符转换为普通 `e`，请使用：

```bash
$ printf "$FOREIGN_STRING" | tr "[eeé]" "e"
```

`-truncate-set-n`（或 `-t`）忽略第一个参数中没有第二个参数中匹配字符的任何字符。

`-complement`（或 `-c`）开关反转匹配的含义。第一个参数中的字符不会映射到第二个参数中，但不在第一个参数中的字符会被更改为指定的字符。

```bash
$ printf "%s\n" "The cow jumped over the moon" | tr -complement 'aeiou' '?'
???e???o??uu???o??e???e???e???moo??
```
