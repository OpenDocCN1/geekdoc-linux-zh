
条件允许所有常用的数学比较（`==`、`!=`、`>`、`<`、`<=`）。注意，你不能在 `if` 语句的条件测试中使用单等号 `=`。单等号用于赋值。双等号用于“等于”。

与 C 语言语言一样，Python 的 `if` 语句并不测试实际值，而是确定简单的真或假。如果条件为真，它的返回码为非零，而为假的返回码为零。返回码的值决定了 `if` 或 `else` 下方的语句是否被执行。

```python
X = 4

Y = 5

if X > Y:
    print A
```

Python 还允许使用 `elif` 结构。你可以有多个级联的 `elif`，这对于分支测试来说可能是必要的，因为 Python 不提供 `switch` 或 `case` 语句。以下是一个使用 `elif` 的示例：

```python
#!/usr/bin/python

if var2 >= 10:
    print 'The value is greater than or equal to ten'
elif var2 <= 5:
    print 'The value is less than five'
else:
    print 'The value is between five and ten'
```

Python 允许几乎无限数量的嵌套，尽管在嵌套过多后你的代码会开始变得缓慢。如果你需要嵌套深度超过三四层，可能应该尝试寻找更好的方法。

```python
#!/usr/bin/python

if var1 < 10:
    var2 = 0
    print "the value is less than ten"
```

```python
else:
    var2 = 1
    print 'the value is ten or more'
```

![](img/f36419c0b225d12fa66de83fa271829b_894_0.png)

## for 循环

循环用于遍历列表或字符串。属于 `for` 语句的语句不能以任何方式修改列表或字符串。Python 中 `for` 循环的语法如下：

```
for var in list or string:
    statements
```

与 `if` 语句一样，Python 通过缩进来确定 `for` 循环体的位置。`for` 语句结尾的冒号也指示解释器继续执行。前语句中的 `var` 假设为列表或字符串中的各个值。

以下简单的 `for` 循环遍历字符串：

```
for ltr in "Hello World":
    print ltr,
```

前面的代码打印字符串的每个字母，后面跟着一个空格：

```
Hello World
```

> 注意
> `print` 语句末尾的逗号会消除输出中的换行符，取而插入单个空格。

“列表与 range()”部分将更详细介绍 `for` 循环。

## 列表和 range() 函数

列表是零或多个项的任何序列。你可以使用括号在 Python 中指定一个列表。使用数字的简单列表看起来像：

```
A = [1, 2, 3, 4, 5]
```

这个名为 `A` 的列表有五个元素。你可以通过变量名调回整个列表，如此代码示例所示：

```
A = [1, 2, 3, 4, 5]
print A
```

前面的代码简单打印括号中的列表，如输出所示：

```
[1, 2, 3, 4, 5]
```

## 开发环境

要调回列表中的任何单个元素，你可以使用变量名和括号中的元素数字下标，如下所示。记住 Python 是一种从零开始索引的语言，这意味着元素的计数从零开始。

```
A = [1, 2, 3, 4, 5]
print A[2]
print A[0]
```

前面的代码打印 3 (`A[2]`)，然后是 1 (`A[0]`)。如果你尝试访问不存在的元素，通常会收到来自解释器的错误消息。

> 注意
> 尽管 Python 对列表中的元素执行了一些边界检查，你不应期望 Python 能够确保你的列表元素是正确的。例如，虽然列表只有五个元素时，Python 会拒绝对 `A[10]` 的引用，但 Python 允许使用 `A[-4]` 引用同一个列表。我们在这里不会讨论负索引元素的用法，但在代码中使用列表元素时应小心，以防止程序出现错误。

### 使用字符串创建列表

你可以同样轻松创建字符串列表，用逗号分隔每个字符串并用引号包裹每个字符串：

```
A = ["Python", "powerful", "is", "language", "a"]
print A[0], A[2], A[4], A[1], A[3]
```

前面的代码按照 `print` 语句中调用的顺序列出 `A` 的元素，输出句子“Python is a powerful language”。你可以同样轻松地混合字符串和数值列表。如果你正确定义了每个元素，Python 允许你随所欲地操作它们：

```
Z = [ 5, "good", "is", 6, "This", 2]
print Z[4], Z[2], Z[1]
print Z[0] + Z[3] / Z[5]
```
