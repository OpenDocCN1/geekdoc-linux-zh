

object, such as entries in a Python dictionary. The sort method is a list method that works on Python lists (there is no need to type in the comments).

```
>>> K = {'x':1, 'y':2, 'z':3}      #creates the dictionary
>>> K
{'y':2, 'x':1, 'z':3}             #not a sequence, thus comes
                                 #back in any order
>>>for key in sorted(K):
...     print key, '=', K[key]     #press Enter twice here
...
x = 1
y = 2
z = 3
>>>
```

## 16.3.12 生成器

一种 Python 函数式程序执行技术，它利用数据流、流和进程管道的高级编程方法，并在函数逐步执行时保留输出生成的状态，被称为生成器。生成器仅在调用 next 方法（或 Python 3.X 中的 next()）时才产生一组输出结果。next 方法由 Python 的 yield 语句执行。当需要在程序执行期间的特定时间按需、可能分步创建大量数据时，就会调用生成器函数。next 内置函数逐步引导你并生成输出。以下示例展示了如何创建和调用生成器函数（无需输入注释）：

### 示例 16.15

```
>>> def generadd(Q):
...     for i in range(Q):
...         yield i      #generates the next value
...         i += 1
...
>>> for i in generadd(4):  #whenever the function is called,
                          #the values are generated
...     print i
...
0
1
2
3
>>> z = generadd(6)        #this passes 6 to generadd
>>> z                     #this will show you the compiled
generator object
<generator object generated at 0x284f6f4>
>>> next(z)               #the next built-in steps you
                        #through and generates the value
```

```
0
>>> next(z)
1
>>> next(z)
2
>>> next(z)
3
>>> next(z)
4
>>> next(z)
5
>>> next(z)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>>
```

以下示例展示了如何在名为 regen.py 的文件中实现递归生成器函数，该文件可使用你喜欢的文本编辑器创建。首先按所示创建文件 regen.py，然后使用 Way3（导入脚本模式）完成本章练习 16.8：

### 示例 16.16

```
def abc():
    a = deff()
    for i in a:
        yield i
    yield 'abc'
def deff():
    a = ijk()
    for i in a:
        yield i
    yield 'deff'
def ijk():
    for i in (1, 2, 3):
        yield i
    yield 'ijk'
```

## 练习 16.8

- 1. 给出将示例 16.16 中的三个函数导入 Python 解释器的确切 Python 代码，假设必须使用 Way 3（导入脚本模式）。
- 2. 给出在 Python 命令行上调用示例 16.16 中的三个函数的确切 Python 代码。

3. 给出允许你逐步执行示例 16.16 中三个函数的调用以生成其输出结果直到达到 StopIteration 的确切 Python 代码。列出递归过程中每一步生成的输出。

## 16.3.13 协程

在上一节中，我们介绍了生成器函数，它们使用 yield 提供输出结果。Python 生成器函数也可以使用 yield 语句“消费”结果。此外，应用于生成器对象的两个新方法 send() 和 close() 为消费和提供值的对象创建了一个框架。定义这些对象的生成器函数称为协程。协程使用 yield 语句在表达式的右侧消费值，如下所示。

```
value = (yield)
```

使用此语法，执行在此语句处暂停，直到使用参数调用对象 send 方法：

```
coroutine.send(data)
```

然后，执行恢复，value 被赋值为 data 的值。为了表示计算结束，我们使用 close() 方法关闭协程。这会在协程内部引发 GeneratorExit 异常，我们可以用 try/except 子句捕获它。

下一个示例说明了这些概念。它是一个协程，用于打印匹配提供的模板模式的字符串：

### 示例 16.17

```
>>>def grepper(template):
...     print ('Searching for ' + template)
...     try:
...         while True:
...             x = (yield)
...             if template in x:
...                 print x
...     except GeneratorExit:
...         print "Done"
...
>>> q = grepper("Pythonista")
>>> q.next()
Pythonista
>>> q.send("After doing this section, you will be known as a Pythonista")
After doing this section, you will be known as a Pythonista
>>> q.send("Not a very Pythonic answer")
