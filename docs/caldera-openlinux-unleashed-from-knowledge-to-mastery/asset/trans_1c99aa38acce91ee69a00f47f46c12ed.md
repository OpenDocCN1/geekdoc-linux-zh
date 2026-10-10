

我们已经复习了绝对基础的内容；现在准备好对 Python 的“内部结构”进行一次快速概览。在下一节中，我们将加快节奏，介绍你可以利用的强大功能。

## Python 的强大功能

为了驾驭 Python 的强大功能，我们首先需要了解如何将代码块分离为逻辑组。Python 使用一种简单而优雅的方法来完成这项任务——缩进：

```python
a=1
while a < 10:
    print a
    a = a + 1
print “done!”
```

在这里我们看到了一个 while 循环的示例。Python 明白缩进的行是 while 循环的一部分，而最后一个 print 命令不是。这不仅使 Python 代码更容易阅读，还消除了一类主要的编程错误来源——程序块的不正确终止。对于那些可能不熟悉 while 循环（它们在大多数结构化编程语言中都被使用）的人，让我们回顾一下代码。首先，我们将对象设置为整数值 1。然后，我们进入 while 循环，只要“while”后面的表达式求值为真（1），它就会执行。每次 while 循环求值时，会执行接下来的两行代码（print a 和 a = a + 1）。当 while 表达式求值为假时，循环终止并执行最后一行。

### 列表处理能力

看看下面这个片段：

```python
mylist=['We',"are","the","knights","who","say","Ni!"]
for x in mylist:
    print x,
print
```

在这个例子中，我们看到了一种清晰且富有表现力的语法和格式，使 Python 易于阅读和理解。让我们更仔细地研究一下代码。

我们做的第一件事是创建一个由七个字符串组成的列表。列表是一个有序的数据集合，可以动态修改——把它们想象成动态数组。第二行是一个 for 语句；它遍历列表 mylist 中的每个项（从左到右），每次将 x 赋给一个新值（这与 bash shell 评估 for 循环的方式类似）。最后一个 print 命令完成该行，因为循环中的 print 命令以逗号结尾，以抑制换行符的打印。

让我们进一步探索列表。在交互模式下启动 Python 解释器，并完全按照前面片段中的类型定义一个 mylist 对象。尝试以下命令：

```python
>>> mylist
['We', 'are', 'the', 'knights', 'who', 'say', 'Ni!']
>>> len(mylist)
7
>>> mylist[0]
'We'
>>> mylist[6]
'Ni!'
>>> mylist[2:4]
['the', 'knights']
```

内置函数 len() 告诉我们列表的长度。注意，在最后一条命令中，我们如何指定列表中项目的范围。以下是一些更高级的列表表达式：

```python
>>> mylist[1:-1]
['are', 'the', 'knights', 'who', 'say']
>>> mylist[1:100]
['are', 'the', 'knights', 'who', 'say', 'Ni!']
>>> mylist[1:1]
[]
>>> mylist[1:2]
['are']
>>> mylist[2:2]
[]
>>> mylist[-3:-2]
['who']
>>> mylist[-2:-3]
[]
```

在第一行中，我们使用负偏移量指定列表范围。当列表索引前面有一个负号时，意味着列表项是从右侧指定的。例如，-1 元素是 'Ni!'，-2 元素是 'say'，等等。现在，注意第二条命令以及我们如何指定了一个越界的非常大范围——Python 为我们着想，简单地将会范围设置为最大的可能“右侧”值，不费吹灰之力。看倒数第二条命令，看看我们如何使用两个负索引，这是完全合法的。这简单地评估为从“右起第三个”（第四个）到“右起第二个”（第五个）元素的切片。切片中的最后一个元素不包含在内；这意味着 mylist[1:1] 评估为一个空列表。这带来了一个额外的好处，我们稍后还会涉及。

### 列表处理运算符

以下是你可以对列表执行的一些额外运算符：

| 运算符 | 描述 |
| :--- | :--- |
| value (not) in mylist | 如果 value 存在于 mylist 中则返回 1；否则返回 0 |
| mylist * intvalve | 返回 mylist 的 intvalve 份副本，拼接在一起 |
| min(mylist) | mylist 中数值最小的值 |
| max(mylist) | mylist 中数值最大的值（min() 和 max() 也适用于字符串） |

你刚才学到的关于列表索引和范围的大部分知识都可以完全应用于字符串值。例如：

```python
>>> mystring='I am a string'
>>> mystring
'I am a string'
>>> mystring[-1]
'g'
>>> mystring[1:-1]
' am a strin'
>>> mystring[-3:-1]
'in'
>>> len(mystring)
13
```

嵌入换行符和控制字符也是可能的。与许多语言一样，你可以使用 `\` 序列来指定特殊字符序列。`\n\n` 是一个包含两个换行符的字符串，`\n\t` 包含一个换行符和一个制表符，`\'\"` 包含双引号和单引号，`\032\xff` 是一个包含八进制值为 32 的 ASCII 字符和十六进制值为 1f 的另一个字符的字符串。

鼓励你启动 Python 解释器，玩玩字符串和列表索引，以便你了解它们的工作方式。

## 更多序列类型

简单来说，序列类型是 Python 中“类似数组”的数据类型，包括字符串、列表和元组。我们已经涉及了字符串和列表，但在深入研究元组之前，了解列表和字符串之间的一个主要区别至关重要：它们的可变性。

### 字符串的可变性

字符串不是可变的。这意味着一旦定义了一个字符串对象，单个字符就不能动态更改为新值。例如：

```python
>>> mytest="Are you mutable?"
>>> mytest[3]='r'
Traceback (innermost last):
  File "<stdin>", line 1, in ?
AttributeError: __setitem__
>>>
```

当我们试图将字符串的第三个字符设置为新值时，解释器卡住了并打印出一个堆栈跟踪。请注意，你可以始终将 *mytest* 重新赋值为一个新的字符串值，但你不能将单个字符设置为新值。从实际角度看，不可变性意味着序列类型中的实际数据是“只读”的。

### 列表的可变性

然而，列表是可变的。单个列表项可以在程序中的任何时候被赋新值。以下是一些示例：

```python
>>> mylist=["This", "is", "a", "test", "of", "mutability!"]
>>> mylist[3]="example"
>>> mylist
['This', 'is', 'a', 'example', 'of', 'mutability!']
>>> mylist[2]='an'
>>> mylist
['This', 'is', 'an', 'example', 'of', 'mutability!']
>>> mylist[5:5]=['wacky']
>>> mylist
['This', 'is', 'an', 'example', 'of', 'wacky', 'mutability!']
>>> del mylist[5]
>>> mylist
['This', 'is', 'an', 'example', 'of', 'mutability!']
>>> mylist.append("The End.")
>>> mylist
['This', 'is', 'an', 'example', 'of', 'mutability!', 'The End.']
```

首先，我们创建一个名为 *mylist* 的新列表。几行之后，我们开始有点滑稽，将单词 'wacky' 插入到列表中。注意，我们使用一个评估为空列表的范围（5:5）。当我们为这个范围赋值新值时，会插入一项。然后我们决定插入这样一个奇怪的词有点过火了，使用 `del` 语句删除了 'wacky' 列表项。最后，我们使用 `append` 方法将字符串添加到列表末尾。

## del 语句

**del** 语句是一个基本工具。使用 **del**，我们可以删除已经定义的对象和可变列表的部分。我们可以使用 **del** 来“清除”几乎任何东西：

```python
>>> mylist
['This', 'is', 'an', 'example', 'of', 'mutability!']
>>> del mylist
>>> mylist
Traceback (innermost last):
  File "<stdin>", line 1, in ?
NameError: mylist
```

如你所见，我们删除了整个列表，并且 **mylist** 现在是未定义的。

### 使用 del 进行大扫除

在 Python 这样的语言中，可以轻松动态创建非常大的对象，这非常容易快速消耗大量内存。一旦你使用完一个大对象并且不再需要它（例如包含几百个或更多项目的列表），建议 **del** 它，以便 Python 可以立即释放为该数据保留的内存。

通过帮助 Python “打扫一下房子”，你的程序将占用更小的内存空间并运行得更快。

## 值 None

特殊值 **None** 可用于“清空”一个对象而不重新定义它。

```python
>>> val=[1,2,3,4,5,6,7]
>>> val
[1, 2, 3, 4, 5, 6, 7]
>>> val=None
>>> val
>>>
```

注意 **val** 不包含任何数据，但仍然被定义。这很实用——我们可以按以下方式创建一个包含两个“空”对象的列表：

```python
>>> val=[None,None]
>>> val
[None, None]
```

**None** 是一个保留字，可用于赋值和比较。我们可以在 **if** 语句中测试某物是否等于 **None**，或在 while 语句中使用 **None** 值作为终止符。**None** 的一个常见用途是从文件中读取单行：

