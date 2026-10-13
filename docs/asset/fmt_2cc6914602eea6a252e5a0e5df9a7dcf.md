
现在输出看起来像

```
$ ./uris.sh uris.txt
uris.txt 4
```

如果你在系统上的输出看起来像以下内容：

```
uris.txt\c
4
```

而不是如图所示，你需要将脚本中的以下行替换：
`echo "$i\c"`
with the line:
`echo -n "$i"`

#### 内置变量

除了您可以定义的变量之外，`awk` 还预定义了几个变量。这些变量的完整列表在表 17.4 中给出。

表 17.4 `awk` 中的内置变量。

| 变量 | 描述 |
|---|---|
| `FILENAME` | 当前输入文件的名称。 不应更改此变量的值。 |
| `NR` | 输入文件中当前输入行或记录的编号。 不应更改此变量的值。 |
| `NF` | 当前行或记录中的字段数。 不应更改此变量的值。 |
| `OFS` | 输出字段分隔符（默认为空格）。 |
| `FS` | 输入字段分隔符（默认为空格和制表符）。 |
| `OFMT` | 数字的输出格式（默认为 `%.6g`）。 |
| `ORS` | 输出记录分隔符（默认为换行符）。 |
| `RS` | 输入记录分隔符（默认为换行符）。 |

#### 使用 `FILENAME` 和 `NR`

在前面的示例中，您使用 `shell` 打印输入文件的名称。通过结合使用变量 `FILENAME` 和 `BEGIN` 语句，您可以在 `awk` 中完成所有这些操作。顺便说一下，您可以使用 `END` 模式中的以下表达式更改之前的脚本，以打印文件中空白行的百分比：

`100*(x/NR)`

这里您使用变量 `NR`，它存储当前记录或行号。在 `END` 模式中，`NR` 的值是已处理的最后一行的行号，这与已处理的总行数相同。

经过这些更改后，脚本如下

```
#!/bin/sh

for i in $*
do

  if [ -f "$i" ] ; then

    awk '/^$/ { file=FILENAME; x+=1; next } END { printf "%s %d %.1f\n", file, x, (100*(x/NR)); }' "$i"

  else

    echo "ERROR: $i not a file." >&2

  fi

done
```

新的输出如下

```
$ ./urls.sh urls.txt

urls.txt    4    36.4
```

请注意，百分比以十进制或浮点值给出。 `awk` 将所有数字都视为浮点值，并从其所有计算中返回浮点值。

#### 更改输入字段分隔符

输入字段分隔符 `FS` 控制 `awk` 如何拆分输入行中的字段。`FS` 的默认值是字符串 `" "`（空格或制表符）。因为大多数命令，例如 `ls` 或 `ps`，使用空格或制表符分隔列，所以此默认值使您能够轻松地使用 `awk` 操作其输出。

您可以手动将 `FS` 设置为其他任何字符，以影响 `awk` 如何拆分输入行。通常，在查看系统数据库（如 `/etc/passwd`）时，会更改此字符。可用于更改 `FS` 的两种方法如下

- 在 `BEGIN` 模式中手动重置 `FS`
- 指定 `awk` 的 `-F` 选项

例如，让我们使用以下 `BEGIN` 模式将 `FS` 设置为冒号 (`:`)：

```
BEGIN { FS=":"; }
```

以下 `awk` 调用等同于 `BEGIN` 模式：

```
awk -F ':' '{ ... }'
```

输出类似于以下内容：

```
root /
daemon /
bin /usr/bin
sys /
adm /var/adm
ranga /home/ranga
```

#### 允许 `awk` 使用 Shell 变量

大多数 `awk` 版本没有直接访问 `shell` 设置的环境变量值的方法。为了使 `awk` 使用这些变量，您必须按如下方式在命令行上将它们转换为 `awk` 变量：

```
awk 'script' awkvar1=value awkvar2=value ... files
```

这里，`script` 是您想要执行的 `awk` 脚本。变量 `awkvar1`、`awkvar2` 等是您想要设置的 `awk` 变量的名称。通常，`files` 是一个文件列表。

假设您想要生成 `fruit_prices.txt` 中所有水果的列表，这些水果的数量小于或等于某个数字 `x`，其中 `x` 由用户提供。为了实现这一点，我们需要将用户提供的 `x` 的值传递给 `awk`。假设用户提供的值 `x` 可用在 `shell` 变量 `$1` 中，脚本如下

```
#!/bin/sh

NUMFRUIT="$1"

if [ -z "$NUMFRUIT" ] ; then NUMFRUIT=75 ; fi

awk '
$3 <= numfruit { print ; }
' numfruit="$NUMFRUIT" fruit_prices.txt
```

只有水果数量少于指定数量的行才会被打印。

假设此脚本名为 `reorder_user.sh` 且位于当前目录中，可以按如下方式执行：

```
$ ./reorder_user.sh 25
```

这会产生以下输出

```
Kiwi    $1.50    22
```

#### 流程控制

`awk` 中有三种主要的流程控制形式：

- `if` 语句
- `while` 语句
- `for` 语句

`if` 和 `while` 语句与 `shell` 中找到的语句相似；而 `for` 语句更接近 C 编程语言中的版本。

#### `if` 语句

`if` 语句使您能够在执行某些 `awk` 命令之前进行测试。

您在前面的示例中使用的模式匹配和表达式本质上是影响 `awk` 程序整体执行过程的 `if` 语句。

`if` 语句的基本语法如下

```
if (expr1) {
    action1
} else if (expr2) {
    action2
} else {
    action3
}
```

这里 `expr1` 和 `expr2` 是使用条件运算符创建的表达式。包围 `expr1` 和 `expr2` 的括号是必需的。操作——`action1`、`action2` 和 `action3`——可以是任何序列的有效 `awk` 命令。包围这些操作的括号仅在操作包含多个语句时才需要，但大多数程序员为了清晰和可维护性总是包含它们。

`else if` 和 `else` 语句都是可选的。`else if` 语句的数量没有限制。

执行过程如下：

- 1. 评估 `expr1`（`if`）。
- 2. 如果 `expr1` 为真，则执行 `action1` 并退出 `if` 语句。
- 3. 如果 `expr1` 为假，则评估 `expr2`（`else if`）。
- 4. 如果 `expr2` 为真，则执行 `action2` 并退出 `if` 语句。
- 5. 如果 `expr2` 为假，则执行 `action3` 并退出 `if` 语句（`else`）。

作为一个简单的示例，让我们编写一个脚本，打印 `fruit_prices.txt` 中的水果列表并突出显示以下条件：

- 项目的价格是否超过一美元
- 是否需要重新订购该项目

与前面的示例一样，您将使用 `*` 字符和字符串 `REORDER` 来突出显示这些条件。

使用 `if` 语句，脚本如下

```
#!/bin/sh

awk '{
    printf "%s\t$%s", $8;
    if ( $2 ~ /[3-9][0-9]*|[0-9][0-9]/ ) {
        printf " * ";
        if ( $3 > 75 ) {
            printf "REORDER\n";
        } else {
            printf "\n";
        }
    } else {
        if ( $3 < 75 ) {
            printf "REORDER\n";
        } else {
            printf "\n";
        }
    }
}' fruit_prices.txt ;
```

如果脚本名为 `reorder_expensive.sh` 且位于当前目录中，可以按如下方式调用：

```
$ ./reorder_expensive.sh
```

输出如下所示

```
Fruit    Price/lbs    Quantity
Banana   $0.89        100
Peach    $0.79        65       * REORDER
Kiwi     $1.50        22       * REORDER
Pineapple $1.29       35       * REORDER
Apple    $0.99        78
```

#### `while` 语句

`while` 语句在表达式为真时执行 `awk` 命令。基本语法如下

```
while (expr) {
    actions
}
```
