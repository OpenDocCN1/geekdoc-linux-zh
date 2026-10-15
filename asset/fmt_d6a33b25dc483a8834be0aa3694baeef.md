
打开文本编辑器：要创建一个 `bash` 脚本，你需要使用文本编辑器创建一个新文件并输入你的命令。你可以使用任何文本编辑器（如 `vi`、`nano` 或 `gedit`）来创建 `bash` 脚本。

添加 `# shebang`：你的 `bash` 脚本的第一行应该是 `#!` 后面跟上 `bash` 解释器的路径。这告诉系统使用哪种解释器来执行脚本。例如，你可以使用以下行来指定 `Bash` 解释器：`#!/bin/bash`。

添加你的命令：在 `shebang` 之后，你可以将 `Bash` 命令添加到脚本中。你可以使用任何有效的 `Bash` 命令，如 `.sh`、`cd`、`mkdir` 或 `rm`，来对系统执行任务或操作。

保存文件：以 `.sh` 扩展名保存文件，以表示这是一个 `Bash` 脚本。例如，你可以将文件保存为 `myscript.sh`。

赋予脚本可执行权限：要使脚本具有可执行，你需要使用 `chmod` 命令更改其权限。例如，你可以使用以下命令使脚本变为可执行：`chmod +x myscript.sh`。

执行脚本：要执行脚本，你可以使用 `./` 命令后跟脚本名称。例如，你可以使用以下命令执行脚本：`./myscript.sh`。

## 编写‘hello world’ 程序

以下是一个简单的 `bash` 脚本示例，它可以显示消息并列出当前目录下的文件：

```bash
#!/bin/bash
echo "Hello, world!"
ls
```

该脚本在执行时将显示消息“Hello, world!”然后列出当前目录下的文件。你可以通过查询在线资源或咨询你特定 Linux 发行版的文档获取更多关于编写和使用 `bash` 脚本的信息。

## 编写 Bash 程序探索所有命令

以下是一个演示常用 `shell` 命令的 `bash` 脚本示例：

```bash
#!/bin/bash

# 显示当前工作目录
echo "Current working directory:"
pwd

# 列出当前目录下的文件和目录
echo "Files and directories in the current directory:"
ls

# 创建一个新目录
echo "Creating a new directory..."
mkdir newdir

# 新新目录
echo "Changing to the new directory..."
cd newdir

# 显示当前工作目录
echo "Current working directory:"
pwd

# 从父目录复制文件
echo "Copying a file from the parent directory..."
cp ../file.txt .

# 显示文件内容
echo "Contents of the file:"
cat file.txt

# 回到父目录
echo "Going back to the parent directory..."
cd ..

# 删除新目录及其内容
echo "Deleting the new directory and its contents..."
rm -rf newdir
```

此脚本演示了如何使用 `pwd`、`ls`、`mkdir`、`cd`、`cp` 和 `rm` 等命令对系统执行任务和操作。你可以通过查询在线资源或咨询你特定 `shell` 的文档来获取更多关于这些及其他常用 `shell` 命令的信息。

以下是上述 `bash` 脚本的输出：

```
Current working directory:
/home/user
Files and directories in the current directory:
file1.txt file2.txt dir dir2
Creating a new directory...
Changing to the new directory...
Current working directory:
/home/user/newdir
Copying a file from the parent directory...
Contents of the file:
This is the contents of the file.
Going back to the parent directory...
Deleting the new directory and its contents...
```

此输出显示了各种命令的结果。

## 使用算术表达式

`Bash` 中的算术表达式允许你执行加、减、乘、除等操作。以下是使用算术表达式的示例：

```bash
# 加法
echo $((10 + 5))

# 减法
echo $((10 - 5))

# 乘法
echo $((10 * 5))

# 除法
echo $((10 / 5))
```

### 显示数字 1 到 10

```bash
for i in {1..10}
do
  echo "$i"
done
```

此脚本使用 `for` 循环来显示数字 1 到 10。`for` 循环遍历范围 `{1..10}`，并将范围内的每个值赋值给变量 `i`。循环循环体中的代码 `echo "$i"` 会对 `i` 的每个值执行一次。该脚本的输出将是：

+ 1

2

3

4

5

6 7

8

9

10

## 使用 While 循环

### 理解 ‘while’ 循环

Linux 中的 `while` 循环是一种循环结构，只要特定条件为真（true），它就会重复执行命令块。`while` 循环的基本语法如下：

```bash
while [condition]; do
  [commands]
done
```

条件指定在 `while` 关键字之后，并括在方括号 `[]` 中。如果条件为真，则将执行 `do` 和 `done` 关键字之间的命令，并且循环将继续。如果条件为假，循环将退出，程序将继续执行下一条指令。

### 使用 ‘while’ 循环的示例程序

这是一个从 1 计数到 10 的 `while` 循环示例：

```bash
#!/bin/bash
count=1
while [ $count -le 10 ]; do
  echo $count
  count=$((count+1))
done
```

此脚本将输出从 1 到 10 的数字，每次迭代都会增加 `count` 变量的值。

脚本的输出如下：

```
1
2
3
4
5
6
7
8
9
10
```

如所示，脚本首先初始化一个名为 `count` 的变量并赋值为 1。然后开始 `while` 循环并评估条件 `[$count -le 10 ]`。由于 `count` 的值为 1 且 1 小于或等于 10，因此执行循环体内的命令。循环内的第一个命令是 `echo $count`，它将 `count` 的当前值打印到终端。第二个命令是 `count=$((count+1))`，它将 `count` 的值加 1。

在执行完循环体内的命令后，循环回到开头并再次评估条件。此过程一直持续，直到 `count` 的值大于 10，此时循环退出，程序继续执行下一条指令。

## 使用函数

### 什么是函数？

Linux 中的函数是将一组命令组合在一起并给它们命名的方法。这允许你多次重用这些命令，而无需再次输入。函数使用 `function` 关键字定义，后面紧跟函数名和一组括在花括号 `{}` 中的命令。函数的基本语法如下：

```bash
function function_name {
  [commands]
}
```

函数也可以通过使用关键字 `function_name ()` 来定义，这是符合 POSIX 标准的定义方式。

```bash
function_name () {
  [commands]
}
```

这是一个向终端打印“Hello, World!”的函数示例：

```bash
#!/bin/bash

hello() {
  echo "Hello, World"
}

hello
```

在这个示例中，函数 `hello` 通过单个命令 `echo "Hello, World!"` 定义。在脚本的最后一行，通过简单输入其名称并执行它来调用该函数。

函数还可以接收参数并返回结果。传递给函数的参数在函数名后的括号内指定，并在函数内部使用 `$1`、`$2` 等变量进行访问。函数还可以使用 `return` 命令返回数值，这会设置函数的退出状态。

函数对于组织和结构化代码以及复杂脚本的模块化非常有用。它们还让代码重用变得简单，并使其更具可读性和可维护性。

### 使用函数的示例程序

以下是一个 `bash` 脚本示例，它定义了一个函数然后调用它来执行命令：
