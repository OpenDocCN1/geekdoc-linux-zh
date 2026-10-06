
你将看到如下输出：

```
field1 field2 field3
```

你可以在以下示例中看到：

```
$ cat datal
data11,data12,data13,data14,data15
data21,data22,data23,data24,data25
data31,data32,data33,data34,data35
$ awk 'BEGIN(FS="*") {print $1,$2,$3}' datal
data11 data12 data13
data21 data22 data23
data31 data32 data33
$
```

`print` 命令会自动将 `OFS` 变量的值放在输出中每个数据字段之间。通过设置 `OFS` 变量，你可以使用任何字符串来分隔输出中的数据字段：

```
$ awk 'BEGIN(FS=""; OFS="") {print $1,$2,$3}' datal
data11-data12-data13
data21-data22-data23
data31-data32-data33
$ awk 'BEGIN(FS="="; OFS="--") {print $1,$2,$3}' datal
data11--data12--data13
data21--data22--data23
data31--data32--data33
$ awk 'BEGIN(FS="<-"); OFS="-->") {print $1,$2,$3}' datal
data11-->data12-->data13
data21-->data22-->data23
data31-->data32-->data33
```

`FIELDWIDTHS` 变量允许你在不使用字段分隔符的情况下读取记录。在某些应用程序中，数据并不是使用字段分隔符，而是放置在记录中的特定列中。在这种情况下，你可以设置 `FIELDWIDTHS` 变量来匹配记录中数据的布局。

一旦设置了 `FIELDWIDTHS`，`awk` 就会忽略 `FS` 并根据提供的字段宽度大小计算数据字段。这是一个使用字段宽度代替字段分隔符的示例：

```
$ cat datalb
1005.3247596.37
115-2.349194.00
05810.1298100.1
$ awk 'BEGIN(FIELDWIDTHS="* 5 2 5*") {print $1,$2,$3,$4}' datalb
100 5234 75 963
```

# 第三部分 高级 Shell 脚本

115-2.34 91 94.00
058 10.12 98 100.1
$

`FIELDWIDTHS` 变量定义了四个数据字段，`gawk` 据此解析数据记录。每条记录中的数字字符串根据定义的字段宽度进行分割。

> 注意：请记住，一旦设置了 `FIELDWIDTHS` 变量，这些值必须保持不变。这种方法无法适应变长的数据字段。

`RS` 和 `ORS` 变量定义了你的 `gawk` 程序如何处理数据流中的记录。默认情况下，`gawk` 将 `RS` 和 `ORS` 变量设置为换行符。默认的 `RS` 变量值表示输入数据流中的每行新文本都是一条新记录。

有时，你会遇到数据字段跨越数据流中多行的情况。一个经典的例子是包含地址和电话号码的数据，每个项目单独占一行：

+ Riley Mullen
123 Main Street
Chicago, IL 60601
(312)555-1234

如果你尝试使用默认的 `FS` 和 `RS` 变量值读取这些数据，`gawk` 将将每一行视为一个独立的记录，并把记录中的每个空格解释为字段分隔符。这并不是你预期的结果。

要解决这个问题，你需要将 `FS` 变量设置为换行符。这表示数据流中的每行都是一个独立的字段，且行上的所有数据都属于该数据字段。然而，你面临不知道记录从何开始的问题。

要解决这个问题，将 `RS` 变量设置为空字符串，并在数据流的记录之间留一个空行。`gawk` 程序将把每个空行解释为记录分隔符。

```
$ cat data2
Riley Mullen
123 Main Street
Chicago, IL 60601
(312)555-1234

Frank Williams
456 Oak Street
Indianapolis, IN 46201
(317)555-9876

Haley Snell
4231 Elm Street
Detroit, MI 48201
(313)555-4938
$ gawk 'BEGIN(FS="\n"; RS="\n") {print $1,$4}' data2
Riley Mullen (312)555-1234
Frank Williams (317)555-9876
Haley Snell (313)555-4938
$
```

完美，`gawk` 程序将文件中的每一行解释为数据字段，并将空行解释为记录分隔符。

# 数据变量

除了字段和记录分隔符变量外，`gawk` 还提供了其他内置变量来帮助你了解数据的情况，表 19-2 显示了它们。

# 更多 gawk 内置变量

| 变量 | 描述 |
| :--- | :--- |
| ARGC | 命令行参数的数量。 |
| ARGV | 命令行参数数组。 |
| CONVFMT | 数字的转换格式。 |
| ERRNO | 上一次系统调用的错误代码。 |
| FILENAME | 当前输入文件的名称。 |
| FNR | 当前文件中处理的记录数。 |
| IGNORECASE | 如果为非零，字符串比较将不区分大小写。 |
| NF | 当前记录中的字段数量。 |
| OFS | 输出字段分隔符。 |
| ORS | 输出记录分隔符。 |
| RS | 输入记录分隔符。 |
| NR | 到此为止处理的记录总数。 |
| FS | 输入字段分隔符。 |
| RLENGTH | 上一次匹配的长度。 |
| RSTART | 上一次匹配的第一个字符的位置。 |
| FIELDWIDTHS | 定义字段宽度的字符串。 |

