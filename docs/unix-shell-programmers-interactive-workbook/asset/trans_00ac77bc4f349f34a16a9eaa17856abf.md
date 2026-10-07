

# 第 6 章：高级变量用法 309

当作为数组的下标使用时，它指的是数组中所有元素的列表。

输入以下命令：

```
print $(#days[@])
```

k) 打印了什么数字？它与数组 `days` 有什么关系？
答案：你的交互界面应该如下所示：

```
[6091]: print $(#days[@])
```

7

```
[6092]:
```

`$(# ... )` 结构是一种参数扩展，这将在第 10 章“模式、扩展与替换”中讨论的话。这种特定的扩展给出的是井号（#）之后内容的长度，在本例中，即数组中元素的个数。

![](img/694fa9f0320e707804a4c650b96a09b4_328_0.png)

你也可以使用 `${ ... }` 来获取字符串的长度。例如，shell 会将 `$(#days[0])` 评估为 6，因为 Sunday 中有六个字母。

输入以下命令：

```
weekend[0]=6 weekend[1]=0
print There are $(#weekend[@]) \
days in the weekend.
print They are ${days[${weekend[0]}]} \
and ${days[${weekend[1]}]}.
```

- i) 解释第一个 print 命令的输出。
答案：你的交互界面应该如下所示：

```
[6092]: weekend[0]=6 weekend[1]=0
[6093]: print There are ${#weekend[@]} \
days in the weekend.
```

周末里有 2 天。
[6094]: print They are ${days[ weekend[0] ]} and \
${days[ weekend[1]]}.

它们是 Saturday 和 Sunday。
[6095]:

数组 `weekend` 有两个元素，因此信息打印了数字 2 以替替了 `${#weekend[@]}`。

# 310 实验 6.2：数组与复合变量

m) 解释第二个 print 命令的输出。

答案：数组 `weekend` 的元素 0 和 1 的值分别为 6 和 0，因此打印了字符串 Saturday 和 Sunday。

这里有两点需要注意。第一点是你可以使用数组元素的引用作为另一个数组的下标。第二点是算术表达式的规则决定了你可以在下标中写什么，允许你在表达式内部插入额外的空格。这些空格并不是必须，但 `weekend[0]` 和 `weekend[1]` 两侧的空格让代码更易读。

![](img/694fa9f0320e707804a4c650b96a09b4_329_0.png)

算术表达式允许你在引用变量时省略美元符号和花括号，并在变量周围插入空格。明智地使用空格会让你的代码更易读。

将值 `Birthday` 赋值给 `days[3]`，并将空字符串赋值给 `days[99]`。

- * 如果现在打印 `$(days[@])` 和 `$(#days[@])` 会发生什么！
答案：你的交互界面应该如下所示：
[6095]: days[3]=birthday days[99]=
[6096]: print ${days[@]}
Sunday Monday Tuesday Wednesday Thursday Friday Saturday Birthday
[6097]: print ${days[@]}
9

shell 会跟踪数组中哪些元素已经被分配了值，哪些还没有。元素 0 到 6、31 和 99 已经分配了值，因此 `${#days[@]}` 打印的值是 9。打印数组的所有元素只会显示分配了非空字符串或数值的元素值。

# 第 6 章：高级变量用法 311

## 6.2.2 答案

输入一个命令，将变量名 `venus` 和 `mars` 声明为关联数组。

- a) 你使用了什么命令？
答案：你应该输入了以下命令：
[6098]: typeset -A mars venus

你可以以相反的顺序输入变量名，也可以使用两个独立的 `typeset` 命令。无论哪种，你必须在 `typeset` 命令上使用 `-A` 选项使变量成为关联数组。

输入以下命令：
venus[domain]=cs.qc.edu
venus[address]=149.4.44.101
venus[building]="Science Building"
venus[room]=A-219
print ${venus[domain]} is in ${venus[building]}\nroom ${venus[room]}.

- b) 打印了什么？
答案：你的交互界面应该如下所示：
[6099]: venus[domain]=cs.qc.edu
[6100]: venus[address]=149.4.44.101
[6101]: venus[building]="Science Building"
[6102]: venus[room]=A-219
[6103]: print ${venus[domain]} is in \n${venus[building]}, room ${venus[room]}.
venus.cs.qc.edu is in Science Building, room A-219.
[6104]:

关联数组的一个常见用途是为某个对象（在本例中为工作站）存储一组相关值。

# 312 实验 6.2：数组与复合变量

你将在下一节看到，复合变量可以完成许多与数组相同的工作，例如为某个对象存储一组相关值。你可以使用这种方法![](/694fa9f0320e707804a4c650b96a09b4_321_0.png)

LAB 6.2

输入以下命令：
print ${mars[domain]} is in ${mars[building]}\room ${mars[room]}.

- 打印了什么？
答案：你的交互界面应该如下所示：
[6105]: print ${mars[domain]} is in \n${mars[building]}, room ${mars[room]}.
mars.cs.qc.edu is in Science Building, room A-219.
[6106]:

因为没有给数组的任何元素赋值，所以信息在任何处都是空白的。

输入以下命令：
print ${#weekend[@]} \
days in the weekend.
print They are ${days[${weekend[0]}]} \
and ${days[${weekend[1]}]}.

周末里有 2 天。
[6094]: print They are ${days[ weekend[0] ]} and \
${days[ weekend[1]]}.

它们是 Saturday 和 Sunday。
[6095]:

数组 `weekend` 有两个元素，因此信息打印了数字 2 以替替了 `${#weekend[@]}`。

# 第 6 章：高级变量用法 332

- e) `${[@]}` 打印什么？
答案：它打印数组的元素。

- f) `${#[@]}` 打印什么？
答案：它打印数组元素的个数。

- g) `${variable}` 打印什么？
答案：它打印变量的值。

- h) 打印了什么？
答案：你的交互界面应该如下所示：
```
[6110]: venus[arbitrary string]=hello
[6111]: print ${venus[arbitrary string]}
hello
[6112]: print ${venus[arbitrary string]}
hello
```

# 314 实验 6.2：数组与复合变量

如果你没有实际输入这段代码，可能会忽略这两个下标之间的差异（开头的大写 A）。但 shell 不会忽略：你用于给数组元素赋值的字符串在大小写上必须与你引用它的字符串完全一致。

## 6.2.3 答案

为了做到这一点，输入以下命令：

```
pluto=(domain=cs.qc.edu
  address=149.4.44.101
  building="Science Building" )
pluto.room=A-219
print $pluto
print ${pluto.domain} is in ${pluto.building},
room ${pluto.room}.
```

- a) 与关联数组 `venus` 相比，你如何访问复合变量 `pluto` 的元素？
答案：你的交互界面应该如下所示：
```
[6113]: typeset pluto
[6114]: pluto=(domain=cs.qc.edu
  address=149.4.44.101
  building="Science Building" )
[6115]: pluto.room=A-219
[6116]: print $pluto
  (building='Science Building' room=A-219
  address=149.4.44.101 domain=cs.qc.edu )
[6117]: print ${pluto.domain} is in ${pluto.building}, room ${pluto.room}.
pluto.qc.edu is in Science Building, room A-219
```

第一个区别是，你必须使用 `typeset` 命令来声明 `pluto`（或者通过给它赋值），但你不需要任何选项来指示 `pluto` 是复合变量。（对于关联数组，你必须使用 `typeset -A`。）

