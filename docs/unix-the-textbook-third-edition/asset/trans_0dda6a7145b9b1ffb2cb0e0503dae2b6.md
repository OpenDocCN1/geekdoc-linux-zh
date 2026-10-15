

你可以使用 ++ 和 -- 运算符，这些运算符也用于大多数当代高级语言，包括 C、C++ 和 Java，来将变量的值增加或减少 1。因此，@ var1++ 和 @ var1-- 分别增加和减少数值变量 var1 的值。类似地，我们可以使用以下语法将 var1 的值增加或减少 N。

```
@ var1 += N
@ var1 -= N
```

在下面的会话中，我们通过示例展示如何使用这些运算符。

```
% @ result = $value1 + $value2
% echo $result
25
% @ result++
% echo $result
26
% @ result += 1
% echo $result
27
% @ result = ( $result + 1 )
% echo $result
28
% @ result--
% echo $result
27
% @ result -= 1
% echo $result
26
% @ result -= $value1
% echo $result
16
%
```

你也可以使用 set 命令声明的变量来存储数值数据。因此，在下面的会话中，变量 side、area 和 volume 是通过使用 set 命令声明的，并通过使用 @ 命令赋予数值。echo 命令显示这些变量的值。

```
% set side = 10 area volume
% @ area = $side * $side
% @ volume = $side * $side * $side
% echo $side $area $volume
10 100 1000
%
```

在下面的章节练习中，你将通过使用 set 和 @ 命令执行数值数据处理。

## EXERCISE 15.1

声明两个数值变量 var1 和 var2，分别初始化为 10 和 30。给出两个将产生并显示它们的和与积的命令版本。

## 15.3 ARRAY PROCESSING

数组是存储在连续内存位置的同一类型项的有名集合。数组项根据其在数组中的位置编号，第一个项位于位置 1。你可以通过使用数组名称后跟方括号中的项编号来访问数组项。因此，你可以使用 people[k] 来引用名为 people 的数组中的第 k 个元素。此过程称为数组索引。你可以通过以下方式使用 set 命令为字符串和整数声明数组。

### SYNTAX

```
set array_name = ( array elements )
```

Purpose: To declare array_name to be an array variable containing "array elements" in parentheses

你可以通过使用前面加上美元符号 ($) 的数组名称来访问整个数组的内容，例如 $name。你可以通过使用前面加上 $# 的数组名称，如 $#name，或简单地使用 $#，就像在 Bourne shell 中一样，来访问数组中的元素总数。$?name 的值为 1，如果命名数组已被初始化，则为 0，如果未被初始化。

在下面的会话中，我们定义了一个包含六个项的字符串数组，称为 students，初始化为括号中包含的字符串。整个数组的内容可以通过使用 $students 访问，如第一个 echo 命令所示。因此，echo $#students 命令显示 6（students 数组的大小），而 echo $?students 命令显示 1，告知你该数组已被初始化。我们还展示了如何声明一个空数组，称为 empty，以及如何使用另一个数组的元素初始化一个数组；在这种情况下为空数组。

```
% set students = ( David James Jeremy Brian Art Charlie )
% echo $students
David James Jeremy Brian Art Charlie
% echo $#students
6
% echo $?students
1
% set empty = ()
% echo $empty
% echo $#empty
0
% echo $?empty
1
```

```
% set students = ( $empty )
% echo $students
%
```

在下面的会话中，我们展示了如何访问和更改 students 数组的元素。你可以通过将其索引为 $students[i] 来访问 students 数组中的第 i 个元素。你可以通过使用 i-j 作为索引值，如 $students[i-j]，来显示从位置 i 的元素到位置 j 的元素的数组元素范围。在下面的会话中，set 命令将 students 数组的第二个元素从 "James" 改为 "Steve Jobs"。第一个 echo 命令显示数组的所有元素。第二个 echo 命令显示 students 数组中的第二项。第三个 echo 命令显示 students 数组的四个元素，从位置 2 的项开始。最后一个 set 命令，我们尝试为 students 数组的第七个槽位分配一个值，显示一旦定义，数组的大小是固定的，不能更改。但是，你可以通过为其分配一组新值来重新定义一个新大小的数组，如下面的会话中第三个 set 和第四个 echo 命令所示。最后，你可以将一个数组的子数组分配给另一个数组变量，如最后两个 set 和 echo 命令所示。图 15.1 描述了原始的和修改后的 students 数组。

```
% set students[2] = "Steve Jobs"
% echo $students
David Steve Jobs Jeremy Brian Art Charlie
% echo $students[2]
Steve Jobs
% echo $students[2-5]
Steve Jobs Jeremy Brian Art
% set students[7] = Jamal
set: Subscript out of range.
% set students = ( "Dennis Ritchie" "Ken Thompson" David James Jeremy "Linus Torvalds" Brian Art Charlie Jamal "Steve Jobs" )
% echo $students
```

![](img/02e070097d401d3bf7de4bf1c470b267_609_0.png)

FIGURE 15.1 The students array (a) before and (b) after changing the contents of the second slot.

