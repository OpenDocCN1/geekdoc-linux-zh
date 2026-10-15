
## 示例 6.137（续）

（命令行）
% awk -f awk.sc datafile3
There are 2 Toms in the file and 4 Marys in the file.

## 说明

+   1. 一个名为 count 的数组包含两个元素：count["tom"] 和 count["mary"]。每个数组元素的初始值均为 0。每当匹配到 tom 时，该数组的值就增加 1。
+   2. count["mary"] 采用相同的过程。注意：每行只记录一个 tom，即使该行出现多次也是如此。
+   3. END 模式会打印每个数组元素中存储的值。

![](img/60a0b5d254bd6007403850f972cbfad8_273_0.png)

图 6.1 在数组中使用字符串作为下标（示例 6.137）。

## 使用字段值作为数组下标

任何表达式都可以用作数组的下标，因此字段也可以。示例 6.138 中的程序统计出现在第二个字段中的所有名字的频率，并引入了一种新的 for 循环形式：

```
for( index_value in array ) statement
```

上一个示例的 END 块中的 for 循环的工作原理如下：变量 name 被设置为 count 数组的下标值。在 for 循环的每次迭代之后，执行 print 操作，先打印下标值，再打印该元素中存储的值。（打印顺序不保证。）

## 示例 6.138

（输入文件）
% cat datafile4
4234 Tom 43
4567 Arch 45
2008 Eliza 65
4571 Tom 22
3298 Eliza 21
4622 Tom 53
2345 Mary 24

## 示例 6.138（续）

（命令行）
% nawk '{count[$2]++}END{for(name in count)print name,count[name] }' datafile4

Tom 3
Arch 1
Eliza 2
Mary 1

## 说明

awk 语句首先将第二个字段用作 count 数组的下标。下标随第二个字段的变化而变化，因此 count 数组的第一个下标是 Tom，存储在 count["Tom"] 中的值是 1。

接下来，count["Arch"] 被设置为 1，count["Eliza"] 被设置为 1，count["Mary"] 被设置为 1。当 awk 在第二个字段中再次遇到 Tom 时，count["Tom"] 增加，现在其值为 2。对于 Arch、Eliza 和 Mary 的每一次出现，都会发生同样的情况。

## 示例 6.139

（输入文件）
% cat datafile4
4234 Tom 43
4567 Arch 45
2008 Eliza 65
4571 Tom 22
3288 Eliza 21
4622 Tom 53
2345 Mary 24

（命令行）
% nawk '{dup[$2]++; if (dup[$2] > 1){name[$2]++} } END{print "The duplicates were\n" for (i in name)print i, name[i]}}' datafile4

（输出）
Tom 2
Eliza 2

## 说明

dup 数组的下标是第二个字段中的值，即人名。该下标对应的值的初始值为 0，每处理一条新记录就增加 1。如果名字重复，该下标对应的值会增加到 2，以此类推。如果 dup 数组中该下标的值大于 1，则另一个名为 name 的数组也会以第二个字段为下标，并记录出现次数大于 1 的名字的数量。

## 数组与 split 函数

awk 的内置 split 函数允许你将一个字符串拆分为单词并存入数组。你可以自行定义字段分隔符，也可以使用当前存储在 FS 中的值。

## 格式

```
split(string, array, field separator)
split (string, array)
```

## 示例 6.140

（命令行）
% nawk BEGIN{ split("/3/15/2004", date, "/"); print "The month is " date[1] " and the year is " date[3]; } filename

（输出）
The month is 3 and the year is 2004.

## 说明

字符串 3/15/2004 被存入数组 date，并使用正斜杠作为字段分隔符。现在 date[1] 包含 3，date[2] 包含 15，date[3] 包含 2004。字段分隔符在第三个参数中指定；如果未指定，则使用 FS 的值作为分隔符。

## delete 函数

delete 函数用于删除一个数组元素。

## 示例 6.141

```
% nawk '{line[x++]= $2}END{for(x in line) delete(line[x])}' filename
```

## 说明

赋给数组 line 的值是第二个字段的值。所有记录处理完毕后，特殊的 for 循环会遍历数组中的每个元素，delete 函数随后会逐一删除每个元素。

## 多维数组（nawk）

尽管 awk 并不正式支持多维数组，但它提供了一种语法，使其呈现出多维数组的样子。这是通过将下标连接成一个字符串来实现的，各下标之间使用特殊的内置变量 SUBSEP 的值分隔。SUBSEP 变量的值为 "\034"，这是一个不可打印字符，该字符十分特殊，几乎不可能作为下标字符出现。表达式 matrix[2,8] 实际上是数组 matrix[2 SUBSEP 8]，其计算结果为 matrix["2\0348"]。该下标成为关联数组中的一个唯一字符串。
