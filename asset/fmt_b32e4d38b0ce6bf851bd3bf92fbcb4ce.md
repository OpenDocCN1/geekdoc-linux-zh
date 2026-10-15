
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

如你所见，`print`命令的作用类似于 UNIX 的`echo`语句。双引号有助于防止字符串被解释，并应在所有`print`语句中使用。单引号也可以包含字符串，但不要使用单反引号。默认情况下，`print`语句将输出发送到标准输出（通常是屏幕）。

你可以将命令行解释器当作计算器。如果你使用变量，它们会自动设置为正确的类型并可以在程序稍后使用。要从 Python 生成输出，不要使用赋值运算符：

```
>>> a = 2
>>> b = 5
>>> a * b
10
>>> bigvar = 37465
>>> smallvar = a / 2
>>> bigvar / smallvar
37465
>>>
```

# Python 编程

## 第 34 章

是动态创建。这消除了在模块顶部进行声明和类型语句的需要，使得 Python 成为快速编程的理想语言。它也让 Python 程序变得更短且更容易读。Python 优秀的对象实现使其成为大型软件开发的理想选择者。

Python 程序的第一行通常如下：

```python
#!usr/bin/python
```

这告诉 shell 使用 python 可执行文件来运行脚本。完整路径在你的系统上可能不同，取决于你安装 Python 文件的位置。此行之后可以跟随任意数量有效的 Python 命令。Python 会忽略空白，因此你可以使用空行来分隔程序的部分，使代码更具可读性。

Python 注释以井号（`#`）开头。你可以在代码中嵌入任意数量的注释，因为解释器忽略任何以井号开头的行。注释也可以放在行的任何位置，注释符号之后的所有内容都会被 Python 忽略：

```python
Var1 = 6 # sets Var1
```

在大多数程序的顶部，你可能会看到`import`语句。`import`语句用于读取另一个模块（类似于 C 语言中的`include`）。Python 代码中最常用的模块称为`sys`，它包含一组系统级组件。如果你在代码中没有使用这些组件中的任何，就不需要在程序顶部包含以下`import`语句，但它不会产生任何影响：

```python
import sys
```

## 命令行参数与环境变量

在 Python 中通过`sys`模块的`argv`列表访问命令行参数。参数的数量（包括程序名在内，类比 C 或 C++ 中的`argc`）可以通过`len(sys.argv)`获取。`sys.argv[0]`是程序名，而`sys.argv[1]`到`sys.argv[len(sys.argv)-1]`是其余参数。为了更深入地了解该主题，将以下代码保存为`test.py`：

```python
#!usr/bin/python
import sys
print("Args are:", sys.argv)
print("Counting program name,"
print("number of args is", len(sys.argv))
print("Program name is,", sys.argv[0])
print("Final arg is,", sys.argv[len(sys.argv)-1])
```

![](img/fbfff30e42d507bc7531108a281d6cf4_1072_0.png)

在命令行中使用以下命令运行它（在执行`chmod a+x test.py`之后）：

`$ ./test.py one two three`

输出如下：

- Args are: ['./test.py', 'one', 'two', 'three']
- Counting program name, number of args is 4
- Program name is ./test.py
- Final arg is three

在 Python 中通过`os`模块的环境字典访问环境变量。由于它是一个字典，使用`os.environ[VARNAME]`语法进行查询，环境变量名需要加引号。如果`VARNAME`不在环境中，该语法会抛出`KeyError`。不幸的是，未处理的`KeyError`会粗劣地终止程序。为了防止这种情况，使用了`try.except.else`语法来处理任何`KeyError`异常。注意以下代码：

```python
#!/usr/bin/python
import os
def getenv(s):
    try:
        x = os.environ[s]
    except KeyError:
        print("No such environment var:", s)
    else:
        print("Env var", s, "has value:", x)
printenv("SHELL")
printenv("OSTYPE")
printenv("JUNK")
```

> 注意：此代码必须按照所示缩进。Python 根据语句的缩进（执行脚本时）或空行（交互式运行时）来决定要执行的代码块的开始和结束位置。`def:`、`try:`、`except:`和`else:`语句各有一个从属代码块。

在你的系统上尝试这段代码。你几乎拥有`SHELL`和`OSTYPE`环境变量，而你可能没有`JUNK`。基于这些假设，你可以预期如下输出：

Env var SHELL has value: /bin/bash
var OSTYPE has value: Linux
No such environment var: JUNK

可以通过标准的字典操作在`os.environ`中添加、更改和删除环境变量：

```python
os.environ["JUNK"] = "added"
printenv("JUNK")
os.environ["JUNK"] = "changed"
printenv("JUNK")
del os.environ["JUNK"]
printenv("JUNK")
```

前面的代码添加了环境变量`JUNK`，更改了它的值并删除了它，调用了之前定义的`printenv()`函数。输出是可预测的：

```text
Env var JUNK has value: added
Env var JUNK has value: changed
No such environment var: JUNK
```

这是非常有用的，因为任何此类环境变量对于通过`os.system()`、`os.popen()`、`os.fork()`和`os.execv()`启动的子进程都是可见的。

## 控制语句

许多编程语言一样，Python 拥有常见的控制语句。最常用的语句是`if`条件判断以及`for`循环和`while`循环。如果你以前编写过其他语言，或者熟悉 shell 脚本，你会发现这些语句并没有什么新意。如果你是编程新手：

### if 语句

`if`语句使用冒号，后跟一个缩进的代码块。`else`是可选的。如下：

```python
if condition:
    statements
else:
    statements
```

### elif 语句

`elif`语句允许多次测试，如下：

```python
if condition:
    statements
elif condition:
    statements
else:
    statements
```

`elif`语句也使用冒号，后跟一个缩进的代码块。`elif`语句是`if-elif-else`序列的一部分：

```python
if condition1:
    statements
elif condition2:
    statements
elif condition3:
    statements
else:
    statements
```
