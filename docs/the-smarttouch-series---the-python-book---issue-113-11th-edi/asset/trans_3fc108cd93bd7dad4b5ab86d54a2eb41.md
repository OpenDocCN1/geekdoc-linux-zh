
## 文件操作与 Python 示例

```python
fileMetadata = [(filename, os.lstat(filename))
for name, meta in fileMetadata:
    if S_ISDIR(meta.st_mode):
        print("It is a directory!")
    else:
        print("It is a regular file")
        print(name, "takes", meta.st_size, "bytes")
        print("File permissions:", stat.filemode(os.lstat(filename).st_mode))
```

Python 3 提供的 `os.lstat()` 和 `os.stat()` 之间的区别在于，`os.lstat()` 不会跟随符号链接，这使得它比 `os.stat()` 更安全。运行 **FileOperations.py** 会生成如下类型的输出：

```text
$ ./FileOperations.py FileOperations.py
It is a regular file
FileOperations.py takes 502 bytes
File permissions: -rw-r-x-r-x
$ ./FileOperations.py .
It is a directory!
. takes 4096 bytes
File permissions: drwxr-x-r-x
```

正如您可以从“File permissions”部分的值中看到的，普通文件以连字符开头，而目录以字母 d 开头。

### 这是作弊！

借助 `os.system()` 方法，Python 允许您在脚本中使用外部命令。因此，您可以使用 `cp` 实用程序本身来实现文件复制。保存在 **cheating.py** 中的以下代码展示了这种技术：

```python
#!/usr/bin/python3
import os
import sys
if len(sys.argv) >= 3:
    # ... (code omitted in OCR)
```

### Python 3 中的文件复制

大多数编程语言，包括 C、Perl 和 C++，都提供了多种复制文件的方法。Python 3 也不例外。

一般来说，当您有多种方式执行任务时，应使用最通用的方式。如果所有方式都是通用的，那么您应该选择最快的那一种。如果您事先不知道哪种技术最快，您可以进行一些测试来找出答案。

本节将介绍在 Python 3 中复制文件的两种方法。第一种方法在 **copy1.py** 文件中：

```python
#!/usr/bin/env python3
from shutil import copyfile
import sys
if len(sys.argv) >= 3:
    source = str(sys.argv[1])
    destination = str(sys.argv[2])
else:
    print("Not enough arguments!")
    sys.exit(0)
try:
    copyfile(source, destination)
except IOError as e:
    errno, strerror = e.args
    print("I/O error(%d): %s" % (errno, strerror))
```

`shutil` 模块的 `copyfile()` 函数为我们完成了所有工作。由于这种技术使用单一方法，您无法对其控制，这有时是好事，但有时也可能是坏事。第二种方法包含在 **copy2.py** 文件中：

```python
#!/usr/bin/env python3
import sys
if len(sys.argv) >= 3:
    source = str(sys.argv[1])
    destination = str(sys.argv[2])
else:
    print("Not enough arguments!")
    sys.exit(0)
size = 16384
try:
    with open(source, 'rb') as f1:
        with open(destination, 'wb') as f2:
            while True:
                buf = f1.read(size)
                if buf:
                    n = f2.write(buf)
                else:
                    break
except IOError as e:
    errno, strerror = e.args
    print("I/O error(%d): %s" % (errno, strerror))
```

这种技术使用 `write()` 方法，利用名为 `buf` 的缓冲区变量将数据复制到新文件中。使用非常小的缓冲区（例如 8 字节）会损害脚本的性能。解决方案是根据您机器的 RAM 使用相对较大的缓冲区。

请注意，**copy1.py** 和 **copy2.py** 都使用 "try" 块来捕获和处理复制操作期间可能出现的错误。虽然这两种技术都不错，但第二种技术让您对过程拥有更多的控制权，并且可能更高效；因此，这里展示的 `cp` 的 Python 3 实现将使用这种技术。

### 快速提示

您可以在 LXF DVD 上找到源代码，或者在 linuxformat.com 的存档中 LXF227 期下找到它，对所有人开放。

### strace 命令行实用工具

strace 实用工具使您可以看到执行程序或脚本时后台发生了什么。严格来说，`strace` 跟踪可执行程序的**系统调用**和**信号**，并显示在您的屏幕上。对 **pycp.py** 使用 `strace` 会显示如下类型的信息：

```text
$ strace ./pycp.py pycp.py
anotherFile
...
stat("/usr/lib/python3.4/os.py", {st_mode=S_IFREG(0644, st_size=33763, ...) = 0
open("./pycp.py", O_RDONLY) = 3
open("anotherFile", O_WRONLY|O_CREAT|O_TRUNC, S_IRUSR|S_IWUSR|S_IRGRP|S_IWGRP|S_IROTH|S_IWOTH, 0666) = 4
write(4, "#!/usr/bin/env python3\n", 21) = 21
...
close(4) = 0
close(3) = 0
...
```

上述输出显示，您的 `pycp.py` 脚本是作为 C 函数和 C 系统调用来执行的，因为这是与 Linux 内核通信的唯一方式。然而，如果用 C 编写相同的程序，需要更多的代码行和更多的调试时间。

## 使用 Python 工作

### 快速提示

C 系统调用只是一个 C 函数。使系统调用与普通 C 函数不同的是，系统调用实现了通常是低层级的功能，并将 UNIX 内核与世界其余部分连接起来。最终，与文件操作相关的 Python 3 命令会被翻译成 C 系统调用。

### 处理选项

在实现 mycp.py 时，需要考虑的最重要的事情是，当目标文件已经存在时，您打算怎么做。简而言之，您是打算删除它，还是停止复制过程？`cp` 实用程序的默认行为是删除目标文件，除非您使用 `-n` 开关。此外，如果您使用 `-i` 选项，`cp` 会询问您是否想要删除目标文件。但是，如果您同时使用 `-n` 和 `-i`，则 `-n` 优先，而 `-i` 将被忽略。第二个任务是能够判断目标文件是否为目录，因为在这种情况下，您将把新文件放入该目录中。

在这里，我们使用 **processOptions.py** 的 Python 3 代码示例来处理与文件复制相关的命令行参数和选项：

```python
#!/usr/bin/env python3
import os
import sys

iSwitch = 0;
nSwitch = 0;

if len(sys.argv) == 3:
    source = str(sys.argv[1])
    destination = str(sys.argv[2])
elif len(sys.argv) == 4:
    source = str(sys.argv[1])
    destination = str(sys.argv[2])
    option1 = str(sys.argv[3])
    if option1 == "-i":
        iSwitch = 1;
    if option1 == "-n":
        nSwitch = 1;
elif len(sys.argv) >= 5:
    source = str(sys.argv[1])
    destination = str(sys.argv[2])
    option1 = str(sys.argv[3])
    option2 = str(sys.argv[4])
    if (option1 == "-i" or option2 == "-i"):
        iSwitch = 1;
    if (option1 == "-n" or option2 == "-n"):
        nSwitch = 1;
else:
    print('Usage: ', sys.argv[0], 'source destination [-in]')
    sys.exit(0)

# If the source is not a file
if os.path.isfile(source) == False:
    print(source, 'is not a file. Exiting...')
    sys.exit(0)

# If the destination is a directory
if os.path.isdir(destination):
    destination = destination + '/' + source
    print('Copying to', destination)

# If the destination already exists
if os.path.isfile(destination):
    print(destination, 'already exists!')
    # If -n switch is OFF, check the -i switch
    if nSwitch == 0:
        if iSwitch == 1:
            answer = input('y\n')
            if answer == 'y' or answer == 'Y':
                print('Copying', source, 'to', destination)
        else:
            print('Cannot overwrite', destination)
            sys.exit(0)
    # If -n switch is ON, stop program execution
    elif nSwitch == 1:
        sys.exit(0)
    else:
        print('Copying', source, 'to', destination)
```

为了简化代码，源文件必须始终排在第一位，目标文件或目录必须排在第二位——这在脚本显示的使用消息中已说明。

接下来，您应该包含您想要的任何选项。运行 **processOptions.py** 会生成如下类型的输出：

```text
$ ./processOptions.py
Usage: ./processOptions.py source destination [-in]

$ ./processOptions.py afile
Usage: ./processOptions.py source destination [-in]

$ ./processOptions.py afile anotherfile
afile is not a file. Exiting...

$ ./processOptions.py processOptions.py newfile
Copying processOptions.py to newfile

$ mkdir test
$ ./processOptions.py processOptions.py test
Copying to test/processOptions.py
Copying processOptions.py to test/processOptions.py
```

> **需要考虑的最重要的事情是，当目标文件已经存在时，您打算怎么做**

