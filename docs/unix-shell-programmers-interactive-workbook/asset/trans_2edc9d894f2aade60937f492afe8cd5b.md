

# 302 实验 6.2: 数组与复合变量

g) ${!venus} 会打印什么？

输入以下命令：

```
venus[an arbitrary string]=hello
print "${venus[an arbitrary string]}"
print "${venus[an arbitrary string]}"
```

h) 打印了什么？

## 6.2.3 使用复合变量和约束函数（DISCIPLINE FUNCTIONS）

我们首先来看一下复合变量和关联数组之间的相似之处。为了这一点，请输入以下命令：

```
typeset pluto
pluto=(domain=.cs.gc.edu \
address=149.4.44.109 \
building="Science Building") 
pluto.room=A-219
print $pluto
print pluto${pluto.domain} is in ${pluto.building}, \
room ${pluto.room}.
```

a) 与关联数组 venus 相比，你如何访问复合变量 pluto 的元素？

# 第 6 章：高级变量用法 303

现在，让我们开始看看复合变量可以执行的操作，这些操作在关联数组中没有等价物。首先，复合变量可以包含任意数量的部分，这些部分按层次结构组织。术语上，你将复合变量的左部分称为所有右侧部分的父，而右部分称为左侧部分的子。

![](img/694fa9f0320e707804a4c650b96a09b4_322_0.png)

# 示例

假设你的某些工作站使用 IP 地址，另一些使用 IPX，还有一些使用 IPv6，每个地址信息的格式都不同。

输入以下命令设置 pluto 的地址类型、其 IP 地址和子网掩码：

```
pluto.address=IP
pluto.address.ip=149.4.44.109
pluto.address.mask=255.255.255
```

- b) address 是谁的子？
- c) address 是的父？
- d) pluto.address 的值是什么？

你还可以创建类似于复合变量的函数定义，称为约束函数（discipline functions）。它们允许你编写函数，每当对变量进行任何“有趣”的操作时，这些函数会自动运行。shell 允许对所有 shell 变量定义三种约束函数：get、set 和 unset。（有一种使用这三个之外的额外函数的机制，但这超出了本练习册的范围。）尽管约束函数与复合变量并没有真正的联系，但 shell 提供了一些你可以在编写约束函数时使用的复合变量。

# 304 实验 6.2: 数组与复合变量

# 实验 6.2

为了查看约束函数如何工作，请将以下代码输入到名为 ~/fun/pluto_stuff 的文件中并点（dot）该文件：

```
# pluto.set -- 用于 pluto 的约束函数。

function pluto.set {
    print -- "${sh.name}" was set to "${.sh.value}"
}

function pluto.get {
    print -- "${sh.name}" was referenced.
    sh.value=${.sh.name}:"a default value"
}

function pluto.unset {
    print -- "${sh.name}" has been unset.
}
```

现在输入以下命令：

```
unset pluto
pluto=hello
print -- This is pluto: \$pluto"
pluto.address="123 Main Street"
```

e) shell 在什么条件下会执行这三个约束函数？

# 第 6 章：高级变量用法 305

f) 当运行约束函数时，复合变量 .sh.name 和 .sh.value 的值是什么？
g) 当复合变量发生变化时，shell 会运行约束函数吗？

# 实验 6.2

# 实验 6.2 答案

本节为你提供了实验 6.2 中问题的某些答案，并对这些答案进行了讨论。你的答案可能会有所不同，但重要的是你的答案是否有效。利用这些讨论来分析你的答案与给出答案之间的差异。如果你对练习中的问题有替代答案，鼓励你在该书的配套网站发布你的答案并进行讨论，地址为：http://www.phptr.com/interactive/

# 6.2.1 答案

days [0]=Sunday
days [1]=Monday
days [2]=Tuesday
days [3]=Wednesday
days [4]=Thursday
days [5]=Friday
days [6]=Saturday

- a) 数组的名字是什么？
答案：数组的名字是 days。启动数组变量不需要任何特殊操作。只需在变量名后的方括号内放入下标即可。

# 实验 6.2: 数组与复合变量

- b) 你如何打印数组元素 5 的值？
答案：使用 ${...} 引用数组元素。你的交互应该如下：

```
[601]: print ${days[5]}
Friday
[602]:
```
确保将变量名和下标都放在大括号内![](img/694fa9f0320e707804a4c650b96a09b4_325_0.png)

- c) 如果尝试打印 days[7] 的值会发生什么？
答案：你的交互应该如下：

```
[602]: print Element 7 is: ${days[7]}
Element 7 is:
```
位置 7 没有被赋值，所以什么都没有打印。引用数组中未初始化的元素就像引用任何未初始化的变量一样：shell 不认为该引用是错误（除非你设置了 noun 选项），并用空字符串作为值。

- d) 如果尝试打印 days[496] 的值会发生什么？
答案：你的交互应该如下：

```
[603]: print ${days[496]}
ksh: days: subscript of range
[604]:
```
你可以使用的最大下标值是 95。

- e) 如果尝试使用 -1 作为下标会发生什么？
答案：你的交互应该如下：

```
[604]: print ${days[-1]}
ksh: days: subscript of range
[605]:
```
你可以使用的最小下标值是零。

# 第 6 章：高级变量用法 307

- f) 如果你使用 3.7 作为下标会发生什么？
答案：你的交互应该如下：

```
[605]: print ${days[3.7]}
Wednesday
[606]:
```
使用非整数作为下标的值是可以的，但 shell 会通过截断数字将其静地转换为整数。小数部分会被丢弃，不进行任何四舍五。在当前情况下，结果与打印 ${days[3 ]} 相同。

- g) 如果不使用任何下标直接打印 days 的引用会发生什么？
答案：你的交互应该如下：

```
[606]: print ${days}
Sunday
[607]:
```
如果你不带任何下标引用数组，你会得到数组第一个元素的值。这种灵活性反过来也适用：如果你已经有一个标量变量（不是数组的变量的名称），你只需通过下标为数组的其他元素赋值，就可以将其转换为数组。你分配给标量的值将保持为元素零的值。

> 你可以把同一个变量名既视为标量又视为数组。这可能很方便，但会让程序变得难以理解![](img/694fa9f0320e707804a4c650b96a09b4_326_0)

- h) 如果使用字符串 hello 作为下标会发生什么？
答案：你可能会看到如下交互：

```
[607]: print ${days[hello]}
Sunday
[608]:
```即使给 hello 加上引号（单引号或双引号），也没有什么让它明确成为字符串；它可能是你想要作为下标的另一个变量的名字。赋值一个 5 给变量 TGIF。

# 6.2

# 308 实验 6.2: 数组与复合变量

然而，即使你把 hello 放在引号中，也没有让它是字符串；它可能是你想要作为下标的变量的名字。

- i) 你如何使用 TGIF 的值打印 days 的第六个元素的值？
答案：你的交互应该如下：

```
[608]: TGIF=5
[609]: print ${days[TGIF]}
Friday
[610]:
```
Friday 是 days[5] 的值。

问题中的 hello 和这个问题中的 TGIF 唯一区别在于第 608 行在使用下标之前给 TGIF 赋值了，而 hello 从未被赋值。

shell “知道”方括号内必须是一个数字，所以如果你给它一个字符串，它会自动检查字符串是否可以作为变量名以及变量的值是否可以作为数字。你不需要使用美元符号告诉 shell 去评估变量。

> 在下标方括号内编写的内容被称为算术表达式。编写算术表达式的规则在练习 6.1.2 中介绍。

![](img/694fa9f0320e707804a4c650b96a09b4_327_0.png)

使用 @ 作为下标打印 days 的值。

- j) shell 打印了什么？
答案：你的交互应该如下：

```
[610]: print ${days[@]}
Sunday Monday Tuesday Wednesday Thursday Friday Saturday
[611]:
```
正如符号 @ (@) 在函数或脚本内部作为变量名使用时引用传递给函数或脚本的所有参数列表一样，它

