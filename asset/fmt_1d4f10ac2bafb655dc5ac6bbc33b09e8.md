
在原始 `awk` 开发之后，出现了其他版本。其他版本包括 `[gawk]`，它是 `awk` 的 GNU 版本；`[mawk]`，它是 `awk` 的一个更快的重写。我将专注于原始 `awk`，因为它存在时间最长，并包含在你正在使用的任何 UNIX 版本中。简单来说，这些都是为了增加改进构想而开发的更新版本。尽管如此，涵盖 `awk` 的主题也适用于新版本。

下表包含你可能想要学习的命令选项，用于比移动输出列更详细的数据处理。

| 命令 | 选项 | 说明 |
| - | - | - |
| `awk` | | |
| | `d` | 删除 |
| | `g` | 全局替换模式空间为保持空间。 |
| | `n` | 除非通过 `p` 选项指示，否则不打印此行。 |
| | `p` | 覆盖 `n` 选项。 |
| | `s` | 替换行的第一个出现处。 |

## ROBERT B. FAY

`awk` 并不真正适合处理大型或复杂的任务。由于 `awk` 是一种解释型语言，`awk` 脚本需要相应的二进制文件来运行。这意味着基本上你无法编译 `awk` 脚本后，然后在一个没有包含 `awk` 二进制程序的系统上单独运行它。与编译后的代码相比，`awk` 脚本的运行速度较慢，因为每次运行 `awk` 脚本时，操作系统都会调用 `awk` 二进制文件对脚本进行解释。然而，正如我所说的，编译代码与解释型脚本在计算机处理时间上的差异是巨大的，但对人类来说，这种差异是可以忽略不计的。你可能甚至不会注意到脚本正在被读取。大多数情况下，执行 `awk` 脚本的响应在命令行提示符应该是瞬时的。如果处理时间差异对你来说是个问题，你可以购买第三方应用程序来编译并加速处理时间，但 `awk` 是随 UNIX 操作系统免费提供的。

虽然我最常用的任务是快速的数据处理，但 `awk` 实际上可以用于更复杂的任务，例如创建小型数据库以及对包含数值数据的文件进行数学运算。`awk` 执行函数的机制足够简单，熟悉 BASIC 或 C 等编程语言的人应该可以轻松学会。如果你以前从未用过任何编程语言，只需观察以下这些单行示例即可弄清楚 `awk` 能够执行哪些单独函数，然后继续学习数据库部分提到的更复杂的函数。你很快就能搞懂的。

## 命令行示例（单行命令）

从命令行使用 `awk` 对文本文件进行简单操作非常容易。假设我有一个名为 `coins` 的文件，它描述了一组硬币收藏。文件中的每行都包含以下信息：硬币的矿物；以盎司为单位的硬币重量、铸造日期、产地以及对硬币的描述。

#### 后续 awk 示例的示例文件

| 矿物 | 重量（盎司） | 日期 | 国家 |  |
| :--- | :--- | :--- | :--- | :--- |
| gold | 1 | 1986 | USA | 美鹰币 |
| silver | 10 | 1981 | USA | 银锭 |
| gold | 1 | 1984 | 瑞士 | 金锭 |
| gold | 1 | 1979 | RSA | 克拉朗金币 |
| gold | 0.1 | 1986 | PRC | 熊猫币 |
| silver | 1 | 1986 | USA | 自由一美元币 |
| gold | 0.25 | 1986 | USA | 自由五美元币 |
| gold | 0.25 | 1987 | USA | 宪法五美元币 |
| gold | 1 | 1988 | Canada | 枫叶金币 |

通过以下方式调用 `awk` 来列出所有金币：

```bash
#awk '/gold/' coins
```

前面的语法告诉 `awk` 在文件中搜索包含字符串 `"gold"` 的文本行，并将其打印出来。结果如下：

gold 1 1986 USA American Eagle

gold 1 1984 Switzerland Ingot

gold 1 1979 RSA Krugerrand

gold 0.1 1986 PRC Panda 

gold 0.25 1986 USA Liberty Five Dollar Piece

gold 0.25 1987 USA Constitution Five Dollar Piece

gold 1 1988 Canada Maple Leaf

这种在文件中搜索内容的操作很容易通过 `grep` 或 `find` 等其他 UNIX 命令完成，所以你可能会问自己为什么要学习如何使用 `awk`。虽然 `grep` 和 `find` 确实能找到文件中的金币，但 `awk` 能做的事情远不止于找到目标并显示找到的内容。例如，假设我对 `coins` 文件中的所有信息感兴趣，只想知道硬币的描述。通过 `awk`，我可以轻松地跳过我不需要的信息。要实现这一点，我只需要重新运行之前的 `awk` 语法，并为我想要打印的列添加数值变量。在这种情况下，我知道描述字段包含一到四个部分数据（单词），并从文件的第 5 列开始。请记住，对于文件中那些只有一个或两个单词描述的行，`awk` 将直接忽略缺失的列或将它们打印为空格。无论哪种方式，对你来说看起来是一样的。因此，我会按如下修改之前的语法，包含第 5 到第 8 列：

```bash
#awk '/gold/ {print $5, $6, $7, $8}' coins
```

新的输出将如下：

American Eagle

Ingot

Krugerrand

Panda

Liberty Five Dollar Piece

Constitution Five Dollar Piece

Maple Leaf

下面的示例展示了 `awk` 脚本中最简单的语法形式：

```bash
#awk <search pattern> {<program actions>} filename
```

`awk` 二进制文件会在输入文件中搜索每个包含搜索模式的行。对于找到的每个符合搜索标准的行，`awk` 然后会执行指定的动作。在这个示例中，动作被指定为 `{print $5, $6, $7, $8}`，因此 `awk` 打印第 5 到第 8 列数据，在 `coins` 文件中就是描述。`print` 语句的目的是只显示第 5 到第 8 列。前面的带有数字列标识符的 `$` 将其标识为字段变量，它通过其 `[index]` 存储每行文本中的单词。

对字符串执行的操作。因此，我们可以对日期字段进行算术比较。

下一个示例打印集合中硬币的数量。更准确地说，该逻辑确定了文件中有多少行或记录。

```
#awk 'END {print NR,"coins"}' coins
```

这一行 `awk` 脚本的结果是： 9 coins。

在本示例中，第一个新项是 `END` 语句。为了解释这一点，我必须将 `awk` 程序的通用形式扩展为：

```
#awk 'BEGIN {<initializations>}'
```

```
<search pattern> {program actions}>
```

```
<search pattern> {program actions}>
```

```
END {<final actions>}
```

`BEGIN` 子句在 `awk` 开始扫描输入文件之前执行任何所需的初始化操作。`awk` 程序的后续主体由一系列搜索模式组成，每个模式都有其自己的程序动作。`awk` 程序会针对每个搜索模式扫描输入文件的每一行，并对找到的每个字符串执行相应的动作。一旦文件扫描完成，可以使用 `END` 子句来执行任何所需的最终动作。

因此，由于所有这些示例都在统计文件中记录的数量，该示例并没有对输入行执行任何处理。整个示例只是扫描文件并执行一个最终动作：打印文件中的行数，这是由 `NR` 变量提供的。`NR` 变量代表“记录数”（number of records）。`NR` 是 `awk` 的预定义变量之一。还有其他变量；例如，变量 `NF` 给每行字段的数量。

如果当前金价为每盎司475 美元，我想计算硬币集中金币的大致总价值，我可以如下所示执行 `awk` 脚本：

```
#awk '/gold/ {ounces += $2} END {print "value = " $475*ounces"} coins
```

这一行 `awk` 脚本的结果是：value = $2185

在本示例中，`ounces` 是一个用户定义的变量。在 `awk` 中可以使用可以使用任何字符字符串作为变量名，只要该名称不与 `awk` 中具有特定含义的字符串冲突（例如 `print` 或 `NF`）。作为字符串处理的变量被初始化为空字符串，因此不需要手动将值设为空。同样，数值变量将被初始化为零。因此，对硬币文件的第二列执行 `ounces += $2` 的程序动作如下：

```
{ounces += $2}
```

上一行将硬币文件中每行匹配行的硬币重量累加到 `ounces` 变量中。`+=` 运算符是以下表达式的简写方式：

```
{ounces = ounces + $2}
```

该 `awk` 脚本的下一个也是最后一个动作是使用以下语法计算并打印硬币文件中金币的价值：

```
END { print "value = " $475*ounces"}
```

唯一值得注意的是，两个 `print` 参数（即字面量 `"value = \$"` 和表达式 `"475*ounces"`）之间是用空格分隔的，而不是逗号。这在输出时将这两个参数连接在一起，在美元符号和硬币的数值值之间没有任何空格。

#### 程序示例（包含单行示例中的逻辑）

之前的每个单行示例都显示了一段用于显示硬币文件信息的程序逻辑。然而，如果将 `awk` 作为程序而不是在命令行中使用它，它可以一次性提取所有信息。以下显示了如何使用 `awk` 在单个程序中执行所有的单行命令行逻辑。

```
#awk -f <awk program file name>
```

## UNIX 从入门到精通

以下摘要报告是硬币瓦片 `awk` 程序的一种可能的输出格式解决方案：

硬币收藏摘要报告：

金币：nn

金币重量：nn.nn

金币价值：n,nn,nn

银币：nn

银币重量：nn.nn

银币价值：n,nn,nn

总数：nn

收藏价值：n,nn,nn

以下 `awk` 程序生成了这些信息：

## 这是一个用于汇总硬币收藏的 awk 程序。

```
/gold/ { num_gold++; wt_gold += $2 } # 金币重量。
/silver/ { num_silver++; wt_silver += $2 } # 银币重量。
END { val_gold = 475 * wt_gold; # 计算金币价值。
val_silver = 15 * wt_silver; # 计算银币价值。
total = val_gold + val_silver;
print "Coin Collection Summary Report:"; # 打印报告头。
printf("\n");
printf(" Gold pieces: %%d\n", num_gold);
printf(" Weight of gold pieces: %%5.2f\n", wt_gold);
printf(" Value of gold pieces: %%7.2f\n", val_gold);
printf("\n");

printf(" Silver pieces: %%2d\n", num_silver);
printf(" Weight of silver pieces: %%5.2f\n", wt_silver);
printf(" Value of silver pieces: %%7.2f\n", val_silver);
printf("\n");

printf(" Total number of pieces: %%2d\n", NR);
printf(" Value of collection: %%7.2f\n", total); }
```
