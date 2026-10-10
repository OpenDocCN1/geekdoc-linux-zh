
# os 模块函数

| 函数 | 摘要 |
| :--- | :--- |
| os.chmod("/myfile",mode) | 设置文件权限为 mode |
| os.chown("/myfile",uid,gid) | 设置文件所有权为 uid, gid |
| os.link("/mysrc","/mydest") | 从 dest->src 创建硬链接 |
| os.listdir("/mydir") | 返回目录列表（字面意思） |
| os.mkdir("/mydir",[mode]) | 创建目录，mode 默认为 777 |
| os.readlink("/mysymlink") | 返回 mysymlink 指向的路径 |
| os.unlink("/myf"),os.remove("/myf") | 删除（解除链接）文件的两种不同方式 |
| os.rename("mysrc","mydest") | 将 mysrc 重命名为 mydest |
| os.rmdir("mypath") | 删除目录 mypath |
| os.symlink("mysrc","mydest") | 从 dest->src 创建符号链接 |

# 异常

Python 具有强大的处理运行时错误（也称为异常）的能力。当程序执行过程中遇到某种非语法相关的错误时，就会引发异常。如果你的代码中没有异常处理功能，Python 通常会打印堆栈跟踪并中止执行。另一种引发异常的方法是使用内置的 raise 语句：

```
>>> raise IOError,"Wazzup?"
Traceback (innermost last):
  File "<stdin>", line 1, in ?
IOError: Wazzup?
```

# try...except

请注意，异常允许使用一个可选的第二个参数来描述该异常。为了处理由 Python 函数或你自己代码引发的异常，我们使用 try ...except 语句：

这个 try...except 语句尝试将字符串转换为浮点数。这种非法转换会引发 ValueError。屏幕上会打印“We couldn't do that!”，并且程序的执行将继续。如果引发了 IOError 或 NameError，屏幕上将会出现"Now look what you did!"：

```
try:
    a=float("23adfadfsf")
except ValueError:
    print "We couldn't do that!"
except (NameError, IOError):
    print "Now look what you did!"
```

以下代码片段在引发任何类型的异常时都会打印"Invalid integer :/"。否则，它会执行可选 else 子句后面的代码并正常执行：

```
try:
    a = atoi(raw_input(" > "))
except:
    print "Invalid integer :/"
else:
    print "Thanks for the int, baby!"
```

# 处理所有异常时要小心

对于未经训练的人来说，这段代码看起来可能完全合法，它尝试将用户输入转换为整数，并在出错时打印错误消息。不幸的是，这段代码根本无法工作，而且由于空的 except 子句，找出原因可能需要花费大量时间。空的 except 子句是完全合法的，但它们会处理所有可能引发的异常。虽然这看起来似乎是个好事情，但实际上并不是。在这个例子中，我们调用了不存在的函数。（Python 使用 int() 函数，并没有像 C 那样的 atoi() 函数。）如果你尝试运行这段代码，它甚至在你有机会输入数据之前就会打印"Invalid integer :/"！对未限定的 except 子句要小心——如果你不仔细，它们可能会给你带来麻烦！

# try...finally

Python 提供了另一种异常处理机制——try...finally 语句。只允许一个 finally 子句，这与允许任意数量 except 子句和一个可选 else 的 except 不同：

```
try:
    a = thingee
finally:
    print "Regardless of what happens, I must tell you: You're kewl!"
```

正如你可能从我们的例子中猜到的那样，finally 子句指定无论发生什么情况都会运行的代码，即使引发了异常也是如此。这允许你的程序在让解释器带着堆栈跟踪退出之前完成必要的任务。

# 大量的异常

下面是一个在 Python 中引发的异常表格。你可以使用这些名称提供更细粒度的异常处理控制。要查看它们是如何使用的，请回顾我们第一个 try...except 代码片段。

| 异常 | 发生时机 |
|---|---|
| EOFError | 当 raw_input() 返回 EOF 字符时 |
| FloatingPointError | 当任何浮点运算失败时 |
| IOError | 当 IO 相关操作失败时，例如权限错误、文件不存在或磁盘已满 |
| ImportError | 当 import 语句指定了一个不存在的模块时 |
| IndexError | 当在列表或元组中指定非法下标时 |
| KeyError | 当指定不存在的字典键时 |
| KeyboardInterrupt | 当用户按下 ^C 中断执行时 |
| NameError | 当在任何命名空间中找不到名称时 |
| ZeroDivisionError | 当除以零时 |

还有其他几种类型的异常。要了解它们是什么，启动 Python 交互模式并开始写一些坏代码吧！

# 现实世界：示例代码

我们花了很多时间使用 Python 解释器的交互模式，这是一个非常棒的学习工具。然而，当你需要使用 Python 编写脚本时，你几乎总是希望创建一个可以反复执行（而不需要你反复键入）的脚本。在这个例子中，我们将展示几个执行有用任务并将本章涵盖的各种概念结合在一起的 Python 脚本示例。

## 示例：图形化目录列表

一位经验丰富的 Linux 用户，如果熟悉 bash shell，可能会问：“如果我可以完成同样的事情，为什么要用 bash shell 脚本而不是 Python 来做这些操作呢？”这位用户确实提出了一个很好的观点。对于小到中等规模的文件导向任务，一个简单的 bash 脚本可能是你的最佳选择。但当你需要执行复杂的文件操作时，bash 无法匹敌 Python。有时候，你只需要 Python 列表的强大功能，而 bash 无法干净或有效地完成任务，如列表 34.4 所示。

![](img/df365d352a104b50fea29e59a052de4d_874_0.png)

![](img/df365d352a104b50fea29e59a052de4d_874_1.png)

## 列表 34.4：图形化目录列表

```python
#! /usr/bin/env python

import sys,string,os
from types import *

mydict={}

def dofile(myfile,mylist):
	global mydict
	if os.path.isdir(myfile):
		mylist.append([myfile])
		mylistdir=os.listdir(myfile)
		mydict[myfile]=(len(mylistdir),os.path.islink(myfile))
		if not mydict[myfile][1]:
			for x in mylistdir:
				dofile(myfile+'/'+x,mylist[-1])

def drawtree(mylist,depth):
	for x in mylist:
		if type(x)==StringType:
			if depth==1:
				myout=x
			else:
				myout=string.split(x,'/')[-1]
			if mydict[x][1]:
				myout=myout+' (symlink to '+os.readlink(x)+')'
			print string.rjust(mydict[x][0],7)
			print ('*'*((depth-1)*2))+myout
		else:
			drawtree(x,depth+1)

def dirtree(mypath):
	if not os.path.isdir(mypath):
		print 'Please specify a directory.'
		sys.exit(1)
	mydirs=[]
	dofile(mypath,mydirs)
	print '\nHIERARCHICAL DIRECTORY LIST OF',mypath
	print '\nNUMOBJ DIRNAME'
	drawtree(mydirs,0)

dirtree(sys.argv[1])
```

我们的脚本扫描特定目录，打印出该目录下目录的层次表示以及每个目录的对象计数；并注明所有符号链接。当处理的任务至少具有如此复杂性时，Python 很可能比简单的 bash shell 脚本是更好的选择，即使处理的是与文件相关的任务，这本来是 bash 的强项。当然，当涉及到创建网络守护进程或客户端或设计图形用户界面时，bash 毫无机会。Python 在通用性方面确实大放异彩。

# Python 强力工具：嵌入式 Python

我们的下一个示例将 Python 变成一种嵌入式语言。“嵌入式”指的是该语言存在于一种不是 Python 脚本的文件类型中，在本例中，是一个 HTML 文本文件。这意味着文本文件看起来像是 HTML 格式，除了那些标记为作为 Python 语句执行的特殊部分。这将允许我们将文本文件传递给我们的 pytext 嵌入式 Python 解释器（见列表 34.6），并让 Python 部分被执行，并将结果输出插入到我们原始文本的正确位置。列表 34.5 是一个简单的示例，说明了嵌入式 Python 语法将如何工作。假设我们有一个看起来像这样的文本文件：

## 列表 34.5：示例文本文件

```html
<HT>This is sample HTML code</HT>

<!--code

for x in range(0,10):
    print "This is Python!"

-->

<b>Here is some more HTML</b>
```

将此文件作为参数传递给我们的嵌入式 Python 解释器后，输出将如列表 34.6 所示。

## 列表 34.6：pytext 处理文本文件后的输出

```html
<HT>This is sample HTML code</HT>
This is Python!
This is Python!
This is Python!
This is Python!
This is Python!
This is Python!
This is Python!
This is Python!
This is Python!
<b>Here is some more HTML</b>
```

