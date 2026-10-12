
这会将导入模块中的所有名称（复制）到本地命名空间。这种最后的形式应谨慎使用，仅适用于专门设计为这样工作的模块。`from ... import` 可能会无警告地覆盖本地命名空间中的变量。

一旦导入，模块中定义的所有名称（变量、函数和类）都可以通过模块名限定来访问：

```python
>>> import sys, getpass

>>> sys.path # sys 模块中的属性

['/usr/local/lib/python/', '/usr/local/lib/python1.5/',

 '/usr/local/lib/python1.5/plat-linux2', '/usr/local/lib/python1.5/lib-tk',

 '/usr/local/lib/python1.5/lib-dynload']

>>> pw = getpass.getpass() # getpass 模块中的函数

Password: 

  >>> print pw

mypassword
```

# Python

## raise

`raise`

用于重新抛出当前由异常处理器处理的最后一个异常。

```
raise exception [ , parameter ]
```

抛出一个新异常，该异常将由外层的异常处理器处理，或会导致程序执行停止。见下文 `try`。

## assert

```
assert expression [ , parameter ]
```

如果开启了调试模式（可以通过命令行选项 `-O` 关闭），且表达式求值为假，则将抛出一个 `AssertionError` 异常，并带有一个可选的参数。见下文 `try`。

## print

```
print [ expression1 , expression ] ...
```

写入标准输出，根据需要将每个表达式转换为字符串。在表达式之间会写入空格，除非表达式位于行开头。在表达式末尾会打印换行符，除非末尾有逗号。

`print` 是一个便利语句；相同的功能可以通过文件对象（如 `sys.stdout`）更直接地实现。

## exec

```
exec "arbitrary Python code in a string"
```

解析并执行存储在字符串中的 Python 代码。这是一个非常强大的工具，但必须小心使用。除了字符串外，`exec` 还可以用于打开的文件对象和代码对象。`eval` 是 `exec` 的功能等价物。

# 复合语句

Python 的复合语句由子句组成；每个子句由一个头后跟一个语句块组成。通常，语句块由多个语句组成……（注：原文此处存在大量重复文本，译文已按要求处理）

# 第 15 章

```
try...finally:
  try:
    finally:
```

`try` 的第二种形式创建一个清理处理程序，用于执行如关闭文件等关键操作。如果在 `try` 块中发生异常，将首先执行 `finally` 块，然后重新抛出异常，以便让任何周围的异常处理器捕获。

如果 `try...finally` 形式位于循环内部，`try` 块中的 `break` 将在退出时执行 `finally` 块，就像在函数或方法内部执行 `return` 一样。

两种 `try` 形式不能混合使用，但可以相互嵌套。

# 函数

函数定义是一个复合语句，它创建一个用户定义的函数对象，并将其绑定到当前本地命名空间中的函数名上（说起来时间过得真快！）：

```
def function_name( parameter_list ):
  suite
```

如果函数要接受参数，则需要提供参数列表。参数列表定义了绑定到函数调用时传入对象的本地名称。Python 参数是通过赋值传递传递的，因此只有可变参数（列表和字典）可以被函数修改，并且这些修改在函数外可见，前提是它们是在原地被修改的。

简单参数的形式为 `name`。在简单的函数调用中，参数是根据位置进行匹配的。然而，如果函数调用包含了关键字，参数的顺序可能会发生变化。以下函数调用是等价：

```python
>>> fi(a, b):
    print a, b
>>> fi(1,2) # 位置参数
1 2
>>> fi(b=1,a=2) # 关键字参数
2 1
```

默认参数的形式为 `name=default`。如果从函数调用中省略了相应的参数，则将使用默认值：

```python
>>> pet("Eric", kind="fish")
    return "%s the %s %(kind)s" % locals()
```

```python
>>> pet("Spot", "cat")
    "Spot the cat"
>>> pet("Spot") # kind 被省略，因为 name 是第一个
    "Spot the fish"
>>> pet("Eric") # name 和 kind 都省略了
    "Eric the fish"
>>> pet("Eric", kind="half a bee") # name 被省略（使用关键字）
    "Eric the half bee"
```

536

# Python

此示例说明了 `return` 语句的使用，它允许函数产生一个值。它还展示了字符串 `%` 运算符的另一个用途：变量替换。`locals` 返回包含所有本地变量的字典（`((name:value))`）。`vars` 和 `globals` 也可以用于各种效果。

`*name` 参数的形式为多余的位置参数定义一个名称。如果存在任何多余的位置参数，它们将变成一个绑定到 `name` 的元组：

```python
>>> def f2(t*):
    print t
>>> f2(1, 'two', ['III'])
(1, 'two', ['III'])
```

`**name` 参数的形式为多余的关键字参数定义一个名称。任何多余参数将被转换为绑定到 `name` 的字典：

```python
>>> def f3(**d):
    print d
>>> f3(bird="swallow", kind="African", cargo="coconut")
{'kind': 'African', 'bird': 'swallow', 'cargo': 'coconut'}
```

不同类型的参数可以在函数定义中一起使用，其中默认参数必须位于所有简单参数之后，任何多余的位置参数 (`*name`) 必须在其之后，而任何多余的关键字参数 (`**name`) 必须最后。

函数定义（以 `def` 开头的复合语句头部）在加载时执行，但函数体在函数被调用之前不会执行。这对于默认值有重要影响：

```python
>>> def alist(mylistist={}): # 默认值：一个空列表
    return mylist
>>> a = alist()
>>> b = alist()
>>> a.append("item")
['item']
```

上述示例中的默认值（空列表）在函数定义执行时求值一次。当 `a` 和 `b` 被赋值为该列表时，它们都绑定到同一个空列表对象。这是 Python 程序中常见的 Bug 来源。

```python
>>> def alist(mylist=None):
    if mylist is None: mylist = []
    return mylist
>>> a = alist()
>>> b = alist()
>>> a.append("item")
['item']
```

537

# 内置函数

Python 定义了许多内置函数。这里是一些我们尚未见过的函数：

```python
chr(65) # 返回包含 ASCII 字符 ord('A') 的字符串
ord('A') # 返回 'A' 的 ASCII 值
cmp(1,2) # 比较：返回 -1（小于），0（相等），1（大于）
coerce(1.0, 2.0) # 将两个参数都转换为公共数值类型
eval('*2 * 3') # 将参数作为 Python 代码求值
hex(31) # 十六进制（基 16）字符串
oct(63) # 八进制（基 8）字符串
a=0
id(a) # 唯一对象 ID（实现为对象地址）
nudge=raw_input("nudge, nudge: ") # 提示从标准输入读取输入
nudge: Say no more! Say no more!
```
