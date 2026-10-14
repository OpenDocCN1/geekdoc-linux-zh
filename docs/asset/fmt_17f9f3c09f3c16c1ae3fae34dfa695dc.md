
'PythonPythonPythonPython'

>>> `mystring` = `mystring` + " rocks!"

>>> `mystring` * 2

'Python rocks! Python rocks!'

除了使用运算符，Python 字符串还有一系列内置方法。你可以使用 `capitalize()`（首字母大写）、`upper()`（所有字母大写）、`lower()`（所有字母小写）、`title()`（每个单词的首字母大写）、`swapcase()`（切换大小写）和 `strip()`（移除空白）来更改字母的大小写。

它已经改变了。这就是可变性的本质：你在没有创建新列表的情况下更改列表。然而，编辑字符串会创建一个新字符串，而旧的字符串保持不变。
这是一个示例：

```
>>> mystring = "hello"

>>> list3 = [1, mystring, 3]

>>> list3

[1, 'hello', 3]

>>> mystring = "world"

>>> list3

[1, 'hello', 3]
```

当然，这引发了一个在引用是默认情况下，你如何在不使用引用的情况下进行复制的问题。对于列表，答案是使用在本章稍早介绍过的 `[:]` 切片。它从第一个元素切到最后一个元素，本质上是对其进行了进行了不带引用的复制。它的工作原理如下：

```
>>> list4 = ["a", "b", "c"]

>>> list5 = list4[:]

>>> list4 = list4 + ["d"]

>>> list5

['a', 'b', 'c']

>>> list4

['a', 'b', 'c', 'd']
```

列表有自己的一套内置方法，如 `sort()`、`append()` 和 `pop()`。后者在列表末尾添加和删除单个元素，`pop()` 还会返回被删除的元素。这是一个示例：

```
>>> list5 = ["nick", "paul", "Julian", "graham"]

>>> list5.sort()

>>> list5

['graham', 'julian', 'nick', 'paul']

>>> list5.pop('paul')

>>> list5

['graham', 'julian', 'nick']

>>> list5.append("Rebecca")
```

此外，字符串的一个有趣方法返回一个列表：`split()`。它接收一个字符作为分割标识符，并给你一个列表，其中每个元素都是字符串中的一个块。
这是一个示例：

```
>>> string = "This is a test string;"

>>> string.split(" ")

['This', 'is', 'a', 'test', 'string']
```

# 字典

列表在 Python 中被广泛使用，尽管随着语言的成熟，这种情况正在发生变化。在 3.x 中，列表比较和排序的方式发生了变化，因此在尝试执行这些任务时，务必检查最新文档。

与列表不同，字典是一个没有固定顺序的集合。相反，它有一个键（元素的名称）和一个值（元素的内容），Python 会为了最大化性能将字典放置在任何它需要的地方。定义字典时，你使用大括号 `{}` 和冒号 `:`。你从一个左括号开始，然后给出每个键和值，用逗号隔开，如下所示：

```
>>> mydict = { "perl": "a language", "php": "another language" }

>>> mydict

{'php': 'another language', 'perl': 'a language'}
```

这个示例有两个元素，分别是 `perl` 和 `php`。然而，当打印字典时，你会发现 `dict` 出现在 `perl` 之前；Python 并没有遵循你输入它们的顺序。你可以通过使用冒号来对字典进行索引：

```
>>> mydict["perl"]

'a language'
```

然而，由于字典没有固定的序列，你无法通过位置获取切片或索引。

和列表一样，字典是可变的，并且可以嵌套；但是，与列表不同的是，你不能通过使用 `+` 来合并两个字典。这是因为字典的元素是位于键中的。因此，你应该使用 `update()` 方法，它通过覆盖冲突的键来合并两个数组。

你还可以使用 `keys()` 方法返回字典中所有键的列表。

3.x 中字典的使用方式与 2.x 相比存在细微差异，因此我们需要让列表调用一次性产生所有值以便打印。再次强调，在你继续学习时，请务必检查最新文档，因为功能上有几处这样的变化，某些工具的行为发生了变化，或者添加了其他新的字典工具。其中一些功能已经进行了后向移植（backported）；例如，Python 2.7 接收了从 Python 3.1 (`https://docs.python.org/dev/whatsnew/2.7.html#peg-0372`) 移植而来的对有序字典（ordered dictionaries）的支持。

# 条件判断与循环

到目前为止，我们只是在看数据类型，这应该向你展示了 Python 数据类型有多强大。然而，没有条件语句和循环，你就无法编写复杂的程序。

Python 拥有大多数标准的条件检查，如 `>`（大于）、`<=`（小于等于）和 `==`（等于），但它也添加了一些新的。例如，我们可以使用 `in` 来检查字符串或列表是否包含给定的字符或元素：

```
>>> mystring = "J Random Hacker"

>>> "e" in mystring

True

>>> "Hacker" in mystring

True

>>> "hacker" in mystring

False
```

这个示例演示了字符串是如何区分大小写的。你可以在列表中使用相等运算符，来：

```
>>> mylist = ["soldier", "sailor", "tinker", "spy"]

>>> "tailor" in mylist

False
```

对这些复杂数据类型进行其他比较是逐项完成的：

```
>>> list1 = ["alpha", "beta", "gamma"]

>>> list2 = ["alpha", "beta", "delta"]

>>> list1 > list2

True
```

在这种情况下，`list1` 的第一个元素 (`alpha`) 与 `list2` 的第一个元素 (`alpha`) 进行比较。如果它们相等，则比较下一个元素。如果一个列表比另一个长，并且所有剩余元素都相等，则较长的列表被认为更大。

循环用于重复执行多次代码。循环有两种：`for` 和 `while`。`for` 循环用于迭代序列，如列表、字符串或 `range`。`while` 循环在特定条件为真时持续。

```python
for fruit in ["apple", "banana", "cherry"]:
    print(fruit)

i = 0
while i < 5:
    print(i)
    i += 1
```

你可以使用 `break` 和 `continue` 关键字控制循环。`break` 退出循环，而 `continue` 跳到下一次迭代。

```python
for i in range(10):
    if i == 3:
        continue
    if i == 7:
        break
    print(i)
```

嵌套循环是在循环内部循环。这在处理多维数据时很常见。

```python
for i in range(3):
    for j in range(2):
        print(i, j)
```

# 函数

函数是一个只在调用时才运行的代码块。函数帮助你组织代码并使其可重用。在 Python 中，函数使用 `def` 关键字定义。

```python
def greet(name):
    print("Hello, " + name + "!")

greet("Alice")
```

函数可以接收参数，即传递给函数的值。

```python
def add(a, b):
    return a + b

result = add(5, 3)
print(result)
```

函数还可以有默认参数值。

```python
def greet(name="Guest"):
    print("Hello, " + name + "!")

greet()
greet("Bob")
```
