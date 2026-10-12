

for x in range(len(grid)):
    for y in range(len(grid[x])):
        for z in range(len(grid[x][y])):
            if grid[x][y][z] == target:
                raise FoundException
    except FoundException:
        print "Found at (%d, %d, %d)" % (x, y, z)
    else:
        print "Not found"

这个版本只有 11 行代码。如果找到目标，我们就抛出异常并处理该情况。如果没有抛出异常，则执行 try 块中的 else 语句块。

在某些情况下，我们希望无论发生什么，某些清理代码都会被调用。例如，即使我们的代码存在 bug，我们也希望确保关闭文件或网络/数据库连接。这通过使用 try ... finally 块来实现，如下例所示：

filehandle = open(filename)
try:
    for line in filehandle:
        process(line)
finally:
    filehandle.close()

在这里，我们使用给定的文件名打开一个文件并获得一个文件句柄。然后，我们在 for 循环的上下文中遍历该文件句柄——它是一个生成器，每次返回一行。如果发生任何异常，解释器会查找作用域范围内最近的 except 或 finally。在这种情况下，它没有找到 except，但找到了 finally，因此解释器将控制权切换到 finally 语句块并执行它。如果没有发生异常，finally 块将在 try 语句块执行完毕后执行。因此，无论如何，文件都会被关闭。

Python 2.5 之前的版本不支持 try ... except ... finally 块。因此，如果我们既需要 except 又需要 finally，必须使用两个块：一个 try ... except 和一个 try ... finally，其中一个嵌套在另一个内部。例如，在 2.4 及更早版本的 Python 中，打开和处理文件的最稳健方法如下所示：

fh = None
try:
    try:
        fh = open(fname)
        process(fh)
    except IOError, e:
        print "I/O error: %s" % e
finally:
    if fh:
        fh.close()

## 异常处理

这段代码使用了一些我们已经讨论过的内容，但为了确保我们牢固掌握异常处理，我们将详细研究这段代码。

如果文件一开始就无法打开，except 块会被执行，随后 finally 块也会被执行——由于文件未能打开，文件句柄仍为 None，所以 finally 块实际上什么也不会做。另一方面，如果文件成功打开并开始处理，可能会发生 I/O 错误。如果这种情况发生，except 块会被执行，然后控制权会再次传递到 finally 块，文件将被关闭。

如果发生的异常不是 IOError 或 IOError 的子类，例如，在我们的 process() 函数中发生了 ValueError——解释器会认为 except 块不适用，并查找最近的、适用的外部异常处理程序。在查找过程中，解释器首先会遇到 finally 块并执行它，之后（即在关闭文件后），它将继续查找适用的异常处理程序。

如果文件成功打开且处理过程中没有抛出任何异常，except 块将被跳过，但由于无论发生什么情况 finally 块都会被执行，因此 finally 块仍然会执行。所以，在所有情况下，除非解释器被用户终止（或在极少数情况下崩溃），只要文件被打开，它最终都会被关闭。

在 Python 2.5 及更高版本中，我们可以使用一种更简单的方法，它具有相同的语义，因为我们可以使用 try ... except ... finally 块：

fh = None
try:
    fh = open(fname)
    process(fh)
except IOError, e:
    print "I/O error: %s" % e
finally:
    if fh:
        fh.close()

使用这种语法，仍然可以拥有用于“未发生异常”情况的 else 块；它位于最后一个 except 块之后，且唯一的 finally 块之前。我们将在第 6 章“文件”的上下文中重新探讨这个主题。

无论使用哪个版本的 Python，finally 块始终只执行一次，无论是否发生异常，要么在 try 语句块结束时，要么在发生将控制流转移到 try 块外部的异常时。

Python 2.6（以及使用 from __future__ import with 语句的 Python 2.5）提供了另一种完全不同的方法：“上下文管理器”。对于文件处理，我们更倾向于使用 try ... finally 方法，但在其他情况下，我们更偏好上下文管理器。例如，我们将在第 19 章中展示如何使用上下文管理器来锁定和解锁线程使用的读写锁。

## 总结

在本章中，我们学习了如何使用 if 进行分支，以及如何通过带有 elif 的 if（可选地配合 else）创建多路分支。我们还学习了如何使用 while 和 for 进行循环，以及如何使用 range() 生成整数列表。我们学习了提供字典的键、值和键值对（items）的字典方法，并简要了解了排序。我们还初步了解如何使用 Python 的列表推导式和生成器。

我们学习了如何使用 def（以及 lambda）创建函数。我们使用了位置参数和关键字参数，并开发了两个有用的函数 frange() 和 simplify()。我们看到了 Python 如何在读取 .py 文件时动态创建函数，以及我们如何利用这种动态性，在较旧的 Python 版本中提供与较新版本中可用的相似功能。我们还看到了如何使用部分函数应用创建包装函数，将函数与其参数封装在一起（闭包）。

我们还学习了如何抛出异常，如何创建自定义异常，以及如何处理异常。我们看到了如何使用 finally 保证清理工作，并讨论了 Python 提供的某些更复杂的异常处理可能性。我们还看到，当我们有多个异常可能发生的语句块时，异常处理可以产生更简洁的代码，以及如何使用异常处理来干净地退出一组深层嵌套的循环。

创建自定义异常引导我们走向创建简单的类；这些类没有属性（没有成员数据）也没有方法。在下一章中，我们将更正式地研究类，学习如何创建类以及实例化具有任意属性和方法的对象。

## 练习

在第 1 章中，练习短到可以直接输入到 IDLE 中。从现在开始，我们建议您将解决方案输入到具有 .py 扩展名的文件中，并在末尾添加一些测试调用。例如，您可能编写一个具有以下结构的文件：

#!/usr/bin/env python
def mysolution(arg0, arg1):
    pass    # 所需的任何代码

mysolution(1, 2)       # 使用一组参数调用
mysolution("a", "b")  # 使用另一组参数调用
# 额外的调用以确保所有边界情况都经过测试

如果您使用的是 Windows，请确保在控制台窗口中运行测试程序；同样，Mac OS X 用户应使用终端。您可能还需要包含 print 语句，以便可以看到结果。（涉及 GUI 应用程序的练习从第二部分开始。）

如果您查看本书的源代码，包括本章的 answers.py 文件，您会发现代码通常包含很长的文档字符串（docstrings），在许多情况下，它们占用的行数比代码本身还多。这是因为文档字符串通常包含用法示例，这些示例同时充当单元测试，正如我们将在第 3 章“使用 doctest 模块”小节中看到的那样。

- 编写一个函数，签名为：

  ```python
  valid(text, chars="ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")
  ```

  该函数应返回一个（可能为空的）字符串，它是 text 的副本，仅包含 chars 中的字符。例如：

  ```python
  valid("Barking!")                                     # 返回 "B"
  valid("KL754", "0123456789")                          # 返回 "754"
  valid("BEAN", "abcdefghijklmnopqrstuvwxyz")          # 返回 ""
  ```

  使用 for 循环和 if 语句，不计文档字符串（也应该编写文档字符串），可以用半打（6行）代码实现。

- 编写一个函数，签名为：

  ```python
  charcount(text)
  ```

  这应该返回一个具有 28 个键的字典，包括 "a"、"b"、...、"z"，加上 "whitespace" 和 "others"。对于 text 中的每个小写字符，如果该字符是字母，则增加对应键的值；如果该字符是空白字符，则增加 "whitespace" 键的值；否则，增加 "others" 键的值。例如，调用：

  ```python
  stats = charcount("Exceedingly Edible")
  ```

  将意味着 stats 是一个包含以下内容的字典：

  ```python
  {'whitespace': 1, 'others': 0, 'a': 0, 'c': 1, 'b': 1, 'e': 5,
   'd': 2, 'g': 1, 'f': 0, 'i': 2, 'h': 0, 'k': 0, 'j': 0, 'm': 0,
   'l': 2, 'o': 0, 'n': 1, 'q': 0, 'p': 0, 's': 0, 'r': 0, 'u': 0,
   't': 0, 'w': 0, 'v': 0, 'y': 1, 'x': 1, 'z': 0}
  ```

  使用字典和 for 循环，可以用略多于一打（12行）的代码实现。

- 创建一个函数，签名为：

  ```python
  integer(number)
  ```

  number 参数是一个数字或一个可以转换为数字的字符串。该函数应将数字返回为 int 类型，如果传入的数字是浮点数，则对其进行舍入。如果转换失败，捕获 ValueError 异常，并返回 0。确保它对字符串和字面数字（如 4.5, 32, "23" 和 "-15.1"）都有效，并且正确
