
## 示例9.55（续）

```
8 % echo $fruit[$#fruit]    # Prints the last element
plums
9 % set fruit[2] = bananas    # Reassigns the second element
% echo $fruit
apples bananas peaches plums
10 % set path = ( ~/usr/bin /usr /usr/local/bin . )
% echo $path
/home/jody/ellie /usr/bin /usr /usr/local/bin .
11 % echo $path[1]
/home/jody/ellie
```

## 说明

- 1. 词表包含在括号内。每个单词由空白字符分隔。该数组称为fruit。
- 2. 打印fruit数组中的单词。
- 3. 打印fruit数组的第一个元素。下标从1开始。
- 4. 打印词表的第二、第三和第四个元素。破折号允许您指定一个范围。
- 5. 该数组没有六个元素。下标超出范围。
- 6. 打印fruit数组的所有元素。
- 7. 数组前的#$用于获取数组中的元素个数。fruit数组中有四个元素。
- 8. 由于下标$#fruit的值等于数组中的元素总数，如果将该值用作数组的索引值，即[$#fruit]，则会打印fruit数组的最后一个元素。
- 9. 数组的第二个元素被赋予一个新值。打印数组时会显示替换后的值bananas。
- 10. path变量是C shell中用于搜索命令的目录数组，是一个特殊数组。通过创建数组，可以访问或更改path的各个元素。
- 11. 打印path的第一个元素。

## shift命令与数组。

如果内建shift命令将数组名作为其参数，它会将数组的第一个元素移出（向左）。数组的长度减少一。（不带参数时，shift命令将内建argv数组的第一个元素移出。参见第534页的“命令行参数”。）

## 示例9.36

```
1  % set names = ( Mark Tom Liz Dan Jody )
2  % echo $names
Mark Tom Liz Dan Jody
3  % echo $names[1]
Mark
4  % shift names
5  % echo $names
Tom Liz Dan Jody
6  % echo $names[1]
Tom
7  % set days = ( Monday Tuesday )
8  % shift days
9  % echo $days
Tuesday
10 % shift days
11 % echo $days
12 % shift days
shift: no more words.
```

## 说明

- 1 该数组名为names。它被赋值为括号中的单词列表。每个单词由空白字符分隔。
- 2 打印该数组。
- 3 打印数组的第一个元素。
- 4 数组向左移动一个元素。单词Mark被移出。
- 5 移动后数组减少了一个元素。
- 6 移动后，数组的第一个元素是Tom。
- 7 创建了一个名为days的数组。它有两个元素：Monday和Tuesday。
- 8 数组days向左移动一位。
- 9 打印该数组。Tuesday是仅剩的元素。
- 10 数组days再次被移动。该数组为空。
- 11 days数组为空。
- 12 这一次，尝试移动会导致shell发送一条错误消息，指示它无法从空数组中移出元素。

## 从字符串创建数组。

您可能希望从带引号的字符串中创建一个词表。这可以通过将字符串变量放在一组括号内来实现。

## 示例9.37

```
1 % set name = "Thomas Ben Savage"
% echo $name[1]
Thomas Ben Savage
2 % echo $name[2]
Subscript out of range.
3 % set name = ( $name )
4 % echo $name[1] $name[2] $name[3]
Thomas Ben Savage
```

## 说明

- 1 变量name被赋值为字符串Thomas Ben Savage。
- 2 当将其视为数组时，只有一个元素，即整个字符串。
- 3 该变量被放在括号内，创建了一个名为name的单词数组。
- 4 显示新数组的三个元素。

### 9.10.5 特殊变量

C shell内建了几个由一个字符组成的变量。字符前的$允许进行变量解释。参见表9.7。

## 表9.7 变量及其含义

| 变量 | 示例 | 含义 |
|---|---|---|
| $?var | echo $?name | 如果变量已设置则返回1，否则返回0。 |
| $#var | echo $#fruit | 打印数组中元素的个数。 |
| $$ | echo $$ | 打印当前shell的PID。 |
| $< | set name = $< | 接受用户输入的一行，直到换行符。 |

## 示例9.36

```
1 % set num
% echo $?num
1
2 % echo $path
/home/jody/ellie /usr/bin/ usr/local/bin
% echo $#path
3
```
