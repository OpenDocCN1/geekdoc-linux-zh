
```
i = buffer.pop(0)
print "Data Consumed", i
condition.notify()
condition.release()
time.sleep(random.random())
Producer().start()
Consumer().start()            # Block 4.
```

上述示例的输出如下：

```
% python Example16_55.py
Data Produced 0
Data Consumed 0

Queue empty, Consumer waiting
Data Produced 1
Data added to queue, Consumer notified
Data Consumed 1
Queue empty, Consumer waiting
Data Produced 2
Data added to queue, Consumer notified
Data Consumed 2
Data Produced 3
Data Produced 4
Data Produced 5
Data Consumed 3
Data Produced 6
Data Consumed 4
Data Produced 7
Data Consumed 5
Data Produced 8
Data Produced 9
Data Consumed 6
Data Consumed 7
Data Consumed 8
Data Consumed 9
%
```

## 练习16.21（参见示例16.55）

简要说明变量MAX_NUM的用途。按照程序的结构方式，该变量必须取什么值才能成功部署（即防止缓冲区溢出）？

## 练习16.22

从运行该程序一次的输出可以看出，数据在缓冲区中的生产和消费是零星的。也就是说，有时数据被产生后立即被消费，有时数据被产生后不会立即被消费。此外，你会注意到，如果你多次运行该程序，每次运行可能会产生不同的生产和消费模式（图16.22）。为什么会这样？

![](img/02e070097d401d3bf7de4bf1c470b267_712_0.png)

### 图16.22 Python 2.7的包管理器显示。

## 总结

我们使用Python 2.7.x版本对Python编程语言进行了广泛介绍。我们结合三种主要的计算机编程范式，说明了其所有编程能力和语法结构。我们展示了在PC-BSD和Solaris这两个基础系统上全新安装2.7.x或3.x版本，或升级这两个版本的详细步骤。我们展示了Python的所有基本语法，包括数字和表达式、变量、语句、从用户获取输入、函数、Python中的OOP、模块、保存和执行Python脚本、字符串和序列操作，以及错误处理。我们还提供了一些实际示例，例如编写shell脚本文件的另一种方式、重写Bash和tcsh脚本、基本用户文件维护、备份文件、使用rsync进行远程复制，以及使用Tkinter进行图形编程。

## 表16.6 Python语法和命令总结

### Python Shell中的交互式帮助

| 命令 | 说明 |
|---|---|
| `help()` | 调用交互式帮助 |
| `help(m)` | 显示模块m的帮助 |
| `help(f)` | 显示函数f的帮助 |
| `dir(m)` | 显示模块m中的名称 |

### 模块导入

```
import module_name
from module_name import name, ...
from module_name import *
```

### 常见数据类型

| 类型 | 说明 | 字面量示例 |
|---|---|---|
| int | 32位整数 | 3, -4 |
| long | 大于32位的整数 | 101L |
| float | 浮点数 | 3.0, -6.55 |
| complex | 复数 | 1.2J |
| bool | 布尔值 | True, False |
| str | 字符序列 | 'Python' |
| tuple | 不可变序列 | (2, 4, 7) |
| list | 可变序列 | [2, x, 3.1] |
| dict | 映射 | { x:2, y:5 } |

### 常见语法结构

**赋值语句**

```
var = exp
```

**控制台输入/输出**

```
var = input( [ prompt ] )
var = raw_input( [ prompt ] )
print exp[,]
```

**选择**

```
if (boolean_exp):
    stmt ...
[elif (boolean_exp):
    stmt ...]
[else:
    stmt ...]
```

**重复**

```
while (boolean_exp):
    stmt ...
```

**迭代**

```
for var in iterable_object(sequence suite):
    stmt ...
```

**函数定义**

```
def function_name( parameters ):
    stmt ...
```

**函数调用**

```
function_name( arguments )
```

## 表16.6（续）Python语法和命令总结

**类定义**

```
class Class_name [ (super_class) ]:
    [ class_variables ]
    def method_name( self, parameters ):
        stmt ...
```

**对象实例化**

```
obj_ref = Class_name( arguments )
```

**方法调用**

```
obj_ref.method_name( arguments )
```

**异常处理**

```
try:
    stmt ...
except [exception_type] [, var]:
    stmt ...
```

### 常见内置函数

| 函数 | 返回值 |
|---|---|
| `abs(x)` | x的绝对值 |
| `dict()` | 空字典，例如：`d = dict()` |
| `float(x)` | 将整数或字符串x转换为浮点数 |
| `id(obj)` | obj的内存地址 |
| `int(x)` | 将浮点数或字符串x转换为整数 |
| `len(s)` | 序列s中的项目数 |
| `list()` | 空列表，例如：`m = list()` |
| `max(s)` | s中项目的最大值 |
| `min(s)` | s中项目的最小值 |
| `open(f)` | 打开文件名f进行输入 |
| `ord(c)` | c的ASCII码 |
| `pow(x,y)` | x的y次方 |
| `range(x)` | 一个包含x个整数的列表，从0到x-1 |
| `round(x,n)` | 浮点数x四舍五入到n位 |
| `str(obj)` | obj的字符串表示形式 |
| `sum(s)` | 数值序列s的和 |
| `tuple(items)` | 项目元组 |
| `type(obj)` | obj的数据类型 |

### 常见数学模块函数

| 函数 | 返回值（均为浮点数） |
|---|---|
| `ceil(x)` | 大于等于x的最小整数 |
| `cos(x)` | x弧度的余弦值 |
| `degrees(x)` | 将x弧度转换为角度 |
| `radians(x)` | 将x角度转换为弧度 |
| `exp(x)` | e的x次方 |
| `floor(x)` | 小于等于x的最大整数 |

