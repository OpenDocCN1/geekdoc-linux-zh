
![](img/3def70414996f811615f713b2077a154_272_0.png)

> 为了匹配 \, 你可以使用它本身进行转义：\\.

## 有用的正则表达式

表 16.3 提供了一些有用的正则表达式。

TABLE 16.3 一些有用的正则表达式

| 字符串类型 | 表达式 |
|---|---|
| 空行 | /^$/ |
| 整行 | /^.*$/ |
| 一个或多个空格 | / +/ |
| HTML（或 XML）标签集 | /<[^>]+>/ |
| 有效 URL | /[a-zA-Z][a-zA-Z0-9+.-]*:\/\/[a-zA-Z0-9][a-zA-Z0-9.-]*\.[a-zA-Z]{2,}/ |
| 格式化的美元金额 | /[$][0-9]+(\.[0-9]{2})?/ |

## 使用 sed

sed 是一个流编辑器，它对输入的每一行执行一组操作。这使得 sed 可以用作过滤器。sed 命令的基本语法是

`sed 'script' files`

这里 files 是一个或多个文件列表，而 script 是以下形式的一个或多个命令

`/pattern/ action`

其中 pattern 是一个正则表达式，action 是表 16.4 中给出的命令之一。如果省略 pattern，则对输入的每一行执行 action。

TABLE 16.4 sed 中可用的一些操作

| 操作 | 描述 |
|---|---|
| p | 打印该行（p as in print） |
| d | 删除该行（d as in delete） |
| s | 用另一个表达式替换一个表达式（s as in substitute） |

### 打印行

让我们从 sed 中最简单的功能开始——打印匹配表达式的行。

以下是一个小型水果市场的价格清单：

```
$ cat fruit_prices.txt
Fruit    Price/lbs
Banana   0.89
Peach    0.79
Kiwi     1.50
Pineapple 1.29
Apple    0.99
Mango    2.20
```

该文件列出了水果名称及其每磅价格。以下大多数示例假定该列表存储在文件 fruit_prices.txt 中。

首先，让我们打印出每磅价格低于 1 美元的水果清单。我们需要使用 sed 命令 p：

```
/pattern/p
```

这里 pattern 是一个正则表达式。

让我们尝试以下 sed 命令：

```
$ sed '/ 0.[0-9][0-9]$/p' fruit_prices.txt
```

这将打印出匹配以下表达式的所有行：

```
/ 0.[0-9][0-9]$/
```

该表达式指定只有以 0.89 和 0.99 等价格结尾的行才会被打印。开头的 0 确保以 2.20 或 10.10 等价格结尾的行不会被打印。

查看输出，

```
Fruit    Price/lbs
Banana   0.89
Banana   0.89
Peach    0.79
Peach    0.79
Kiwi     1.50
Pineapple 1.29
Apple    0.99
Apple    0.99
Mango    2.20
```

我们发现价格低于一美元的水果行被打印了两次，而价格高于一美元的水果行只打印了一次。这演示了 sed 的默认行为——它会将每一行输入打印到输出。为了避免这种行为，我们可以按如下方式指定 sed 的 -n 选项：

```
$ sed -n '/0.[0-9][0-9]$/p' fruit_prices.txt
```

这会将输出更改为如下：

```
Banana 0.89
Peach 0.79
Apple 0.99
```

### 删除行

假设我们用完了芒果，因此需要从列表中删除它们。为了完成此任务，我们可以使用 sed 命令 d：

```
/pattern/d
```

这里 pattern 是一个正则表达式。

我们可以使用以下 sed 命令：

```
$ sed '/^[Mm]ango/d' fruit_prices.txt
```

此命令删除以单词 mango 或 Mango 开头的行。输出如下：
Fruit Price/lbs
Banana 0.89
Peach 0.79
Kiwi 1.50
Pineapple 1.29
Apple 0.99

请注意，你不需要指定 sed 的 -n 选项即可获得正确的输出。p 命令告诉 sed 生成额外的输出，而 d 命令告诉 sed 修改常规输出。

虽然你已经修改了输出并验证其正确，但文件仍需要更新。你可以借助 shell 来完成：
$ mv fruit_prices.txt fruit_prices.txt.$$
$ sed '/^[Mm]ango/d' fruit_prices.txt.$$ > fruit_prices.txt
$ cat fruit_prices.txt

首先，我们将文件 fruit_prices.txt 重命名为 fruit_prices.txt.$$。请记住，变量 $$ 的值是当前 shell 的进程 ID。将 $$ 的值附加到文件末尾是创建具有唯一名称的临时文件的常用方法。

接下来，我们使用 sed 从临时文件中删除以 Mango 或 mango 开头的行。然后将 sed 命令的输出重定向到文件 fruit_prices.txt。

我们使用 cat 来显示更新是否成功：

| 水果 | 每磅价格 |
| Banana | 0.89 |
| Paech | 0.79 |
| Kiwi | 1.50 |
| Pineapple | 1.29 |
| Apple | 0.99 |

现在我们知道更新已正确完成，可以按如下方式删除临时文件：

```
$ rm fruit_prices.txt.$$
```

### 执行替换

到目前为止，你可能已经注意到我们文件中 Peach 被拼写为 Paech。我们可以使用 sed 命令 s 将 Paech 替换为正确的拼写来修复它：

```
/pattern1/s/pattern2/pattern3/
```

这里 pattern1、pattern2 和 pattern3 都是正则表达式。s 命令在匹配 pattern1 的任何行上将 pattern2 替换为 pattern3。

经常省略 pattern1，因此你会看到 s 命令如下使用：

```
s/pattern2/pattern3/
```

如果省略 pattern1，则对每一行输入执行 s 命令。

要修复 Paech 的拼写，可以使用以下 sed 命令：

```
$ sed 's/Paech/Peach/' fruit_prices.txt
```

现在输出类似于以下内容：

| 水果 | 每磅价格 |
| Banana | 0.89 |
| Peach | 0.79 |
| Kiwi | 1.50 |
| Pineapple | 1.29 |
| Apple | 0.99 |

你不需要指定 sed 的 -n 选项即可获得所需输出。s 命令与 d 命令类似，因为它告诉 sed 修改其正常输出。

### 常见错误

s 命令的一个常见错误是忘记一个或多个 / 字符。例如，假设你要发出以下命令：

```
$ sed 's/Peach/Peach' fruit_prices.txt
```

会产生类似以下的错误信息：

```
sed: command garbled: s/Peach/Peach
```

此错误信息说明了 sed 错误信息的标准样式：

```
sed: command garbled: command
```

sed 只是重复命令并说明它无法理解该命令。不会产生任何额外的错误信息或信息，因此你必须自己确定出了什么问题。

### 执行全局替换

在上一个示例中，你只需要修复单行上的一个拼写错误。有时你可能需要执行多次更正。例如，查看以下文件：

```
$ cat nash.txt
```

things that are equal to the same thing are equal to each other

在此文件中，单词 equal 被拼写为 eqal。你可以尝试使用 s 命令按如下方式修复它：

```
$ sed 's/eqal/equal/' nash.txt
```

things that are equal to the same thing are equal to each other

如你所见，第一个拼写错误已修复，但第二个未修复。这是 s 命令的默认行为：它在每一行上只执行一次替换。要执行多次替换，我们需要使用 g（表示 global）操作符：

/pattern1/s/pattern2/pattern3/g

g 操作符告诉 s 命令在匹配 pattern1 的行上将 pattern2 的每个出现替换为 pattern3。如果省略 pattern1，则对输入的每一行进行操作。

在这种情况下，我们需要按如下方式使用 g 操作符：

```
$ sed 's/eqal/equal/g' nash.txt
```

### 重用表达式的值

回到水果价格清单，假设我们想通过在每个价格前加上 $ 字符来更改列表以反映价格以美元计。通过使用以下表达式，我们可以匹配所有以价格结尾的行：

/ *([0-9][0-9]?)\.[0-9][0-9]/

问题在于用前面加上 $ 字符的价格替换现有价格。看起来我们需要为文件中的每一行编写单独的 s 命令。幸运的是，s 命令提供了 & 操作符，使我们能够在 pattern2 中重用来自 pattern1 的匹配字符串。

我们可以按如下方式重用匹配到的价格：

```
$ sed 's/ *([0-9][0-9]?)\.[0-9][0-9]/\$&/' fruit_prices.txt
Fruit      Price/lbs
Banana     $0.89
Peach      $0.79
Kiwi       $1.50
Pineapple  $1.29
Apple      $0.99
```

### 使用多个 sed 命令

从上一个示例可以看出，我们能够更新价格，但 Peach 仍然被拼写为 Paech。为了执行这两个更改，你必须对文件执行多个 sed 命令。这可以通过以下两种方式之一实现：

- 执行第一次更改然后更新文件。执行第二次更改命令然后更新文件。
- 使用单个 sed 命令执行两次更改，然后更新文件。

正如你所猜测的，第二种方法更高效且不易出错，因为文件只更新一次。你可以按如下方式使用单个 sed 命令执行两次更改：

```
sed -e 'cmd1'... -e 'cmdN' files
```

这里 cmd1 ... cmdN 是前面讨论的类型 sed 命令。每个命令都应用于 files 指定的每个文件中的每一行。

我们可以使用以下任一命令执行两次更新：

```
$ sed -e 's/Paech/Peach/' -e 's/ *([0-9][0-9]?)\.[0-9][0-9]/\$&/' fruit_prices.txt
$ sed -e 's/ *([0-9][0-9]?)\.[0-9][0-9]/\$&/' -e 's/Paech/Peach/' fruit_prices.txt
