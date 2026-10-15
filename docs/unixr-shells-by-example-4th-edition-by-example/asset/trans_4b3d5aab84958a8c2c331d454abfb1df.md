

## 6.22 内置算术函数

### 示例 6.156

```
% awk 'END{print 31/3}' filename
10.333
```

```
% awk 'END{print int(31/3)}' filename
10
```

### 解释

1 在 END 块中，除法的结果被打印为浮点数。

2 在 END 块中，int 函数导致除法的结果在小数点处被截断。显示一个整数。

### 6.22.2 随机数生成器

rand 函数。rand 函数生成一个大于或等于 0 且小于 1 的伪随机浮点数。

### 示例 6.157

```
% awk '{print rand()}' filename
0.513871
0.175726
0.308634
```

每次程序运行时，都会打印相同的数字集。srand 函数可用于为 rand 函数提供新的起始值。否则，如本例所示，每次调用 rand 时都会重复相同的序列。

srand 函数。没有参数的 srand 函数使用当前时间来为 rand 函数生成种子。srand(x) 使用 x 作为种子。通常，x 应在程序运行期间变化。

### 示例 6.158

```
% nawk 'BEGIN{srand()};{print rand()}' filename
0.508744
0.639485
0.657277

% nawk 'BEGIN{srand()};{print rand()}' filename
0.133518
0.324747
0.691794
```

### 解释

srand 函数为 rand 设置新的种子。起点是当前时间。每次调用 rand 时，都会打印一组新的数字。

### 示例 6.159

```
% nawk 'BEGIN{srand()};{print 1 + int(rand() * 25)}' filename
6
24
14
```

### 解释

srand 函数为 rand 设置新的种子。起点是当前时间。rand 函数在 0 到 25 之间选择一个随机数并将其转换为整数值。

## 6.23 用户定义函数 (nawk)

用户定义函数可以放置在脚本中的任何位置，该位置可以放置模式动作规则。

### 格式

```
function name ( parameter, parameter, parameter, ... ) {
    statements
    return expression
    (The return statement and expression are optional)
}
```

变量按值传递，并且在使用的函数中是局部的。只使用变量的副本。数组按地址或按引用传递，因此可以在函数内部直接更改数组元素。函数内部使用的任何未在参数列表中传递的变量都被视为全局变量；也就是说，它对整个 awk 程序可见，如果在函数中更改，则在整个程序中都会更改。在函数内提供局部变量的唯一方法是将其包含在参数列表中。此类参数通常放在列表末尾。如果函数调用中没有提供形式参数，则该参数最初设置为 null。return 语句将控制权和可能的值返回给调用者。

### 示例 6.160

（排序前的 grades 文件命令行显示）
% cat grades
44 55 66 22 77 99
100 22 77 99 33 66
55 66 100 99 88 45

（脚本）
% Scriptname: sorter.sc

```
# Scriptname: sorter
# It sorts numbers in ascending order
function sort ( scores, num_elements, temp, i, j ) {
  # temp, i, and j will be local and private,
  # with an initial value of null.
  for ( i = 2; i <= num_elements; ++i ) {
    for ( j = i; scores[j-1] > scores[j]; --j ) {
      temp = scores[j]
      scores[j] = scores[j-1]
      scores[j-1] = temp
    }
  }
}
{for ( i = 1; i <= NF; i++)
  grades[i]=$i
}
sort(grades, NF)  # Two arguments are passed
{for ( j = 1; j <= NF; ++j )
  printf("%d ", grades[j])
  printf("\n")
}
```

（排序后）
% awk -f sorter.sc grades
22 44 55 66 77 99
22 33 66 77 99 100
45 55 66 88 99 100

### 解释

+   1. 定义了名为 `sort` 的函数。函数可以在脚本中的任何位置定义。除了作为参数传递的变量外，所有变量在函数中都是全局作用域。如果在函数中更改，它们将在整个 `awk` 脚本中更改。数组按引用传递。五个形式参数被括在括号内。`scores` 数组按引用传递，因此如果在函数内部修改数组的任何元素，原数组将被修改。变量 `num_elements` 是一个局部变量，是原变量的副本。变量 `temp`、`i` 和 `j` 是函数中的局部变量。
+   
+   2. 外层 `for` 循环将遍历一个数字数组，只要有至少两个数字可比较。
+   
+   3. 内层 `for` 循环将当前数字与 `scores[j-1]` 中的前一个数字进行比较。如果前一个数组元素大于当前元素，`temp` 将被赋值为当前数组元素的值，当前数组元素将被赋值为前一个元素的值。
+   
+   4. 外层循环块结束。
+   
+   5. 这是函数定义的结束。
+   
+   6. 脚本的第一个动作块从此处开始。`for` 循环遍历当前记录的每个字段，创建一个数字数组。
+   
+   7. 调用 `sort` 函数，传递当前记录的数字数组和当前记录的字段数。
+   
+   8. `sort` 函数完成后，程序控制从此处开始。`for` 循环打印排序后数组中的元素。

## 6.24 复习

除非另有说明，本节中的示例使用以下数据文件，为方便起见定期重复。

| % Cat datafile |  |  |  |  |  |  |
|---|---|---|---|---|---|---|
| northwest | NW | Joel Craig | 3.0 | .98 | 3 | 4 |
| western | WE | Sharon Kelly | 5.3 | .97 | 5 | 23 |
| southwest | SW | Chris Foster | 2.7 | .8 | 2 | 18 |
| southern | SO | May Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Derek Johnson | 4.0 | .7 | 4 | 17 |
| eastern | EA | Susan Beal | 4.4 | .84 | 5 | 20 |
| northeast | NE | TJ Nichols | 5.1 | .94 | 3 | 13 |
| north | NO | Val Shultz | 4.5 | .89 | 5 | 9 |
| central | CT | Sherl Watson | 5.7 | .94 | 5 | 13 |

