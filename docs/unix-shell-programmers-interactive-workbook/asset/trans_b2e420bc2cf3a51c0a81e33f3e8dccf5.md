

# 第5章：参数 245

c) 编写一个 set 命令，其效果与第 5051 行等，但仅使用两个参数。

答案：你可以使用 --vudo，如如下命令行所示。交互的其余部分与示例中提供的相同：

```
[5051]: set --vudo hello
```

d) 编写另一个 set 命令，其效果与第 5051 行等，但使用了五个参数。

答案：你将使用 -v -u -d -o，如如下命令行所示。同样，交互的其余部分与示例中提供的相同：

```
[5051]: set --v -u -d -o hello
```

e) 如果再次运行 getopts 命令，optletter 会发生什么变化？

答案：它将被设置为一个问号（?），如下所示交互所示：

```
[5060]: getopts -douv optletter
[5061]: print optletter
?
```

```
[5062]:
```

在这个例子中，当 getopts 看到开头没有横字符的 hello 时，它知道没有更多选项了，并将 optletter 设置为问号，无论再被调用多少次。

> ![一顶高帽图像](image)

这里需要注意的关键点是，连续调用 getopts 会在 optletter 中返回连续的选项。即使你运行了完全相同的命令，命令的行为也不同。这意味着该命令有一种方法可以跟踪它已经处理了哪些选项。你能猜出这是如何做到的吗？（提示：(1) 这不能在 shell 内部完成，因为外部 getopts 的工作方式与内置命令相同；(2) 这一章是关于变量的。）你将在下一个练习中看到答案。

## 5.2.2 答案

A) 在完成上一个练习后，OPTIND 和 @ 的值是多少？

答案：OPTIND 为 3，@ 拥有三个值 -vu、-do 和 hello，如下交互所示：

```
[5062]: print $OPTIND: $@
3: -vu -do hello
[5063]:
```

注意，OPTIND 的值 (3) 是第一个位置参数 hello 的索引。

- b) 将 OPTIND 设置为 1，并证明这让你能够从头开始处理选项。

答案：你的交互应该如下：

```
[5063]: OPTIND=1
[5064]: getopts dou optletter
[5065]: print $optletter
v
[5066]: getopts dou optletter
[5067]: print $optletter
u
[5068]: getopts dou optletter
[5069]: print $optletter
d
[5070]: getopts dou optletter
[5071]: print $optletter
o
[5072]: print $OPTIND: $@
3: -vu -do hello
[5073]:
```

如果你将 OPTIND 设置为 2，你就可以从 -d 选项 own -v 开始。

c) 编写一个 shift 命令，使用 OPTIND 将 hello 放入参数 $1 中，并验证它是有效的。

答案：你必须从 OPTIND 的值中减一，如下交互所示：

```
[5073]: shift $OPTIND-1
[5074]: print $1
hello
[5075]:
```

第 5073 行的巧妙之处在于，相同的语句会将第一个位置参数放入变量 $1，无论用户在命令行上提供了多少选项（或在我们的示例 set 命令中），也无论在横字符后面放了多少选项。

## 5.2.3 答案

a) 将 $1 赋值给 OPTIND 的原因是什么？

答案：上一个练习可能让 OPTIND 留在一个非 $1 的值。set 命令对 OPTIND 没有影响；它只是设置参数的值。

现在运行以下成对命令三次：

```
getopts c optletter
print $OPTINDOPTARG
```

b) 每次打印了什么？

答案：你的交互应该如下：

```
[5075]: set --a -b -c hello
[5076]: OPTIND=1
[5077]: getopts c optletter
[5078]: print $OPTIND $OPTARG
2: a
[5079]: getopts c optletter
[5080]: print $OPTIND $OPTARG
4: b
[5081]: getopts c optletter
[5082]: print $OPTIND $OPTARG
5: c
```

## 实验 5.2：处理选项参数

```
5: c
[5083]: getopts c optletter
[5084]: print $OPTIND $OPTARG
5: ?
[5085]:
```

在这里你可以看到 OPTIND 正在逐一通过参数，跳过了数字 3，因为那是 -b 选项的参数位置。此外，注意第 5080 行是唯一一个为 OPTARG 打印非空值的行。每当选项后面跟着一个参数时，但当选项没有参数时，getopts 会取消 OPTARG 的值设置，因此在那些情况下它被打印为空字符串。

## 5.2.4 答案

运行以下命令：

```
set --a -b
OPTIND=1
getopts c optletter
```

- a. 显示了什么错误信息？

答案：Shell 显示在 -b 选项之后预期有一个参数，如下交互所示：

```
[5085]: set --a -b
[5086]: OPTIND=1
[5087]: getopts c optletter
[5088]: getopts c optletter
ksh: -b: argument expected
[5089]:
```

第 5087 行没有引起问题，因为 -a 不接受参数，所以它被 getopts 识别并接受。然而，当运行第 5088 行时，getopts 发现 -b 选项后面没有参数并生成了所示信息。如果你不知道错误信息开头的 ksh 是什么，下一个问题将会解释。

编写名为 s524 的脚本，仅包含命令 `getopts c optletter`，并使用命令行 `s524 -a -b` 运行它。

b) 与之前的相比，错误信息的开头有什么不同？

答案：它以 s524 开头，而不是 ksh:，如下交互所示：

```
[5089]: cat bin/s24
getopts c optletter
[5090]: s524 -b
s524: -b: argument expected
[5091]:
```

getopts 打印的错误以出错的命令名称开头，后面是出错的选项字母，最后是说明。(1) 你可以通过引用 $0 来做到这一点。(2) 如果 $0 显示字符串，请查看第 10 节。

```
getopts c bucketname optletter
```

将你 s524 脚本中的 getopts 命令替换为上面的命令，并在不提供参数的情况下再次运行它。

c) 你现在得到了什么错误信息？

答案：你的交互应该如下：

```
[5091]: cat bin/s24
getopts c [bucket] optletter
[5092]: s524 -b
s524: -b: bucketname argument expected
[5093]:
```

括号内的字符串打印在 -b: 和 argument expected 之间。你可以对该字符串进行任何格式设置。如果你想在字符串中使用空格或其他字符，必须将字符串（或整个 getopts 参数）放在引号内。

确保冒号（:）和括号之间没有空格。空格会标记 getopts 参数的结束，它会将括号视为本应接收值的无效名称。

如果你决定为带有参数的选项提供错误信息，请确保它在打印“argument expected”之前是有意义的。

## 实验 5.2 自测题

为了测试你的进展，你应该能够回答以下问题。

- 1) getopts 命令的第一个参数是什么？
a) 包含有效选项的变量名。
b) 有效选项的列表。
c) 接收选项值的变量名。
d) 有效选项的数量。
e) 出现问题时联系的人。

- 2) getopts 命令的第二个参数是什么？
a) 包含有效选项的变量名。
b) 有效选项的列表。
c) 接收选项值的变量名。
d) 有效选项的数量。
e) 出现问题时联系的人。

- 3) 如何指示必须跟随参数的选项字母？
a) 在 getopts 的第一个参数中选项字母后加一个冒号（:）。
b) 在 getopts 的第一个参数中将参数名称放在括号内。

