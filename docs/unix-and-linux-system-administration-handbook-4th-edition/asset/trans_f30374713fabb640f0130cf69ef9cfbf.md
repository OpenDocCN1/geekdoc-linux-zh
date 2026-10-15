

第三行导入了 sys 模块，其中包含了 argv 数组。then 和 else 子句各有两行，且缩进级别相同。最后的 print 语句位于 if 语句的上下文之外。与 Perl 类似，Python 的 print 语句接受任意数量的参数。但与 Perl 不同，Python 在每对参数之间插入一个空格并自动提供换行。你可以通过在 print 行末尾加上一个额外的逗号来抑制换行；这个空参数告诉 print 不要输出换行字符。

行尾的冒号通常是提示该行引入并与随后跟随的缩进块相关联的线索。

```
$ python blockexample 1
a is one
This is still the then clause of the if statement.
This is after the if statement.
```

```
$ python blockexample 2
a is 2
This is still the else clause of the if statement.
This is after the if statement.
```

Python 的缩进约定使你在代码格式上具有的灵活性更少，但它具有的优点是使不同人编写的代码看起来相同，而且意味着你无需在代码中撒上烦人的分号来终止语句。

注释以井号（#）引入，并在行尾结束，就像在 bash 和 Perl 中一样。

你可以通过在行尾反斜杠来拆分长行。这样做时，只有第一行的缩进才有意义。你可以随意缩进续行。具有不平衡的圆括号、方括号或花括号的行即使没有反斜杠也会自动表示续行，但如果你认为这样能澄清代码结构，也可以包含反斜杠。

某些剪切和粘贴操作会将制表符转换为空格，除非你知道自己在寻找什么，否则这会让你抓狂。黄金法则是永远不要混合使用制表符和空格；对于缩进，使用其中一种即可。许多软件都做出传统假设，即制表符应落在 8 个空格间隔处，这对于可读代码来说缩进实在太多了。Python 社区的大多数人似乎更喜欢空格和 4 个字符的缩进。

无论你如何决定处理缩进问题，大多数编辑器都有选项可以帮助你保持理智，要么禁止使用制表符而只使用空格，要么以不同的方式显示空格和制表符。最后的办法，你可以使用 **expand** 命令将制表符转换为空格，或使用 **perl -pe** 将制表符替换为更易于识别的字符字符串。

## 对象、字符串、数字、列表、字典、元组和文件

Python 中的所有数据类型都是对象，这赋予了它们比在 Perl 中更多的功能和灵活性。

在 Python 中，列表用方括号括起来而不是圆括号。数组从零开始索引，这是本章涵盖的三种脚本语言中少数几个不变的概念之一。

Python 中新增的是“元组”，它们本质上是不可变的列表。元组比数组更快，并且有助于表示实际上应不可修改的数据。元组的语法与列表相同，只是分隔符是圆括号而不是方括号。由于 (thing) 看起来像一个简单的代数表达式，只包含单个元素的元组需要一个额外的逗号来消除歧义：(thing,).

以下是 Python 中一些基本的变量和数据类型操作：

```
#!/usr/bin/python

name = 'Gwen'
rating = 10
characters = [ 'SpongeBob', 'Patrick', 'Squidward' ]
elements = ( 'lithium', 'carbon', 'boron' )

print 'name:\t%s\nrating:\t%d' % (name, rating)
print 'characters:\t%s' % characters
print 'elements:\t%s' % (elements,)
```

此示例产生以下输出：

```
$ python objects
name: Gwen
rating: 10
characters: ['SpongeBob', 'Patrick', 'Squidward']
elements: ('lithium', 'carbon', 'boron')
```

Python 中的变量在语法上没有标记或按类型声明，但它们所引用的对象确实具有底层类型。在大多数情况下，Python 不会自动为你转换类型，但个别函数或运算符可能会这样做。例如，你不能在不显式将数字转换为其字符串表示形式的情况下连接字符串和数字（使用 + 运算符）。然而，格式化运算符和语句确实会将所有内容强制转换为字符串形式。每个对象都有一个字符串表示。

字符串格式化运算符 % 与 C 或 Perl 中的 sprintf 函数非常相似，但它可以在字符串出现的地方使用。它是一个二元运算符，左侧为字符串，右侧为要插入的值。如果要插入的值多于一个，则值必须以元组形式呈现。

