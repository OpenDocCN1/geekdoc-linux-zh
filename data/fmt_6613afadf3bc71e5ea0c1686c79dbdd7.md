
# Python 编程基础

## 列表 17-1：你的 Python 程序

第一行简单地告诉系统你想使用 Python 解释器来运行此程序，而不是任何其他语言。第二行定义了一个变量名并为其分配了一个值（在这种情况下是 "OccupyTheWeb"）。你应该将此值改为你自己的名字。该变量的值是字符串字符数据格式，这意味着内容包含在引号中并被视为文本。你也可以将数字放在字符串中，它们会被视为文本，但你将无法在数值计算中使用它们。

第三行创建了一个 `print()` 语句，将 "Greetings to " 与 `name` 变量中的值拼接，随后是来自 "Hackers-Arise. The Best Place to Learn Hacking!" 的文本。`print()` 语句会将你传递给括号内的任何内容显示在你的屏幕上。

现在，在运行此脚本之前，你需要赋予自己执行权限。我们需要使用 `chmod` 命令来实现（更多关于 Linux 权限的信息，请参阅第 5 节）：

```bash
kali$ chmod 755 hackers-arise_greetings.py
```

就像你在第 8 节中处理批脚本一样，要执行脚本，要在脚本名称前加上点和正斜杠。出于安全考虑，你的当前目录不在 `PATH` 变量中，因此我们需要在脚本名称前加上 `./`，告诉系统在当前目录查找文件名并执行它。

要运行此脚本，输入以下内容：

```bash
kali@ ./hackers-arise_greetings.py
```

输出结果：
```text
Greetings to OccupyTheWeb from Hackers-Arise. The Best Place to Learn Hacking!
```

在 Python 中，每个变量都被视为一个类（class）。类是用于创建对象的某种模板。更多信息请参阅第 189 页的“面向对象编程 (OOP)”。在下面的脚本中，我尝试演示了几类变量。变量可以包含的不只是字符串。列表 17-2 显示了包含不同数据类型的变量。

```python
#!/usr/bin/python3

HackersAriseStringVariable = "Hackers-Arise Is the Best Place to Learn Hacking"
HackersAriseIntegerVariable = 12
HackersAriseFloatingPointVariable = 3.1415
HackersAriseList = [1, 2, 3, 4, 5]
HackersAriseDictionary = {'name': 'OccupyTheWeb', 'value': 27}

print(HackersAriseStringVariable)
print(HackersAriseIntegerVariable)
print(HackersAriseFloatingPointVariable)
```

列表 17-2：与变量的一系列数据结构。这创建了包含不同数据类型的五个变量：字符串（被视为文本）；整数（没有小数的数字类型，可用于数值运算）；浮点数（带小数的数字类型，也可用于数值运算）；列表（存储在一起的一系列值）；以及字典（无序的数据集，其中每个值都与一个键配对，意味着字典中的每个值都有一个唯一的标识键）。这在你想要通过键名引用或更改值时非常有用。例如，假设你有一个名为 `fruit_color` 的字典，配置如下：

```python
fruit_color = {'apple': 'red', 'grape': 'green', 'orange': 'orange'}
```

如果在脚本后期你想获取葡萄的 `fruit_color`，只需通过其键调用即可：

```python
print(fruit_color['grape'])
```

你也可以更改特定键的值；例如，在这里我们更改苹果的颜色：

```python
fruit_color['apple'] = 'green'
```

我们将在本章稍后更详细地讨论列表和字典。在任何编辑器中创建此脚本 `secondscript.py`，然后像这样赋予自己执行权限：

```bash
kali$ chmod 755 secondscript.py
```

当运行脚本时，它会打印字符串、整数和浮点数的值，如下：

```bash
kali@ ./secondscript.py
Hackers-Arise Is the Best Place to Learn Hacking
12
3.1415
```

## 注释

与其他任何编程语言一样，Python 具有添加注释的能力。注释是代码的部分——单词、句子——用于解释代码的作用。虽然注释不是必须的，但非常有用。

Python 使用 `#` 符号表示单行注释的开始。如果你想写多行注释，可以使用三引号（`"""`）。在下面的脚本中，我为 `hackers-arise_greetings.py` 添加了简短的多行注释。

```python
#!/usr/bin/python3

"""
这是我带有注释的 Python 脚本。注释有助于我们和其他程序员。在这种情况下，这个简单的脚本为用户创建一个问候。
"""

name = "OccupyTheWeb"
print("Greetings to " + name + " from Hacker-Arise. The Best Place to Learn Hacking!")
```

当我们再次执行脚本时，与上次执行相比没有变化：

```bash
kali@ ./hackers-arise_greetings.py
Greetings to OccupyTheWeb from Hacker-Arise. The Best Place to Learn Hacking!
```

## 函数

函数是执行特定操作的代码段。例如你之前使用的 `print()` 语句，就是一个显示你传递给它的任何值的函数。Python 有许多我们可以立即导入并使用的内置函数。大多数函数在 Kali Linux 默认安装的 Python 中都是可用的，但更多函数可以从下载的库中获得。让我们看看你可以使用的数千函数中的几个：

- `exit()`：退出程序。
- `float()`：将参数作为浮点数返回。例如，`float(1)` 将返回 1.0。
- `help()`：对指定的对象显示帮助信息。
- `int()`：返回参数的整数部分（截断）。
- `len()`：返回列表或字典中元素的数量。
- `max()`：从参数（列表）中返回最大值。
- `open()`：按照参数指定的模式打开文件。
- `range()`：返回两个指定值之间的整数列表。
- `sorted()`：接受列表作为参数，并按顺序返回它。
- `type()`：返回参数的类型（例如 int, float, method, function）。

你可以创建自己的函数来执行自定义任务。由于语言中内置了许多函数，在费力构建之前，总是值得检查是否已经存在该函数。有许多方法可以进行这种检查。一种方法是查看位于 https://docs.python.org 的官方 Python 文档。选择你正在使用的版本，并选择“Library Reference”（库引用指南）。

## 列表

许多编程语言使用数组来存储多个独立的对象。数组是一个值列表，可以通过在列表中的位置引用特定值，从而以各种方式对这些值进行检索、替换或处理。需要注意的是，Python 与其他编程环境一样，索引从 0 开始计数，列表中的第一个元素索引为 0，第二个是索引 1，第三个是索引 2，以此类推。因此，如果我们想访问数组中的第三个值，可以通过 `array[2]` 实现。在 Python 中，数组的实现较少，但最常见的实现被称为 `list`（列表）。

### Python 中的列表是可迭代的

现在，假设我们需要显示列表 17-2 中 `HackersAriseList` 列表的第四个元素。我们可以通过调用列表名 `HackersAriseList` 并在其后的方括号中加上索引来访问并打印该元素。

为了测试这一点，请在你的 `secondscript.py` 底部添加以下行，以打印 `HackersAriseList` 中索引为 3 的元素：

```python
# --snip--
print(HackersAriseStringVariable)
print(HackersAriseIntegerVariable)
print(HackersAriseFloatingPointVariable)
print(HackersAriseList[3])
```

当我们再次运行此脚本时，可以看到新的 `print` 语句在其他输出旁边打印了 4：

```bash
kali> ./pythonscript.py
HackerArise Is the Best Place to Learn Hacking
12
3.1415
4
```

## 模块

模块仅仅是保存在单独文件中的代码段，这样你就可以在程序根据需要多次使用它，而无需重新输入一遍。如果你想使用某个模块或模块中的任何代码，你需要 `import`（导入）它。正如之前讨论的，使用标准模块和第三方模块是让 Python 对黑客如此强大的关键特性之一。如果我们想使用早之前安装的 `nmap` 模块，可以在脚本中添加以下行：

```python
import nmap
```

在本章稍后的部分，我们将使用两个非常有用的模块：`socket` 和 `ftplib`。

## 面向对象编程 (OOP)

深入研究 Python 之前，可能值得花一点时间讨论面向对象编程（OOP）的概念。Python 与现在的许多编程语言（如 C++、Java 和 Ruby 等）一样遵循 OOP 模型。

图 17-1 显示了 OOP 背后的基本概念：语言的主要工具是“对象”，它具有属性和状态形式的属性，以及在对象上执行或对对象执行的操作的方法。

| 属性 | 方法 |
| --- | --- |
| 属性或状态 | 函数或过程 |

图 17-1：面向对象编程说明

基于 OOP 的编程语言的核心思想是创建像现实世界事物一样的对象。例如，汽车是一个具有属性的对象，如轮子、颜色、尺寸和引擎类型；它还有方法，即汽车采取的动作，如加速和锁门。从人类自然语言的角度来看，对象是一个名词，属性是一个形容词，而方法通常是一个动词。

对象是类的成员，类是创建对象的模板，具有共享变量、属性和方法。例如，假设我们有一个名为 `cars` 的类；我们的 `car`（汽车）就是该类的成员。该类还包括其他对象，如 Mercedes 和 Audi，如图 17-2 所示。

![](img/7f106d14c88c195ac2085e43b615b_229)
图 17-2：类与对象

类也可以有子类。我们的 `car` 类有一个 `BMW` 子类，该子类可能是特定的模型。每个对象都可能拥有属性（品牌、型号、颜色）和方法（启动、行驶），如图 17-3 所示。

![](img/7f106d14c88c195ac2085e43b615b_229)
图 17-3：属性与方法

在 OOP 语言中，对象继承类的特性，因此 `BMW` 会继承启动和行驶。这些 OOP 概念对于理解 Python 和其他语言的工作原理至关重要，你将在后面的章节中看到。

## 网络通信

在学习更多 Python 概念之前，让我们回顾一下目前为止学了什么，编写一些处理网络连接的脚本。

### 构建 TCP 客户端

我们将使用 `socket` 模块在 Python 中创建一个网络连接。对于本节，将在 Metploitable-2 系统上创建一个网络连接。该 Linux 系统是易受攻击的，你可以从 https://sourceforge.net/projects/metploitable/ 下载它。

查看列表 17-3 中名为 `HackerAriseSSHGrab.py` 的脚本（我知道名字很长，但请耐心）。banner 是当有人连接到它时呈现的内容。黑客使用称为“banner grabbing”（指纹抓取）的技术来查找端口上运行的应用程序或服务信息。

```python
#!/usr/bin/python3

import socket

s = socket.socket()
s.connect(("127.0.0.1", 22))
answer = s.recv(1024)
print(answer)
```

首先，我们导入 `socket` 模块以便可以使用它的函数和工具。`socket` 为计算机之间的通信提供了方法。通常一个是服务器，另一个是客户端。

然后，我们从 `socket` 类中创建一个名为 `s` 的新对象。我们现在可以使用此对象执行后续操作，如连接和读取数据。我们使用 `socket` 模块中的 `connect()` 方法向特定的 IP 和端口建立网络连接。在这种情况下，我连接到 `127.0.0.1`（这是运行此脚本的机器的 IP 地址）和端口 22（默认 SSH 端口）。你可以在任何 Linux 或 Kali 实例上测试此。

一旦建立了连接，就可以做很多事情。在这里，我们使用 `recv` 方法从 `socket` 读取 1024 字节的数据并将其存储在变量 `answer` 中；这 1024 字节将包含 banner 信息。我们使用 `print()` 函数将该变量的内容打印到屏幕上，查看通过 socket 传递了什么！最后一行关闭连接。

将此脚本保存为 `HackerAriseSSHGrab.py`，然后使用 `chmod` 命令更改其权限。运行此脚本连接到端口 22 的 Linux 系统（你可能会使用 Ubuntu 系统或另一个 Kali 系统）。如果端口上运行着 SSH，我们应该能够将 banner 读取到我们的 `answer` 变量并打印到屏幕上，如下：

```bash
kali> ./HackerAriseSSHGrab.py
SSH-2.0-OpenSSH 7.3p1 Debian-1
```

我们刚刚创建了一个简单的 banner grabbing Python 脚本！我们可以使用此脚本查找该 IP 地址和端口运行的版本和操作系统。这提供了黑客在攻击系统之前所需的关键信息。这基本上是 Shodan.io 网站对地球上几乎每个 IP 地址所做的事情，它为我们搜索并索引搜索。

### 创建 TCP 监听器

我们刚刚创建一个 TCP 客户端，它可以连接到另一个 TCP/IP 地址和端口以监控正在传输的信息。该 socket 也可以用于创建 TCP 监听器，监听外部到你服务器的连接。让我们尝试一下。

在列表 17-4 所示 Python 脚本中，你将在系统的任意端口创建一个 socket，当有人连接到该 socket 时，收集连接者系统的关键信息。输入脚本并将其保存为 `tcp_server.py`。确保使用 `chmod` 赋予自己执行权限。

```python
#!/usr/bin/python3

import socket

TCP_IP = "192.168.1.190"
TCP_PORT = 6996
BUFFER_SIZE = 100

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind((TCP_IP, TCP_PORT))
s.listen(1)

conn, addr = s.accept()
print('Connection address: ', addr)

while True:
    data = conn.recv(BUFFER_SIZE)
    if not data:
        break
    print("Received data: ", data)
    conn.send(data)  # echo

conn.close()
```

列表 17-4：一个 TCP 监听 Python 脚本

我们声明脚本将使用 Python 解释器运行，并像以前一样导入 `socket` 模块，这样我们就可以使用它的功能。我们定义了变量来存储 TCP/IP 地址信息、监听的端口以及我们想要从连接的系统中获取的数据缓冲区大小。

我们定义了 socket，并使用创建的变量将其绑定到 IP 地址和端口。我们使用 `socket` 库中的 `listen()` 方法让 socket 开始监听。

我们使用 `socket` 库的 `accept` 方法获取连接系统的 IP 地址和端口，并将这些信息打印到屏幕上供用户查看。注意 `while` 循环的语法：这些内容在本章的较靠后的部分才会出现，但现在只需要知道它是无限运行缩进代码的，这意味着 Python 会一直检查数据，直到程序停止。

最后，我们将来自连接系统的信息放入缓冲区中，然后关闭连接。

现在，打开浏览器并访问 http://localhost:6996 以进入我们设计的 6996 端口。运行 `tcp_server.py` 脚本，你应该能够连接并收集有关该系统的信息，如下：

```bash
kali> ./tcp_server.py
Connection Address: '192.168.181.190', 45368
Received data: Get /HTTP/1.1
Host:192.168.181.190:6996
User-Agent: Mozilla/5.0 (X11; x86_64; rv:24.0) Ge
```

```text
--snip--
```
