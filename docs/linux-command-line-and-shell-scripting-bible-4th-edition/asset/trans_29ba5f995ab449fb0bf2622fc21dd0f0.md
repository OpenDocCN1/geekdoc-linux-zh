
data31<-->data32<-->data33

`FIELDWIDTHS` 变量允许你在不使用字段分隔符的情况下读取记录。在某些应用程序中，数据不使用字段分隔符，而是放置在记录内的特定列中。在这些情况下，你必须将 `FIELDWIDTHS` 变量设置为与记录中数据的布局相匹配。

设置 `FIELDWIDTHS` 变量后，gawk 会忽略 `FS`，并根据提供的字段宽度大小计算数据字段。下面是一个使用字段宽度而非字段分隔符的示例：

```
$ cat data1b
1005.3247596.37
115-2.349194.00
05810.1298100.1
$ gawk 'BEGIN{FIELDWIDTHS="3 5 2 5"}{print $1,$2,$3,$4}'
data1b
100 5.324 75 96.37
115 -2.34 91 94.00
058 10.12 98 100.1
$
```

`FIELDWIDTHS` 变量定义了四个数据字段，gawk 会相应地解析数据记录。每个记录中的数字字符串会根据定义的字段宽度值进行拆分。

> **警告**
>
> 重要的是要记住，一旦设置了 FIELDWIDTHS 变量，这些值必须保持恒定。此方法无法适应可变长度的数据字段。

`RS` 和 `ORS` 变量定义了你的 gawk 程序如何处理数据流中的记录。默认情况下，gawk 将 `RS` 和 `ORS` 变量设置为换行符。默认的 `RS` 变量值表明输入数据流中的每一行新文本都是一个新的记录。

有时你会遇到数据字段分布在数据流多行中的情况。一个经典的例子是包含地址和电话号码的数据，每一项都在单独的一行上：

```
Ima Test
123 Main Street
Chicago, IL 60601
(312) 555-1234
```

如果你尝试使用默认的 $FS 和 $RS 变量值来读取这些数据，gawk 会将每一行读取为独立的记录，并将记录中的每个空格解释为字段分隔符。这并不是你预期的结果。

为了解决这个问题，你需要将 FS 变量设置为换行符。这表明数据流中的每一行都是一个独立的字段，并且该行上的所有数据都属于该数据字段。

然而，这样做时，你不知道新记录从哪里开始。为了解决这个问题，请将 RS 变量设置为空字符串，并在数据流中的数据记录之间留一个空行。gawk 程序将把每个空行解释为记录分隔符。

下面是使用此技术的示例：

```
$ cat data2
Ima Test
123 Main Street
Chicago, IL 60601
(312) 555-1234

Frank Tester
456 Oak Street
Indianapolis, IN 46201
(317) 555-9876

Haley Example
4231 Elm Street
Detroit, MI 48201
(313) 555-4938
$ gawk 'BEGIN{FS="\n"; RS=""} {print $1, $4}' data2
Ima Test (312) 555-1234
Frank Tester (317) 555-9876
Haley Example (313) 555-4938
$
```

完美——gawk 程序将文件中的每一行解释为数据字段，将空行解释为记录分隔符。

# 数据变量

除了字段和记录分隔符变量外，`gawk` 还提供了一些其他内置变量，帮助你了解数据的情况并从 shell 环境中提取信息。表 22.2 展示了 `gawk` 中的其他内置变量。

| **变量** | **描述** |
|---|---|
| ARGC | 存在的命令行参数数量。 |
| ARGIND | 当前正在处理的文件在 ARGV 中的索引。 |
| ARGV | 命令行参数的数组。 |
| CONVFMT | 数字的转换格式（参见 printf 语句）。默认值为 %.6g。 |
| ENVIRON | 当前 shell 环境变量及其值的关联数组。 |
| ERRNO | 如果读取或关闭输入文件时发生错误，则为系统错误。 |
| FILENAME | 用于 `gawk` 程序输入的数据文件名。 |
| FNR | 数据文件中的当前记录编号。 |
| IGNORECASE | 如果设置为非零值，忽略在 `gawk` 命令中使用的字符串中字符的大小写。 |
| NF | 数据文件中数据字段的总数。 |
| NR | 处理的输入记录数量。 |
| OFMT | 显示数字的输出格式。默认为 %.6g，这将以较短的形式显示值，即使用小数点或科学计数法，最多使用六位小数。 |
| RLENGTH | 在 match 函数中匹配的 substring 的长度。 |
| RSTART | 在 match 函数中匹配的 substring 的起始索引。 |

**表 22.2 更多的 gawk 内置变量**

```
$ gawk 'BEGIN{print ARGC,ARGV[1]}' data1
2 data1
$
```

ARGC 变量表明命令行上有两个参数。这包括 gawk 命令和 data1 参数（请记住，程序脚本不计入参数）。ARGV 数组从索引 0 开始，代表命令。第一个数组值是 gawk 命令之后的第一个命令行参数。

> 请注意，与 shell 变量不同，当你在脚本中引用 gawk 变量时，不需要在变量名前面加美元符号。

ENVIRON 变量对你来说可能有点奇怪。它使用关联数组来获取 shell 环境变量。关联数组使用文本作为数组索引值，而不是数值。

数组索引中的文本是 shell 环境变量。数组的值是 shell 环境变量的值。下面是一个示例：

```
$ gawk '
> BEGIN{
> print ENVIRON["HOME"]
> print ENVIRON["PATH"]
> }'
/home/rich
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin/
$
```

`ENVIRON["HOME"]` 变量从 shell 中获取 HOME 环境变量的值。同样，`ENVIRON["PATH"]` 变量获取 PATH 环境变量的值。你可以使用这种技术从 shell 中获取任何环境变量的值，以便在 *gawk* 程序中使用。

*FNR*、*NF* 和 *NR* 变量在你试图跟踪 *gawk* 程序中的数据字段和记录时非常有用。有时你处于一种不知道记录中确切有多少数据字段的情况。*NF* 变量允许你指定记录中的最后一个数据字段，而无需知道其位置：

```
$ gawk 'BEGIN{FS=";"; OFS=""} {print $1,$NF}' /etc/passwd
root::/bin/bash
daemon:/usr/sbin/nologin
bin:/usr/sbin/nologin
sys:/usr/sbin/nologin
sync:/bin/sync
games:/usr/sbin/nologin
man:/usr/sbin/nologin
...
rich:/bin/bash
$
```

*NF* 变量包含数据文件中最后一个数据字段的数值。然后你可以通过在其前面加上美元符号将其用作数据字段变量。

*FNR* 和 *NR* 变量彼此相似，但略有不同。*FNR* 变量包含当前数据文件中已处理的记录数。*NR* 变量包含已处理的总记录数。让我们看几个例子来了解这种区别：

```
$ gawk 'BEGIN{FS=","}{print $1,"FNR="FNR}' data1 data1
data11 FNR=1
data21 FNR=2
data31 FNR=3
data11 FNR=1
data21 FNR=2
data31 FNR=3
$
```

在这个示例中，`gawk` 程序命令行定义了两个输入文件。（它指定了同一个输入文件两次。）脚本打印第一个数据字段值以及 `FNR` 变量的当前值。请注意，当 `gawk` 程序处理第二个数据文件时，`FNR` 的值重置为 1。

现在，让我们添加 `NR` 变量，看看会产生什么结果：

```
$ gawk '
> BEGIN {FS=","}
> {print $1, "FNR="FNR, "NR="NR}
> END{print "There were",NR,"records processed"}' data1 data1
data11 FNR=1 NR=1
data21 FNR=2 NR=2
data31 FNR=3 NR=3
data11 FNR=1 NR=4
data21 FNR=2 NR=5
data31 FNR=3 NR=6
There were 6 records processed
$
```

当 `gawk` 处理第二个数据文件时，`FNR` 变量的值被重置，但 `NR` 变量保持其对第二个数据文件的计数。结论是，如果你只使用一个数据文件作为输入，`FNR` 和 `NR` 的值将是相同的。如果你使用多个数据文件作为输入，`FNR` 的值将为每个数据文件重置，而 `NR` 的值将在所有数据文件中保持计数。

# 注意

> 你会注意到，在使用 `gawk` 时，`gawk` 脚本通常会变得比你的 shell 脚本的其余部分更大。在本章的示例中，为了简单起见，我们只是直接从命令行运行 `gawk` 脚本，利用 shell 的多行功能。当你在 shell 脚本中使用 `gawk` 时，你应该将不同的 `gawk` 命令放在单独的行上。这样做会让你更容易阅读和跟踪，而不是试图将所有内容挤在 shell 脚本的一行中。此外，如果你发现自己在不同的 shell 脚本中使用相同的 `gawk` 脚本，请记得

