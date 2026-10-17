
$ -vn the grepfile ...这次更具体一点！

2:所以把灯关掉，

5:美丽的人鱼将在海中畅游，

-$

## 第 3 章 高级用户 UNIX 工具

```
用法: uniq -c [ 输入文件 [ 输出文件 ]]
```

`uniq` 是一个实用程序，它会显示输入文件，并将所有相邻的重复行合并为单次出现的重复行。如果未指定输入文件，则从标准输入读取。`-c` 选项会在每行前面加上该行出现的次数。如果指定了数字，则会忽略每行的前该数字个字段。

图 3.6
`uniq` 命令的描述。

这里有一个示例：

```
$ cat animals ...查看测试文件。
cat snake
monkey snake
dolphin elephant
dolphin elephant
goat elephant
pig pig
pig pig
monkey pig
$ uniq animals ...过滤掉相邻的重复行。
cat snake
monkey snake
dolphin elephant
goat elephant
pig pig
monkey pig
$ uniq -c animals ...显示行及其对应的计数。
1 cat snake
1 monkey snake
2 dolphin elephant
1 goat elephant
2 pig pig
1 monkey pig
$ uniq -l animals ...忽略每行的第一个字段。
cat snake
dolphin elephant
pig pig
$
```

## 排序文件：sort

`sort` 实用程序根据一个或多个排序字段按升序或降序对文件进行排序。它的工作方式如图 3.7 所示。单个字段按字典顺序排序。

### 排序文件：sort 89

```
用法: sort -tc -r { 排序字段-bfMn }* {文件名 }*
```

`sort` 是一个实用程序，根据指定的排序标准对一个多个文件进行排序。默认情况下，行按升序排序。`-r` 选项指定为降序。输入行通过空格或制表符拆分为字段。要指定不同的字段分隔符，请使用 `-t` 选项。默认情况下，执行排序时会考虑一行的所有字段。可以通过指定一个或多个排序字段来覆盖这一约定，这些字段的格式在本节的稍后部分描述。可以通过在排序字段后紧跟一个或多个选项来自定义单个排序字段。`-f` 选项使 `sort` 忽略字段的大小写。`-M` 选项按月份顺序对字段排序。`-n` 选项按数字顺序对字段排序。`-b` 选项忽略领先空格。

图 3.7

`sort` 命令的描述。

这意味着根据 ASCII 值比较相应的字符。（参见 "`man ascii`" 以获取所有字符及其对应值的列表。）这一约定的两个结果是：大写字母比其小写对应字母“小”，空格“小于”字母。在示例中，我使用默认排序规则按升序和降序对一个文本文件进行了排序：

```
$ cat sortfile ...列出要排序的文件
Jan Start chapter 3 10th
Jan Start chapter 1 30th
Jan Start chapter 5 23rd
Jan End chapter 3 23rd
Mar Start chapter 7 27
May End chapter 7 17th
Apr End Chapter 5 1
Feb End chapter 1 14 ...$ sortfile
Feb End chapter 1 14
Jan End chapter 3 23rd
Jan Start chapter 5 23rd
May End chapter 7 17th
Apr End Chapter 5 1
Jan Start chapter 1 30th
Mar Start chapter 7 27
Jan Start chapter 3 10th
$ sort -r sortfile ...按反序排序。
Jan Start chapter 3 10th
Mar Start chapter 7 27
Jan Start chapter 1 30th
Apr End Chapter 5 1 *
```

## 90 第 3 章 高级用户 UNIX 工具

```
may End chapter 7 17th
Jan Start chapter 5 23rd
Jan End chapter 3 23rd
Feb End chapter 1 14
$
```

要按特定字段进行排序，必须使用带有 `-` 前缀的指定排序字段编号，后跟带有 `+` 前缀的不包含在内的结束字段编号。字段编号从索引 0 开始。如果省略了结束字段编号，则起始字段之后的所有字段将包含在排序中。在下一个示例中，我按第一个字段（即 0 号）对前一个示例中的文本文件进行了排序：

```
$ sort +0 -1 sortfile ...按第一个字段排序。
Feb End chapter 1 14
Jan End chapter 3 23rd
Jan Start chapter 5 23rd
may End chapter 7 17th
Apr End chapter 5 1
Jan Start chapter 1 30th
Mar Start chapter 7 27
jan Start chapter 3 10th
$
```

注意，领先空格被计算为第一个字段的一部分，这导致了奇怪的排序序列。此外，我希望月份按正确的顺序排序，JanJan”在“Feb”之前，以此类推。`-b` 选项忽略领先空白，`-M` 选项按月份顺序排序。这里有一个可以工作的示例：

```
$ sort +0 -bM sortfile ...按第一个月份排序。
Jan End chapter 3 23rd
Jan Start chapter 5 23rd
Jan Start chapter 1 30th
jan Start chapter 3 10th
Feb End chapter 1 14
Mar Start chapter 7 27
Apr End chapter 5 1
may End chapter 7 17th
$
```

示例文本文件已按月份正确排序，但日期仍然是乱的。`sort` 实用程序允许你指定多个字段来处理这个问题。在示例中，我先按月份再按日期对文本排序。

## 91 第 3 章 高级用户 UNIX 工具

```
$ sort -tc -r { 排序字段-bfMn }* {文件名 }*
```

`sort` 是一个实用程序，根据指定的排序标准对一个多个文件进行排序。默认情况下，行按升序排序。`-r` 选项指定为降序。输入行通过空格或制表符拆分为字段。要指定不同的字段分隔符，请使用 `-t` 选项。默认情况下，执行排序时会考虑一行的所有字段。可以通过指定一个或多个排序字段来覆盖这一约定，这些字段的格式在本节的稍后部分描述。可以通过在排序字段后紧跟一个或多个选项来自定义单个排序字段。`-f` 选项使 `sort` 忽略字段的大小写。`-M` 选项按月份顺序对字段排序。`-n` 选项按数字顺序对字段排序。`-b` 选项忽略领先空格。

图 3.7

`sort` 命令的描述。

这意味着根据 ASCII 值比较相应的字符。（参见 "`man ascii`" 以获取所有字符及其对应值的列表。）这一约定的两个结果是：大写字母比其小写对应字母“小”，空格“小于”字母。在示例中，我使用默认排序规则按升序和降序对一个文本文件进行了排序：

```
$ cat sortfile ...列出要排序的文件
Jan Start chapter 3 10th
Jan Start chapter 1 30th
Jan Start chapter 5 23rd
Jan End chapter 3 23rd
Mar Start chapter 7 27
May End chapter 7 17th
Apr End Chapter 5 1
Feb End chapter 1 14 ...sortfile
Feb End chapter 1 14
Jan End chapter 3 23rd
Jan Start chapter 5 23rd
May End chapter 7 17th
Apr End Chapter 5 1
Jan Start chapter 1 30th
Mar Start chapter 7 27
Jan Start chapter 3 10th
$ sort -r sortfile ...按反序排序。
Jan Start chapter 3 10th
Mar Start chapter 7 27
Jan Start chapter 1 30th
Apr End Chapter 5 1 *
```

## 90 第 3 章 高级用户 UNIX 工具

```
may End chapter 7 17th
Jan Start chapter 5 23rd
Jan End chapter 3 23rd
Feb End chapter 1 14
$
```
