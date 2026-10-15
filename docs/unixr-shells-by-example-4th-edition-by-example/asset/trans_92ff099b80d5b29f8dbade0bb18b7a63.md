

## 示例 6.161

```
% nawk '{if ($8 > 15) { print $3 " has a high rating" } else print $3 "---NOT A COMPETITOR---"}' datafile
```

```
Joel---NOT A COMPETITOR---
Sharon has a high rating
Chris has a high rating
May---NOT A COMPETITOR---
Derek has a high rating
Susan has a high rating
TJ---NOT A COMPETITOR---
Val---NOT A COMPETITOR---
Sheri---NOT A COMPETITOR---
```

### 说明

`if` 语句是一种操作语句。如果表达式后面跟有多条语句，则必须使用花括号将它们括起来。（在本例中不需要花括号，因为表达式后面只有一条语句。）该表达式的含义是：如果第 8 个字段大于 15，则打印第 3 个字段以及字符串 `has a high rating`；否则打印第 3 个字段和 `---NOT A COMPETITOR---`。

## 示例 6.162

```
% nawk '{ i = 1; while (i <= NF && NR < 2) { print $i; i++ } }' datafile
```

```
northwest
NW
Joel
Craig
3.0
.98
3
4
```

### 说明

用户自定义变量 `i` 被赋值为 1。进入 `while` 循环并测试表达式。如果表达式计算结果为真，则执行 `print` 语句，打印第 `i` 个字段的值。先打印 `i` 的值，然后将 `i` 递增 1，再重新进入循环。当 `i` 的值大于 `NF` 且 `NR` 的值大于等于 2 时，循环表达式将变为假。在处理下一条记录之前，变量 `i` 不会重新初始化。

```
% cat datafile
```

|    |    |    |    |    |    |    |    |
|----|----|----|----|----|----|----|----|
| northwest | NW | Joel | Craig | 3.0 | .98 | 3 | 4 |
| western | WE | Sharon | Kelly | 5.3 | .97 | 5 | 23 |
| southwest | SW | Chris | Foster | 2.7 | .8 | 2 | 18 |
| southern | SO | May | Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Derek | Johnson | 4.0 | .7 | 4 | 17 |
| eastern | EA | Susan | Beal | 4.4 | .84 | 5 | 20 |
| northeast | NE | TJ | Nichols | 5.1 | .94 | 3 | 13 |
| north | NO | Val | Shultz | 4.5 | .89 | 5 | 9 |
| central | CT | Sheri | Watson | 5.7 | .94 | 5 | 13 |

## 示例 6.163

```
% nawk '{ for (i = 3; i <= NF && NR == 3; i++) print $i }' datafile
```

```
Chris
Foster
2.7
.8
2
18
```

### 说明

这在功能上与 `while` 循环类似。初始化、测试和循环控制语句都在同一个表达式中。`i` 的值（`i = 3`）仅对当前记录初始化一次。接着测试表达式。如果 `i` 小于等于 `NF`，且 `NR` 等于 3，则执行 `print` 块。打印完第 `i` 个字段的值后，控制返回到循环表达式。`i` 的值递增并重复测试。

## 示例 6.164

```
(The Command Line)
% cat nawk.sc4
# Awk script illustrating arrays
BEGIN { OFS = "\t" }
{ list[NR] = $1 }  # The array is called list. The index is
                    # the number of the current record. The value of the
                    # first field is assigned to the array element.
END { for (n = 1; n <= NR; n++) {
        print list[n]   # for loop is used to loop through the array.
     }
}
```

```
(The Command Line)
% nawk -f nawk.sc4 datafile
northwest
western
southwest
southern
southeast
eastern
northeast
north
central
```

### 说明

数组 `list` 使用 `NR` 作为索引值。每处理一行输入，第一个字段就被赋给 `list` 数组。在 `END` 块中，`for` 循环遍历数组的每个元素。

## 示例 6.165

```
(The Command Line)
% cat nawk.sc5
# Awk script with special for loop
/north/ { name[count++] = $3 }
END {
    print "The number living in a northern district: " count
    print "Their names are:"
    for (i in name)   # Special nawk for loop is used to
        print name[i] # iterate through the array.
}
```

```
(The Command Line)
% nawk -f nawk.sc5 datafile
The number living in a northern district: 3
Their names are:
Joel
TJ
Val
```

### 说明

每当行中出现正则表达式 `north` 时，`name` 数组就会获得第三个字段的值。每处理一条新记录，索引 `count` 都会递增，从而在数组中产生一个新元素。在 `END` 块中，使用特殊的 `for` 循环来遍历数组。

