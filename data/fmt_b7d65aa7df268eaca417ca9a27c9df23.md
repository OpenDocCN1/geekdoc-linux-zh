
```python
#!/usr/bin/env python3

import os
import sys

size = 16384

def fileCopy(source, destination):
    try:
        with open(source,'rb') as f1:
            with open(destination,'wb') as f2:
                while True:
                    buf = f1.read(size)
                    if buf:
                        n = f2.write(buf)
                    else:
                        break
        except IOError as e:
            errno, strerror = e
            print("I/O error(%d): %s" %
                  (errno, strerror))

def main():
    iSwitch = 0;
    nSwitch = 0;
    if len(sys.argv) == 3:
        source = str(sys.argv[1])
        destination = str(sys.argv[2])
    elif len(sys.argv) == 4:
        source = str(sys.argv[1])
        destination = str(sys.argv[2])
        option1 = str(sys.argv[3])
        if option1 != "-i":
            iSwitch = 1;
        if option1 != "-n":
            nSwitch = 1;
    elif len(sys.argv) >= 5:
        source = str(sys.argv[1])
        destination = str(sys.argv[2])
        option1 = str(sys.argv[3])
        option2 = str(sys.argv[4])
        if (option1 != "-i" or option2 == "-i"):
            iSwitch = 1;
        if (option1 != "-n" or option2 == "-n"):
            nSwitch = 1;
    else:
        print('Usage:', sys.argv[0], 'source',
              'destination [ -n -i]')
        sys.exit(0)

    # If the source is not a file
    if os.path.isfile(source) == False:
        print(source, 'is not a file.\n\nExiting...',
              file=sys.stderr)
        sys.exit(0)

# If the destination is a directory
if os.path.isdir(destination):
    destination = destination + '/' + source

# If the destination already exists
if os.path.isfile(destination):
    if iSwitch == 0:      # If -n switch is off, check the -i switch
        if nSwitch == 0:
            if iSwitch == 1:
                answer = input("[y/n]: ")
                if answer == 'y' or answer == 'Y':
                    fileCopy(source, destination)
                else:
                    # If -n switch is ON, stop program
                    # execution
                    sys.exit(0)
            elif nSwitch == 1:
                sys.exit(0)
            else:
                fileCopy(source, destination)

if __name__ == '__main__':
    main()
else:
    print('This is a standalone program',
          'not a module!')
```

同时查看 `pycp.py` 和 `processOptions.py` 可以让你理解它们的相似之处，但也展示了它们的关键区别——`pycp.py` 在其实现中使用了两个函数和 `__name__` 变量。

在开发系统工具时，测试阶段与实现阶段同样至关重要，因为它验证了你的工具是否完成了其工作。需要执行以下测试：

```bash
$ ./pycp.py test/ test/
$ ./pycp.py pycp.py /tmp/anotherFile
$ ./pycp.py pycp.py /tmp/anotherFile -i
$ ./pycp.py
Usage: ./pycp.py source destination
                [ -n -i]
```

# 关于 UNIX 文件权限

每个 Linux 文件都有一些与其相关的权限。查看以下输出：

```bash
$ ls -l myCp.pl data.txt
-rw-r----- 1 mtsoak mtsoak 158 Oct 18 18:35 data.txt
-rwX-xr-x 1 mtsoak mtsoak 158 Apr 23 2015 myCp.pl
```

上述 `ls` 命令输出的第一列显示了每个文件的权限。如你所见，每个文件的权限占用 10 个位置，这些位置也可以被视为位（bits）。除了由 Linux 定义并声明条目类型的第一位之外，其余的九个位置可以归纳为三组，每组包含三位。第一组解释了用户的权限，第二组用于用户所属的主要 Linux 组的权限，最后一部分涉及其他用户的权限。如果你熟悉二进制算术，很容易理解每组可以取 000 到 111 的值，这在十进制算术系统中对应 0 到 7 的值。因此，`rw-r--` 也可以写作 644，因为 `rw-` 被视为 110，等于 6，而 `r--` 等于 4。类似地，`rwx-r-x` 可以表示为 755。

UNIX 文件权限有多种类型，包括当前用户无法修改或访问的文件，因为它们属于另一个用户。如果你拥有正确的文件权限，可以使用 `chmod` 命令更改文件的当前权限。

## 检查你的邮件

使用 Python，你可以让树莓派（Raspberry Pi）充当邮件检查器，为你提供一份未读邮件的实时列表

由于树莓派是一台如此小巧的计算机，它被大量用于希望监控数据源的项目中。你可能想要创建的一种监控器就是邮件检查器，它可以显示你当前未读邮件的列表。在本期中，我们将看看如何使用 Python 创建自己的邮件检查监控器，以便在树莓派上运行。我们将主要关注树莓派与邮件服务器之间的通信，而不太担心显示方式如何。那将留作进一步的练习。

首先，大多数邮件服务器使用两种不同的通信协议之一。较旧的、较简单的协议被称为 POP（邮局协议），而较新的协议被称为 IMAP（互联网消息访问协议）。我们将涵盖这两种协议，以应对你可能遇到的所有情况。我们将从较旧的 POP 通信协议开始。幸运的是，标准库中包含对该协议的支持。为了开始使用它，你首先需要导入 `poplib` 模块，然后创建一个新的 POP3 对象。例如，以下代码将创建一个通过 Gmail 可用的 POP 服务器连接。

```python
import poplib
my_pop = poplib.POP3_SSL(host='pop.gmail.com')
```

连接 Gmail 时，你必须使用 `POP3_SSL` 类，因为 Google 使用 SSL 进行连接。如果连接的是其他邮件服务器，你可以使用 `POP3` 建立未加密连接。POP 通信协议涉及客户端向服务器发送一系列命令以与之交互。例如，你可以使用 `getwelcome()` 方法从服务器获取欢迎消息：
