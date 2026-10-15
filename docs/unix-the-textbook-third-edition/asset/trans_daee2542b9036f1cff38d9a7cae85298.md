

## 16.4.1 另一种编写 Shell 脚本文件的方式

如果你尚未阅读并完成第 12 章至第 15 章中的示例和练习，你应该阅读并完成它们，以便回顾并更好地掌握在 UNIX 环境中进行基础和高级 shell 脚本编程的感觉。在本节中，我们不回顾 shell 脚本的基础知识，而是提供方法和实用示例，包括重写第 12 章至第 15 章中的部分 shell 脚本，说明如何使用 Python 语言的语法和结构实现 UNIX shell 脚本所能完成的功能。使用 Python 的优势在于它是一种更健壮、可扩展的语言，拥有比任何 UNIX 脚本语言都多得多的特性和功能。

### 16.4.1.1 重写 Bourne 和 tcsh 脚本

我们从一个简单的 Bourne shell 脚本重写为 Python 的示例开始。首先给出用于打印某个目录路径是否存在于我们文件系统中的 Bourne shell 脚本，然后在示例 16.22b 中展示其 Python 等价版本。你应该输入并运行这两个代码示例，并注意你在系统上的输出：

# 示例 16.22b

```
#!/bin/sh
if [ -d "/usr/bin" ] ; then
    echo "/usr/bin is a directory"
else
    echo "/usr/bin is not a directory"
fi
```

```
#!/usr/local/bin/python
import os
if os.path.isdir("/usr/bin"):
    print "/usr/bin is a directory"
else:
    print "/usr/bin is not a directory"
```

对于 Bourne shell 脚本的 Python 版本，我们可以使用方式 2（脚本模式）运行脚本文件。关于 Python 代码需要注意的重要事项是

- 1. 在脚本文件顶部导入了一个名为 os 的标准库模块。
- 2. os.path 是一个嵌套模块，除了 os 标准库模块中的工具外，还提供了目录和路径名工具。

# 练习 16.12

- 1. 给出你在 UNIX shell 命令行上运行示例 16.22b 中所示的 Bourne shell 脚本时使用的确切语法。

2. 参考在线文档，标准库中还有哪些其他 os 模块可以用来实现与示例 16.22b 中 Python 代码相同的功能？

3. 编辑示例 16.22b 的 Python 代码，将 /usr/bin 替换为 /usr/bin/yyy。做出此更改后运行它时，你会得到什么程序输出？

另一个从 Bourne shell 脚本转换为 Python 的简单示例如下。Bourne shell 脚本取自第 12 章。

# 示例 16.23

Bourne shell 代码

```
#!/bin/sh
echo "Enter input: \c"
read line
echo "You entered: $line"
echo "Enter another line: \c"
read word1 word2 word3
echo "The first word is: $word1:"
echo "The second word is: $word2:"
echo "The rest of the line is: $word3:"
exit 0
```

Python 代码

```
#!/usr/local/bin/python
import sys
s = raw_input("Enter input:")
print "You entered:", s
r = raw_input("Enter another line:")
words = r.split(' ')
print "The first word is:", words[0]
print "The second word is:", words[1]
rest = (' '.join(words[2:]))
print "The rest of the line is:", rest
sys.exit() #normal exit status
```

请注意示例 16.23 中使用的 Python 字符串方法和切片。

# 练习 16.13

- 1. 给出示例 16.23 中使用的两个列表索引或切片示例。

- 2. 给出示例 16.23 中的两个字符串方法示例。

下面是另一个将 Bourne shell 脚本转换为 Python 的示例。Bourne shell 脚本 cmdargs_demo 取自第 12.4 节。

# 示例 16.24

```sh
#!/bin/sh
echo "The command name is $0."
echo "The number of command line arguments passed as parameters is: $#."
echo "The value of the command line arguments are: $1 $2 $3 $4"
echo "$5 $6 $7 $8 $9."
echo "Another way to display values of all the arguments: $@."
echo "Yet another way is: $*."
exit 0
```

```python
#!/usr/local/bin/python
import sys
x = (sys.argv)
print "The command name is ", sys.argv[0]
print "The number of command line arguments passed as parameters is: ", len(sys.argv)
print "The value of the command line arguments are: ", x[1:]
print "Another way to display values of all the arguments: ", sys.argv[1:]
print "Yet another way is: ", sys.argv[slice(1,9)]
sys.exit()
```

与 Bourne shell 在语法和结构上类似，C shell 具有功能能力，可以通过 Python 轻松实现。以下是脚本文件 if_demo1 的示例，取自第 14.6.1 节，其语法结构和程序功能已转换为 Python 脚本文件，你应该以方式 2（脚本模式）运行它。请注意，在我们的 Python 转换中，我们还有条件地检查是否将隐藏文件或点（.）文件作为参数输入：

# 示例 16.25

```sh
#!/bin/csh
if ( $#argv == 0 ) || ( $#argv > 1 ) then
echo "Usage: $0 ordinary_file"
exit 1
endif
if ( -f $argv[1] ) then
set filename = $argv[1]
set fileinfo = 'ls -l1 $filename'
set inode = ${filename[1]}
```
