
在第二个示例中，你以普通用户身份登录，当使用 `su -c` 运行 `whoami` 时，它显示的是 `root` 用户。

# 第 3 章：使用 Shell

输出显示 `root` 用户。

## 使用环境变量 (Environment Variables)

对你的环境非常有用的少量信息存储在被称为环境变量的内容。按照惯例，环境变量名全全大写（尽管并非强制要求）。

```bash
$ set | less
BASH=/bin/bash
COLORS=/etc/DIR_COLORS.xterm
COLUMNS=118
DISPLAY=:0.0
HOME=/home/fcaen
HOSTNAME=einstein
```

显示的输出仅包含你将看到的环境变量的少数示例。你也可以自己设置或重置任何变量。例如，将变量 `123` 赋值给 `ABC`（然后显示 `ABC` 的内容），输入以下内容：

```bash
$ ABC=123
$ echo $ABC
123
```

变量 `ABC` 只存在于创建它的 `shell` 中。如果你从该 `shell` 启动命令（`ls`、`cat`、`firefox` 等），该新进程将看不到该变量。启动一个新进程并测试这一点：

```bash
$ bash
$ echo $ABC
```

你可以通过 `export` 命令使变量成为环境变量的一部分，并被子进程继承：

```bash
$ export ABC=123
$ bash
$ echo $ABC
123
```

此外，你可以将字符串连接到现有变量上：

```bash
$ export PATH=$PATH:/home/fcaen
```

列出你 `bash` 的环境变量：

```bash
$ env
```

当你准备创建自己的环境变量时，避免使用系统已常用的环境变量名称。请参阅附录 B 中的 `shell` 环境变量列表。

## 创建简单的重复性脚本

`Shell` 脚本非常适合自动化重复性的 `Shell` 任务。`Bash` 和其他 `shell` 包含了各种编程语言中的基本结构，例如循环、测试、`case` 语句等。主要的区别在于它只有一种类型的变量：字符串。

### 编辑和运行脚本

`Shell` 脚本是简单的文本文件。你可以使用你喜欢的文本编辑器（如 `vi`）创建它们。要运行脚本，该文件必须具有执行权限。例如，如果你创建了一个名为 `myscript.sh` 的 `shell` 脚本，可以通过以下方式使其具有可执行性：

```
$ chmod u+x myscript.sh
```

此外，你的 `bash` 脚本的第一行始终应该是以下内容：

```
#!/bin/bash
```

与任何命令一样，除了执行你创建的 `shell` 脚本，它必须在你的 `PATH` 中，或者在运行时通过其完整路径或相对路径来识别。换句话说，如果你直接尝试运行脚本，可能会得到以下结果：

```
$ myscript.sh
bash: myscript.sh: command not found
```

在这个示例中，包含 `myscript.sh` 的命令未包含在你的 `PATH` 中。要解决这个问题，你可以编辑你的路径、将脚本复制到 `PATH` 中的某个目录，或者输入它的完整路径或相对路径。这四个示例下所示：

```
$ mkdir /bin; cp myscript.sh /bin/; PATH=$PATH:-/bin
$ cp myscript.sh /usr/local/bin
$ ./myscript.sh
$ /tmp/myscript.sh
```

避免将点号 (`.`) 引入 `PATH`，以表示可以从当前目录运行命令。这种技术可能会导致与重要、常用命令（如 `ls` 或 `cat`）文件名相同的命令，如果当前目录中存在同名命令，它们可能会被覆盖。

### 向脚本中添加内容

虽然 `shell` 脚本可以是简单的命令序列，但也可以像使用任何编程语言一样使用 `shell` 脚本。例如，脚本根据不同的输入产生不同的结果。本节描述了如何在 `shell` 脚本中使用组合复合命令，例如 `if/then` 语句、`case` 语句和 `for/while` 循环。

下面的示例代码将字符串 `abc` 赋值给变量 `MYSTRING`。然后测试输入以检查其是否等于 `abc`，并根据测试结果采取行动。测试发生在括号 (`[ ]`) 之间：

```
MYSTRING=abc
if [ $MYSTRING = abc ]; then
echo "The variable is abc"
fi
```

要对测试进行取反，如下所示，使用 `!` 代替 `=`：

```
if [ $MYSTRING != abc ]; then
echo "$MYSTRING is not abc"
fi
```

以下是测试数字的示例：

```
if [ $MYNUMBER -eq 1 ]; then echo "MYNUMBER equals 1"; fi
if [ $MYNUMBER -lt 0 ]; then echo "MYNUMBER < 2"; fi
if [ $MYNUMBER -le 1 ]; then echo "MYNUMBER <= 1"; fi
if [ $MYNUMBER -gt 0 ]; then echo "MYNUMBER > 0"; fi
if [ $MYNUMBER -ge 1 ]; then echo "MYNUMBER >= 1"; fi
```

让我们来看一些对文件的测试。在这个示例中，你可以检查文件是否存在 (`-e`)、它是否为普通文件 (`-f`)，或者它是否为目录 (`-d`)。这些检查通过 `if/then` 完成。如果没有匹配，则使用 `else` 语句来产生结果。

表 3-1 显示了你可以在文件、字符串和变量上执行的测试示例。

#### 表 3-1：测试表达式的运算符

| 运算符 | 执行的测试 |
|---|---|
| `-a file` | 检查文件是否存在（同 `-e`） |
| `-b file` | 检查是否为特殊块设备 |
| `-c file` | 检查是否为特殊字符设备 |
| `-d file` | 检查是否为目录 |
| `-e file` | 检查文件是否存在（同 `-a`） |
| `-f file` | 检查文件是否存在且为普通文件（例如不是目录、套接字、管道、链接或设备） |
| `-g file` | 检查是否设置了组 ID |
| `-h file` | 检查是否为符号链接（同 `-L`） |
| `-k file` | 检查是否设置了粘滞位 |
| `-n string` | 检查字符串长度是否大于0 |
| `-O file` | 检查你是否拥有该文件 |
| `-p file` | 检查是否为命名管道 |
| `-r file` | 检查你是否有权限读取该文件 |
| `-s file` | 检查文件是否存在且大于0字节 |
| `-S file` | 检查文件是否存在且为套接字 |
| `-t fd` | 检查文件描述符是否连接到终端 |
| `-u file` | 检查是否设置了用户 ID |
| `-w file` | 检查你是否有权限写入该文件 |
| `-x file` | 检查文件是否可执行 |
| `-z string` | 检查字符串长度是否为0 |
| `-a expr2` | 检查两个表达式是否都为真 |
| `-o expr2` | 检查两个表达式是否有一个为真 |
| `-nt file` | 检查第一个文件是否比第二个文件新 |
| `-ot file` | 检查第一个文件是否比第二个文件旧 |

# 第 4 章：文件操作
