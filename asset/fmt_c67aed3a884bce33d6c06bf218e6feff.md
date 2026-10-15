
# 第 3 章 高级用户 UNIX 工具

## `sort` 命令

```
用法: sort -tc -r { 排序字段-bfMn }* {文件名 }*
```

`sort` 是一个实用程序，根据指定的排序标准对一个或多个文件进行排序。默认情况下，行按升序排序。`-r` 选项指定为降序。输入行通过空格或制表符拆分为字段。要指定不同的字段分隔符，请使用 `-t` 选项。默认情况下，执行排序时会考虑一行的所有字段。可以通过指定一个或多个排序字段来覆盖这一约定，这些字段的格式在本节的稍后部分描述。可以通过在排序字段后紧跟一个或多个选项来自定义单个排序字段。`-f` 选项使 `sort` 忽略字段的大小写。`-M` 选项按月份顺序对字段排序。`-n` 选项按数字顺序对字段排序。`-b` 选项忽略领先空格。

图 3.7：`sort` 命令的描述。

`sort` 根据 ASCII 值比较相应的字符。（参见 `man ascii` 以获取所有字符及其对应值的列表。）这一约定的两个结果是：大写字母比其小写对应字母“小”，空格“小于”字母。在示例中，我使用默认排序规则按升序和降序对一个文本文件进行了排序：

```
$ cat sortfile ...列出要排序的文件
Jan Start chapter 3 10th
Jan Start chapter 1 30th
Jan Start chapter 5 23rd
Jan End chapter 3 23rd
Mar Start chapter 7 27
May End chapter 7 17th
Apr End Chapter 5 1
Feb End chapter 1 14
...
$ sort sortfile
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
Apr End Chapter 5 1
may End chapter 7 17th
Jan Start chapter 5 23rd
Jan End chapter 3 23rd
Feb End chapter 1 14
$
```

### 按特定字段排序

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

注意，领先空格被计算为第一个字段的一部分，这导致了奇怪的排序序列。此外，我希望月份按正确的顺序排序，“Jan”在“Feb”之前，以此类推。`-b` 选项忽略领先空白，`-M` 选项按月份顺序排序。这里有一个可以工作的示例：

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

## 比较文件

以下两个实用程序允许你比较两个文件的内容：

- `cmp`，找到文件之间第一个不同的字节
- `diff`，显示文件之间所有的差异和相似之处

### 测试相同性：`cmp`

`cmp` 用于测试两个文件是否相同。`fileName1` 和 `fileName2` 完全相同，`cmp` 返回退出码 0 不显示任何内容；`cmp` 返回退出码 1 并显示第一个匹配字节的偏移量和行号。如果一个文件是另一个文件的前缀，则显示较短文件的 `EOF` 信息。`-l` 选项显示所有匹配字节的偏移量和值。`-s` 选项禁止所有输出。可选值 `offset1` 和 `offset2` 分别指定 `fileName1` 和 `fileName2` 的起始偏移量，并让比较从那里开始。

```
用法: cmp -ls fileName1[offset] [offset2]
```

```
81 145 56
82 40 12
cmp: EOF on lady2 ...lady2 is smaller than lady1.
$ _
```

### 文件差异：`diff`

`diff` 工具比较两个文件，并列出编辑更改列表，这些更改可以将第一个文件转换为第二个文件。它的工作方式如图 3.9 所示。有三种类型的编辑更改：添加行 (a)、修改行 (c) 和删除行 (d)。图 3.10 显示了 `diff` 用于描述每种编辑的格式。注意：

```
Utility: diff -i -dflag fileName fileName
```

`diff` 是一个比较两个文件并输出其差异描述的工具。（有关此输出格式的信息，请参见本节的其余部分。）`-i` 标志忽略行的大小写。`-D` 选项导致 `diff` 生成为 C 预处理器设计的输出。
