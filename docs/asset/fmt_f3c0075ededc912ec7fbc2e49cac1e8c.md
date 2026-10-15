
## 16.3.12 生成器

一种 Python 函数式程序执行技术，它利用数据流、流和进程管道的高级编程方法，并在函数逐步执行时保留输出生成的状态，被称为生成器。生成器仅在调用 `next` 方法（或 Python 3.X 中的 `next()`）时才产生一组输出结果。`next` 方法由 Python 的 `yield` 语句执行。当需要在程序执行期间的特定时间按需、可能分步创建大量数据时，就会调用生成器函数。`next` 内置函数逐步引导你并生成输出。以下示例展示了如何创建和调用生成器函数（无需输入注释）：

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

以下示例展示了如何在名为 `regen.py` 的文件中实现递归生成器函数，该文件可使用你喜欢的文本编辑器创建。首先按所示创建文件 `regen.py`，然后使用 Way3（导入脚本模式）完成本章练习 16.8：

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
- 3. 给出允许你逐步执行示例 16.16 中三个函数的调用以生成其输出结果直到达到 `StopIteration` 的确切 Python 代码。列出递归过程中每一步生成的输出。

## 16.3.13 协程

在上一节中，我们介绍了生成器函数，它们使用 `yield` 提供输出结果。Python 生成器函数也可以使用 `yield` 语句“消费”结果。此外，应用于生成器对象的两个新方法 `send()` 和 `close()` 为消费和提供值的对象创建了一个框架。定义这些对象的生成器函数称为协程。协程使用 `yield` 语句在表达式的右侧消费值，如下所示。

```
value = (yield)
```

使用此语法，执行在此语句处暂停，直到使用参数调用对象 `send` 方法：

```
coroutine.send(data)
```

然后，执行恢复，`value` 被赋值为 `data` 的值。为了表示计算结束，我们使用 `close()` 方法关闭协程。这会在协程内部引发 `GeneratorExit` 异常，我们可以用 `try/except` 子句捕获它。

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
```
>>> q.send("Python makes C look high maintenance and too complex*")
>>> q.close()
Done
>>>
```

当我们调用 `q.send` 时传入一个值，协程 `q` 中的求值会在语句 `line= (yield)` 处恢复，其中发送的值被赋给变量 `line`。求值在 `q` 内部继续，如果该行匹配则打印出来，循环进行直到再次遇到语句 `line= (yield)`。然后，求值在 `q` 内部暂停并恢复到调用 `q.send` 的位置。

我们可以将调用 `send()` 的函数与产生 `yield` 的函数串联起来，以实现复杂的行为，类似于流式处理或管道处理，这在本书前面关于 shell 编程的章节中已有说明。在下一个示例中，函数 `read` 将名为 `text` 的字符串拆分为单词并将每个单词发送给另一个协程。

## Example 16.18

```
>>> def read(text, next_coroutine):
...     for line in text.split():
...         next_coroutine.send(line)
...     next_coroutine.close()
```

每个单词都被发送到绑定到 `next_coroutine` 的协程，导致 `next_coroutine` 开始执行，而该函数暂停并等待。它等待直到 `next_coroutine` 暂停，此时该函数通过发送下一个单词或以 Done 退出而恢复。

如果我们将此函数与示例 16.17 中定义的函数 `grepper` 组合成管道，我们可以创建一个程序，只打印出匹配特定单词的单词。

```
>>> text = "0110 1100 0101 1000 1010 0111 1111 0001 0110"
>>> found = grepper('01')
>>> found.next()
Looking for 01
>>> read(text, found)
0110
0101
1010
0111
0001
0110
Done
>>>
```

`x = (yield)` 等待每个发送的单词，并在到达时将控制权交还给 `read`。

## EXERCISE 16.9

- 1. (a) 将示例 16.17 中的代码放入一个文件中（如果尚未完成），并使用方式 3（导入脚本模式），在模板 `"1201"` 上调用协程 `grepper`。
- (b) 然后使用该模板搜索以下内容：`"0120 1201 1020"`、`"3012 3013 3212"`、`"12010203101213012"`。
- (c) 当你使用适当的命令时，屏幕上会打印出什么，与示例 16.17 中函数定义后的后续代码所示类似？
- 2. (a) 将示例 16.18 中的代码放入一个文件中（如果尚未完成），并使用方式 3（导入脚本模式），在字符串 `"Python is the most Pythonic enterprise a Pythonista can practice"` 上调用协程 `read`。
- (b) 然后使用协程 `grepper` 和 `read` 搜索字符串 `"Python"`。
