
```bash
#!/bin/bash
clear
echo "Font Color Menu"
echo "=================="
echo -en "[1] Red\n[2] Green\n[3] Brown\n"
echo -en "[4] Blue\n[5] Purple\n[6] Cyan\n"
echo -n "[X] Exit or make a selection: "
read CHOICE
case $CHOICE in
1) echo -e "\e[033;1m"
2) echo -e "\e[033;2m"
3) echo -e "\e[033;3m"
4) echo -e "\e[033;4m"
5) echo -e "\e[033;5m"
6) echo -e "\e[033;6m"
x) echo -e "\e[033;7m"
esac
if [ $CHOICE != "x" ]
then echo -e "Thank you for choosing $CHOICE\n"
fi
```

这些颜色标识类似于第 148 页用于自定义 shell 提示符的那些。

**Linux Linux**

当用户输入一个可能的选项时，`read` 命令将其值赋值给变量。`case` 语句检查匹配的值，然后执行其命令。在这种情况下，命令设置临时字体颜色显示消息，然后 shell 恢复常规颜色：

![](img/0494b98ec9ddc4515587e9808d73902e_218_0.png)

![](img/0494b98ec9ddc4515587e9808d73902e_218_1.png)

## 循环结构

循环允许在条件为真时重复执行一个或多个命令。循环每次迭代（pass）都会评估指定的表达式，当发现为真时循环继续。shell 提供了三种循环：

- `while` 循环结构为 `while` 关键字指定测试表达式以及在 `do` 和 `done` 之间执行的命令。它将持续直到评估为假。
- 同样，`until` 循环结构为 `until` 关键字指定测试表达式以及在 `do` 和 `done` 之间执行的命令。细微的差别在于，它将持续直到评估为真。
- `for-in` 循环只需为给定列表中的每个项目执行一次迭代。通过在任何类型的循环中插入 `if` 语句可以跳过单次迭代。这可以产生进一步的评估，当为真时调用 `continue` 关键字跳到下次迭代。除非循环体改变了测试评估，否则循环永远不会结束，除非意外按下 Ctrl+C 停止循环运行。或者，插入的 `if` 语句可以在发现时调用 `break` 关键字完全结束循环。

每种类型的循环都出现在脚本中，并初始设置为进行八次迭代，每次通过时输出当前迭代的数字。`for` 循环包含一个 `if` 语句强制跳过第三次迭代。它还包含一个在第七次迭代时终止循环的 `if` 语句。

注意添加到此脚本的注释——在 `#!` 行之后，`#` 字符被忽略。简单的计数器变量通常是小写的——例如此示例中的 `$i`、`$j` 和 `$k`。

![](img/0494b98ec9ddc4515587e9808d73902e_220_0.png)

尽管此例中的 `for` 循环迭代的是数字列表，但它可以使用 `$string` 相等运算符代替 `-eq` 数值相等运算符来迭代字符串列表。

![](img/0494b98ec9ddc4515587e9808d73902e_220_1.png)

```bash
#!/bin/bash
clear
i=1; echo -n "While loop: "
while [ $i -lt 9 ] #test
do
echo -n "...$i" #output
i=$(expr $i + 1) #increment
done; echo ""

j=1; echo -n "Until loop: "
until [ $j -eq 9 ] #test
do
echo -n "...$j" #output
j=$(expr $j + 1) #increment
done; echo ""
echo -n "For loop: "
for k in 1 2 3 4 5 6 7 8
do
if [ $k -eq 3 ]; then continue; fi
if [ $k -eq 7 ]; then break; fi
echo -n "...$k"
done; echo " "
```

![](img/0494b98ec9ddc4515587e9808d73902e_220_2.png)

```
While loop: ...1...2...3...4...5...6...7...8
Until loop: ...1...2...3...4...5...6...7...8
For loop: ...1...2...4...5...6...8
user> █
```

## 生成随机数

`$RANDOM` 变量每次被调用时生成一个从 0 到 32767 的“随机”整数。要为随机数设置范围，使用 `模` 运算符指定最大数。例如，要将范围设置为 0 到 19，使用 `($RANDOM % 20)` 将生成的任何数字除以 20，留下零到 19 之间的数字。在表达式中加上 1 `($RANDOM % 20 + 1)` 会扩大范围，使随机数位于 1 到 20 之间。

`$RANDOM` 生成的数字并不是真正的随机，因为它在给定起始点（种子）的情况下生成相同的序列：

![](img/0494b98ec9ddc4515587e9808d73902e_221_0.png)

```
会话 编译 视图 设置 帮助
user RANDOM=1
user echo $RANDOM; echo $RANDOM; echo $RANDOM
17767
9158
6249
user RANDOM=1
user echo $RANDOM; echo $RANDOM; echo $RANDOM
17767
9158
6249
user> 
```

为了确保 `$RANDOM` 变量在调用时生成不同的数字序列，有必要使用不同的起始种子值对其设置。

解决方案是使用 `date` 命令从它的选项之一中提取动态值。它的选项之一 `+%s` 交付了自太元以来流过的当前秒数。使用这来为 `$RANDOM` 变量种子可以获得更好的随机数生成。

相反脚本首先从 `date` 命令的选项中提取当前流逝时间，为 `$RANDOM` shell 变量种子。

`let` 命令允许你对 shell 变量进行算术运算，在这里用于保存一个 1-20 之间的随机数，用户可以进行猜测：

![](img/0494b98ec9ddc4515587e9808d73902e_222_0.png)

注意循环如何反复评估输入，直到给出正确的匹配。

```
I have chosen a number between 1 and 20
Guess what it is? 10
No - try lower... 3
No - try higher... 8
Yes the number is 8
user>
```

## 数组操作

你可以在 shell 中创建存储多个值的变量，这些变量被称为“数组”。这些变量数组将每个值存储在名为“元素”（element）的唯一独立索引隔中。

![](img/0494b98ec9ddc4515587e9808d73902e_223_0.png)

通过将一对圆括号 `()` 内的空格分隔的值列表赋值给你指定的变量名来创建数组。值可以是数字、文本或两者的混合。

为了访问存储在数组元素中的值，你必须对它们进行解引用，使用花括号 `{}` 包围变量名和索引。你也可以使用通配符 `*` 代替数字来访问所有元素：

```
Shell - Konsole
session Edit Bookmarks Settings
user> ARR=(a two 3)
user> ARR[2]=6
user> echo ${ARR[*]}
a two 6
user> echo ${ARR[0]}
a
```

![](img/0494b98ec9ddc4515587e9808d73902e_223_1.png)

这个脚本有效地结合了本章的几个方面：随机数生成、表达式求值、值输出、循环和数组。它通过初始化随机数器创建一个 0–49 的顺序整数数组。接下来，生成的 1–49 范围内的随机数用于洗牌元素。这意味着数组包含了 1–49 的所有数字，顺序是随机的，且重复任何数字。元素 1–6 的值用于格式化输出：

![](img/0494b98ec9ddc4515587e9808d73902e_224_0.png)

这个高级脚本运行就像一个程序。你可以使用 C 语言创建自己的编译程序，例如 `gcc` 来查看它是否已经安装，或者从你的发行版中安装。
