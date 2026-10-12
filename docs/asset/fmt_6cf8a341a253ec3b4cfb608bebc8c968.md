
For details type `warranty`.

```
10+13.7
23.7
29.37/13.03
2
scale=3; 29.37/13.03
2.254
29.37/13.03*12
24
scale=6; 29.37/13.03*12
27.048348
quit
$
```

接下来的会话展示了几个 Bash 命令，它们通过管道将由 `bc` 求值的某些数学表达式传递给 `bc`。

```
$ echo '29.37/13.03' | bc
2
$ echo 'scale=4; 29.37/13.03' | bc
2.2540
$ echo '29.37/13.03*12' | bc
24
$ echo 'scale=6; 29.37/13.03*12' | bc
27.048348
$
```

你也可以通过使用 `<<<` 运算符将表达式传递给 `bc`，如下会话所示：

```
$ bc <<< 'scale=6; 29.37/13.03*12'
27.048348
$
```

### 高级 Bash 编程

最后，你可以用 `bc` 求一个表达式，将结果保存在 shell 变量中，并使用 `echo` 命令显示结果，如下会话所示：

```
$ x=echo 'scale=6; 29.37/13.03*12' | bc
$ echo $x
27.048348
```

你可以通过带有 `-l` 选项运行 `bc` 来使用数学函数。下面的命令展示了使用正弦函数 `s(Q)` 计算弧度角的正弦值。

```bash
$ echo "s(2)" | bc -l
.9092974268256819539
```

接下来的会话展示了 `bc` 中 `if` 和 `for` 语句的使用。注意这些结构与 C 语言对应结构之间的相似之处。

```bash
$ echo 'a=10; b=20; if(a>b) print "a is greater" else print "b is greater\n' | bc
b greater
$ echo 'for(i=1; i<=10; i++) {i};' | bc
```

### 练习 13.4

在你的系统上重复本节讨论的命令和脚本。你能够重现结果吗？请记录任何差异。

## 13.3 数组处理

Bash 支持一维数组。数组是存储在连续内存位置中的相同类型项的名称集合。数组项（称为数组成员）的索引从 0 开始。Bash 中对数组的大小没有限制，且数组元素并不要求连续赋值。这意味着当你有一个数组时，可以为任何数组元素赋值（参见下例）。你可以使用以下任何语法来声明数组变量。

```
Syntax:
array_name[subscript]=value
declare -a array_name
declare -a array_name[subscript]
local -a array_name
readonly array_name
```

Purpose: 将 `array_name` 声明为数组变量。`subscript` 被视为算术表达式，必须求值为大于等于 0 的数字。第二、第三种语法是等价的，因为第三种声明中的 `subscript` 被忽略。第四种语法用于声明作用域为函数的数组变量。第五种语法可用于声明只读数组变量。

可以在声明时使用以下语法初始化数组：

`array_name=(value ... valueN)`

“value”的格式为 `[subscript]=string`。注意下标是可选的，但如果提供，则相应的值将赋值给指定的数组槽；否则，值将赋值给最后一个槽的下一个槽。

你可以使用 `${name[subscript]}` 语法引用数组项。该过程被称为数组索引。如果 `subscript` 是 0 或 `*`，则引用所有元素。`@` 与 `*` 在 `"${name[@]}"` 中的区别是将数组名称的每个元素展开为单独单词。

在此示例中，数组变量 `movies` 被分配了三个值：前两个值分配给位置 0 和 1，第三个分配给槽位 65。使用 `echo` 命令显示这三个变量的值。

```
$ movies="Silence of the Lambs" "Malcolm X" [65]="The Birds"
$ echo ${movies[0]}
Silence of the Lambs
$ echo ${movies[1]}
Malcolm X
$ echo ${movies[2]}
$ echo ${movies[65]}
The Birds
$ echo ${movies[*]}
Silence of the Lambs Malcolm X The Birds
$ echo ${movies[0]}
Silence of the Lambs
```

366
Linux

$F_2 = 1$
$F_n = F_{n-1} + F_{n-2}$, 对于 $n \ge 3$

因此，斐波那契数列的前十个数字是 0, 1, 1, 2, 3, 5, 8, 13, 21, 和 34。

`num_array_demo` 文件中的脚本注释详细且相当容易理解。它显示了前十个斐波那契数字数的和。代码之后是脚本的运行示例。

```bash
$ cat num_array_demo
# File Name: ~/linux/ch13/bash/num_array_demo
# Author: Syad Mansoor
# Date Written: August 16, 2017
# Last Modified: July 16, 2017
# Purpose: 
# Brief Description: 
```

```bash
# 为了演示在 Bash 中处理数值数组的操作
# 在数值 'sum' 中维护前 10 个斐波那契数字
# 的运行累和，从 0 开始。
# 读取下一个数字并将其加到 sum。当
# 最后一个数字被加到 sum 时，显示答案。
```

```bash
# 初始化数组为任意数量的斐波那契数字；在此情况下为前 15 个
declare -aFibonacci=(0 1 2 3 5 8 13 21 34 55 89 144 233 377)
# 字符串格式的斐波那契数组的大小
# 索引指向第二个元素
size=${#Fibonacci[@]}
# 初始化运行累和为 0
sum=0
next=0
while [ $index -le $size ]; do
	next=${Fibonacci[$index]} # 获取下一个整数值
	sum=$((sum + next)) # 更新运行累和
	index=$((index + 1)) # 数组索引加 1
done
```
