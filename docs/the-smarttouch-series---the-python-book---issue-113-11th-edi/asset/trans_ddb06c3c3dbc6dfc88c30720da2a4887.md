

## 我们希望列表中包含的整数数量

```python
#!/usr/bin/env python2

# 我们将编写一个程序，要求用户输入任意数量的整数，将它们存储在集合中，
# 并演示该集合如何与各种控制结构一起使用。
import sys # 用于 sys.exit 函数
target_int = raw_input("多少个整数？")

# 此时，变量 target_int 包含用户输入内容的字符串表示形式。我们需要尝试将其
# 转换为整数，但要准备好处理如果它不是整数的错误。否则程序将崩溃。
try:
    target_int = int(target_int)
except ValueError:
    sys.exit("您必须输入一个整数")

# 一个用于存储整数的列表
ints = list()

# 这些用于跟踪我们当前拥有的整数数量
count = 0

# 继续请求输入整数，直到达到所需数量
while count < target_int:
    new_int = raw_input("请输入第 {0} 个整数:".format(count + 1))
    isint = False
    try:
        new_int = int(new_int)
        isint = True
    except:
        print("您必须输入一个整数")

# 只有当我们有一个整数时才继续。如果没有，我们将再次循环
# 注意下面我使用 ==，它与 = 不同。单个等号是赋值运算符，而双等号是
# 比较运算符。
if isint == True:
    # 将整数添加到集合中
    ints.append(new_int)
    # 将计数增加 1
    count += 1

# 此时，用户要么放弃，要么我们有一个装满整数的列表。我们可以在几种方式中循环遍历这些。第一种方式是使用 for 循环
print("使用 for 循环")
for value in ints:
    print(str(value))
```

## # 开始使用 Python

**提示**
如果你想在不传递任何变量的情况下调用函数，可以定义变量的默认值。你通过在变量名后面加一个等号来实现。例如

```python
# 或者使用 while 循环：
print("使用 while 循环")
# 我们在上面已经有了总数，但知道 len 函数非常有用。
total = len(ints)
count = 0
while count < total:
    print(str(ints[count]))
    count += 1
```

## 函数和变量作用域

函数在编程中用于将过程分解为更小的部分。这通常使代码更易于阅读。如果以特定方式设计，函数也可以重复使用。函数可以接受传入的变量。Python 中的变量始终是按值传递的，这意味着变量的副本被传递到函数中，并且仅在函数作用域内有效。在函数内部对原始变量所做的任何更改都将被丢弃。然而，函数也可以返回值，所以这不是问题。函数通过关键字 `def` 定义，后跟函数名。可以传入的任何变量都放在函数名后的括号中。多个变量由逗号分隔。在这些括号中赋予变量的名称是它们在函数作用域内的名称，无论传入函数的变量叫什么。让我们看看这个动作。

对面程序的输出如下：

> “函数在编程中用于将过程分解为更小”

我们现在位于 `modify_string` 函数的作用域之外，因为我们减少了缩进级别

测试字符串不会在这段代码中被更改

然而，我们可以这样调用函数

```python
#!/usr/bin/env python2

# 下面是一个名为 modify_string 的函数，它接受一个变量，该变量在函数作用域内
# 称为 original。在函数定义下方用 4 个空格缩进的任何内容都在作用域内。

def modify_string(original):
    original += " that has been modified."
    # 目前，只有此字符串的本地副本已被修改

def modify_string_return(original):
    original += " that has been modified."
    # 但是，我们可以将本地副本返回给调用者。函数在使用 return 语句时立即
    # 结束，无论它位于函数中的什么位置。
    return original

test_string = "This is a test string"
modify_string(test_string)
print(test_string)

test_string = modify_string_return(test_string)
print(test_string)
# 函数的返回值存储在变量 test_string 中，
# 覆盖了原始值，因此改变了打印出的值。
```

## # 开始使用 Python

```bash
[liam@liam-laptop Python]$ ./functions_and_scope.py
This is a test string
This is a test string that has been modified.
```

作用域是一个需要掌握的重要概念，否则可能会让你养成一些坏习惯。让我们快速编写一个程序来演示这一点。它将有一个名为 `cont` 的布尔变量，该变量将决定是否在 ‘if’ 语句中将数字赋值给变量。然而，该变量除了在 ‘if’ 语句的作用域外，在任何地方都没有定义。

我们将通过尝试打印该变量来完成。

```python
#!/usr/bin/env python2
cont = False
if cont:
  var = 1234
print(var)
```

在上面的代码段中，Python 会在打印之前将整数转换为字符串。然而，明确地将事物转换为字符串总是一个好主意 – 特别是当涉及到拼接字符串时。如果你试图在字符串和整数上使用 + 运算符，会出现错误，因为需要发生什么并不明确。+ 运算符通常会将两个整数相加。话虽如此，我们之前演示的 Python 字符串格式化器是执行此操作的更干净的方式。你看到问题了吗？`Var` 仅在 ‘if’ 语句的作用域中定义。这意味着当我们尝试访问 `var` 时会得到一个非常讨厌的错误。

```bash
[liam@liam-laptop Python]$ ./scope.py
Traceback (most recent call last):
  File "./scope.py", line 8, in <module>
  print var
NameError: name 'var' is not defined
```

如果将 `cont` 设置为 `True`，变量将被创建，我们可以正常访问它。然而，这是一种不好的做法。正确的方法是在 ‘if’ 语句的作用域之外初始化变量。

```python
#!/usr/bin/env python2

cont = False

var = 0
if cont:
  var = 1234

if var != 0:
  print(var)
```

变量 `var` 在比 ‘if’ 语句更广泛的作用域中定义，并且仍然可以由 ‘if’ 语句访问。在 ‘if’ 语句内部对 `var` 所做的任何更改都是更改较大作用域中定义的变量。此示例除了说明潜在问题外并没有做太多有用的事情，但最坏的情况已经从程序崩溃变为打印零。甚至那也不会发生，因为我们添加了一个额外的结构，在打印之前测试 `var` 的值。

## 编码风格

花一点时间谈谈编码风格是值得的。编写整洁的代码很简单。关键在于一致性。例如，你应该始终以相同的方式命名变量。无论你想使用 camelCase 还是像我们那样使用下划线，都没关系。一件关键的事情是为变量使用自文档标识符。你不应该不得不猜测一个变量的作用。与之相关的另一件事是始终注释你的代码。这将帮助任何阅读你代码的人，以及未来的你自己。在代码文件顶部放置一个简要总结，描述应用程序做什么，或者如果由多个文件组成，则描述应用程序的一部分，也很有用。

## 比较运算符

Python 中常见的比较运算符包括：

| 运算符 | 描述 |
| :--- | :--- |
| < | 严格小于 |
| <= | 小于或等于 |
| > | 严格大于 |
| >= | 大于或等于 |
| == | 等于 |
| != | 不等于 |

## 总结

本文应该已经向你介绍了 Python 编程的基础。希望你已经习惯了 Python 程序的语法、缩进以及整体外观和感觉。下一步是学习如何提出你想解决的问题，并将其分解为足够小的步骤，以便你能够在编程语言中实现。

谷歌或任何其他搜索引擎都非常有帮助。如果你在任何地方卡住了，或者有一个你不知道如何修复的错误消息，把它放进谷歌，你应该更接近解决你的问题。例如，如果我们搜索 ‘用 python 播放 mp3 文件’，第一个链接会将我们带到一个包含许多有用回复的 Stack Overflow 线程。不要害怕深入钻研 – 编程的真正乐趣在于一次解决一个可控块的问题。

快乐编程！

