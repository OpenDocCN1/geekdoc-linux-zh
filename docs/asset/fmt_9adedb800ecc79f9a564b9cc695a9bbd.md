
重复使用 `next()` 函数调用生成器对象将继续执行函数，直到引发异常。可以通过将 `yield` 语句封装在一个无限循环中来避免这种情况，这样每次迭代都会返回下一个值。例如，要在每次调用时产生一个递增的值：

```python
def incrementer():
    i = 1
    while True:
        yield i
        i += 1

inc = incrementer()
print(next(inc))
print(next(inc))
print(next(inc))
```

这些调用显示整数值 1，然后是 2，然后是 3。

或许更有用的是，生成器对象可以从循环中引用，以依次遍历各个值。

![](img/d06b1f1cf83677f6647237f0c7827141_107_0.png)

将此循环中的条件测试更改为 `while i < 3` 将导致在第三次调用时引发 `StopIteration` 错误。

1. 通过定义一个函数来开始一个新的 Python 脚本，该函数首先将两个变量初始化为整数 1

```python
def fibonacci_generator():
    a = b = 1
```

![](img/d06b1f1cf83677f6647237f0c7827141_107_1.png)

2. 接下来，在函数体中插入一个缩进的无限循环，以生成前两个值之和

```python
while True:
    yield a
    a, b = b, a + b
```

3. 现在，将返回的生成器对象赋值给一个变量

`fib = fibonacci_generator()`

4. 最后，添加一个循环，依次调用生成器函数并在每次迭代中显示其值

```python
for i in fib:
    if i > 100:
        break
    else:
        print('Generated:', i)
```

5. 将文件保存在你的脚本目录中，然后在该目录下打开一个命令提示符窗口并运行此程序——以查看循环显示逐渐增大的生成值

![](img/d06b1f1cf83677f6647237f0c7827141_108_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_108_1.png)

在此处，变量通过一条语句初始化为相同的值。

![](img/d06b1f1cf83677f6647237f0c7827141_108_2.png)

你可以使用内置的 `type()` 函数来确认对象类型——此处，确认 `type(fib)` 为生成器类对象。

### 处理异常

在 Python 脚本中，某些部分（例如处理用户输入的部分）可能会预见到错误发生，这些部分可以被包裹在 `try except` 块中，以处理“异常错误”。要执行的语句被分组在 `try :` 块中，而异常则传递给随后的 `except :` 块进行处理。可选地，这之后可以跟一个 `finally :` 块，其中包含在异常被处理后需要执行的语句。

Python 识别许多内置异常，例如：`NameError`，当变量名未找到时发生；`IndexError`，当试图访问不存在的列表索引时发生；以及 `ValueError`，当内置操作或函数接收到值不适当的参数时发生。

每个异常都会返回一个描述性消息，该消息可以有用地通过 `as` 关键字赋值给一个变量。这样就可以在异常发生时，用来显示该异常的性质。

1. 通过初始化一个字符串值变量来开始编写新的 Python 脚本

```python
title = 'Python In Easy Steps'
```

![](img/d06b1f1cf83677f6647237f0c7827141_109_0.png)

`try.py`

2. 接下来，添加一个 try 语句块，尝试显示该变量的值 – 但错误地指定了名称

```python
try :
    print( titel )
```

3. 现在，添加一个 except 语句块，以便在发生 `NameError` 时显示错误消息

```python
except NameError as msg :
    print( msg )
```

4. 将文件保存到你的脚本目录中，然后在那里打开一个命令提示符窗口并运行此程序 – 以查看错误是如何被处理的

![](img/d06b1f1cf83677f6647237f0c7827141_110_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_110_1.png)

在 [http://docs.python.org/3/library/exceptions.html](http://docs.python.org/3/library/exceptions.html) 在线发现更多内置异常

可以通过在 `except` 块内的括号中指定以逗号分隔的类型列表来处理多个异常：

```python
except (NameError, IndexError) as msg:
    print(msg)
```

你还可以使用 `raise` 关键字强制解释器报告异常，通过指定要识别的异常类型以及括号中的自定义描述性消息来实现。

1. 通过初始化一个整数值变量来开始编写新的 Python 脚本

```python
day = 32
```

![](img/d06b1f1cf83677f6647237f0c7827141_110_2.png)

2. 接下来，添加一个 try 语句块，测试变量值，然后指定异常和自定义消息

```python
try:
    if day > 31:
        raise ValueError('Invalid Day Number')
    # More statements to execute get added here.
```

3. 现在，添加一个 except 语句块，以便在发生 `ValueError` 时显示错误消息

```python
except ValueError as msg:
    print('The Program found An', msg)
```

4. 然后，添加一个 finally 语句块，以便在异常被成功处理后显示一条消息

```python
finally :
    print(‘But Today Is Beautiful Anyway.’)
```

5. 将文件保存到你的脚本目录中，然后在那里打开一个命令提示符窗口并运行此程序 – 以查看引发的错误被处理

**Command Prompt**

```
C:\MyScripts>python raise.py
The Program Found An Invalid Day Number
But Today Is Beautiful Anyway.

C:\MyScripts> ▫
```

![](img/d06b1f1cf83677f6647237f0c7827141_111_0.png)

除非或直到发生异常，否则 try 块中的语句都会被执行。

### 调试断言

在追踪（调试）代码中的错误时，通常通过在每个行前添加 `#` 井号字符来“注释掉”一行或多行代码，这对定位问题所在很有用 – 就像用于注释那样。Python 解释器将忽略这些行的执行，从而有助于定位问题所在。例如，如果你怀疑变量赋值存在问题，可以像这样将其排除：

![](img/d06b1f1cf83677f6647237f0c7827141_112_0.png)

```python
# elem = elem / 2
```

如果程序现在没有错误地运行了，那么被注释掉的赋值就可以被假定为是有问题的。

另一种有用的调试技术是利用 Python 的 `assert` 关键字向脚本中添加错误检查代码。这会检查指定的测试表达式是否得到布尔 True 或 False 结果，并在测试失败时报告 “AssertionError”。可选地，assert 语句可以包含一个描述性消息，用于在报告 AssertionError 时提供，其语法如下：

`assert 测试表达式 , 描述性消息`

当测试表达式失败时，解释器报告 AssertionError 并停止脚本的执行；但当测试成功时，assert 语句不做任何事，脚本的执行继续。

使用 assert 语句是记录脚本的有效方式，因为其描述性消息提供了解释，并且其测试会在代码有错误时提醒你。

#### 断言与异常

乍一看，AssertionError 可能与 Exception 混淆相似，但重要的是要认识到它们的区别：

- `Exceptions` 提供了一种处理可能在运行时合法发生的错误的方法。
- `AssertionErrors` 提供了一种在开发期间提醒程序员注意错误的方法。
