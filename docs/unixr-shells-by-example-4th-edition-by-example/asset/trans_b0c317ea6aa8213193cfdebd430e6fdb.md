

## 6.20 数组

awk 中的数组称为关联数组，因为下标可以是数字或字符串。下标通常称为键，与分配给相应数组元素的值相关联。键和值在内部存储在一个表中，其中对所讨论键的值应用哈希算法。由于用于哈希的技术，数组元素不会按顺序存储，并且在显示数组内容时，可能不会按您期望的顺序显示。

数组与变量一样，是通过使用它来创建的，awk 可以推断它用于存储数字还是字符串。数组元素根据上下文初始化为数值零和字符串值 null。您不必声明 awk 数组的大小。awk 数组用于从记录中收集信息，可用于累积总数、计数单词、跟踪模式出现的次数等等。

### 6.20.1 关联数组的下标

使用变量作为数组索引。[参见示例 6.135 的演示。

### 示例 6.135

（输入文件）
% cat employees
Tom Jones      4424   5/12/66    543354
Mary Adams     5346   11/4/63    28765
Sally Chang    1654   7/22/54    658000
Billy Black    1683   9/23/44    336500

（命令行）
1 % awk '{name[++i]=$2};END{for(i=0; i<NR; i++) print i, name[i]}' employees
0 Jones
1 Adams
2 Chang
3 Black

2 % awk '{id[NR]=$3};END{for(x = 1; x <= NR; x++) print id[x]}' employees
4424
5346
1654
1683

### 解释

1 数组 name 中的下标是用户定义的变量，x。++ 表示数值上下文。awk 将 x 初始化为 0，并在使用后（后增运算符）将其递增 1。第二字段的值被分配给 name 数组的每个元素。在 END 块中，for 循环用于遍历数组，打印存储在其中的值，从下标 0 开始。因为下标只是一个键，所以它不必从 0 开始。它可以从任何值开始，无论是数字还是字符串。

2 awk 变量 NR 包含当前记录的编号。通过使用 NR 作为下标，第三字段的值被分配给每个记录的数组的每个元素。最后，for 循环将遍历数组，打印存储在其中的值。

特殊 for 循环。特殊 for 循环用于在 for 循环不切实际的情况下遍历关联数组；也就是说，当使用字符串作为下标或下标不是连续数字时。特殊 for 循环使用下标作为与之关联的值的键。

### 格式

```
{for(item in arrayname){
print arrayname[item]
}
}
```

### 示例 6.136

（输入文件）
% cat db
1 Tom Jones
2 Mary Adams
3 Sally Chang
4 Billy Black
5 Tom Savage
6 Tom Chung
7 Reggie Steel
8 Tommy Tucker

（命令行，for 循环）
1 % nawk '/^Tom/{name[NR]=$1};\
END{for(i = 1; i <= NR; i++) print name[i]}' db
Tom

Tom
Tom

Tommy

### 示例 6.136（续）

```
（命令行，特殊 for 循环）
2 % nawk '/Tom/{name[NR]=$1;}
END{for(i in name){print name[i]}}' db
Tom
Tommy
Tom
Tom
```

### 解释

- 1 如果正则表达式 Tom 与输入行匹配，则 name 数组被赋予一个值。NR 值，即当前记录的编号，将用作 name 数组中的索引。每次在行上匹配到 Tom 时，name 数组都会被赋予 $1 的值，即第一个字段的值。当到达 END 块时，name 数组由四个元素组成：name[1]、name[5]、name[6] 和 name[8]。因此，使用传统 for 循环打印 name 数组的值时，索引 2、3、4 和 7 的值为空。
- 2 特殊 for 循环遍历数组，仅打印与该值相关联的下标存在的值。打印的顺序是随机的，因为关联数组的存储方式（哈希）。

使用字符串作为数组下标。下标可以由包含字符串的变量或字面字符串组成。如果字符串是字面值，则必须用双引号括起来。

### 示例 6.137

```
（输入文件）
% cat datafile3
tom
mary
sean
tom
mary
mary
bob
mary
alex
```

```
（脚本）
# awk.sc 脚本
1 /tom/ { count["tom"]++ }
2 /mary/ { count["mary"]++ }
3 END{print "There are " count["tom"] " Toms in the file and " count["mary"] " Marys in the file."}
```

