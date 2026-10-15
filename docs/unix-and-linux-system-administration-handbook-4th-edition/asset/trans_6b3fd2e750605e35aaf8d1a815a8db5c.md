

Python 字典与 Perl 哈希相同；也就是说，它是一个键/值对的列表。字典字面量用花括号括起来，每个键/值对用冒号分隔：

```
#!/usr/bin/python
ordinal = { 1 : 'first', 2 : 'second', 3 : 'third' }
print "The ordinal array contains", ordinal
print "The ordinal of 1 is", ordinal[1]
```

在使用时，Python 字典与数组非常相似，只是下标（键）可以是整数以外的对象。

```
$ python dictionary
The ordinal array contains {1: 'first', 2: 'second', 3: 'third'}
The ordinal of 1 is first
```

Python 将打开的文件处理为具有关联方法的对象。忠实于其名称，readline 方法读取单行，因此下面的示例从 /etc/passwd 文件中读取并打印两行。

```
#!/usr/bin/python
f = open('/etc/passwd', 'r')
print f.readline(),
print f.readline(),
f.close()
```

```
$ python fileio
atx:25:25:Batch jobs daemon:/var/spool/atjobs:/bin/true
bin:x:1:1:bin:/bin:/bin/true
```

print 语句中的尾随逗号用于抑制换行，因为每行在从原始文件读取时已包含换行符。

## 输入验证示例

下面的脚本是迄今为止我们熟悉的输入验证器的 Python 版本。它演示了子程序和命令行参数的使用以及一些其他的 Python 特性。

```
#!/usr/bin/python
import sys
import os
def show_usage(message, code = 1):
    print message
    print "%s: source_dir dest_dir" % sys.argv[0]
    sys.exit(code)
```

```
if len(sys.argv) != 3:
    show_usage("2 arguments required; you supplied %d" % (len(sys.argv) - 1))
elif not os.path.isdir(sys.argv[1]):
    show_usage("invalid source directory")
elif not os.path.isdir(sys.argv[2]):
    show_usage("invalid destination directory")

source, dest = sys.argv[1:3]

print "Source Directory is", source
print "Destination Directory is", dest
```

除了导入 sys 模块，我们还导入了 os 模块以获得对 os.path.isdir 例程的访问权限。请注意，import 并不会缩短你对模块定义的符号的访问；你必须使用以模块名称开头的完全限定名称。

show_usage 例程的定义为退出代码提供了一个默认值，以防调用者未明确指定此参数。由于所有数据类型都是对象，函数参数按引用传递。

sys.argv 数组在第 0 个位置包含脚本名称，因此其长度比实际提供的命令行参数数量多 1。形式 sys.argv[1:3] 是一个数组切片。有趣的是，切片不包括指定范围的远端元素，因此此切片仅包括 sys.argv[1] 和 sys.argv[2]。你也可以简单地说 sys.argv[1:] 以包含第二个及后续的参数。

与 bash 和 Perl 一样，Python 也有专用的 "else if" 条件；关键字是 elif。没有显式的 case 或 switch 语句。

source 和 dest 变量的并行赋值与 Perl 版本有点不同，因为变量本身不在列表中。Python 允许以任一形式进行并行赋值。

Python 对数值和字符串值使用相同的比较运算符。"不相等" 比较运算符是 !=，但没有一元 ! 运算符；对此使用 not。布尔运算符 and 和 or 也都是拼写出来的。

## 循环

下面的片段使用 for...in 构造遍历 1 到 10 的范围。

```
for counter in range(1, 10):
    print counter,
```

与前一个示例中的数组切片一样，范围的右端点实际上不包含在内。输出仅包括 1 到 9 的数字：

```
1 2 3 4 5 6 7 8 9
```

这是 Python 的唯一一种 for 循环类型，但它功能强大。Python 的 for 有几个区别于其他语言中 for 的特性：

- 数值范围没有什么特别之处。任何对象都可以支持 Python 的迭代模型，并且大多数常见对象都支持。你可以遍历字符串（按字符）、列表、文件（按字符、行或块）、数组切片等。
- 迭代器可以产生多个值，并且你可以有多个循环变量。每次迭代顶部的赋值就像 Python 的常规多重赋值一样工作。
- for 和 while 循环都可以在末尾有 else 子句。else 子句仅在循环正常终止时执行，而不是通过 break 语句退出。这一特性最初可能看起来违反直觉，但它能非常优雅地处理某些用例。

下面的示例脚本在命令行接受一个正则表达式，并将其与白雪公主的七个小矮人及其小矮人服装的颜色列表进行匹配。第一个匹配项会被打印出来，其中与正则表达式匹配的部分用下划线包围。

```
#!/usr/bin/python
import sys
import re

suits = { 'Bashful':'red', 'Sneezy':'green', 'Doc':'blue', 'Dopey':'orange',
          'Grumpy':'yellow', 'Happy':'taupe', 'Sleepy':'puce' }
pattern = re.compile('%s' % sys.argv[1])
for dwarf, color in suits.items():
    if pattern.search(dwarf) or pattern.search(color):
        print "%s's dwarf suit is %s." % \
              (pattern.sub(r"_\1_", dwarf), pattern.sub(r"_\1_", color))
        break
else:
    print "No dwarves or dwarf suits matched the pattern."
```

以下是一些示例输出：

```
$ python dwarfsarch '[aeiou](2)'
Sn_ee_zy's dwarf suit is gr_ee_n.

$ python dwarfsarch go
No dwarves or dwarf suits matched the pattern.
```

对 suits 的赋值演示了 Python 编码字面量字典的语法。suits.items() 方法是键/值对的迭代器——请注意，我们在每次迭代中同时提取一个小矮人和一件服装颜色。如果你只想遍历键，可以简单地说 for dwarf in suits。
