
| 函数 | 描述 |
| :--- | :--- |
| stdin, stdout, stderr | 这些对象指向解释器当前的标准输入、输出和错误流。它们是文件对象，可以将其设置为新值以影响解释器的默认行为。 |
| `__stdin__`, `__stdout__`, `__stderr__` | 这些文件对象是在解释器加载时初始化的默认标准输入、输出和错误流。使用这些对象可以在操作完 `sys.stdin`、`sys.stdout` 和 `sys.stderr` 对象后，将解释器恢复为正常操作状态。 |

# types 模块

types 模块包含不同对象类型的名称，可用于比较：

```python
from types import *
if type(myintobj) is IntType:
    mystring = "myintobj is now a string"
```

建议直接通过 `from types import *` 命令将此模块导入到全局命名空间中，这样既方便又推荐。

| 名称 | 描述 | 示例 |
| :--- | :--- | :--- |
| NoneType | 特殊值 None | None |
| IntType | 整数类型 | 23 |
| LongType | 长整数类型 | `40000000L` |
| FloatType | 浮点数类型 | 3.25 |
| ComplexType | 复数类型 | `3 + 4j` |
| StringType | 字符串类型 | "Hello" |
| TupleType | 元组类型 | `(1, 2, (3, 4))` |
| ListType | 列表类型 | `[1, 2, "fred", "*"]` |
| DictType | 字典类型 | `{'a': 12, 'b': 6}` |
| FunctionType | 函数类型 | `sys.exit` |
| FileType | 文件类型 | `open("foo.txt", "r")` |

# string 模块

`string` 模块包含有用的字符串常量以及强大的字符串操作函数。你很可能会大量使用此模块，因此提供了对象和函数的重要（但不全面）总结。

| 对象/函数 | 描述 |
| :--- | :--- |
| `digits` | 字符串 `"0123456789"` |
| `hexdigits` | 字符串 `"0123456789abcdefABCDEF"` |
| `lowercase` | 包含所有小写字母的字符串 |
| `uppercase` | 包含所有大写字母的字符串 |
| `letters` | 包含所有字母的字符串 |
| `whitespace` | 包含被视为空白的字符的字符串，例如空格、制表符和换行符 |
| `atof(string)` | 将字符串转换为浮点数 |
| `atoi(string[,base])` | 将字符串转换为整数，可选基数 |
| `atol(string[,base])` | 将字符串转换为长整数，可选基数 |
| `capitalize(word)` | 将字符串的首字符大写 |
| `capwords(string)` | 将所有单词首字母大写，将单词之间的空白替换为单个空格，并去除首尾空白 |
| `expandtabs(str[,tabsize])` | 将制表符转换为空格，默认 tabsize 为 8 |
| `find(str,substring)` | 返回完整子串 substring 首次出现的索引，若未找到则返回 -1 |
| `rfind(str,substring)` | 返回完整子串 substring 最后一次出现的索引，若未找到则返回 -1 |
| `count(str,substring)` | 返回完整子串 substring 非重叠出现的次数 |
| `split(str[,separator])` | 将字符串分割为单词，返回列表；可选分隔符默认为任意空白 |
| `join(mylist[,separator])` | 连接单词列表或元组，使用 separator 分隔每个单词，默认为 `""` |
| `lstrip(str)` | 去除首部空白 |
| `rstrip(str)` | 去除尾部空白 |
| `strip(str)` | 去除首部和尾部空白 |
| `ljust(str,mywidth)` | 返回左对齐在指定宽度字符串中的 str |
| `rjust(str,mywidth)` | 返回右对齐在指定宽度字符串中的 str |
| `center(str, mywidth)` | 返回在指定宽度字符串中居中的 `str`。 |
| `replace(str, old, new)` | 在 `str` 中用 `new` 替换所有 `old` 的出现。 |

# math 模块

**math** 模块提供访问标准数学函数的功能。所有函数都接受数值参数并返回浮点值。以下是一个摘要。

| 对象/函数 | 描述 |
| :--- | :--- |
| `pi` | 3.14159... |
| `e` | 2.71828... |
| `acos(x)` | 反余弦 |
| `asin(x)` | 反正弦 |
| `atan(x)` | 反正切 |
| `atan2(y,x)` | 返回 `atan(y/x)`。 |
| `ceil(x)` | 返回 x 向上取整到下一个最大的整数。 |
| `cos(x)` | 余弦 |
| `exp(x)` | e**x |
| `fabs(x)` | 返回 x 的绝对值。 |
| `floor(x)` | 返回 x 向下取整到下一个最小的整数。 |
| `fmod(x,y)` | x % y |
| `log(x)` | 自然对数 |
| `log10(x)` | 以 10 为底的对数 |
| `pow(x,y)` | x**y |
| `sin(x)` | 正弦 |
| `sqrt(x)` | 平方根 |
| `tan(x)` | 正切 |

> **注意**
> 
> **cmath** 模块提供几乎相同的函数，用于操作复数。

# time 模块

**time** 模块提供时间查询和打印函数，以及一个方便的 `sleep()` 函数。

| 函数 | 描述 |
| :--- | :--- |
| `sleep(x)` | 暂停程序 x 秒（可以是浮点数）。 |
| `time(x)` | 返回当前时间，表示为浮点数。此值可以作为以下三个函数的参数： |
| `ctime(x)` | 接受一个浮点值并打印当前的本地日期和时间。用法示例： |
| `gtime(x)` | 接受一个浮点值并返回表示当前 UTC 时间的元组，然后可以作为 `strftime()` 的第二个参数来定制日期和/或时间的输出。 |
| `localtime(x)` | 类似于 `gtime()`，但返回代表当前（本地）时区时间的元组。 |
| `strftime(format,x)` | 给定字符串 "format" 和来自 `gtime()` 或 `localtime()` 调用的元组，`strftime()` 将返回自定义格式的日期/时间字符串。在格式字符串中，以下特殊序列将被替换为对应的值： |

| 序列 | 值 |
| :--- | :--- |
| `%a` | 简短的星期名称 |
| `%A` | 完整的星期名称 |
| `%b` | 简短的月份名称 |
| `%B` | 完整的月份名称 |
| `%d` | 月份中的日期 |
| `%H` | 24 小时制的小时 |
| `%I` | 12 小时制的小时 |
| `%j` | 一年中的第几天 |
| `%m` | 月份，数字 |
| `%M` | 分钟 |
| `%p` | am 或 pm |
| `%S` | 秒 |
| `%y` | 年份的最后两位数字 |
| `%Y` | 完整年份 |
| `%z` | 时区 |
| `%%` | % |

```python
from time import *
print ctime(time())
```

# shutil 模块

shutil 模块包含一批高级文件操作命令，非常实用。以下是 shutil 中的一些有用命令：

| 命令 | 描述 |
| :------------------ | :--------------------------------------------------------------------------------- |
| `copyfile(source,dest)` | 将文件 *source* 复制到 *dest*，替换任何现有文件且不复制权限位 |
| `copymode(source,dest)` | 将文件权限位从 *source* 复制到 *dest*，但不复制所有者和组 |
| `copystat(source,dest)` | 复制文件权限位、*atime* 和 *mtime*，但不复制所有者和组 |
| `copy(source,dest)` | 复制文件，包括权限位 |
| `copy2(source,dest)` | 复制文件，包括权限位、*atime* 和 *mtime* |

# commands 模块

commands 模块允许你在 Python 程序内部执行任何可执行程序，并捕获程序的输出和/或退出代码。此模块对于偶尔访问 shell 命令很有用。请注意，如果你的整个 Python 程序由对此模块中函数的调用组成，那么标准的 bash shell 脚本将更好地满足你的需求！

| 命令 | 描述 |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `getstatusoutput(string)` | 在新 shell 中执行 *string* 中指定的命令，并返回一个包含两个项目的元组：退出状态（整数）和输出（字符串）。注意，程序输出包括标准输出 (stdout) 和标准错误 (stderr)。因此，你可能会得到包含在输出数据中的不需要的错误消息。 |
| `getstatus(string)` | 与 `getstatusoutput()` 非常相似，但仅返回命令的整数退出状态。当你只是想验证命令是否成功完成，而不关心程序的文本输出时，请使用此函数。注意，退出状态为零被视为正常，而任何大于或等于一的整数都被视为错误条件。 |

